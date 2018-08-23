---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: 配置数据访问层的连接和命令级别的设置 (VB) |Microsoft Docs
author: rick-anderson
description: 类型化数据集内的 Tableadapter 自动负责连接到数据库中，发出的命令，并填充 DataTable 与结果...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: d44372ef3eaf7634d3bf3a82bd2c1eb1d710f786
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832932"
---
<a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>配置数据访问层的连接和命令级别的设置 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip)或[下载 PDF](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> 类型化数据集内的 Tableadapter 自动负责连接到数据库中，发出的命令，并填充 DataTable 的结果。 但是，如果我们想要处理的这些详细信息，并在本教程中我们将了解如何访问 TableAdapter 中的数据库连接和命令级别设置有情况。


## <a name="introduction"></a>介绍

整个系列教程我们使用了类型化数据集来实现数据访问层和业务对象的分层式体系结构。 如中所述[第一篇教程](../introduction/creating-a-data-access-layer-vb.md)，s 数据表用作数据的存储库而 Tableadapter 充当包装与要检索和修改基础数据的数据库进行通信的类型化数据集。 Tableadapter 封装在处理数据库中所涉及的复杂性，并使我们无需编写代码以连接到数据库中，发出命令，或填充到 DataTable 的结果。

有些的时候，但是，当我们需要的 TableAdapter burrow 和编写代码，直接使用 ADO.NET 对象。 在中[包装事务内的数据库修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)教程中，例如，我们添加方法到 TableAdapter 的开始、 提交和回滚 ADO.NET 的事务。 使用这些方法内部，手动创建`SqlTransaction`对象分配给 TableAdapter 的`SqlCommand`对象。

在本教程中，我们将说明如何访问 TableAdapter 中的数据库连接和命令级别设置。 具体而言，我们将添加到功能`ProductsTableAdapter`允许访问为基础的连接字符串和命令超时设置。

## <a name="working-with-data-using-adonet"></a>使用 ADO.NET 处理数据

Microsoft.NET Framework 包含大量专门用于处理数据的类。 这些类中找到[`System.Data`命名空间](https://msdn.microsoft.com/library/system.data.aspx)，称为*ADO.NET*类。 某些 ADO.NET 之下的类绑定到特定*数据提供程序*。 可以数据访问接口视为允许将信息 ADO.NET 类和基础数据存储区之间流动的通信通道。 没有通用提供程序，如 OleDb 和 ODBC，以及专门设计用于特定的数据库系统的提供程序。 例如，可能会连接到使用 OleDb 访问接口的 Microsoft SQL Server 数据库时，SqlClient 提供程序是高效得多因为它的设计和优化专门用于 SQL Server。

当以编程方式访问数据时，通常使用以下模式：

1. 建立到数据库的连接。
2. 发出命令。
3. 有关`SELECT`查询，处理生成的记录。

有单独的 ADO.NET 类来执行每个步骤。 若要连接到使用 SqlClient 提供程序的数据库，例如，使用[`SqlConnection`类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)。 颁发`INSERT`， `UPDATE`， `DELETE`，或`SELECT`命令到数据库，请参考[`SqlCommand`类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)。

除[包装事务内的数据库修改](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md)教程中，我们不不得不编写任何低级别的 ADO.NET 代码，我们自己因为 Tableadapter 自动生成的代码包括到所需的功能连接到数据库、 发出命令，检索数据和该数据填充到数据表。 但是，可能是我们需要自定义这些低级别的设置。 通过以下几个步骤中，我们将说明如何利用在内部使用 Tableadapter 的 ADO.NET 对象。

## <a name="step-1-examining-with-the-connection-property"></a>第 1 步： 检查连接属性

每个 TableAdapter 类具有`Connection`属性，用于指定数据库连接信息。 此属性的数据类型和`ConnectionString`值由 TableAdapter 配置向导中所做的选择。 回想一下，我们首先将 TableAdapter 添加到类型化数据集时此向导将询问我们数据库源 （请参阅图 1）。 此第一步中的下拉列表包括这些配置文件，以及在服务器资源管理器的数据连接中的任何其他数据库中指定的数据库。 如果下拉列表中，我们想要使用的数据库不存在，则可以通过单击新建连接按钮并提供所需的连接信息指定新的数据库连接。


[![TableAdapter 配置向导第一步](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**图 1**: 第一步的 TableAdapter 配置向导 ([单击以查看实际尺寸的图像](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))


允许 s 花点时间检查 TableAdapter s 代码`Connection`属性。 如中所述[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中，我们可以转到类视图窗口中，向下合适的类，钻取，然后双击成员名称查看自动生成的 TableAdapter 代码。

通过转到视图菜单并选择类视图 （或通过键入 Ctrl + Shift + C），请导航到类视图窗口。 从类视图窗口的上半部分，向下钻取`NorthwindTableAdapters`命名空间，然后选择`ProductsTableAdapter`类。 这将显示`ProductsTableAdapter`的成员在类视图，如图 2 中所示的下半部分。 双击`Connection`属性以查看其代码。


![双击要查看其自动生成的代码的类视图中的连接属性](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**图 2**： 双击要查看其自动生成的代码的类视图中的连接属性


TableAdapter 的`Connection`属性和其他与连接相关的代码如下所示：


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

TableAdapter 类实例化时，成员变量`_connection`等同于`Nothing`。 当`Connection`访问属性时，它首先检查以查看是否`_connection`已实例化成员变量。 如果没有，`InitConnection`调用方法时，实例化`_connection`，并设置其`ConnectionString`TableAdapter 配置向导 s 第一个步骤中指定的连接字符串值的属性。

`Connection`还可以将属性分配给`SqlConnection`对象。 执行此操作将相关联的新`SqlConnection`对象与每个 TableAdapter 的`SqlCommand`对象。

## <a name="step-2-exposing-connection-level-settings"></a>步骤 2： 公开连接级别的设置

连接信息应保持在 TableAdapter 中封装和无法访问应用程序体系结构中其他层。 但是，可能有的方案必须是可访问或进行自定义查询、 用户或 ASP.NET 页面的 TableAdapter 的连接级别信息。

让我们来扩展`ProductsTableAdapter`中`Northwind`要包括数据集`ConnectionString`业务逻辑层可以使用用于读取或更改所用的 TableAdapter 的连接字符串属性。

> [!NOTE]
> 一个*连接字符串*是一个字符串，指定数据库连接信息，如要使用的数据库、 身份验证凭据和其他与数据库相关的设置的位置的提供程序。 使用的各种数据存储和提供程序的连接字符串模式的列表，请参阅[ConnectionStrings.com](http://www.connectionstrings.com/)。


如中所述[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中，可以通过使用分部类扩展类型数据集的自动生成的类。 首先，创建新的子文件夹中名为的项目`ConnectionAndCommandSettings`下方`~/App_Code/DAL`文件夹。


![添加一个名为 ConnectionAndCommandSettings 子](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**图 3**： 添加名为的子文件夹 `ConnectionAndCommandSettings`


添加名为的新类文件`ProductsTableAdapter.ConnectionAndCommandSettings.vb`并输入以下代码：


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

此分部类添加`Public`名为属性`ConnectionString`到`ProductsTableAdapter`类，该类允许读取或更新基础连接的 TableAdapter s 的连接字符串的任何层。

与此分部类创建 （和保存），打开`ProductsBLL`类。 请转到现有的方法之一，然后键入`Adapter`然后按句点键来打开智能感知。 你应看到新`ConnectionString`提供 IntelliSense，这意味着您可以以编程方式读取或调整此值从 BLL 中的属性。

## <a name="exposing-the-entire-connection-object"></a>公开整个连接对象

此部分的类公开基础连接对象的一个属性： `ConnectionString`。 如果你想要使整个连接对象由于篇幅所限 TableAdapter 的更高版本，或者可以更改`Connection`属性的保护级别。 我们在步骤 1 中检查自动生成的代码演示的 TableAdapter s`Connection`属性标记为`Friend`，这意味着，它只能访问由在同一程序集中的类。 这可以更改，但是，通过 TableAdapter 的`ConnectionModifier`属性。

打开`Northwind`数据集，单击`ProductsTableAdatper`在设计器并导航到属性窗口。 您会看见`ConnectionModifier`设置为其默认值， `Assembly`。 若要使`Connection`属性的类型化数据集 s 程序集，更改外部可用`ConnectionModifier`属性设置为`Public`。


[![可通过 ConnectionModifier 属性配置连接属性 s 可访问性级别](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**图 4**:`Connection`通过属性可访问性级别可配置的 s`ConnectionModifier`属性 ([单击以查看实际尺寸的图像](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png))


保存的数据集，然后返回到`ProductsBLL`类。 如之前，请转到现有的方法之一，然后键入`Adapter`然后按句点键来打开智能感知。 此列表应包括`Connection`属性; 也就是说，现在可以以编程方式读取或从 BLL 分配任何连接级别的设置。

## <a name="step-3-examining-the-command-related-properties"></a>第 3 步： 检查与命令相关的属性

包含的主查询，默认情况下，具有自动生成的 TableAdapter `INSERT`， `UPDATE`，和`DELETE`语句。 此主查询 s `INSERT`， `UPDATE`，并`DELETE`语句中的 TableAdapter 的代码实现作为 ADO.NET 数据适配器对象通过`Adapter`属性。 喜欢使用其`Connection`属性，`Adapter`属性的数据类型由使用的数据提供程序。 这些教程使用 SqlClient 提供程序，因为`Adapter`属性属于类型[ `SqlDataAdapter` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)。

TableAdapter s`Adapter`属性具有三个属性的类型`SqlCommand`，它使用到问题`INSERT`， `UPDATE`，和`DELETE`语句：

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

一个`SqlCommand`对象负责将特定的查询发送到数据库，而且属性，例如： [ `CommandText` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx)，其中包含的临时 SQL 语句或存储的过程来执行; 和[ `Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)，这是一系列`SqlParameter`对象。 返回中可以看到[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程中，这些命令通过属性窗口可以自定义对象。

除了其主查询，TableAdapter 还可以包含数目可变的方法，调用时，调度到的数据库指定的命令。 主查询的命令对象和所有其他方法的命令对象存储在 TableAdapter 的`CommandCollection`属性。

允许 s 花点时间查看生成的代码`ProductsTableAdapter`在`Northwind`这两个属性及其支持的成员变量和帮助器方法的数据集：


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

代码`Adapter`并`CommandCollection`属性精确模拟的`Connection`属性。 有保存的属性使用的对象的成员变量。 属性`Get`访问器首先检查是否有相应的成员变量`Nothing`。 如果是这样，它创建成员变量的实例并将核心分配与命令相关的属性调用初始化方法。

## <a name="step-4-exposing-command-level-settings"></a>步骤 4： 公开命令级别的设置

理想情况下，命令级别信息应保持不封装内数据访问层。 应体系结构的其他层级中需要此信息，但是，它可以通过公开一个分部类，就像使用连接级设置。

因为 TableAdapter 仅具有单个`Connection`属性，用于公开连接级设置的代码是非常简单。 以下事项的更复杂时修改命令级别的设置，因为 TableAdapter 可以有多个命令对象的`InsertCommand`， `UpdateCommand`，并`DeleteCommand`，以及变量中的命令对象数目`CommandCollection`属性。 当更新命令级别的设置，这些设置将需要传播到所有命令对象。

例如，假设已发生的某些查询中所需执行特别长时间的 TableAdapter。 在使用 TableAdapter 执行其中一个查询，我们可能想要增加命令对象 s [ `CommandTimeout`属性](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)。 此属性指定要等待的时间要执行的命令的秒数，默认为 30。

若要允许`CommandTimeout`属性来进行调整的 BLL，添加以下`Public`方法`ProductsDataTable`步骤 2 中使用分部类文件创建 (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`):


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

无法从设置命令的所有问题的命令超时的 BLL 或表示层调用此方法，通过该 TableAdapter 实例。

> [!NOTE]
> `Adapter`并`CommandCollection`属性标记为`Private`，这意味着它们只能访问从 TableAdapter 中的代码。 与不同`Connection`属性，这些访问修饰符不能配置。 因此，如果您需要公开其他层体系结构中的命令级别属性必须使用以提供上文所述的分部类方法`Public`方法或属性，可读取或写入`Private`命令对象。


## <a name="summary"></a>总结

类型化数据集内的 Tableadapter 用于封装数据的访问细节和复杂性。 使用 Tableadapter，我们无需担心如何编写 ADO.NET 代码，以便连接到数据库中，发出命令，或填充到 DataTable 的结果。 它是所有处理自动为我们。

但是，可能是我们需要自定义的低级别的 ADO.NET 细节，例如，更改连接字符串值或默认连接或命令超时值。 TableAdapter 具有自动生成`Connection`， `Adapter`，并`CommandCollection`属性，但这些是`Friend`或`Private`，默认情况下。 可以通过扩展 TableAdapter 使用分部类包含公开此内部信息`Public`方法或属性。 或者，TableAdapter s`Connection`属性访问修饰符可以配置通过 TableAdapter 的`ConnectionModifier`属性。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Burnadette Leigh，S ren Jacob Lauritsen Teresa Murphy 和 Hilton Geisenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](working-with-computed-columns-vb.md)
> [下一页](protecting-connection-strings-and-other-configuration-information-vb.md)
