---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 使用实体框架 4.0 和 ObjectDataSource 控件，第 1 部分： 入门 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与实体框架教程系列入门教程为基础。 如果 yo...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 5eaeaa0aa474e1aed86954e6c10dd1703b938944
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834674"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>使用实体框架 4.0 和 ObjectDataSource 控件，第 1 部分： 入门
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。
> 
> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 示例应用程序是虚构的 Contoso 大学网站。 它包括诸如学生入学、 课程创建和导师分配等功能。
> 
> 本教程介绍了 C# 中的示例。 [可下载的示例](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)包含 C# 和 Visual Basic 中的代码。
> 
> ## <a name="database-first"></a>数据库优先
> 
> 有三种方法可以使用实体框架中的数据： *Database First*， *Model First*，并*Code First*。 本教程适用于第一个数据库。 有关如何选择最适合你的方案指南这些工作流之间的差异信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="web-forms"></a>Web Forms — Web 窗体
> 
> 入门系列中，如本系列教程使用 ASP.NET Web 窗体模型，并假设你已了解如何使用 Visual Studio 中的 ASP.NET Web 窗体。 如果不这样做，请参阅[Getting Started with ASP.NET 4.5 Web 窗体](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 如果想要使用的 ASP.NET MVC 框架，请参阅[开始使用 ASP.NET MVC 的 Entity Framework 使用](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="software-versions"></a>软件版本
> 
> | **本教程中所示** | **也可用于** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Web 的 visual Studio 2010 Express。 本教程不经过了更高版本的 Visual Studio。 有许多差异菜单选项、 对话框和模板。 |
> | .NET 4 | .NET 4.5 是与.NET 4 中，向后的兼容，但尚未安装.NET 4.5 测试本教程。 |
> | 实体框架 4 | 本教程不经过了实体框架的更高版本。 从 Entity Framework 5 开始，默认情况下使用 EF `DbContext API` ，引入了 EF 4.1。 EntityDataSource 控件设计为使用`ObjectContext`API。 有关如何使用 EntityDataSource 控件，其`DbContext`API，请参阅[这篇博客文章](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)。 |
> 
> ## <a name="questions"></a>问题
> 
> 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)，则[实体框架和 LINQ to 实体论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。


`EntityDataSource`控件可以非常快速地创建应用程序，但它通常要求您保留大量的业务逻辑和中的数据访问逻辑应用 *.aspx*页。 如果希望应用程序复杂性增长而增加，并要求不间断的维护，您可以为了创建预先投入更多的开发时间*n 层*或*分层*应用程序结构这就是更易于维护。 若要实现此体系结构，请从业务逻辑层 (BLL) 和数据访问层 (DAL) 分隔的表示层。 若要实现此结构的一种方法是使用`ObjectDataSource`而不是控制`EntityDataSource`控件。 当你使用`ObjectDataSource`控件，实现你自己的数据访问代码，然后调用其 *.aspx*页使用具有许多相同的控件功能的其他数据源控件。 这允许您将 n 层方法的优点与使用 Web 窗体控件进行数据访问的优势相结合。

`ObjectDataSource`控制可以让你更大的灵活性以及通过其他方式。 编写你自己的数据访问代码，因为它是更轻松地执行不止是读取、 插入、 更新或删除特定实体类型，这是任务的`EntityDataSource`控件旨在执行。 例如，可以执行日志记录每次更新实体时，存档数据，每次删除一个实体，或自动检查和更新相关数据根据需要时具有的外键值的行插入。

## <a name="business-logic-and-repository-classes"></a>业务逻辑和存储库类

`ObjectDataSource`控件通过调用创建的类的工作原理。 类包含方法用于检索和更新数据，并提供对这些方法的名称`ObjectDataSource`标记中的控件。 在呈现或回发处理期间`ObjectDataSource`调用你指定的方法。

除了基本的 CRUD 操作，创建要用于类`ObjectDataSource`控件可能需要执行业务逻辑时`ObjectDataSource`读取或更新数据。 例如，更新部门时，您可能需要验证没有其他部门具有相同的管理员，因为一个人不能为多个部门的管理员。

在某些`ObjectDataSource`文档，如[ObjectDataSource 类概述](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)，该控件调用的类称为*业务对象*包括业务逻辑和数据访问逻辑. 在本教程将创建单独的类为业务逻辑和数据访问逻辑。 封装数据访问逻辑的类称为*存储库*。 业务逻辑类包括业务逻辑的方法和数据访问方法，但数据访问方法调用的存储库来执行数据访问任务。

您还将创建一个抽象层之间 BLL 和 DAL 有助于自动化的单元测试的 BLL。 此抽象层是通过创建一个接口并实例化业务逻辑类中的存储库时使用该接口实现的。 这使您的业务逻辑类提供对任何实现存储库接口的对象的引用。 对于正常操作中，需要提供适用于实体框架的存储库对象。 对于测试，需要提供适用于一种方法，可以轻松地进行处理，如类变量定义为集合中存储的数据的存储库对象。

下图显示了一个业务逻辑类，包含数据访问逻辑，而无需存储库，另一个使用存储库之间的差异。

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

将首先在其中创建网页`ObjectDataSource`控件绑定到的存储库直接，因为它仅执行基本的数据访问任务。 在下一教程将使用验证逻辑创建业务逻辑类并将绑定`ObjectDataSource`到存储库类而不是该类的控件。 此外将创建单元测试用于验证逻辑。 在此系列中的第三个教程中，您将添加排序和筛选的应用程序的功能。

本教程中创建的页面可使用`Departments`中创建的数据模型的实体集[入门系列教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>更新数据库和数据模型

在将开始本教程通过更改的数据库，这两个需要进行相应更改到数据模型中创建的两个[开始使用实体框架和 Web 窗体](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程。 在这些教程之一，设计器中手动数据库更改后与数据库同步数据模型进行更改。 在本教程中，您将使用设计器的**从数据库更新模型**工具来自动更新数据模型。

### <a name="adding-a-relationship-to-the-database"></a>添加到数据库的关系

在 Visual Studio 中，打开 Contoso University web 应用程序中创建[开始使用实体框架和 Web 窗体](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)系列教程，然后打开`SchoolDiagram`数据库关系图。

如果您看一下`Department`表在数据库关系图中，你将看到它具有`Administrator`列。 此列是外键的`Person`表中，但没有外键关系在数据库中定义。 您需要创建该关系并更新数据模型，使实体框架可以自动处理这种关系。

在数据库关系图中，右键单击`Department`表，然后选择**关系**。

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

在中**Foreign Key Relationships**中，单击**添加**，然后单击省略号**表和列规范**。

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

在**表和列**对话框框中，设置主键表和字段`Person`并`PersonID`，并设置外键表和字段`Department`和`Administrator`。 (关系名称时执行此操作时，将从`FK_Department_Department`到`FK_Department_Person`。)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

单击**确定**中**表和列**框中，单击**关闭**中**外键关系**框，并保存所做的更改。 在系统询问你是否要保存`Person`并`Department`表，单击**是**。

> [!NOTE]
> 如果已删除`Person`相对应的中已存在的数据行`Administrator`列中，您将无法保存此更改。 在这种情况下，使用中的表编辑器**服务器资源管理器**若要确保`Administrator`中的值每`Department`行包含中是否实际存在的记录 ID`Person`表。
> 
> 保存更改后，你将不能删除中的行将`Person`表如果该人是部门管理员。 在生产应用程序中，会提供特定错误消息，当数据库约束会阻止删除，或将指定的级联删除。 有关如何指定级联删除的示例，请参阅[实体框架和 ASP.NET – 获取启动第 2 部分](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)。


### <a name="adding-a-view-to-the-database"></a>将视图添加到数据库

在新*Departments.aspx*你将需要创建的页上，你想要提供名称采用"姓氏，名字"格式的讲师，下拉列表，以便用户可以选择部门管理员。 若要更加轻松地执行此操作，将在数据库中创建一个视图。 该视图将包括只需通过下拉列表所需的数据: （正确格式） 的完整名称和记录密钥。

在中**服务器资源管理器**，展开*School.mdf*，右键单击**视图**文件夹，然后选择**添加新视图**。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

单击**关闭**时**添加表**对话框随即出现，并将以下 SQL 语句粘贴到 SQL 窗格：

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

保存为视图`vInstructorName`。

### <a name="updating-the-data-model"></a>更新数据模型

在中*DAL*文件夹中，打开*SchoolModel.edmx*文件，右键单击设计图面上，然后选择**从数据库更新模型**。

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

在中**选择数据库对象**对话框中，选择**添加**选项卡并选择刚创建的视图。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

单击 **“完成”**。

在设计器中，可以看到该工具创建`vInstructorName`实体和新的关联之间`Department`和`Person`实体。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> 在中**输出**并**错误列表**windows 可能会看到一条警告消息，通知您该工具自动创建主数据库密钥的新`vInstructorName`视图。 这是预期行为。


到新引用时`vInstructorName`在代码中的实体，你不想要使用的前缀为其小写字母"v"的数据库约定。 因此，您将重命名的实体和实体集在模型中。

打开**模型浏览器**。 您看到`vInstructorName`列为实体类型和视图。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

下**SchoolModel** (不**SchoolModel.Store**)，右键单击**vInstructorName** ，然后选择**属性**。 在中**属性**窗口中，更改**名称**属性设置为"InstructorName"，并更改**实体集名称**属性设置为"InstructorNames"。

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

保存并关闭数据模型中，然后再重新生成项目。

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>使用存储库类和 ObjectDataSource 控件

创建新的类文件中*DAL*文件夹中，其命名*SchoolRepository.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

此代码提供单个`GetDepartments`方法返回的实体中的所有`Departments`实体集。 因为您知道您将会访问`Person`导航属性的每一行返回，您指定的预先加载该属性使用`Include`方法。 类还实现`IDisposable`接口，以确保释放对象时释放数据库连接。

> [!NOTE]
> 一种常见做法是创建每个实体类型的存储库类。 在本教程中，使用多个实体类型的一个存储库类。 有关存储库模式的详细信息，请参阅中的帖子[实体框架团队的博客](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)并[Julie Lerman 的博客](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)。


`GetDepartments`方法将返回`IEnumerable`对象而非`IQueryable`为了确保即使存储库对象本身被释放后返回的集合的可用对象。 `IQueryable`每当访问，但可能会尝试呈现数据的数据绑定控件时释放存储库对象，对象可能会导致数据库访问权限。 您可以返回另一个集合类型，如`IList`对象而不是`IEnumerable`对象。 但是，返回`IEnumerable`对象，可以确保你可以如执行典型的只读列表处理任务`foreach`循环和 LINQ 查询，但您不能添加或删除项在集合中，这可能意味着，此类更改会保存到数据库。

创建*Departments.aspx*使用页面*Site.Master*母版页，并添加中的以下标记`Content`控件命名为`Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

此标记创建`ObjectDataSource`控件，以使用刚刚创建的存储库类和一个`GridView`控件来显示数据。 `GridView`控件指定**编辑**并**删除**命令，但你尚未添加代码以尚未支持它们。

多个列使用`DynamicField`控件，以便可以充分利用自动数据格式设置和验证功能。 对于这些工作，您必须调用`EnableDynamicData`中的方法`Page_Init`事件处理程序。 (`DynamicControl`控件中不使用`Administrator`字段，因为它们不使用导航属性。)

`Vertical-Align="Top"`属性将变得重要更高版本时，添加具有嵌套列`GridView`到网格控件。

打开*Departments.aspx.cs*文件，并添加以下`using`语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

然后添加以下处理程序的页面的`Init`事件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

在中*DAL*文件夹中，创建名为的新类文件*Department.cs*和现有代码替换为以下代码：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

此代码添加到数据模型元数据。 它指定`Budget`的属性`Department`实体实际上表示货币，尽管其数据类型是`Decimal`，并指定值必须介于 0 到 1000，000.00 美元之间。 它还指定`StartDate`属性的格式应为日期格式 mm/dd/yyyy。

运行*Departments.aspx*页。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

请注意，尽管未指定的格式字符串*Departments.aspx*页面标记**预算**或**开始日期**货币和日期的列，默认值格式设置已应用到通过在它们`DynamicField`控件，使用中提供的元数据*Department.cs*文件。

## <a name="adding-insert-and-delete-functionality"></a>添加插入和删除功能

打开*SchoolRepository.cs*，添加以下代码以创建`Insert`方法和一个`Delete`方法。 该代码还包括一个名为方法`GenerateDepartmentID`计算以供下一步的可用记录密钥值`Insert`方法。 这是必需的因为数据库未配置为计算此自动为`Department`表。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 方法

`DeleteDepartment`方法调用`Attach`方法，以重新建立在内存中的实体和数据库之间的对象上下文的对象状态管理器维护的链接行它表示。 此方法调用之前必须发生`SaveChanges`方法。

术语*对象上下文*派生的实体框架类是指`ObjectContext`类，用于访问实体集和实体。 在此项目的代码中，类命名为`SchoolEntities`，和它的一个实例始终命名为`context`。 对象上下文*对象状态管理器*是派生一个类`ObjectStateManager`类。 对象与使用对象状态管理器来存储实体对象，并用于跟踪是否每个为其相应的表行或数据库中的行与同步。

读取实体时，对象上下文将其存储在对象状态管理器和跟踪的对象的表示形式是否与数据库同步。 例如，如果更改属性值，是设置标志以指示您更改的属性不再与数据库同步。 然后调用`SaveChanges`方法，对象上下文知道要执行的操作数据库中由于对象状态管理器知道究竟什么是实体的当前状态和数据库的状态之间差别。

但是，此过程通常不使用在 web 应用程序，因为不读取实体，以及其对象状态管理器中的所有内容的对象上下文实例将在页面呈现后进行处理。 必须将更改应用的对象上下文实例是一个为回发处理实例化的新。 情况下`DeleteDepartment`方法，`ObjectDataSource`控件的实体的原始版本重新创建为你上，从视图状态中值，但此重新创建`Department`对象状态管理器中不存在实体。 如果您调用`DeleteObject`此重新创建实体的方法，该调用会失败，因为对象上下文不知道实体是否与数据库同步。 但是，调用`Attach`方法重新建立最初自动执行操作在对象上下文的早期实例读取实体时在数据库中重新创建的实体和值之间的同一个跟踪。

有不想要跟踪对象状态管理器中中的实体的对象上下文，并可以设置标志以防止它执行该操作。 本系列教程的后续教程中显示了此示例。

### <a name="the-savechanges-method"></a>SaveChanges 方法

此简单的存储库类说明了如何执行 CRUD 操作的基本原则。 在此示例中，`SaveChanges`每次更新后立即调用方法。 在生产应用程序中，可能想要调用`SaveChanges`从单独的方法来为您提供更好地控制更新数据库时的方法。 （下一个教程结尾处将找到指向讨论工作模式，这是一种协调相关的更新的方法的单元的白皮书的链接。）此外请注意，在示例中，`DeleteDepartment`方法不包括用于处理并发冲突的代码; 将在本系列后面的教程中添加代码来执行该操作。

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>检索讲师名称来选择插入时

用户必须能够从下拉列表中的讲师列表中选择管理员创建的新部门时。 因此，将以下代码添加到*SchoolRepository.cs*若要创建一个方法来检索讲师使用前面创建的视图的列表：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>用于插入部门创建页

创建*DepartmentsAdd.aspx*使用页面*Site.Master*页上，并添加中的以下标记`Content`控件命名为`Content2`:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

此标记创建两个`ObjectDataSource`控件，另一个用于插入新`Department`实体，另一个用于检索有关出现教师姓名`DropDownList`用于选择院系管理员的控制。 创建标记`DetailsView`输入新部门，和它，则指定的处理程序控件的控件`ItemInserting`事件，以便您可以设置`Administrator`外键的值。 在结束时`ValidationSummary`控件来显示错误消息。

打开*DepartmentsAdd.aspx.cs*并添加以下`using`语句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

添加以下类变量和方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init`方法可启用动态数据功能。 处理程序`DropDownList`控件的`Init`事件保存到控件，并且的处理程序的引用`DetailsView`控件的`Inserting`事件使用该引用获取`PersonID`的所选的讲师和更新的值`Administrator`的外键属性`Department`实体。

运行页上，为新系添加信息，然后单击**插入**链接。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

输入的另一个新的部门值。 输入一个大于 1000，在 000.00**预算**字段和选项卡移动到下一个字段。 在字段中，会显示一个星号，如果鼠标指针悬停在其上时，可以看到该字段中输入的元数据中的错误消息。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

单击**插入**，并查看显示的错误消息`ValidationSummary`控件在页面底部。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

接下来，关闭浏览器并打开*Departments.aspx*页。 添加到删除功能*Departments.aspx*通过添加页面`DeleteMethod`属性为`ObjectDataSource`控件，和一个`DataKeyNames`属性为`GridView`控件。 这些控件的开始标记现在将类似于下面的示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

运行页。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

删除在运行时添加了系*DepartmentsAdd.aspx*页。

## <a name="adding-update-functionality"></a>添加更新功能

打开*SchoolRepository.cs*并添加以下`Update`方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

当您单击**更新**中*Departments.aspx*页上，`ObjectDataSource`控件创建两个`Department`实体要传递给`UpdateDepartment`方法。 一个包含视图状态中存储的原始值，另一个包含输入的新值`GridView`控件。 中的代码`UpdateDepartment`方法传递`Department`具有到的原始值的实体`Attach`方法，以建立的实体之间定义什么是数据库中跟踪。 然后代码将传递`Department`具有新值的实体`ApplyCurrentValues`方法。 对象上下文将旧的和新值进行比较。 如果新值不同于旧值，则对象上下文更改的属性值。 `SaveChanges`方法然后更新数据库中仅已更改的列。 （但是，如果此实体的更新函数映射到存储过程，整个行会更新而不考虑其列已更改。）

打开*Departments.aspx*文件，并添加以下属性，`DepartmentsObjectDataSource`控件：

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 为此原因旧值存储在视图状态，以便它们可以与中的新值进行比较`Update`方法。
- `OldValuesParameterFormatString="orig{0}"`   
 这会通知的控件的原始值参数的名称是`origDepartment`。

开始标记的标记`ObjectDataSource`控件现在类似于下面的示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

添加`OnRowUpdating="DepartmentsGridView_RowUpdating"`属性为`GridView`控件。 将使用此设置`Administrator`属性值根据用户选择下拉列表中的行。 `GridView`现在开始标记类似于下面的示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

添加`EditItemTemplate`控制`Administrator`列与`GridView`控制后立即,`ItemTemplate`为该列的控件：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

这`EditItemTemplate`控件是类似于`InsertItemTemplate`控制*DepartmentsAdd.aspx*页。 不同之处是使用设置该控件的初始值`SelectedValue`属性。

之前`GridView`控件中，添加`ValidationSummary`控制中那样*DepartmentsAdd.aspx*页。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

打开*Departments.aspx.cs* ，并立即分部类声明后，添加以下代码以创建私有字段以引用`DropDownList`控件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

然后将处理程序添加`DropDownList`控件的`Init`事件并`GridView`控件的`RowUpdating`事件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

处理程序`Init`事件将保存到的引用`DropDownList`类字段中的控件。 处理程序`RowUpdating`事件使用的引用以获取用户输入的值并将其应用于`Administrator`属性的`Department`实体。

使用*DepartmentsAdd.aspx*页以添加新系，然后运行*Departments.aspx*页上，单击**编辑**您添加的行上。

> [!NOTE]
> 你将无法再编辑未添加的行 (即，已在数据库中)，由于数据库; 中的无效数据创建与数据库的行的管理员是学生。 如果你尝试编辑其中之一，则会报告类似的错误的错误页 `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`


[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

如果输入无效**预算**金额，然后单击**更新**，请参阅相同星号和您在中看到的错误消息*Departments.aspx*页。

更改字段值或选择不同的管理员，然后单击**更新**。 会显示更改。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

这将完成介绍如何使用`ObjectDataSource`控件的基本的 CRUD （创建、 读取、 更新、 删除） 操作使用 Entity Framework。 已生成一个简单的 n 层应用程序，但与数据访问层，这会增加复杂性自动化的单元测试仍紧密耦合的业务逻辑层。 以下教程中，您将了解如何实现存储库模式，以便单元测试。

> [!div class="step-by-step"]
> [下一篇](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
