---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: 使用 SQL 缓存依赖项 (C#) |Microsoft Docs
author: rick-anderson
description: 最简单的缓存策略是时间的允许缓存的数据在指定段后过期。 但是，此简单的方法意味着，缓存的数据 maintai...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 16766ce7d741a9bcaea7cc676ed87978ea9f9f68
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385899"
---
<a name="using-sql-cache-dependencies-c"></a>使用 SQL 缓存依赖项 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip)或[下载 PDF](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> 最简单的缓存策略是时间的允许缓存的数据在指定段后过期。 但此简单的方法意味着，则缓存的数据会保留对其基础的数据源，从而导致保存太长的陈旧数据或太即将过期的最新数据没有关联。 更好的方法是使用 SqlCacheDependency 类，以便数据保持缓存，直到其基础数据已修改的 SQL 数据库中。 本教程演示如何。


## <a name="introduction"></a>介绍

在中检查的缓存技术[使用 ObjectDataSource 缓存数据](caching-data-with-the-objectdatasource-cs.md)并[体系结构中缓存数据](caching-data-in-the-architecture-cs.md)教程使用基于时间的到期后指定逐出缓存中的数据时间段。 这种方法是最简单的方法来平衡的数据失效针对缓存的性能提升。 通过选择的时间到期*x*秒，页面开发人员 concedes 享受仅缓存的性能优势*x*秒，但可以高枕无忧，她的数据永远不会将过时时间超过最大值*x*秒。 当然，对于静态数据， *x*中检查已作为可以扩展到 web 应用程序的生存期[在应用程序启动时缓存数据](caching-data-at-application-startup-cs.md)教程。

当缓存数据库数据，基于时间的到期选择通常其易于使用，但通常是不能满足需要的解决方案。 理想情况下，数据库中，数据将保留缓存之前已在数据库中，在修改基础数据然后仅将逐出缓存。 这种方法最大缓存的性能优势，并最大程度减少过时的数据的持续时间。 但是，为了享受这些权益有必须知道当基础数据库数据已被修改，逐出缓存中的相应项的位置中的某些系统。 在 ASP.NET 2.0 之前页面开发人员是负责实现此系统。

ASP.NET 2.0 提供了[`SqlCacheDependency`类](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)和必要的基础结构以确定何时发生了更改数据库中，以便相应缓存项可以被逐出。 有两种技术用于确定基础数据已更改时： 通知和轮询。 在讨论后通知和轮询之间的差异，我们将创建基础结构支持轮询，然后探讨如何使用所需`SqlCacheDependency`类中声明性和以编程方式方案。

## <a name="understanding-notification-and-polling"></a>了解通知和轮询

有两种技术可以用于确定数据库中的数据修改时： 通知和轮询。 通知，当自上次执行该查询以来已更改的特定查询的结果时数据库的自动警报 ASP.NET 运行时，逐出的哪个点与查询关联的缓存的项。 通过轮询，数据库服务器服务维护有关上次更新时间特定的表的信息。 ASP.NET 运行时定期轮询数据库以检查表已发生的更改因为它们已输入到缓存。 这些修改其数据的表具有逐出及其关联的缓存项。

通知选项需要较少的设置比轮询和是更精细，因为它跟踪的更改在查询级别而不是在表级别。 遗憾的是，通知只是 Microsoft SQL Server 2005 （即，非速成版） 的完整版本中提供的。 但是，轮询选项可用于从 7.0 的 Microsoft SQL Server 2005 的所有版本。 由于这些教程使用的 SQL Server 2005 Express edition，我们将重点设置和使用轮询选项。 请进一步阅读部分查阅本教程，了解更多 SQL Server 2005 的通知功能的资源的末尾。

使用轮询，必须配置数据库包含名为的表`AspNet_SqlCacheTablesForChangeNotification`具有三列- `tableName`， `notificationCreated`，和`changeId`。 此表包含每个表都有可能需要在 web 应用程序中的 SQL 缓存依赖项中使用的数据行。 `tableName`列指定时，表的名称`notificationCreated`指示的日期和时间向表添加行。 `changeId`列的类型是`int`和初始值为 0。 其值会递增与每次修改的表。

除了`AspNet_SqlCacheTablesForChangeNotification`表，需要将数据库还在 SQL 缓存依赖项中包含每个可能出现的表上的触发器。 这些触发器时插入、 更新或删除某行执行，并递增表 s`changeId`中的值`AspNet_SqlCacheTablesForChangeNotification`。

ASP.NET 运行时跟踪当前`changeId`表时缓存数据使用`SqlCacheDependency`对象。 定期检查该数据库和任何`SqlCacheDependency`对象的`changeId`不同于数据库中的值不同以来逐出`changeId`值指示发生了对表的更改被缓存数据后。

## <a name="step-1-exploring-theaspnetregsqlexecommand-line-program"></a>步骤 1： 浏览`aspnet_regsql.exe`命令行程序

使用轮询方法时，数据库必须安装程序以包含上面所述的基础结构： 预定义的表 (`AspNet_SqlCacheTablesForChangeNotification`)，少量的存储的过程和触发器在每个可在 web 中的 SQL 缓存依赖项表应用程序。 可以通过命令行程序创建这些表、 存储的过程和触发器`aspnet_regsql.exe`，它出现在`$WINDOWS$\Microsoft.NET\Framework\version`文件夹。 若要创建`AspNet_SqlCacheTablesForChangeNotification`表和关联的存储的过程，从命令行运行以下命令：


[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> 若要执行的指定的数据库登录名必须在这些命令[ `db_securityadmin` ](https://msdn.microsoft.com/library/ms188685.aspx)并[ `db_ddladmin` ](https://msdn.microsoft.com/library/ms190667.aspx)角色。 若要检查发送到的数据库 T-SQL`aspnet_regsql.exe`命令行程序，请参阅[此博客文章](http://scottonwriting.net/sowblog/posts/10709.aspx)。


例如，若要将轮询的基础结构添加到 Microsoft SQL Server 数据库名为`pubs`名为数据库服务器上`ScottsServer`使用 Windows 身份验证，导航到相应的目录并，请从命令行中，输入：


[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

添加数据库级别基础结构后，我们需要将触发器添加到将 SQL 缓存依赖项中使用这些表。 使用`aspnet_regsql.exe`命令行程序，但指定表名称使用`-t`切换，而不是使用`-ed`切换使用`-et`，如下所示：


[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

若要添加到触发器`authors`并`titles`表上`pubs`上的数据库`ScottsServer`，使用：


[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

本教程将添加到触发器`Products`， `Categories`，和`Suppliers`表。 我们将介绍在步骤 3 中的特定命令行语法。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inappdata"></a>步骤 2： 引用中的 Microsoft SQL Server 2005 Express Edition 数据库`App_Data`

`aspnet_regsql.exe`命令行程序需要数据库和服务器名称才能添加必要的轮询基础结构。 什么是 Microsoft SQL Server 2005 Express 数据库中驻留的数据库和服务器名称，但`App_Data`文件夹？ 而不是无需发现的数据库和服务器名称是什么，我已找到的最简单方法是将附加到的数据库`localhost\SQLExpress`数据库实例和数据使用重命名[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。 如果必须在计算机上安装 SQL Server 2005 的完整版本之一，然后您可能已经在计算机上安装 SQL Server Management Studio。 如果您只有 Express edition，则可以下载免费[Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

首先关闭 Visual Studio。 接下来，打开 SQL Server Management Studio，然后选择要连接到`localhost\SQLExpress`使用 Windows 身份验证服务器。


![将附加到 localhost\SQLExpress 服务器](using-sql-cache-dependencies-cs/_static/image1.gif)

**图 1**： 将附加到`localhost\SQLExpress`服务器


Management Studio 连接到服务器后，会显示服务器并可能对数据库、 安全性和等的子文件夹。 右键单击数据库文件夹并选择附加选项。 这将显示附加数据库对话框 （请参见图 2）。 单击添加按钮，然后选择`NORTHWND.MDF`database 文件夹中您的 web 应用程序 s`App_Data`文件夹。


[![将附加 northwnd 不。MDF App_Data 文件夹中的数据库](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**图 2**： 将附加`NORTHWND.MDF`数据库从`App_Data`文件夹 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image2.png))


这会将数据库添加到数据库文件夹中。 数据库名称可能是数据库文件的完整路径或完整路径前面带有[GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)。 若要避免无需使用 aspnet 时此长时间的数据库名称键入\_regsql.exe 命令行工具，附加到更加用户友好名称只是在数据库上右键单击该数据库重命名并选择重命名。 我已重命名为 DataTutorials 的我的数据库。


![附加的数据库重命名为更多的用户友好名称](using-sql-cache-dependencies-cs/_static/image3.gif)

**图 3**： 附加的数据库重命名为更多的用户友好名称


## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>步骤 3： 将轮询基础结构添加到 Northwind 数据库

现在，我们已附加`NORTHWND.MDF`数据库从`App_Data`文件夹中，我们准备就绪后，若要添加的轮询基础结构。 假设你已重命名为 DataTutorials 的数据库，运行以下四个命令：


[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

后运行以下四个命令，右键单击 Management Studio 中的数据库名称，转到任务子菜单，并选择分离。 然后关闭 Management Studio 并重新打开 Visual Studio。

一旦已重新打开 Visual Studio，深入了解通过服务器资源管理器数据库。 请注意新表 (`AspNet_SqlCacheTablesForChangeNotification`)，新存储过程和触发器上`Products`， `Categories`，和`Suppliers`表。


![Database 现在包括必要的轮询基础结构](using-sql-cache-dependencies-cs/_static/image4.gif)

**图 4**: Database 现在包括必要的轮询基础结构


## <a name="step-4-configuring-the-polling-service"></a>步骤 4： 配置轮询服务

在创建后所需的表、 触发器和存储的过程在数据库中，最后一步是配置轮询服务，通过完成`Web.config`通过指定以毫秒为单位的轮询频率和使用数据库。 以下标记将每隔一秒一次轮询 Northwind 数据库。


[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

`name`中的值`<add>`元素 (NorthwindDB) 将与特定数据库相关联的可读名称。 在使用 SQL 缓存依赖项，我们将需要引用基于缓存的数据的表以及在此处定义的数据库名称。 我们将了解如何使用`SqlCacheDependency`类以编程方式将与 SQL 缓存依赖项相关联的缓存在步骤 6 中的数据。

轮询系统建立 SQL 缓存依赖项之后，将连接到数据库中定义`<databases>`元素每`pollTime`毫秒并执行`AspNet_SqlCachePollingStoredProcedure`存储过程。 在步骤 3 中使用此存储的过程-已添加回`aspnet_regsql.exe`命令行工具-将返回`tableName`并`changeId`中的每个记录的值`AspNet_SqlCacheTablesForChangeNotification`。 从缓存逐出过时的 SQL 缓存依赖项。

`pollTime`设置引入了性能和数据过期时间之间的权衡。 一个较小`pollTime`值将会增大到的数据库的请求数，但更多快速逐出缓存中的陈旧数据。 更大`pollTime`值可减少数据库请求数，但会增加后端数据的更改时和时逐出的相关的缓存项之间的延迟。 幸运的，数据库请求正在执行的简单存储的过程从简单的轻型表返回只需几行的 s。 执行试验不同，但`pollTime`值理想之间找到平衡数据库应用程序的访问和数据过期。 最小`pollTime`允许值为 500。

> [!NOTE]
> 上面的示例中提供了单个`pollTime`中的值`<sqlCacheDependency>`元素，但是您可以选择指定`pollTime`中的值`<add>`元素。 如果你有多个指定的数据库，并想要自定义每个数据库的轮询频率，这非常有用。


## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>步骤 5： 以声明方式使用 SQL 缓存依赖项

在步骤 1 到 4 中我们介绍了如何设置必要的数据库基础结构和配置轮询系统。 使用此基础结构，我们现在可以添加项目数据缓存有关联 SQL 缓存依赖项的使用以编程方式或声明性技术。 在此步骤中，我们将介绍如何以声明方式使用 SQL 缓存依赖项。 在步骤 6 中，我们将介绍编程方法。

[使用 ObjectDataSource 缓存数据](caching-data-with-the-objectdatasource-cs.md)教程探讨了 ObjectDataSource 的声明性缓存功能。 通过轻松`EnableCaching`属性设置为`true`和`CacheDuration`属性设置为某个时间间隔，ObjectDataSource 自动将缓存从其基础对象返回指定间隔内的数据。 ObjectDataSource 还可以使用一个或多个 SQL 缓存依赖项。

若要演示如何以声明方式使用 SQL 缓存依赖项，打开`SqlCacheDependencies.aspx`页中`Caching`文件夹，然后拖动 GridView 从工具箱拖到设计器。 设置 GridView s`ID`到`ProductsDeclarative`，并从其智能标记，选择要绑定到名为新 ObjectDataSource `ProductsDataSourceDeclarative`。


[![创建名为 ProductsDataSourceDeclarative 新 ObjectDataSource](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**图 5**： 创建新对象数据源命名`ProductsDataSourceDeclarative`([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image4.png))


配置要使用 ObjectDataSource`ProductsBLL`类，然后在选择选项卡中设置下拉列表`GetProducts()`。 在更新选项卡，选择`UpdateProduct`带有三个输入参数的重载`productName`， `unitPrice`，和`productID`。 在 INSERT 和 DELETE 选项卡中设置为 （无） 下拉列表。


[![带有三个输入参数，请使用 UpdateProduct 重载](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**图 6**： 带有三个输入参数使用 UpdateProduct 重载 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image6.png))


[![设置为 （无） 用于插入和删除选项卡的下拉列表](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**图 7**： 用于插入和删除选项卡或设置为 （无） 的下拉列表 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image8.png))


完成配置数据源向导后，Visual Studio 将创建 BoundFields 和 CheckBoxFields 在 GridView 中每个数据字段。 删除所有字段，但`ProductName`， `CategoryName`，和`UnitPrice`，并根据需要设置这些字段的格式。 从 GridView s 智能标记，选中启用分页、 启用排序和启用编辑复选框。 Visual Studio 将设置 ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`。 为了使 GridView 的编辑功能才能正常工作，或者此属性完全从声明性语法或删除的设置回其默认值， `{0}`。

最后，添加一个标签 Web 控件上方的 GridView 并设置其`ID`属性设置为`ODSEvents`并将其`EnableViewState`属性设置为`false`。 进行这些更改后，在页面 s 声明性标记应类似于以下。 请注意，我已进行了大量不需要为了演示 SQL 缓存依赖项功能的 GridView 字段的美观自定义设置。


[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

接下来，创建事件处理程序的 ObjectDataSource s`Selecting`事件并在其添加以下代码：


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

请记住，ObjectDataSource 的`Selecting`仅从其基础对象检索数据时，会触发事件。 如果 ObjectDataSource 从其自己的缓存访问数据，不激发此事件。

现在，请访问此页上的通过浏览器。 自我们 ve 尚未来实现任何缓存，每个页上，对此进行排序，或编辑的网格页的时间，应显示的文本、 选择事件触发，如图 8 所示。


[![每个时间分页 GridView 编辑，或者按，就会触发 ObjectDataSource 的选择事件](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**图 8**: ObjectDataSource s`Selecting`事件将触发每个时间分页 GridView、 编辑或按 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image10.png))


中可以看到[使用 ObjectDataSource 缓存数据](caching-data-with-the-objectdatasource-cs.md)教程中，设置`EnableCaching`属性设置为`true`ObjectDataSource 来缓存其数据以便通过指定的持续时间将导致其`CacheDuration`属性。 ObjectDataSource 还有[`SqlCacheDependency`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)，从而将一个或多个 SQL 缓存依赖项添加到缓存的数据使用模式：


[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

其中*databaseName*中指定的数据库的名称`name`的属性`<add>`中的元素`Web.config`，和*tableName*是数据库表的名称。 例如，若要无限期地缓存数据对象数据源基于创建针对 Northwind s SQL 缓存依赖项`Products`表中，设置 ObjectDataSource s`EnableCaching`属性设置为`true`并将其`SqlCacheDependency`属性NorthwindDB:Products。

> [!NOTE]
> 可以使用 SQL 缓存依赖项*并*通过设置基于时间的到期`EnableCaching`到`true`，`CacheDuration`为时间间隔，和`SqlCacheDependency`到数据库和表名称。 ObjectDataSource 会逐出其数据到达的基于时间的过期时间时或当轮询系统就会注意，基础数据库数据已更改，以先发生者为准。


在 GridView`SqlCacheDependencies.aspx`显示来自两个表的数据`Products`并`Categories`(产品 s`CategoryName`通过检索字段`JOIN`上`Categories`)。 因此，我们想要指定两个 SQL 缓存依赖项： NorthwindDB:Products;NorthwindDB:Categories。


[![配置对象数据源来支持缓存产品和类别上使用 SQL 缓存依赖项](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**图 9**： 在配置为支持缓存使用 SQL 缓存依赖项 ObjectDataSource`Products`并`Categories`([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image12.png))


配置对象数据源来支持缓存之后, 重新访问通过浏览器页面。 同样，激发的文本选择事件应显示在第一次的页面访问，但应消失时分页、 排序，或单击编辑或取消按钮。 这是因为数据加载到 ObjectDataSource 的缓存后，它会一直保留直到`Products`或`Categories`表有修改或通过 GridView 数据进行了更新。

通过网格分页并记下缺少选择事件触发后的文本，打开一个新的浏览器窗口并导航到编辑、 插入和删除部分中的基础知识教程 (`~/EditInsertDelete/Basics.aspx`)。 更新的名称或产品的价格。 然后，从第一个浏览器窗口中，查看不同的数据页、 排序网格中，或单击行的编辑按钮。 这一次，选择事件触发应重新出现，因为基础数据库的数据已被修改 （请参阅图 10）。 如果未显示的文本，不会等待一段时间，然后重试。 请记住，轮询服务正在检查的更改`Products`表每个`pollTime`毫秒，以便更新基础数据时和时逐出缓存的数据之间存在延迟。


[![修改 Products 表逐出缓存的产品数据](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**图 10**： 修改产品表逐出缓存产品数据 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image14.png))


## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>步骤 6： 以编程方式使用`SqlCacheDependency`类

[体系结构中缓存数据](caching-data-in-the-architecture-cs.md)教程介绍了使用单独的缓存层中而不是紧密耦合使用 ObjectDataSource 缓存体系结构的好处。 在该教程中我们创建`ProductsCL`类，以演示如何以编程方式使用数据缓存。 若要利用缓存层中的 SQL 缓存依赖项，请使用`SqlCacheDependency`类。

使用轮询系统`SqlCacheDependency`对象必须与一个特定的数据库和表对相关联。 下面的代码，例如，创建`SqlCacheDependency`对象，基于 Northwind 数据库的`Products`表：


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

两个输入参数`SqlCacheDependency`s 构造函数分别是数据库和表名称。 使用 ObjectDataSource s 喜欢`SqlCacheDependency`属性，使用的数据库名称是在中指定的值相同`name`的属性`<add>`中的元素`Web.config`。 表名是数据库表的实际名称。

若要将相关联`SqlCacheDependency`添加到数据缓存的项，请使用其中一个`Insert`接受依赖关系的方法重载。 下面的代码添加*值*到无限期的持续时间的数据缓存，但将其与`SqlCacheDependency`上`Products`表。 简单地说，*值*将保留在缓存中，直到被逐出，否则由于内存约束或轮询系统已检测到因为`Products`表已更改自缓存。


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

缓存层 s`ProductsCL`类当前缓存中的数据`Products`表可使用 60 秒的基于时间的到期。 让我们来更新此类，以便它改为使用 SQL 缓存依赖项。 `ProductsCL`类的`AddCacheItem`方法，它负责将数据添加到缓存，当前包含以下代码：


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

更新此代码以使用`SqlCacheDependency`对象而不是`MasterCacheKeyArray`缓存依赖项：


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

若要测试此功能，向下的现有页添加 GridView `ProductsDeclarative` GridView。 设置此新 GridView s`ID`到`ProductsProgrammatic`并通过其智能标记，请将其绑定到名为新 ObjectDataSource `ProductsDataSourceProgrammatic`。 配置要使用 ObjectDataSource`ProductsCL`类，设置下拉列表中选择和更新选项卡添加到`GetProducts`和`UpdateProduct`分别。


[![配置对象数据源以使用 ProductsCL 类](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**图 11**： 配置为使用 ObjectDataSource`ProductsCL`类 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image16.png))


[![从选择的选项卡的下拉列表中选择 GetProducts 方法](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**图 12**： 选择`GetProducts`方法，从下拉列表中的选择选项卡 s ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image18.png))


[![从更新选项卡的下拉列表中选择 UpdateProduct 方法](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**图 13**： 从更新选项卡的下拉列表中选择 UpdateProduct 方法 ([单击以查看实际尺寸的图像](using-sql-cache-dependencies-cs/_static/image20.png))


完成配置数据源向导后，Visual Studio 将创建 BoundFields 和 CheckBoxFields 在 GridView 中每个数据字段。 像使用第一个 GridView 添加到此页中，删除所有字段，但`ProductName`， `CategoryName`，和`UnitPrice`，并根据需要设置这些字段的格式。 从 GridView s 智能标记，选中启用分页、 启用排序和启用编辑复选框。 如同`ProductsDataSourceDeclarative`ObjectDataSource、 Visual Studio 将设置`ProductsDataSourceProgrammatic`ObjectDataSource s`OldValuesParameterFormatString`属性设置为`original_{0}`。 为了使 GridView 的编辑功能，若要正常工作，请将此属性设置回`{0}`（或从声明性语法中完全删除属性赋值）。

完成这些任务后, 所得的 GridView 和 ObjectDataSource 声明性标记应如下所示：


[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

若要测试 SQL 缓存依赖项中缓存层中设置断点`ProductCL`类的`AddCacheItem`方法，然后开始调试。 当你首次访问`SqlCacheDependencies.aspx`，如第一次请求数据并将其放入缓存，应会命中断点。 接下来，移到 GridView 中的另一页或排序的列之一。 这将导致 GridView 来重新查询其数据，但应以来在缓存中找到数据`Products`尚未修改数据库表。 如果在缓存中重复未找到数据，请确保有足够的内存，可在计算机上，然后重试。

在 GridView 中的若干页进行分页后, 打开第二个浏览器窗口并导航到编辑、 插入和删除部分中的基础知识教程 (`~/EditInsertDelete/Basics.aspx`)。 更新 Products 表中的记录，然后，从第一个浏览器窗口中，查看新的页或单击一个排序的标头。

在此方案中您将看到两个条件之一： 任一断点将被命中，，该值指示缓存的数据已被逐出由于中在数据库中，更改或者，将不会命中断点，这意味着，`SqlCacheDependencies.aspx`现在显示过时的数据。 如果未命中断点，它可能是因为数据已更改的轮询服务不尚未触发。 请记住，轮询服务正在检查的更改`Products`表每个`pollTime`毫秒，以便更新基础数据时和时逐出缓存的数据之间存在延迟。

> [!NOTE]
> 这种延迟是更有可能在编辑通过 GridView 中的产品之一时显示`SqlCacheDependencies.aspx`。 在中[体系结构中缓存数据](caching-data-in-the-architecture-cs.md)教程中我们添加了`MasterCacheKeyArray`缓存依赖关系，以确保通过正在编辑的数据`ProductsCL`类的`UpdateProduct`方法已从缓存逐出。 但是，我们替换为此缓存依赖项修改时`AddCacheItem`方法之前在此步骤中的，因此`ProductsCL`类将继续显示缓存的数据，直到轮询系统就会注意到更改`Products`表。 我们将了解如何重新引入`MasterCacheKeyArray`缓存在步骤 7 中的依赖关系。


## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>步骤 7： 将多个依赖项与缓存的项相关联

请记住，`MasterCacheKeyArray`缓存依赖项用于确保*所有*更新中其关联的任何单个项时，与产品相关的数据从缓存中逐出。 例如，`GetProductsByCategoryID(categoryID)`方法缓存`ProductsDataTables`实例为每个唯一*categoryID*值。 如果其中某个对象被逐出，`MasterCacheKeyArray`缓存依赖项可确保其他人也会删除。 不缓存此依赖项，修改缓存的数据的可能性是存在的其他缓存的产品数据可能会过期。 因此，它非常重要，我们维护`MasterCacheKeyArray`缓存依赖项时使用 SQL 缓存依赖项。 但是，数据缓存 s`Insert`方法只允许单个依赖关系对象。

此外，使用 SQL 缓存依赖项时我们可能需要将作为依赖项的多个数据库表相关联。 例如，`ProductsDataTable`缓存在`ProductsCL`类包含用于每个产品类别和供应商名称，但`AddCacheItem`方法仅使用一个依赖项上`Products`。 在此情况下，如果用户更新的类别或供应商的名称将保留在缓存中缓存的产品数据和超时的后果。 因此，我们想要使缓存的产品数据依赖于不仅`Products`表，但在`Categories`和`Suppliers`以及表。

[ `AggregateCacheDependency`类](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)提供了一种将多个依赖项的缓存项与相关联。 首先创建`AggregateCacheDependency`实例。 接下来，添加的依赖项使用一套`AggregateCacheDependency`s`Add`方法。 此后将项插入到数据缓存，当传入`AggregateCacheDependency`实例。 当*任何*的`AggregateCacheDependency`实例 s 依赖项更改，将逐出缓存的项。

下面显示了有关更新的代码`ProductsCL`类的`AddCacheItem`方法。 该方法将创建`MasterCacheKeyArray`缓存依赖项一起`SqlCacheDependency`对象的`Products`， `Categories`，和`Suppliers`表。 这些所有合并成一个`AggregateCacheDependency`名为对象`aggregateDependencies`，后者再传递到`Insert`方法。


[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

测试出此新代码。现在将变为`Products`， `Categories`，或`Suppliers`表会导致被逐出缓存的数据。 此外，`ProductsCL`类 s`UpdateProduct`方法，称为编辑通过 GridView 产品时，逐出`MasterCacheKeyArray`缓存依赖项，这会导致缓存`ProductsDataTable`逐出和下一步重新检索的数据请求。

> [!NOTE]
> SQL 缓存依赖项也可以用于[输出缓存](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)。 此功能的演示，请参阅：[使用 ASP.NET 输出缓存用于 SQL Server](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)。


## <a name="summary"></a>总结

除非在数据库中修改，否则，当缓存数据库数据，数据将理想情况下会保留在缓存中。 使用 ASP.NET 2.0 中，可以创建并在声明性和编程方案中使用 SQL 缓存依赖项。 使用此方法的挑战之一就是发现修改的数据时。 完整版本的 Microsoft SQL Server 2005 提供的查询结果发生更改时可以发出警报应用程序的通知功能。 对于 Express 版本的 SQL Server 2005 和较旧版本的 SQL Server，必须改为使用轮询系统。 幸运的是，设置必要的轮询基础结构是非常简单。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [Microsoft SQL Server 2005 中使用查询通知](https://msdn.microsoft.com/library/ms175110.aspx)
- [创建查询通知](https://msdn.microsoft.com/library/ms188669.aspx)
- [在缓存中使用的 ASP.NET`SqlCacheDependency`类](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 注册工具 (`aspnet_regsql.exe`)](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [概述 `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Marko Rangel、 Teresa Murphy 和 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-at-application-startup-cs.md)
> [下一页](caching-data-with-the-objectdatasource-vb.md)
