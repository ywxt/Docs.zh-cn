---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 数据源控件 |Microsoft Docs
author: microsoft
description: DataGrid 控件在 ASP.NET 1.x 标记为在 Web 应用程序中的数据访问中一项重大改进。 但是，它不是因为它可能是用户友好的...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 15a09e8ac7da6d23216a92863ae7ce6db7ecd57a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809347"
---
<a name="data-source-controls"></a>数据源控件
====================
by [Microsoft](https://github.com/microsoft)

> DataGrid 控件在 ASP.NET 1.x 标记为在 Web 应用程序中的数据访问中一项重大改进。 但是，它不是因为它可能是用户友好的。 它仍然需要相当长的代码可以从中获得更有用的功能。 在 1.x 中的所有数据访问工作中的模型就是这样。


DataGrid 控件在 ASP.NET 1.x 标记为在 Web 应用程序中的数据访问中一项重大改进。 但是，它不是因为它可能是用户友好的。 它仍然需要相当长的代码可以从中获得更有用的功能。 在 1.x 中的所有数据访问工作中的模型就是这样。

ASP.NET 2.0 解决此问题与部分与数据源控件。 数据源控件在 ASP.NET 2.0 为开发人员提供用于检索数据、 显示数据，并编辑数据的声明性模型。 数据源控件的用途是提供而不考虑这些数据源的数据绑定控件的数据的一致表示形式。 ASP.NET 2.0 中的数据源控件的核心是 DataSourceControl 抽象类。 DataSourceControl 类提供基实现 IDataSource 接口和 IListSource 接口，后者允许您为数据绑定控件 （通过新的 DataSourceId 属性的数据源分配的数据源控件稍后讨论），并公开与其中一个列表的数据。 每个列表的数据，数据源控件公开为 DataSourceView 对象。 由 IDataSource 接口提供对 DataSourceView 实例的访问。 例如，GetViewNames 方法返回与特定数据源控件，使您能够枚举 DataSourceViews 是 ICollection 关联和 GetView 方法，可按名称访问特定的 DataSourceView 实例。

数据源控件具有没有用户界面。 它们被实现和作为服务器控件，以便它们可以支持声明性语法，使其为页状态具有访问权限，如果所需。 数据源控件不呈现给客户端的任何 HTML 标记。

> [!NOTE]
> 正如您将看到更高版本，存在还缓存通过使用数据源控件获得的权益。


## <a name="storing-connection-strings"></a>存储连接字符串

在我们开始了解一下如何配置数据源控件之前，我们应涵盖有关连接字符串的 ASP.NET 2.0 中的新功能。 ASP.NET 2.0 引入了新的节，可轻松地将存储的连接字符串，可以在运行时动态地读取配置文件中。 &lt;ConnectionStrings&gt;部分使得更轻松地存储连接字符串。

下面的代码段添加一个新的连接字符串。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> 正如使用&lt;appSettings&gt;部分中， &lt;connectionStrings&gt;之外的部分会出现&lt;system.web&gt;配置文件中的部分。


若要使用此连接字符串，可以使用以下语法设置服务器控件的 ConnectionString 属性时。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;ConnectionStrings&gt;部分也进行加密，以便不公开敏感信息。 在更高版本的模块，将介绍该功能。

## <a name="caching-data-sources"></a>缓存数据源

每个 DataSourceControl 提供四个属性配置缓存;EnableCaching、 CacheDuration、 CacheExpirationPolicy 和 CacheKeyDependency。

## <a name="enablecaching"></a>EnableCaching

EnableCaching 是一个布尔属性，确定是否使用缓存启用数据源控件。

## <a name="cacheduration-property"></a>CacheDuration 属性

CacheDuration 属性设置缓存保持有效的秒的数。 此属性设置为**0**导致要仍有效，直到显式失效的缓存。

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy 属性

CacheExpirationPolicy 属性可以设置为**绝对**或**可调**。 将其设置为绝对意味着将缓存数据的最大时长是 CacheDuration 属性指定的秒数。 通过将其设置为可调，每个操作执行时重置的过期时间。

## <a name="cachekeydependency-property"></a>CacheKeyDependency 属性

如果为 CacheKeyDependency 属性指定一个字符串值，ASP.NET 将设置该字符串上基于新的缓存依赖项。 这允许您显式使缓存失效只需更改或删除 CacheKeyDependency。

**重要**： 如果模拟已启用和访问数据源和/或数据的内容取决于客户端标识，建议将通过 EnableCaching 设置为 False 禁用缓存。 如果在此方案中启用了缓存并最初请求数据的用户以外的用户发出的请求，不能强制授权与数据源。 只需将从缓存提供数据。

## <a name="the-sqldatasource-control"></a>SqlDataSource 控件

SqlDataSource 控件允许开发人员为访问存储在任何支持 ADO.NET 的关系数据库中的数据。 它可以使用 System.Data.SqlClient 提供程序访问 SQL Server 数据库、 System.Data.OleDb 提供程序、 System.Data.Odbc 提供程序或 System.Data.OracleClient 提供商联系以访问 Oracle。 因此，SqlDataSource 是当然不只用于访问 SQL Server 数据库中的数据。

若要使用 SqlDataSource，您只需为 ConnectionString 属性提供值和指定的 SQL 命令或存储过程。 SqlDataSource 控件负责使用基础 ADO.NET 体系结构。 它打开的连接、 查询数据源或执行存储的过程、 返回的数据，然后关闭您的连接。

> [!NOTE]
> 因为 DataSourceControl 类会自动关闭的连接，它应减少生成的数据库连接泄漏的客户调用数。


以下代码段将 DropDownList 控件绑定到使用如上所示的配置文件中存储的连接字符串使用 SqlDataSource 控件。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

如上图所示，SqlDataSource DataSourceMode 属性指定数据源的模式。 在上面的示例中，DataSourceMode 设置为 DataReader。 在这种情况下，SqlDataSource 将返回 IDataReader 对象使用和只进只读游标。 指定的类型的对象，则返回该对象由使用提供程序控制。 在这种情况下，我使用 System.Data.SqlClient 提供程序中的规定&lt;connectionStrings&gt; web.config 文件部分。 因此，返回的对象将是类型 SqlDataReader。 通过指定 DataSourceMode 值为数据集，数据可以存储在服务器上的数据集。 此模式下，可添加功能，如排序、 分页，等等。如果我的数据绑定到 GridView 控件 SqlDataSource，我将选择的数据集模式。 但是，对于下拉列表中，DataReader 模式是正确的选择。

> [!NOTE]
> 当缓存 SqlDataSource 或 AccessDataSource，DataSourceMode 属性必须设置为数据集。 如果启用了使用 DataSourceMode DataReader 缓存，会发生异常。


## <a name="sqldatasource-properties"></a>SqlDataSource 属性

以下是一些 SqlDataSource 控件的属性。

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

一个布尔值，该值指定其中一个参数为 null 时是否取消选择命令。 默认情况下，则为 true。

### <a name="conflictdetection"></a>ConflictDetection

在其中多个用户可能正在更新数据源在同一时间的情况下，ConflictDetection 属性确定 SqlDataSource 控件的行为。 此属性计算结果为 ConflictOptions 枚举值之一。 这些值是**CompareAllValues**并**OverwriteChanges**。 如果设置为 OverwriteChanges，若要将数据写入到数据源的最后一个人将覆盖任何以前的更改。 但是，如果 ConflictDetection 属性设置为 CompareAllValues，为 SelectCommand 返回的列创建参数，参数还会创建用于保存每个允许到 SqlDataSource 这些列中的原始值确定自执行 SelectCommand 以来已更改值。

### <a name="deletecommand"></a>DeleteCommand

设置或获取从数据库中删除行时使用的 SQL 字符串。 这可以是 SQL 查询或存储的过程名称。

### <a name="deletecommandtype"></a>DeleteCommandType

设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 可以获取的 delete 命令的类型。

### <a name="deleteparameters"></a>DeleteParameters

返回由 SqlDataSourceView 对象与 SqlDataSource 控件相关联的 DeleteCommand 的参数。

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

此属性用于在其中 ConflictDetection 属性设置为 CompareAllValues 的情况下指定的原始值参数的格式。 默认值是{0}这意味着原始值参数，将需要与原始参数同名。 换而言之，如果字段名称为雇员 id，则原始值参数应为@EmployeeID。

### <a name="selectcommand"></a>SelectCommand

设置或获取用于从数据库检索数据的 SQL 字符串。 这可以是 SQL 查询或存储的过程名称。

### <a name="selectcommandtype"></a>SelectCommandType

设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 或者获取 select 命令的类型。

### <a name="selectparameters"></a>SelectParameters

返回由 SqlDataSourceView 对象与 SqlDataSource 控件相关联的 SelectCommand 的参数。

### <a name="sortparametername"></a>SortParameterName

获取或设置用于排序数据检索的数据源控件存储的过程参数的名称。 仅当 SelectCommandType 设置为 StoredProcedure 时才有效。

### <a name="sqlcachedependency"></a>SqlCacheDependency

以分号分隔的字符串，指定数据库和 SQL Server 缓存依赖项中使用的表。 （SQL 缓存依赖项将讨论在更高版本的模块中。）

### <a name="updatecommand"></a>UpdateCommand

设置或获取更新数据库中的数据时使用的 SQL 字符串。 这可以是 SQL 查询或存储的过程名称。

### <a name="updatecommandtype"></a>UpdateCommandType

设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 可以获取的更新命令的类型。

### <a name="updateparameters"></a>UpdateParameters

返回由 SqlDataSourceView 对象与 SqlDataSource 控件相关联的 UpdateCommand 的参数。

## <a name="the-accessdatasource-control"></a>AccessDataSource 控件

AccessDataSource 控件从 SqlDataSource 类派生，用于数据绑定到 Microsoft Access 数据库。 AccessDataSource 控件的 ConnectionString 属性是只读的属性。 而不是使用 ConnectionString 属性，用于指向 Access 数据库，如下所示的数据文件属性。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource 将始终设置为 System.Data.OleDb 的基 SqlDataSource ProviderName 并连接到该数据库使用的 Microsoft.Jet.OLEDB.4.0 OLE DB 访问接口。 AccessDataSource 控件不能用于连接到受密码保护 Access 数据库。 如果您必须连接到受密码保护数据库，则应使用 SqlDataSource 控件。

> [!NOTE]
> 应将存储在 Web 站点内访问数据库放在应用\_数据目录。 ASP.NET 不允许要浏览此目录中的文件。 将需要授予对应用的读取和写入权限的进程帐户\_数据目录时使用 Access 数据库。


## <a name="the-xmldatasource-control"></a>XmlDataSource 控件

XmlDataSource 可用来对数据绑定控件数据绑定 XML 数据。 可以将它们绑定到 XML 文件使用数据文件属性或可以绑定到一个 XML 字符串，使用数据属性。 XmlDataSource 公开为可绑定的字段的 XML 特性。 在需要将绑定到不表示为属性的值的情况下，需要使用 XSL 转换。 此外可以使用筛选器的 XML 数据的 XPath 表达式。

请考虑下面的 XML 文件：

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

请注意 XmlDataSource 使用的 XPath 属性*用户/个人*以便筛选只&lt;人员&gt;节点。 DropDownList 然后数据将绑定到使用 DataTextField 属性 LastName 属性。

XmlDataSource 控件主要用于数据绑定到只读的 XML 数据，而是可以编辑 XML 数据文件。 请注意，在这种情况下，自动插入、 更新和删除的 XML 文件中的信息不会自动发生，这与其他数据源控件。 相反，必须编写代码来手动编辑使用以下方法的 XmlDataSource 控件的数据。

### <a name="getxmldocument"></a>GetXmlDocument

检索一个 XmlDocument 对象，包含由 XmlDataSource 检索的 XML 代码。

### <a name="save"></a>保存

将内存中 XmlDocument 保存回数据源。

请务必意识到 Save 方法仅适用时满足以下两个条件：

1. XmlDataSource 使用数据文件属性绑定到 XML 文件而不是数据属性将绑定到内存中 XML 数据。
2. 通过转换或 TransformFile 属性不指定任何转换。

另请注意 Save 方法会产生意外的结果时同时调用多个用户。

## <a name="the-objectdatasource-control"></a>ObjectDataSource 控件

到目前为止我们已经介绍的数据源控件是两个层应用程序的极佳选择位置直接与数据存储进行通信的数据源控件。 但是，许多实际的应用程序是多层应用程序数据源控件可能需要到这，反过来，与数据层进行通信的业务对象进行通信。 在这些情况下，ObjectDataSource 可以很好地填充帐单。 ObjectDataSource 协同工作与源对象。 ObjectDataSource 控件将创建的源对象、 调用指定的方法和释放单个请求的范围内的所有对象实例的实例，如果您的对象具有实例方法，而不是静态方法 (在 Visual Basic 中为 Shared)。 因此，您的对象必须是无状态。 也就是说，您的对象应获取和释放单个请求的范围内的所有所需的资源。 您可以控制如何通过处理 ObjectDataSource 控件 ObjectCreating 事件创建的源对象。 可以创建源对象的实例，然后将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。 ObjectDataSource 控件将使用 ObjectCreating 事件而不是自己创建实例中创建的实例。

如果 ObjectDataSource 控件源对象公开的公共静态方法 (在 Visual Basic 中为 Shared)，可以调用以检索和修改数据，ObjectDataSource 控件将直接调用这些方法。 如果 ObjectDataSource 控件必须以进行方法调用创建源对象的实例，该对象必须包含不带参数的公共构造函数。 ObjectDataSource 控件将调用此构造函数，当创建源对象的新实例。

如果源对象不包含不带参数的公共构造函数，可以创建将由 ObjectCreating 事件中的 ObjectDataSource 控件源对象的实例。

## <a name="specifying-object-methods"></a>指定对象的方法

ObjectDataSource 控件源对象可以包含任意数量的方法，用于选择、 插入、 更新或删除数据。 ObjectDataSource 控件基于方法的名称，如通过使用 ObjectDataSource 控件 SelectMethod、 InsertMethod、 UpdateMethod 或 DeleteMethod 属性确定调用这些方法。 源对象还可以包含一个可选的 SelectCount 方法，它由 ObjectDataSource 控件使用 SelectCountMethod 属性，返回的数据源的对象总数的计数。 在调用 Select 方法来检索分页时使用的数据源中的记录的总数后，ObjectDataSource 控件将调用 SelectCount 方法。

## <a name="lab-using-data-source-controls"></a>实验室中使用数据源控件

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>练习 1-使用 SqlDataSource 控件显示数据

以下练习中使用 SqlDataSource 控件连接到 Northwind 数据库。 它假定你有权访问 Northwind 数据库的 SQL Server 2000 实例上。

1. 创建一个新的 ASP.NET 网站。
2. 添加新的 web.config 文件。

    1. 右键单击解决方案资源管理器中的项目，然后单击添加新项。
    2. 从模板列表中选择 Web 配置文件，并单击添加。
3. 编辑&lt;connectionStrings&gt;部分，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 切换到代码视图，然后添加 ConnectionString 属性和到 SelectCommand 属性&lt;asp: SqlDataSource&gt;控制，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 从设计视图中，添加新的 GridView 控件。
6. 从 GridView 任务菜单的选择数据源下拉列表中，选择 sqldatasource1。
7. 右键单击 Default.aspx，然后在浏览器中从菜单中选择视图。 当系统提示你保存，单击是。
8. GridView 显示产品表中的数据。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>练习 2-使用 SqlDataSource 控件编辑数据

下面的练习演示如何将数据绑定 DropDownList 控件并使用声明性语法，并允许您编辑 DropDownList 控件中显示的数据。

1. 在设计视图中，从 Default.aspx 中删除 GridView 控件。 

    **重要**： 保留 SqlDataSource 控件在页上的。
2. 将 DropDownList 控件添加到 Default.aspx。
3. 切换到源视图。
4. 添加到属性的 DataSourceId、 DataTextField 和 DataValueField &lt;asp: DropDownList&gt;控制，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. 保存 Default.aspx，并在浏览器中查看它。 请注意，下拉列表包含所有 Northwind 数据库中的产品。
6. 关闭浏览器。
7. 在源视图中的 Default.aspx，添加新的 TextBox 控件 DropDownList 控件的下方。 将文本框的 ID 属性更改为 txtProductName。
8. 在文本框控件，将添加一个新的按钮控件。 将按钮的 ID 属性更改为 btnUpdate 和 Text 属性改**更新产品名称**。
9. 在 Default.aspx 源视图中，添加 UpdateCommand 属性和两个新 UpdateParameters SqlDataSource 标记，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 请注意，有两个更新此代码中添加的参数 （产品名称和产品 id）。 这些参数映射到 txtProductName 文本框的 Text 属性和 ddlProducts DropDownList 的 SelectedValue 属性。
10. 切换到设计视图，并双击要添加的事件处理程序的按钮控件。
11. 将以下代码添加到 btnUpdate\_单击代码： 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. 右键单击 Default.aspx，然后选择在浏览器中查看。 当系统提示你保存所有更改，单击是。
13. ASP.NET 2.0 的分部类实现在运行时编译。 不需要生成的应用程序来查看代码更改才会生效。
14. 从下拉列表中选择一个产品。
15. 在文本框中输入所选产品的新名称，然后单击更新按钮。
16. 产品名称更新数据库中。

## <a name="exercise-3-using-the-objectdatasource-control"></a>练习 3： 使用 ObjectDataSource 控件

本练习将演示如何使用 ObjectDataSource 控件和源对象与 Northwind 数据库进行交互。

1. 右键单击解决方案资源管理器中的项目并单击添加新项。
2. 在模板列表中选择 Web 窗体。 将名称更改为 object.aspx 并单击添加。
3. 右键单击解决方案资源管理器中的项目并单击添加新项。
4. 在模板列表中选择类。 将类的名称更改为 NorthwindData.cs 并单击添加。
5. 单击是将类添加到应用程序出现提示时\_代码文件夹。
6. 将以下代码添加到 NorthwindData.cs 文件： 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 将以下代码添加到 object.aspx 的源视图： 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 保存所有文件，并浏览 object.aspx。
9. 通过查看详细信息、 编辑员工、 员工、 添加和删除员工与接口进行交互。
