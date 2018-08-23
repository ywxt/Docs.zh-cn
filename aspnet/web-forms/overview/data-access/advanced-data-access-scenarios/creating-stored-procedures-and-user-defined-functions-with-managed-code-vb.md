---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: 创建存储的过程和用户定义函数使用托管代码 (VB) |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 与.NET 公共语言运行时以允许开发人员能够创建通过托管代码的数据库对象。 本教程...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 438ebfa474ab510d90738c4a3ee40e172d838dcb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834536"
---
<a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>创建存储过程和用户定义函数使用托管代码 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip)或[下载 PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 与.NET 公共语言运行时以允许开发人员能够创建通过托管代码的数据库对象。 本教程演示如何创建托管存储的过程，并托管在 Visual Basic 或 C# 代码与用户定义函数。 我们还看到这些版本的 Visual Studio 如何使你能够调试此类托管的数据库对象。


## <a name="introduction"></a>介绍

使用如 Microsoft 的 SQL Server 2005 的数据库[Transact-Structured 查询语言 (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL)插入、 修改和检索数据。 大多数数据库系统包括进行分组的一系列然后可作为单个可重用单元执行的 SQL 语句的构造。 存储的过程是一个示例。 另一个是*用户定义的函数*(Udf)，我们将在步骤 9 中的更详细地检查的构造。

在其核心而言，SQL 专为处理的数据集。 `SELECT`， `UPDATE`，并`DELETE`语句本质上是应用于相应的表中的所有记录，并仅受到其`WHERE`子句。 然而，存在着许多语言功能，旨在用于一次处理一条记录，并用于标量数据进行操作。 [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553)允许的一组记录进行循环通过一次一个。 字符串操作函数，如`LEFT`， `CHARINDEX`，和`PATINDEX`和标量数据一起工作。 SQL 还包括控制流语句，如`IF`和`WHILE`。

在 Microsoft SQL Server 2005 之前, 存储的过程和 Udf 无法只能定义为一个 T-SQL 语句的集合。 SQL Server 2005 中，但是，旨在提供与集成[公共语言运行时 (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)，这是所有.NET 程序集都使用的运行时。 因此，存储的过程和 SQL Server 2005 数据库中的 Udf 可以创建使用托管的代码。 也就是说，可以为方法在 Visual Basic 类中创建存储的过程或 UDF。 这样，这些存储的过程和 Udf 以利用.NET Framework 中并从您自己的自定义类的功能。

在本教程中我们将说明如何创建托管存储过程和用户定义的函数以及如何将其集成到我们的 Northwind 数据库。 让我们来开始 ！

> [!NOTE]
> 托管的数据库对象提供了通过 SQL 对应的一些好处。 语言丰富性和熟悉程度和能够重复使用现有的代码和逻辑的主要优势。 但托管的数据库对象，可能需要使用不涉及多过程逻辑的数据集时效率较低。 有关使用与 T-SQL 的托管的代码的优点的更全面讨论，请参阅[优点的使用托管代码创建数据库对象](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)。


## <a name="step-1-moving-the-northwind-database-out-ofappdata"></a>步骤 1： 移动的 Northwind 数据库`App_Data`

所有我们的教程到目前为止都使用 Microsoft SQL Server 2005 Express Edition 数据库文件中的 web 应用程序的`App_Data`文件夹。 将数据库中的放置`App_Data`简化分发和运行这些教程中的所有文件已位于一个目录和任何其他配置步骤来测试本教程所需的。

但是，对于本教程，让 s 移动共 Northwind 数据库`App_Data`并显式将其注册使用 SQL Server 2005 Express Edition 数据库实例。 虽然我们可以在本教程中的数据库执行的步骤`App_Data`文件夹中，多个步骤都要简单得多的显式注册数据库，使用 SQL Server 2005 Express Edition 数据库实例。

本教程中下载具有两个数据库文件-`NORTHWND.MDF`并`NORTHWND_log.LDF`-放置在名为的文件夹`DataFiles`。 如果您以及您自己的实现的教程，关闭 Visual Studio 和移动`NORTHWND.MDF`和`NORTHWND_log.LDF`文件从网站的`App_Data`到外部网站的文件夹的文件夹。 数据库文件已移到另一个文件夹后，我们需要注册 Northwind 数据库使用 SQL Server 2005 Express Edition 数据库实例。 这可以从 SQL Server Management Studio。 如果有非-Express Edition 的 SQL Server 2005 计算机上安装然后可能已经安装的 Management Studio。 如果仅在计算机上安装 SQL Server 2005 Express Edition，则请花费片刻时间来下载并安装[Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

启动 SQL Server Management Studio。 如图 1 所示，Management Studio 首先会询问要连接到的服务器。 输入 localhost\SQLExpress 作为服务器名称，在身份验证下拉列表中，选择 Windows 身份验证并单击连接。


![连接到相应的数据库实例](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**图 1**： 连接到相应的数据库实例


你已连接后，对象资源管理器窗口将列出有关 SQL Server 2005 Express Edition 数据库实例，包括数据库、 安全信息、 管理选项和等的信息。

我们需要将附加 Northwind 数据库中的`DataFiles`文件夹 （或任何位置你可能已移） 到 SQL Server 2005 Express Edition 数据库实例。 右键单击数据库文件夹并从上下文菜单中选择的附加选项。 此时会弹出附加数据库对话框。 单击添加按钮，向下钻取到相应`NORTHWND.MDF`文件，然后单击确定。 此时您的屏幕应类似于图 2。


[![连接到相应的数据库实例](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**图 2**： 连接到相应的数据库实例 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png))


> [!NOTE]
> 当连接到 SQL Server 2005 Express Edition 实例通过 Management Studio 附加数据库对话框中不允许您向下钻取到用户配置文件目录，如我的文档。 因此，请确保放置`NORTHWND.MDF`和`NORTHWND_log.LDF`非用户配置文件目录中的文件。


单击确定按钮附加该数据库。 附加数据库对话框将关闭，并且在对象资源管理器现在应列出的只是附加的数据库。 您很可能的 Northwind 数据库具有一个名称，如`9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`。 通过右键单击数据库，然后选择重命名数据库重命名为 Northwind。


![数据库重命名为 Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**图 3**: 数据库重命名为 Northwind


## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>步骤 2： 在 Visual Studio 中创建一个新解决方案和 SQL Server 项目

若要在 SQL Server 2005 中创建托管存储的过程或 Udf 我们将作为在类中的 Visual Basic 代码中编写的存储的过程和 UDF 逻辑。 一旦已编写代码，我们将需要此类编译为程序集 (`.dll`文件)，注册该程序集与 SQL Server 数据库，并指向中的相应方法在数据库中创建的存储的过程或 UDF 对象程序集。 这些步骤可以所有手动执行。 我们可以在任何文本编辑器创建代码，从命令行使用 Visual Basic 编译器对其进行编译 (`vbc.exe`)，注册该数据库使用[ `CREATE ASSEMBLY` ](https://msdn.microsoft.com/library/ms189524.aspx)命令或从 Management Studio 中，并添加存储过程或 UDF 对象通过类似的方式。 幸运的是，Visual Studio Professional 和 Team 系统版本包括一个 SQL Server 项目类型，可以自动执行这些任务。 在本教程中我们将引导完成使用 SQL Server 项目类型以创建托管存储的过程和 UDF。

> [!NOTE]
> 如果使用 Visual Web Developer 或 Visual Studio Standard edition，您将需要改为使用手动方法。 步骤 13 中提供了有关手动执行这些步骤的详细的说明。 我鼓励您之前需要阅读的步骤 2 到 12 读取第 13 步，因为这些步骤包括重要必须应用无论使用哪个版本的 Visual Studio 的 SQL Server 配置说明。


首先打开 Visual Studio。 从文件菜单中，选择要显示新建项目对话框中的新项目框 （请参阅图 4）。 深化到数据库项目类型，然后，从右侧列出模板中选择要创建新的 SQL Server 项目。 我已选择此项目命名为`ManagedDatabaseConstructs`并放在名为的解决方案内`Tutorial75`。


[![创建新的 SQL Server 项目](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**图 4**： 创建新的 SQL Server 项目 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))


单击新建项目对话框中，创建解决方案和 SQL Server 项目中的确定按钮。

SQL Server 项目绑定到特定数据库。 因此，在创建新的 SQL Server 项目后我们会立即要求指定此信息。 图 5 显示了已填写为指向我们在步骤 1 中返回的 SQL Server 2005 Express Edition 数据库实例中注册的 Northwind 数据库的新数据库引用对话框。


![将 SQL Server 项目与 Northwind 数据库相关联](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**图 5**： 将 SQL Server 项目与 Northwind 数据库相关联


若要调试的托管存储的过程和 Udf，我们将创建此项目中，我们需要启用 SQL/CLR 调试连接支持。 每当将 SQL Server 项目将与新的数据库相关联 （就像我们一样在图 5） 时，Visual Studio 会询问我们是否我们想要启用 SQL/CLR 调试连接上 （请参阅图 6）。 单击是。


![启用 SQL/CLR 调试](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**图 6**： 启用 SQL/CLR 调试


此时新的 SQL Server 项目具有已添加到解决方案。 它包含名为的文件夹`Test Scripts`与名为的文件`Test.sql`，用于调试的项目中创建的托管的数据库对象。 我们将介绍在步骤 12 中进行调试。

我们现在可以向此项目中，添加新的托管存储的过程和 Udf，但好让我们之前首先包括现有的 web 应用程序解决方案中。 从文件菜单选择添加选项并选择现有网站。 浏览到相应的网站文件夹并单击确定。 如图 7 所示，这会更新以包括两个项目的解决方案： 在网站和`ManagedDatabaseConstructs`SQL Server 项目。


![在解决方案资源管理器现在包括两个项目](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**图 7**： 解决方案资源管理器现在包括两个项目


`NORTHWNDConnectionString`中的值`Web.config`当前引用`NORTHWND.MDF`文件中`App_Data`文件夹。 由于已删除此数据库从`App_Data`和显式注册在 SQL Server 2005 Express Edition 数据库实例中，我们需要相应地更新`NORTHWNDConnectionString`值。 打开`Web.config`文件中的网站和更改`NORTHWNDConnectionString`值，以便连接字符串中读取： `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`。 此更改后你`<connectionStrings>`主题中`Web.config`应如下所示：


[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> 如中所述[前面的教程](debugging-stored-procedures-vb.md)，当调试 SQL Server 对象从客户端应用程序，如 ASP.NET 网站，我们需要禁用连接池。 如上所示的连接字符串禁用连接池 ( `Pooling=false` )。 如果您不打算从 ASP.NET 网站中调试托管存储的过程和 Udf，启用连接池。


## <a name="step-3-creating-a-managed-stored-procedure"></a>步骤 3： 创建托管的存储过程

若要将托管的存储的过程添加到 Northwind 数据库我们首先需要创建存储的过程作为 SQL Server 项目中的方法。 从解决方案资源管理器，右键单击`ManagedDatabaseConstructs`项目名称，然后选择要添加新项。 这将显示添加新项对话框中，列出了可以添加到项目的托管的数据库对象的类型。 如图 8 所示，这包括的其他项中存储的过程和用户定义函数。

让我们来添加存储的过程只需返回所有已停用的产品。 将新的存储的过程文件`GetDiscontinuedProducts.vb`。


[![添加新的存储的过程名为 GetDiscontinuedProducts.vb](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**图 8**： 添加新存储过程名为`GetDiscontinuedProducts.vb`([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png))


这将创建新的 Visual Basic 类文件包含以下内容：


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

请注意，作为实现存储的过程`Shared`方法内的`Partial`名为的类文件`StoredProcedures`。 此外，`GetDiscontinuedProducts`方法用修饰[`SqlProcedure`属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx)，表示将标记作为存储过程的方法。

下面的代码创建`SqlCommand`对象并设置其`CommandText`到`SELECT`返回所有的各列的查询`Products`表中的产品`Discontinued`字段等于 1。 然后执行命令，并将结果发送回客户端应用程序。 添加到此代码`GetDiscontinuedProducts`方法。


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

所有托管的数据库对象都有权访问[`SqlContext`对象](https://msdn.microsoft.com/library/ms131108.aspx)表示调用方的上下文。 `SqlContext`提供对访问[`SqlPipe`对象](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)通过其[`Pipe`属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)。 这`SqlPipe`对象用于在 SQL Server 数据库和调用应用程序之间 ferry 信息。 正如其名， [ `ExecuteAndSend`方法](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)执行传入的`SqlCommand`对象，并将结果返回到客户端应用程序。

> [!NOTE]
> 托管的数据库对象非常适合于存储的过程和 Udf 使用过程逻辑，而不是基于集的逻辑。 过程逻辑包括在行的行的基础上使用的数据集或使用标量数据。 `GetDiscontinuedProducts`我们只需创建的方法，但是，涉及到任何过程逻辑。 因此，它会在理想情况下实现作为 T-SQL 存储过程。 它被实现为托管的存储的过程来演示用于创建和部署所必需的步骤托管存储的过程。


## <a name="step-4-deploying-the-managed-stored-procedure"></a>步骤 4： 部署的托管存储过程

使用此完整的代码，我们已做好将其部署到 Northwind 数据库。 部署 SQL Server 项目将代码编译为程序集、 数据库后，注册该程序集和在数据库中，将其链接到程序集中适当的方法创建相应的对象。 更确切地说步骤 13 中拼确切的一组任务执行的部署选项。 右键单击`ManagedDatabaseConstructs`项目在解决方案资源管理器的名称，然后选择部署选项。 但是，部署将失败并出现以下错误: 外部附近有语法错误。 您可能需要将当前数据库的兼容性级别设置为更高版本的值，以启用此功能。 请参阅为存储过程的帮助`sp_dbcmptlevel`。

尝试对 Northwind 数据库中注册该程序集时，将出现此错误消息。 若要注册程序集与 SQL Server 2005 数据库，数据库 s 兼容性级别必须设置为 90。 默认情况下，新的 SQL Server 2005 数据库具有兼容性级别为 90。 但是，使用 Microsoft SQL Server 2000 创建的数据库具有默认兼容级别为 80。 Northwind 数据库最初是 Microsoft SQL Server 2000 数据库，因为其兼容性级别当前设置为 80，因此需要增加为 90 以便注册托管的数据库对象。

若要更新数据库 s 兼容性级别，请在 Management Studio 中打开一个新查询窗口并输入：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

单击以运行上述查询中的执行图标。


[![更新 Northwind 数据库 s 兼容性级别](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**图 9**： 更新 Northwind 数据库 s 兼容性级别 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png))


在更新后的兼容性级别，重新部署 SQL Server 项目。 这一次部署应完成不会出错。

返回到 SQL Server Management Studio，Northwind 数据库中对象资源管理器，右键单击并选择刷新。 接下来，向下钻取到可编程性文件夹，然后展开程序集文件夹。 如图 10 所示，Northwind 数据库现在包括生成的程序集`ManagedDatabaseConstructs`项目。


![ManagedDatabaseConstructs 程序集是 Northwind 数据库中现在注册](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**图 10**:`ManagedDatabaseConstructs`程序集是 Northwind 数据库中现在注册


此外扩展存储过程文件夹。 你将看到一个名为的存储的过程`GetDiscontinuedProducts`。 此存储的过程已通过的部署过程和指向`GetDiscontinuedProducts`中的方法`ManagedDatabaseConstructs`程序集。 当`GetDiscontinuedProducts`执行存储的过程时，它，将依次执行`GetDiscontinuedProducts`方法。 由于这是托管存储的过程不能编辑它通过 Management Studio (因此存储的过程名称旁边的锁定图标)。


![GetDiscontinuedProducts 存储过程列出存储过程文件夹中](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**图 11**:`GetDiscontinuedProducts`存储过程文件夹中列出的存储过程


还有一个要克服前我们可以调用托管存储的过程的多个障碍： 数据库配置为阻止托管代码的执行。 通过打开新查询窗口并执行对此进行验证`GetDiscontinuedProducts`存储过程。 你将收到以下错误消息： 已禁用的.NET Framework 中的用户代码的执行。 启用 clr 已启用配置选项。

若要检查的 Northwind 数据库的配置信息、 输入和执行命令`exec sp_configure`在查询窗口中。 这将显示 clr 已启用设置当前设置为 0。


[![Clr 已启用设置是当前设置为 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**图 12**: clr 已启用设置是当前设置为 0 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png))


请注意，图 12 中的每个配置设置都有与其一起列出的四个值： 所需的最低和最大值的配置和运行的值。 若要更新 clr 已启用设置的配置值，请执行以下命令：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

如果重新运行`exec sp_configure`你将看到，上述语句更新 clr 已启用设置的配置值为 1，但仍将运行的值设置为 0。 我们需要执行此配置更改生效[`RECONFIGURE`命令](https://msdn.microsoft.com/library/ms176069.aspx)，它将运行的值设置为当前的配置值。 只需输入`RECONFIGURE`在查询窗口中，单击工具栏中的执行图标。 如果您运行`exec sp_configure`现在应看到 clr 已启用设置的配置的 1 的值并运行值。

使用完整 clr 已启用配置时，我们已准备好运行的托管`GetDiscontinuedProducts`存储过程。 在查询窗口中输入并执行命令`exec` `GetDiscontinuedProducts`。 调用存储的过程会导致相应的托管的代码中`GetDiscontinuedProducts`要执行的方法。 此代码发出`SELECT`查询以返回已不再使用并返回到调用应用程序，这是此实例中的 SQL Server Management Studio 的此数据的所有产品。 Management Studio 收到这些结果，并在结果窗口中显示它们。


[![存储的过程将返回所有 GetDiscontinuedProducts 废止产品](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**图 13**:`GetDiscontinuedProducts`存储过程返回所有废止产品 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png))


## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>步骤 5： 创建托管存储过程接受输入的参数

查询和我们已在这些教程创建的存储的过程的许多用*参数*。 例如，在[创建新存储过程的类型化数据集 s Tableadapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程中，我们创建一个名为的存储的过程`GetProductsByCategoryID`接受输入的参数名为`@CategoryID`。 存储的过程，则返回所有产品的`CategoryID`字段与所提供的值匹配`@CategoryID`参数。

若要创建托管的存储的过程接受输入的参数，只需在 s 方法定义中指定这些参数。 若要说明这一点，让 s，将添加到另一个托管存储的过程`ManagedDatabaseConstructs`名为项目`GetProductsWithPriceLessThan`。 此托管的存储的过程将接受输入的参数指定价格，并将返回所有产品的`UnitPrice`字段小于参数的值。

若要将新的存储的过程添加到项目中，右键单击`ManagedDatabaseConstructs`项目名称，然后选择要添加新的存储的过程。 为 `GetProductsWithPriceLessThan.vb` 文件命名。 正如我们在步骤 3 中看到的这将使用一个名为方法创建新的 Visual Basic 类文件`GetProductsWithPriceLessThan`放在`Partial`类`StoredProcedures`。

更新`GetProductsWithPriceLessThan`s 方法定义，以便它可以接受[ `SqlMoney` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx)名为输入的参数`price`和编写代码来执行并返回查询结果：


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan` S 方法定义和代码非常相似的定义和代码`GetDiscontinuedProducts`步骤 3 中创建的方法。 唯一的区别是`GetProductsWithPriceLessThan`方法接受作为输入参数 (`price`)，则`SqlCommand`s 查询包含一个参数 (`@MaxPrice`)，并将参数添加到`SqlCommand`s`Parameters`集合是和分配的值`price`变量。

添加此代码后，重新部署 SQL Server 项目。 接下来，返回到 SQL Server Management Studio 并刷新存储过程文件夹。 您应看到一个新条目， `GetProductsWithPriceLessThan`。 从查询窗口中，输入并执行该命令`exec GetProductsWithPriceLessThan 25`，后者将列表小于 25 美元，所有产品，如图 14 所示。


[![显示产品下 25 美元](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**图 14**： 显示产品下 25 美元 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png))


## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>步骤 6： 从数据访问层中调用托管存储的过程

现在我们已添加`GetDiscontinuedProducts`并`GetProductsWithPriceLessThan`托管存储的过程来`ManagedDatabaseConstructs`项目，并具有与 Northwind SQL Server 数据库中注册它们。 我们还需要调用这些托管存储的过程从 SQL Server Management Studio （请参阅图 13 和 14）。 为了使我们的 ASP.NET 应用程序以使用这些托管存储的过程，但是，我们需要将它们添加到数据访问和业务逻辑层体系结构中。 在此步骤中，我们将添加到两个新方法`ProductsTableAdapter`中`NorthwindWithSprocs`类型的数据集在最初创建[创建新存储过程的类型化数据集 s Tableadapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程。 在步骤 7 中我们将在 BLL 中添加相应的方法。

打开`NorthwindWithSprocs`类型在 Visual Studio 并开始通过添加到新的方法中的数据集`ProductsTableAdapter`名为`GetDiscontinuedProducts`。 若要将新方法添加到 TableAdapter，TableAdapter s 名称在设计器中右键单击并从上下文菜单中选择添加查询选项。

> [!NOTE]
> 自迁移后从 Northwind 数据库`App_Data`到 SQL Server 2005 Express Edition 数据库实例的文件夹，则必须在 Web.config 中相应的连接字符串进行更新以反映此更改。 在步骤 2 中，我们讨论更新`NORTHWNDConnectionString`中的值`Web.config`。 如果您忘记了此更新，你将看到要添加查询的错误消息失败。 找不到连接`NORTHWNDConnectionString`对象`Web.config`对话框时尝试将新方法添加到 TableAdapter 中。 若要解决此错误，单击确定，然后转到`Web.config`并更新`NORTHWNDConnectionString`值在步骤 2 中所述。 然后尝试重新添加到 TableAdapter 的方法。 这次它应工作正常。


添加新方法将启动 TableAdapter 查询配置向导中，我们有很多时间在过去的教程中使用。 第一步会要求我们指定 TableAdapter 应如何访问数据库： 通过临时 SQL 语句或通过新的或现有的存储过程。 由于我们已经创建并注册`GetDiscontinuedProducts`托管存储的过程与数据库中，选择使用现有存储过程选项并按下一步。


[![选择使用现有存储的过程选项](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**图 15**： 选择使用现有存储过程选项 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png))


下一个屏幕提示我们输入方法将调用该存储过程。 选择`GetDiscontinuedProducts`托管存储的过程，从下拉列表并按下一步。


[![选择 GetDiscontinuedProducts 托管存储的过程](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**图 16**： 选择`GetDiscontinuedProducts`托管存储过程 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png))


我们然后会要求指定存储的过程返回的行、 单个值，或执行任何操作。 由于`GetDiscontinuedProducts`返回集的已中止的产品行，选择第一个选项 （表格数据），然后单击下一步。


[![选择表格数据选项](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**图 17**： 选择表格的数据选项 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png))


最后一个向导屏幕可以指定使用的数据访问模式和生成的方法的名称。 将选中的复选框和名称保留方法`FillByDiscontinued`和`GetDiscontinuedProducts`。 单击完成以完成向导。


[![名称方法 FillByDiscontinued 和 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**图 18**： 命名方法`FillByDiscontinued`并`GetDiscontinuedProducts`([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))


重复上述步骤，创建名为的方法`FillByPriceLessThan`并`GetProductsWithPriceLessThan`中`ProductsTableAdapter`为`GetProductsWithPriceLessThan`托管存储的过程。

图 19 显示了添加到方法后的数据集设计器的屏幕截图`ProductsTableAdapter`有关`GetDiscontinuedProducts`和`GetProductsWithPriceLessThan`的托管存储的过程。


[![ProductsTableAdapter 包括在此步骤中添加了新方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**图 19**:`ProductsTableAdapter`包括在此步骤中的添加新方法 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png))


## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>步骤 7： 将相应的方法添加到业务逻辑层

现在，我们已更新数据访问层，以便包括调用在步骤 4 和 5 中添加托管存储的过程的方法，我们需要将相应的方法添加到业务逻辑层。 添加到以下两种方法`ProductsBLLWithSprocs`类：


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

这两种方法是调用相应的 DAL 方法并返回`ProductsDataTable`实例。 `DataObjectMethodAttribute`标记每个方法会导致这些方法包含在 ObjectDataSource s 配置数据源向导的选择选项卡中的下拉列表中。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>步骤 8： 调用的托管存储过程从表示层

与业务逻辑和数据访问层扩充，以包括对调用的支持`GetDiscontinuedProducts`和`GetProductsWithPriceLessThan`的托管存储的过程，我们现在可以显示这些存储过程通过 ASP.NET 页面的结果。

打开`ManagedFunctionsAndSprocs.aspx`页中`AdvancedDAL`文件夹并从工具箱将 GridView 拖到设计器。 设置 GridView s`ID`属性设置为`DiscontinuedProducts`并从其智能标记，请将其绑定到名为新 ObjectDataSource `DiscontinuedProductsDataSource`。 配置对象数据源以提取其数据从`ProductsBLLWithSprocs`类的`GetDiscontinuedProducts`方法。


[![配置对象数据源以使用 ProductsBLLWithSprocs 类](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**图 20**： 配置为使用 ObjectDataSource`ProductsBLLWithSprocs`类 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png))


[![从下拉列表中选择的选项卡选择 GetDiscontinuedProducts 方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**图 21**： 选择`GetDiscontinuedProducts`从选择选项卡中的下拉列表的方法 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png))


将用于此网格将仅显示产品的信息，因为设置下拉列表中插入、 更新和删除选项卡添加到 （无），然后单击完成。

完成该向导，时 Visual Studio 将自动添加 BoundField 或 CheckBoxField 中每个数据字段`ProductsDataTable`。 请花费片刻时间来删除所有这些字段除外`ProductName`和`Discontinued`、 的点在 GridView 和 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

请花费片刻时间来查看此页上的通过浏览器。 访问页面时，ObjectDataSource 调用`ProductsBLLWithSprocs`类的`GetDiscontinuedProducts`方法。 步骤 7 中可以看到，此方法调用向下为 DAL s`ProductsDataTable`类 s`GetDiscontinuedProducts`方法，调用`GetDiscontinuedProducts`存储过程。 此存储的过程是在托管的存储过程和执行我们在步骤 3 中，返回停产的产品中创建的代码。

托管存储过程返回的结果被打包成`ProductsDataTable`dal 然后返回到的 BLL，然后将其返回到表示层其中绑定到 GridView 并显示它们。 按预期运行，则网格将列出已停止使用这些产品。


[![列出了停止使用的产品](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**图 22**： 列出了停止使用的产品 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png))


为进一步操作，向页面添加一个文本框和另一个 GridView。 具有此 GridView 显示产品小于输入到 TextBox，通过调用金额`ProductsBLLWithSprocs`类的`GetProductsWithPriceLessThan`方法。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>步骤 9： 创建和调用 T-SQL 的 Udf

用户定义的函数或 Udf，即数据库对象逼真地模仿编程语言中的函数的语义。 在 Visual Basic 中的函数，如 Udf 可包含数目可变的输入参数并返回特定类型的值。 UDF 可以返回标量数据-字符串、 整数和等的或表格数据。 让我们来快速看一下 Udf，UDF 将返回标量数据类型从这两种类型。

以下 UDF 计算特定产品的库存的估计的值。 它会在三个输入参数的取`UnitPrice`， `UnitsInStock`，并`Discontinued`某一特定产品的值，并返回类型的值`money`。 它将计算库存估计的值乘以`UnitPrice`通过`UnitsInStock`。 对于已停止使用的项，此值是缩减了一半。


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

此 UDF 添加到数据库后，它可以通过展开可编程性文件夹，然后函数，然后的标量值函数来找到通过 Management Studio。 可在`SELECT`查询如下所示：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

我已添加`udf_ComputeInventoryValue`到 Northwind 数据库中; UDF图 23 显示上述输出`SELECT`时通过 Management Studio 查看查询。 另请注意对象资源管理器中的标量值函数文件夹下列出了 UDF。


[![列出每个产品的清单值](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**图 23**： 每个产品 s 列出清单值 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png))


Udf 还可以返回表格数据。 例如，我们可以创建返回属于特定类别的产品的 UDF:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID` UDF 接受`@CategoryID`输入的参数并指定将结果返回`SELECT`查询。 创建后，可以在引用此 UDF `FROM` (或`JOIN`) 的子句`SELECT`查询。 下面的示例将返回`ProductID`， `ProductName`，和`CategoryID`饮料的每个值。


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

我已添加`udf_GetProductsByCategoryID`到 Northwind 数据库中; UDF图 24 显示上述输出`SELECT`时通过 Management Studio 查看查询。 可以在对象资源管理器的表值函数文件夹中找到返回表格数据的 Udf。


[![产品 id、 产品名称和类别 Id 列出的每个饮料](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**图 24**: `ProductID`， `ProductName`，和`CategoryID`列出的每个饮料 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png))


> [!NOTE]
> 有关创建和使用 Udf 的详细信息，请参阅[用户定义的函数对简介](http://www.sqlteam.com/item.asp?ItemID=1955)。 另请参阅[优点和 Drawbacks of User-Defined 函数](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)。


## <a name="step-10-creating-a-managed-udf"></a>步骤 10： 创建一个托管的 UDF

`udf_ComputeInventoryValue`和`udf_GetProductsByCategoryID`上面的示例中创建的 Udf 是 T-SQL 的数据库对象。 SQL Server 2005 还支持托管的 Udf，可以添加到`ManagedDatabaseConstructs`项目就像托管存储过程从步骤 3 和 5。 对于此步骤，让我们来实现`udf_ComputeInventoryValue`在托管代码中的 UDF。

若要添加到一个托管的 UDF`ManagedDatabaseConstructs`项目，右键单击解决方案资源管理器中的项目名称并选择要添加新项。 从添加新项对话框中选择用户定义模板，然后将新的 UDF 文件`udf_ComputeInventoryValue_Managed.vb`。


[![将新的托管的 UDF 添加到 ManagedDatabaseConstructs 项目](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**图 25**： 添加到新的托管 UDF`ManagedDatabaseConstructs`项目 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png))


用户定义的函数模板创建`Partial`名为类`UserDefinedFunctions`使用方法： 名称为类文件的名称相同 (`udf_ComputeInventoryValue_Managed`，在这种情况)。 此方法使用修饰[`SqlFunction`属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)，该标记作为一个托管 UDF 方法。


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

`udf_ComputeInventoryValue`方法当前返回[`SqlString`对象](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)并且不接受任何输入参数。 我们需要更新，使它接受三个输入参数的方法定义`UnitPrice`， `UnitsInStock`，并`Discontinued`-并返回`SqlMoney`对象。 逻辑以用于计算的库存值等同于在 T-SQL 中`udf_ComputeInventoryValue`UDF。


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

请注意，UDF 的方法输入的参数是其相应 SQL 类型的：`SqlMoney`有关`UnitPrice`字段中， [ `SqlInt16` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx)有关`UnitsInStock`，以及[ `SqlBoolean` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx)有关`Discontinued`。 这些数据类型反映中定义的类型`Products`表：`UnitPrice`列的类型是`money`，则`UnitsInStock`类型的列`smallint`，并且`Discontinued`类型的列`bit`。

代码首先创建`SqlMoney`实例名为`inventoryValue`分配值为 0。 `Products` Table 允许使用的数据库`NULL`中的值`UnitsInPrice`和`UnitsInStock`列。 因此，我们需要先检查，查阅这些值是否包含`NULL`s，我们通过执行此操作`SqlMoney`对象 s [ `IsNull`属性](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)。 如果这两个`UnitPrice`并`UnitsInStock`包含非`NULL`值，则我们计算`inventoryValue`为两个产品。 然后，如果`Discontinued`为 true，则我们四倍值。

> [!NOTE]
> `SqlMoney`对象只允许两个`SqlMoney`实例一起相乘。 它不允许`SqlMoney`实例要乘以的文字的浮点数。 因此，若要四倍`inventoryValue`我们将其由一个新`SqlMoney`具有值 0.5 的实例。


## <a name="step-11-deploying-the-managed-udf"></a>步骤 11： 部署托管的 UDF

现在，已创建托管的 UDF，我们已准备好将其部署到 Northwind 数据库。 正如我们看到在步骤 4 中，通过右键单击解决方案资源管理器中的项目名称并从上下文菜单中选择部署选项部署 SQL Server 项目中的托管的对象。

一旦部署了项目后，返回到 SQL Server Management Studio 并刷新标量值函数文件夹。 现在应看到两个条目：

- `dbo.udf_ComputeInventoryValue` -在步骤 9 中创建的 T-SQL 的 UDF 和
- `dbo.udf ComputeInventoryValue_Managed` -在刚才部署的步骤 10 中创建托管的 UDF。

若要测试此托管的 UDF，请执行以下查询从 Management Studio 中：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

此命令使用的托管`udf ComputeInventoryValue_Managed`而不是 T-SQL 的 UDF `udf_ComputeInventoryValue` UDF，但输出是相同。 回顾图 23，若要查看的 UDF 的输出屏幕截图。

## <a name="step-12-debugging-the-managed-database-objects"></a>步骤 12： 调试托管的数据库对象

在中[调试存储过程](debugging-stored-procedures-vb.md)调试通过 Visual Studio 的 SQL Server 教程中，我们讨论了这三个选项： 直接数据库调试、 应用程序调试和从 SQL Server 项目的调试。 托管的数据库对象不能通过直接数据库调试调试，但可以进行调试，从客户端应用程序和直接从 SQL Server 项目。 为了使调试工作，但是，SQL Server 2005 数据库必须允许 SQL/CLR 调试。 回想一下，我们首次创建时`ManagedDatabaseConstructs`Visual Studio 要求我们是否我们想要启用 SQL/CLR 调试 （见图 6 在步骤 2 中） 的项目。 可以通过右键单击服务器资源管理器窗口中的数据库修改此设置。


![请确保数据库允许 SQL/CLR 调试](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**图 26**： 请确保数据库允许 SQL/CLR 调试


假设我们想要调试`GetProductsWithPriceLessThan`托管存储的过程。 我们将首先设置断点的代码中`GetProductsWithPriceLessThan`方法。


[![GetProductsWithPriceLessThan 方法中设置断点](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**图 27**： 中设置断点`GetProductsWithPriceLessThan`方法 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png))


让我们来首先看一下调试 SQL Server 项目中的托管的数据库对象。 由于我们的解决方案包括两个项目- `ManagedDatabaseConstructs` SQL Server 项目，以及我们的网站的我们需要指示 Visual Studio 启动 SQL Server 项目中调试`ManagedDatabaseConstructs`我们开始调试时的 SQL Server 项目。 右键单击`ManagedDatabaseConstructs`项目在解决方案资源管理器中，并为启动项目选项，从上下文菜单选择集。

当`ManagedDatabaseConstructs`从执行 SQL 语句在调试器中启动项目`Test.sql`文件，它位于`Test Scripts`文件夹。 例如，若要测试`GetProductsWithPriceLessThan`托管存储的过程替换现有`Test.sql`文件内容与以下语句，将调用`GetProductsWithPriceLessThan`托管存储的过程中传递`@CategoryID`14.95 的值：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

你已输入到上述脚本后`Test.sql`、 开始通过转到调试菜单并选择开始调试，或通过点击 F5 调试或在工具栏中的绿色播放图标。 这将生成解决方案中的项目、 对 Northwind 数据库中，部署托管的数据库对象，然后执行`Test.sql`脚本。 此时，将命中断点，然后我们可以单步执行`GetProductsWithPriceLessThan`方法，检查输入参数的值等。


[![点击 GetProductsWithPriceLessThan 方法中的断点](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**图 28**： 中的断点`GetProductsWithPriceLessThan`命中方法 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png))


为了使 SQL 数据库对象调试通过客户端应用程序，则必须将数据库配置为支持应用程序进行调试。 右键单击服务器资源管理器中的数据库，并确保选中应用程序调试选项。 此外，我们需要配置 ASP.NET 应用程序将与 SQL 调试器集成并禁用连接池。 以下步骤所述的步骤 2 中的详细信息[调试存储过程](debugging-stored-procedures-vb.md)教程。

配置 ASP.NET 应用程序和数据库后，将 ASP.NET 网站设置为启动项目并启动调试。 如果访问页，可调用其中一个包含断点的托管对象，该应用程序将暂停，并且控件将会移交给调试程序，其中你可以逐句通过代码图 28 中所示。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>步骤 13： 手动编译和部署托管数据库对象

SQL Server 项目轻松地创建、 编译和部署托管的数据库对象。 遗憾的是，SQL Server 项目才可用于 Visual Studio Professional 和 Team 系统版本。 如果您使用的 Visual Web Developer 或标准版的 Visual Studio，并想要使用托管的数据库对象，将需要手动创建并部署它们。 这涉及到四个步骤：

1. 创建包含托管的数据库对象的源代码文件
2. 编译为程序集，该对象
3. SQL Server 2005 数据库后，注册该程序集和
4. 指向在程序集中的相应方法的 SQL Server 中创建的数据库对象。

若要演示这些任务，让我们来创建新托管存储的过程将返回这些产品的`UnitPrice`大于指定值。 创建名为你计算机上的新文件`GetProductsWithPriceGreaterThan.vb`和文件中输入下面的代码 （您可以使用 Visual Studio、 记事本或任何文本编辑器来实现此目的）：


[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

此代码是几乎完全相同的`GetProductsWithPriceLessThan`步骤 5 中创建的方法。 唯一的区别是方法名称`WHERE`子句，并在查询中使用的参数名称。 回到`GetProductsWithPriceLessThan`方法，`WHERE`子句读取： `WHERE UnitPrice < @MaxPrice`。 此处，请在`GetProductsWithPriceGreaterThan`，我们使用： `WHERE UnitPrice > @MinPrice` 。

现在，我们需要此类编译为程序集。 从命令行中，导航到保存位置的目录`GetProductsWithPriceGreaterThan.vb`文件，并使用 C# 编译器 (`csc.exe`) 若要将类文件编译到程序集：


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

如果包含 v 的文件夹`bc.exe`中不在系统 s `PATH`，需要将完全引用其路径`%WINDOWS%\Microsoft.NET\Framework\version\`，如下所示：


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]


[![GetProductsWithPriceGreaterThan.vb 编译为程序集](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**图 29**： 编译`GetProductsWithPriceGreaterThan.vb`到程序集 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png))


`/t`标志指定 Visual Basic 类文件，应编译为 DLL （而非可执行文件）。 `/out`标志指定生成的程序集的名称。

> [!NOTE]
> 而不是编译`GetProductsWithPriceGreaterThan.vb`从命令行或者，可以使用的类文件[Visual Basic 速成版](https://msdn.microsoft.com/vstudio/express/vb/)或在 Visual Studio Standard Edition 中创建一个单独的类库项目。 S ren Jacob Lauritsen 请先将其提供的代码具有此类的 Visual Basic 速成版项目`GetProductsWithPriceGreaterThan`存储的过程和两个托管存储的过程和步骤 3、 5 和 10 中创建的 UDF。 S ren s 项目还包括添加相应的数据库对象所需的 T-SQL 命令。


代码编译到程序集中，我们已准备好注册 SQL Server 2005 数据库中的程序集。 这可以通过 T-SQL，使用该命令执行`CREATE ASSEMBLY`，或通过 SQL Server Management Studio。 使用 Management Studio 让 s 焦点。

从 Management Studio 中，展开 Northwind 数据库中的可编程性文件夹。 它的子文件夹之一是程序集。 若要手动将新的程序集添加到数据库中，右键单击程序集文件夹，并从上下文菜单中选择新的程序集。 新建程序集对话框中 （见图 30） 此显示。 单击浏览按钮，选择`ManuallyCreatedDBObjects.dll`我们只需编译，并单击确定以向数据库添加程序集的程序集。 不应看到`ManuallyCreatedDBObjects.dll`在对象资源管理器中的程序集。


[![向数据库添加 ManuallyCreatedDBObjects.dll 程序集](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**图 30**： 添加`ManuallyCreatedDBObjects.dll`到数据库的程序集 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png))


![在对象资源管理器中列出 ManuallyCreatedDBObjects.dll](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**图 31**:`ManuallyCreatedDBObjects.dll`对象资源管理器中列出


虽然我们已添加到 Northwind 数据库的程序集，我们还未将使用存储的过程相关联`GetProductsWithPriceGreaterThan`中程序集的方法。 若要完成此操作，打开新查询窗口并执行以下脚本：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

这将在名为 Northwind 数据库中创建新的存储的过程`GetProductsWithPriceGreaterThan`并将它与托管方法关联`GetProductsWithPriceGreaterThan`(这是在类中`StoredProcedures`，这是在程序集中`ManuallyCreatedDBObjects`)。

执行上述脚本之后, 刷新对象资源管理器中的存储过程文件夹。 你应看到新的存储的过程项目- `GetProductsWithPriceGreaterThan` -它具有一个锁状图标旁边。 若要测试此存储的过程，请输入，并在查询窗口中执行以下脚本：


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

如图 32 所示，上面的命令将显示与这些产品的信息`UnitPrice`大于 24.95 美元。


[![在对象资源管理器中列出 ManuallyCreatedDBObjects.dll](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**图 32**:`ManuallyCreatedDBObjects.dll`对象资源管理器中列出 ([单击以查看实际尺寸的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png))


## <a name="summary"></a>总结

Microsoft SQL Server 2005 提供了集成使用公共语言运行时 (CLR)，它允许使用托管的代码创建数据库对象。 以前，仅可以使用 T-SQL、 创建这些数据库对象，但现在，我们可以创建这些对象使用的.NET 编程语言，如 Visual Basic。 在本教程中我们创建了两个托管的存储的过程和托管用户定义的函数。

Visual Studio 的 SQL Server 项目类型便于创建、 编译和部署托管的数据库对象。 此外，它提供了丰富的调试支持。 但是，SQL Server 项目类型才可用于 Visual Studio Professional 和 Team 系统版本。 对于使用 Visual Web Developer 或标准版的 Visual Studio、 创建、 编译和部署步骤必须手动执行，因为我们在步骤 13 中看到。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [优点和缺点的用户定义的函数](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [在托管代码中创建 SQL Server 2005 对象](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [创建 SQL Server 2005 中使用托管的代码的触发器](http://www.15seconds.com/issue/041006.htm)
- [如何： 创建和运行 CLR SQL Server 存储过程](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [如何： 创建并运行一个 CLR SQL Server 用户定义函数](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [如何： 编辑`Test.sql`脚本运行 SQL 对象](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [对用户定义的函数](http://www.sqlteam.com/item.asp?ItemID=1955)
- [托管的代码和 SQL Server 2005 （视频）](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [TRANSACT-SQL 参考](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [演练： 在托管代码中创建的存储的过程](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 S ren Jacob Lauritsen。 除了查看此文章，S ren 还创建了此项目的下载用于手动编译托管的数据库对象中包含 Visual C# Express Edition 项目。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](debugging-stored-procedures-vb.md)
