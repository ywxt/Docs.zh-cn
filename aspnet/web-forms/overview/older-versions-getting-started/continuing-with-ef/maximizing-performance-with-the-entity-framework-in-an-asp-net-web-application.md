---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: 使用 Entity Framework 4.0 ASP.NET 4 Web 应用程序中性能最大化 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 7d7c66289f09179a98e09532172477d5b06c70bd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824476"
---
<a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>最大化 Entity Framework 4.0 中的 ASP.NET 4 Web 应用程序的性能
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。 如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。


在前面的教程，您已了解如何处理并发冲突。 本教程介绍可用于提高使用实体框架的 ASP.NET web 应用程序的性能选项。 你将了解几种方法最大化性能或诊断性能问题。

以下各节中提供信息很可能是在各种方案中有用：

- 有效地加载相关的数据。
- 管理视图状态。

以下各节中显示的信息可能具有单独的查询存在性能问题的情况下很有用：

- 使用`NoTracking`合并选项。
- 预编译 LINQ 查询。
- 检查发送到数据库的查询命令。

以下部分中介绍的信息是可能适用于具有极大的数据模型的应用程序：

- 预生成视图。

> [!NOTE]
> Web 应用程序性能受许多因素，其中包括诸如请求和响应数据的大小，数据库查询、 多少个请求服务器可以排入队列和速度它可以提供服务，以及甚至任何效率的速度你可能正在使用的客户端脚本库。 如果是在应用程序中关键的性能或测试或体验显示了应用程序性能并不令人满意，应遵循正常协议以进行性能优化。 度量值以确定性能瓶颈的发生位置，然后再解决会对应用程序的总体性能产生重大影响的区域。
> 
> 本主题主要侧重于在其中也许可以提高性能的 ASP.NET 中的实体框架的方式。 此处的建议是确定数据访问是一个在应用程序中的性能瓶颈时很有用。 但如前所述，此处所述的方法不应被视为&quot;最佳做法&quot;一般情况下，其中许多是适合仅在发生异常情况或地址非常特定的一种性能瓶颈。


若要开始本教程，启动 Visual Studio 并打开在您使用在上一教程中的 Contoso University web 应用程序。

## <a name="efficiently-loading-related-data"></a>有效地加载相关的数据

有几种方法，实体框架可以相关的数据加载到实体的导航属性：

- *延迟加载*。 首次读取实体时，不检索相关数据。 然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。 这会导致发送到数据库的多个查询 — 一个用于实体本身，一个必须检索每个相关实体数据的时间。 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*预先加载*。 读取该实体时，会同时检索相关数据。 此时通常会出现单一联接查询，检索所有必需数据。 使用指定预先加载`Include`方法中，为您已看到在这些教程。

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *显式加载*。 这是类似于延迟加载的只不过显式检索相关的数据中的代码;它不会自动发生时您访问导航属性。 加载相关的数据使用手动`Load`导航属性的集合，或者你的方法使用`Load`保存单个对象的属性的引用属性的方法。 (例如，调用`PersonReference.Load`方法以加载`Person`导航属性`Department`实体。)

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

因为它们不立即检索属性值，延迟加载和显式加载也都称为*延迟加载*。

延迟加载是由设计器生成的对象上下文的默认行为。 如果您打开*SchoolModel.Designer.cs*文件，用于定义对象上下文类，您会发现三个构造函数方法，以及每个包含以下语句：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

一般情况下，如果您知道你需要相关的数据对于每个实体检索到的预先加载提供最佳性能，因为发送到数据库的单个查询通常比个检索每个实体的单独查询更有效。 另一方面，如果你需要仅不常访问的实体的导航属性或仅为一个较小组实体、 延迟加载或显式加载可能是更高效，因为预先加载将检索数据超过所需的数据。

在 web 应用程序中，延迟加载可能相对较小值的因为会影响对相关数据的需求的用户操作将在浏览器，没有连接到呈现的页，在对象上下文中。 另一方面，当您数据绑定控件，您通常知道哪些所需的数据，并因此它通常是最佳选择预先加载或延迟的加载根据什么是适用于每个方案。

此外，数据绑定控件可能使用的实体对象后释放对象上下文。 在这种情况下，若要延迟加载导航属性的尝试会失败。 您收到的错误消息十分明显： &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource`控件默认情况下禁用延迟加载。 有关`ObjectDataSource`控件当前教程中使用 （或如果访问对象上下文从页面代码），有几种方法可以进行延迟加载默认情况下禁用。 实例化对象上下文时，可以禁用它。 例如，可以将以下行添加到构造函数方法`SchoolRepository`类：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

对于 Contoso 大学应用程序，你将进行自动禁用延迟加载，以便不需要时实例化上下文设置此属性的对象上下文。

打开*SchoolModel.edmx*数据模型，单击设计图面上，，然后在属性窗格中设置**已启用延迟加载**属性设置为`False`。 保存并关闭数据模型。

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>管理视图状态

为了提供更新功能，ASP.NET web 页必须存储实体的原始属性值时将在页面呈现。 处理控件的回发期间可以重新创建该实体的原始状态，并调用实体的`Attach`方法，然后再应用更改并调用`SaveChanges`方法。 默认情况下，ASP.NET Web 窗体数据控件使用视图状态来存储原始值。 但是，视图状态会影响性能，因为它会显著增加的大小发往和来自浏览器的页的隐藏字段中存储。

管理视图状态或替代项，例如会话状态的方法不是唯一的实体框架中，因此本教程不会转到本主题中详细信息。 有关详细信息，请参阅链接，在本教程末尾。

但是，版本 4 的 ASP.NET 提供了新的 Web 窗体应用程序的每个 ASP.NET 开发人员应注意的视图状态的工作方式：`ViewStateMode`属性。 可以在页面或控件级别，设置此新属性，它使您的页面的默认情况下禁用视图状态并使其仅对需要它的控件。

对于性能很重要的应用程序，一个好的做法是始终禁用页级视图状态并启用该只需要它的控件。 Contoso University 页中的视图状态的大小不会显著减少了这种方法，但若要查看其工作原理，您无需劳*Instructors.aspx*页。 该页面包含许多控件，包括`Label`禁用了视图状态的控件。 无此页上的控件实际需要能够查看已启用状态。 (`DataKeyNames`的属性`GridView`控件指定了回发，之间必须保持的状态，但这些值保存在控件状态，不会受`ViewStateMode`属性。)

`Page`指令和`Label`控件标记当前类似于下面的示例：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

进行以下更改：

- 添加`ViewStateMode="Disabled"`到`Page`指令。
- 删除`ViewStateMode="Disabled"`从`Label`控件。

标记现在类似于下面的示例：

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

现在所有控件禁用视图状态。 如果您稍后添加确实需要使用视图状态的控件，您需要做是包括`ViewStateMode="Enabled"`为该控件的属性。

## <a name="using-the-notracking-merge-option"></a>使用 NoTracking 合并选项

当对象上下文检索数据库行，并创建表示它们的实体对象时，默认情况下它还跟踪这些实体对象使用其对象状态管理器。 此跟踪数据充当缓存并更新实体时使用。 Web 应用程序通常具有生存期较短的对象上下文实例，因为查询通常返回不需要进行跟踪，因为读取它们的对象上下文将会被释放之前再次使用它读取的实体的任何数据或更新。

在实体框架中，您可以指定是否在对象上下文跟踪实体对象通过设置*合并选项*。 可以设置的单个查询或实体集的合并选项。 如果将其设置为实体集，这意味着您将设置为该实体集创建的所有查询的默认合并选项。

对于 Contoso 大学应用程序，跟踪的任何实体集，因此您可以合并选项设置为从存储库中，访问不需要`NoTracking`的实例化存储库类中的对象上下文时这些实体集。 （请注意，在本教程中，设置的合并选项不会有显著影响应用程序的性能。 `NoTracking`选项有可能使仅在某些大数据容量方案中的可观察性能改进。)

在 DAL 文件夹中，打开*SchoolRepository.cs*文件，并添加设置的合并选项，有关该实体集在存储库访问的构造函数方法：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>预编译 LINQ 查询

实体框架将执行 Entity SQL 查询的生存期内的第一个时间给定`ObjectContext`实例，需要一段时间来编译查询。 缓存的编译结果，这意味着查询的后续执行速度快得多。 LINQ 查询将按照类似的模式，只不过每次执行查询时完成一些工作来进行编译查询。 换而言之，对于 LINQ 查询，默认情况下不是所有编译的结果进行缓存。

如果希望反复运行对象上下文的生命周期中的 LINQ 查询，可以编写代码，使所有编译缓存首次运行 LINQ 查询的结果。

为说明，将执行此操作两个`Get`中的方法`SchoolRepository`类，其中一个不采用任何参数 (`GetInstructorNames`方法)，另一个需要一个参数 (`GetDepartmentsByAdministrator`方法)。 这些方法根据所代表现在实际上无需编译，因为它们不是 LINQ 查询：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

但是，以便你可以尝试编译的查询，将继续像这些编写为以下 LINQ 查询：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

可以将这些方法中的代码更改为什么具有上面所示，运行应用程序以验证它一起工作，然后再继续。 但以下说明直接跳转到创建预编译的版本。

创建一个类文件中的*DAL*文件夹中，其命名*SchoolEntities.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

此代码将创建一个分部类以扩展自动生成的对象上下文类。 分部类包含两个已编译的 LINQ 查询使用`Compile`方法的`CompiledQuery`类。 它还将创建可用于调用查询的方法。 保存并关闭此文件。

接下来，在*SchoolRepository.cs*，更改现有`GetInstructorNames`和`GetDepartmentsByAdministrator`存储库中的方法的类，使它们调用已编译的查询：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

运行*Departments.aspx*页后，可以验证它是否像以前一样工作。 `GetInstructorNames`为了填充管理员下拉列表中，调用方法和`GetDepartmentsByAdministrator`单击时调用方法**更新**以验证没有讲师是多个管理员部门。

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

在 Contoso 大学应用程序，只是为了不是因为它也会显著提高性能，请参阅如何执行此操作，已预编译的查询。 预编译 LINQ 查询 does 添加到代码中的复杂性，因此请确保不要仅供查询，它们实际上代表你的应用程序中的性能瓶颈。

## <a name="examining-queries-sent-to-the-database"></a>检查发送到数据库的查询

当正在调查性能问题时，有时很必要了解确切的实体框架将发送到数据库的 SQL 命令。 如果您正在使用`IQueryable`对象，若要执行此操作的一种方法是使用`ToTraceString`方法。

在中*SchoolRepository.cs*，更改中的代码`GetDepartmentsByName`方法以匹配下面的示例：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

`departments`变量必须强制转换为`ObjectQuery`类型，只因为`Where`上一行末尾处的方法创建`IQueryable`对象; 而无需`Where`方法，强制转换不会有必要。

上设置断点`return`行，然后运行*Departments.aspx*在调试器中的页。 当命中断点时，检查`commandText`变量中**局部变量**窗口并使用文本可视化工具 (中的放大镜**值**列) 以显示其值在**文本可视化工具**窗口。 您可以看到此代码生成的整个 SQL 命令：

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

或者，在 Visual Studio Ultimate 中的 IntelliTrace 功能使您能够查看生成的实体框架，不需要您要更改代码或甚至设置断点的 SQL 命令。

> [!NOTE]
> 仅当你具有 Visual Studio Ultimate，您可以执行以下过程。


还原中的原始代码`GetDepartmentsByName`方法，并运行*Departments.aspx*在调试器中的页。

在 Visual Studio 中，选择**调试**菜单，然后**IntelliTrace**，然后**IntelliTrace 事件**。

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

在中**IntelliTrace**窗口中，单击**全部中断**。

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**IntelliTrace**窗口将显示最新事件的列表：

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

单击**ADO.NET**行。 它将展开以显示命令文本：

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

可以将整个命令文本字符串复制到从剪贴板**局部变量**窗口。

假设在您使用具有多个表、 关系和列比简单的数据库`School`数据库。 您可能会发现，收集所有信息的查询需要在单个`Select`包含多个语句`Join`子句变得太复杂，无法有效地工作。 在这种情况下可以从预先加载与显式加载，以简化查询进行切换。

例如，请尝试更改中的代码`GetDepartmentsByName`中的方法*SchoolRepository.cs*。 当前，方法可让对象查询具有`Include`方法`Person`和`Courses`导航属性。 替换为`return`语句的执行显式加载，如下面的示例中所示的代码：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

运行*Departments.aspx*页在调试器中，选中**IntelliTrace**之前未再次为您的窗口。 现在，其中没有单个查询之前，您将看到一长串的它们。

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

单击第一个**ADO.NET**行以查看发生了什么问题复杂查询您查看前面。

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

将查询从部门已成为一个简单`Select`查询不使用`Join`子句，但它后跟检索相关的课程和管理员的单独查询，每个部门使用一组的两个查询返回的原始查询。

> [!NOTE]
> 如果将延迟加载已启用，在这里，使用同一查询重复很多时候，看到的模式可能会导致从延迟加载。 你通常想要避免一模式是主表中的每一行的延迟加载相关的数据。 除非你已验证的单一联接查询太过复杂，来有效地，您通常可以通过更改主查询以使用预先加载来提高性能，在这种情况下。


## <a name="pre-generating-views"></a>预生成视图

当`ObjectContext`对象首次创建新的应用程序域中，实体框架将生成一组类，它用来访问数据库。 这些类称为*视图*，和如果您有一个非常大的数据模型，生成这些视图可以延迟到页的第一个请求的 web 站点的响应后初始化新的应用程序域。 通过在编译时，而不在运行时创建视图，可以减少此第一个请求延迟。

> [!NOTE]
> 如果你的应用程序没有任何一个极大的数据模型，或者如果它具有较大的数据模型，但无需考虑性能问题影响仅第一次页面请求回收 IIS 后，可以跳过此部分。 每次实例化的操作不会创建视图`ObjectContext`对象，因为视图是否已缓存在应用程序域。 因此，除非频繁正在回收 IIS 应用程序，很少的页请求将受益预生成的视图。


您可以预生成视图使用*EdmGen.exe*命令行工具或通过使用*文本模板转换工具包*(T4) 模板。 在本教程将使用 T4 模板。

中*DAL*文件夹中，添加文件 using**文本模板**模板 (它位于**常规**中的节点**已安装的模板**列表)，并将其命名*SchoolModel.Views.tt*。 文件中的现有代码替换为以下代码：

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

此代码生成的视图 *.edmx*文件位于模板所在的文件夹并为模板文件具有相同名称。 例如，如果模板文件名为*SchoolModel.Views.tt*，它将查找名为的数据模型文件*SchoolModel.edmx*。

保存该文件，然后右键单击该文件中的**解决方案资源管理器**，然后选择**运行自定义工具**。

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio 生成的代码文件创建视图，其名称为*SchoolModel.Views.cs*基于该模板。 (您可能已经注意到，即使你选择之前会生成代码文件**运行自定义工具**，只要保存模板文件。)

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

现在可以运行该应用程序并验证它像以前一样工作。

有关预生成视图的详细信息，请参阅以下资源：

- [如何： 预生成视图以提高查询性能](https://msdn.microsoft.com/library/bb896240.aspx)MSDN 网站上。 说明如何使用`EdmGen.exe`命令行工具预生成视图。
- [隔离使用预编译或预生成视图性能 Entity Framework 4](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx) Windows Server AppFabric 客户顾问团队博客上。

为提高性能的 ASP.NET web 应用程序使用实体框架中已介绍完毕。 有关更多信息，请参见以下资源：

- [性能注意事项 （实体框架）](https://msdn.microsoft.com/library/cc853327.aspx) MSDN 网站上。
- [实体框架团队博客上与性能相关的帖子](https://blogs.msdn.com/b/adonet/archive/tags/performance/)。
- [EF 合并选项和已编译的查询](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx)。 博客文章，说明已编译的查询和合并的意外的行为选项，例如`NoTracking`。 如果您计划使用已编译的查询或处理应用程序中的合并选项设置，这首先阅读。
- [实体框架相关将数据和建模客户顾问团队博客中发布](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)。 包含已编译的查询和使用 Visual Studio 2010 Profiler 来发现性能问题的帖子。
- [实体框架提供了有关提高了高度复杂的查询的性能建议的论坛主题](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)。
- [ASP.NET 状态管理建议](https://msdn.microsoft.com/library/z1hkazw7.aspx)。
- [使用实体框架和 ObjectDataSource： 自定义分页](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx)。 在这些教程中创建的 ContosoUniversity 应用程序说明如何实现分页中的为基础的博客文章*Departments.aspx*页。

下一步的教程介绍了一些对实体框架版本 4 中新增的重要增强功能。

> [!div class="step-by-step"]
> [上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [下一页](what-s-new-in-the-entity-framework-4.md)
