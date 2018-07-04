---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: 处理使用 Entity Framework 4.0 ASP.NET 4 Web 应用程序中的并发 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: c22f06e68b15d3fbf13e9f2af0e19631abe076ec
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37392732"
---
<a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>使用 Entity Framework 4.0 ASP.NET 4 Web 应用程序中处理并发
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。 如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。


上一教程中介绍了如何进行排序和筛选器数据使用`ObjectDataSource`控件和 Entity Framework。 本教程介绍使用实体框架的 ASP.NET web 应用程序中的并发处理的选项。 将创建一个新的网页，专用于更新讲师的办公室分配。 将处理该页面中和在前面创建的部门页面中的并发问题。

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>并发冲突

一个用户编辑记录和另一个用户编辑同一个记录之前的第一个用户更改写入到数据库时，将发生并发冲突。 如果不设置实体框架来检测此类冲突，最后更新数据库的人员覆盖其他用户的更改。 在许多应用程序，这种风险是可接受的并且无需配置要处理可能的并发冲突的应用程序。 (如果有几个用户或几个更新，或如果并不重要的某些更改将被覆盖，如果并发编程的成本可能胜过权益。)如果不需要担心并发冲突，则可以跳过本教程;系列中的其余两个教程不依赖于在本视频中生成的所有内容。

### <a name="pessimistic-concurrency-locking"></a>悲观并发 （锁定）

如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。 这称为*保守式并发*。 例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。 如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为他们得到的是正在更改的数据的副本。 如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。

管理锁定有一些缺点。 编程可能很复杂。 它需要大量的数据库管理资源，并且它可能导致性能问题的应用程序的用户数增加 （即，它不能很好）。 由于这些原因，并不是所有的数据库管理系统都支持悲观并发。 实体框架不提供内置支持，以及本教程不展示如何实现它。

### <a name="optimistic-concurrency"></a>开放式并发

悲观并发的替代方法是*乐观并发*。 悲观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。 例如，John 运行*Department.aspx*页上，单击**编辑**历史记录部门中的链接并减少**预算**从 1000 美元，000.00 金额为 $125,000.00。 （John 管理竞争部门和想要释放了他自己部门成本）

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 单击之前**更新**，Jane 运行在同一页上，单击**编辑**链接，获取的历史记录部门，然后更改**开始日期**字段从 2011 年 1 月 10 日到 1/1 /1999。 （Jane 管理历史记录部门和想要为其提供更多的资历。）

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John 单击**更新**Jane 单击的第一次，然后**更新**。 Jane 的浏览器现在列表**预算**金额为 $ 1000，000.00，但这不正确，因为已由 John 到 $125,000.00 更改量。

一些可在此方案中执行的操作包括：

- 可以跟踪用户已修改的属性，并仅更新数据库中相应的列。 在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。 下次有人浏览历史记录系时，他们将看到 1/1/1999年和 125,000.00 美元。 

    这是实体框架中的默认行为，它可以显著减少可能导致数据丢失的冲突数。 但是，此行为不能避免数据丢失，如果实体的同一属性进行竞争性更改。 此外，此行为并不总是可行;当存储的过程映射到的实体类型时，所有实体的属性更新时在数据库中进行了任何更改到的实体。
- 可以让 John 的更改覆盖 Jane 的更改。 Jane 单击后**更新**，则**预算**量将恢复为 1000，000.00 美元。 这称为“客户端优先”或“最后一个优先”。 （客户端的值优先于什么是数据存储区中。）
- 您可以防止 Jane 的更改更新数据库中。 通常情况下，会显示一条错误消息，给她提供数据的当前状态，让其重新输入她的更改，如果仍想要使它们。 通过将保存其输入为她提供机会来重新将其应用而无需重新输入它，可以进一步自动化该过程。 这称为“存储优先”方案。 （数据存储值优先于客户端提交的值。）

### <a name="detecting-concurrency-conflicts"></a>检测并发冲突

在实体框架中，您可以通过处理中解决冲突`OptimisticConcurrencyException`Entity Framework 引发的异常。 为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。 因此，你必须正确配置数据库和数据模型。 启用冲突检测的某些选项包括：

- 在数据库中，包括可用于确定何时已更改行的表格列。 然后，可以配置实体框架，将该列中的包含`Where`的 SQL 子句`Update`或`Delete`命令。

    目的就在于`Timestamp`中的列`OfficeAssignment`表。

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    数据类型`Timestamp`也称为列`Timestamp`。 但是，列实际上不包含日期或时间值。 相反，值是每次更新行时递增的序列号。 在中`Update`或`Delete`命令，`Where`子句包括原始`Timestamp`值。 如果正在更新的行已由另一个用户中的值更改`Timestamp`不同于原始值，因此`Where`子句将返回要更新的行。 实体框架找到任何行，已更新由当前`Update`或`Delete`命令 （即，在受影响的行数为零），将其解释为并发冲突。
- 配置实体框架，以便在表中包含的每个列的原始值`Where`子句`Update`和`Delete`命令。

    如下所示的第一个选项，如果自第一次读取一行，该行中的任何内容已更改`Where`子句不会返回的行，若要更新，该实体框架将解释为并发冲突。 此方法是尽可能使用更有效`Timestamp`字段，但可能会降低效率。 对于包含许多列的数据库表，它可能会导致非常大`Where`子句，并在 web 应用程序需要维护大量的状态。 维护大量的状态会影响应用程序性能，因为它需要服务器资源 （例如，会话状态） 或必须包含在网页本身 （例如，视图状态）。

在本教程中，您将添加错误处理不具有跟踪属性的实体的开放式并发冲突 (`Department`实体) 和实体具有跟踪属性 (`OfficeAssignment`实体)。

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>处理开放式并发，且无跟踪属性

若要实现的乐观并发`Department`实体，其不具有跟踪 (`Timestamp`) 属性，将完成以下任务：

- 将数据模型更改为启用并发跟踪`Department`实体。
- 在中`SchoolRepository`类中的处理并发异常`SaveChanges`方法。
- 在中*Departments.aspx*页上，通过向用户警告尝试的更改未成功显示一条消息的处理并发异常。 然后，用户可以查看的当前值，然后重试所做的更改，如果仍然需要它们。

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>启用跟踪数据模型中的并发

在 Visual Studio 中，打开在您使用在此系列中的上一教程中的 Contoso University web 应用程序。

打开*SchoolModel.edmx*，然后在数据模型设计器中，右键单击`Name`中的属性`Department`实体，然后单击**属性**。 在中**属性**窗口中，更改`ConcurrencyMode`属性设置为`Fixed`。

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

执行相同的其他非主键标量属性 (`Budget`， `StartDate`，和`Administrator`。)（您不能执行此操作的导航属性。）这会指定，只要实体框架生成`Update`或`Delete`SQL 命令来更新`Department`（与原始值） 这些列必须包含在数据库中的实体，`Where`子句。 如果未不找到任何行`Update`或`Delete`命令执行时，实体框架将引发开放式并发异常。

保存并关闭数据模型。

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL 中处理并发异常

打开*SchoolRepository.cs*并添加以下`using`语句`System.Data`命名空间：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

添加以下新`SaveChanges`方法，用于处理开放式并发异常：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

如果并发错误发生时调用此方法，在内存中的实体的属性值将替换为数据库中的当前值。 使网页能够应对其将被重新引发并发异常。

在中`DeleteDepartment`并`UpdateDepartment`方法，将替换现有调用`context.SaveChanges()`通过调用`SaveChanges()`为了调用新方法。

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>在表示层中处理并发异常

打开*Departments.aspx*并添加`OnDeleted="DepartmentsObjectDataSource_Deleted"`属性为`DepartmentsObjectDataSource`控件。 控件的开始标记现在将类似于下面的示例。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

在中`DepartmentsGridView`控件，指定表的列中的所有`DataKeyNames`属性，如下面的示例中所示。 请注意，这将创建非常大的视图状态字段，其中的原因之一是使用跟踪字段的原因通常是跟踪并发冲突的首选的方法。

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

打开*Departments.aspx.cs*并添加以下`using`语句`System.Data`命名空间：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

添加以下新方法，将从数据源控件调用`Updated`和`Deleted`事件处理程序处理并发异常：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

此代码检查异常类型，并且如果它是并发异常，该代码动态创建`CustomValidator`又显示一条消息中的控件`ValidationSummary`控件。

调用新方法从`Updated`前面添加的事件处理程序。 此外，创建一个新`Deleted`事件处理程序调用同一方法 （但不执行任何其他操作）：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>在部门页中测试乐观并发

运行*Departments.aspx*页。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

单击**编辑**行中，将在值更改**预算**列。 (请记住，您只能编辑已为本教程中，创建记录因为现有`School`数据库记录包含一些无效数据。 经济部门的记录是尝试使用一个安全密码）。

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

打开新浏览器窗口并运行页再次 （复制到第二个浏览器窗口中的第一个浏览器窗口的地址框的 URL）。

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

单击**编辑**在同一行，之前编辑和更改**预算**为其他值。

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

在第二个浏览器窗口中，单击**更新**。 **预算**量成功更改为此新值。

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

在第一个浏览器窗口中，单击**更新**。 更新将失败。 **预算**量将重新显示使用在第二个浏览器窗口中，设置的值，你看到一条错误消息。

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>使用跟踪属性的处理开放式并发

若要处理的跟踪属性的实体的开放式并发，您将完成以下任务：

- 将存储的过程添加到数据模型来管理`OfficeAssignment`实体。 （跟踪属性和存储的过程不需要一起使用; 它们只需组合在一起此处是为了进行说明。）
- 将 CRUD 方法添加到 DAL 和为 BLL`OfficeAssignment`实体，包括代码来处理在 DAL 的开放式并发异常。
- 创建一个办公室分配 web 页面。
- 测试新的 web 页面中的开放式并发。

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>添加 OfficeAssignment 存储到数据模型的过程

打开*SchoolModel.edmx*文件在模型设计器中，右键单击设计图面上，然后单击**从数据库更新模型**。 在**添加**选项卡**选择数据库对象**对话框中，展开**存储过程**，然后选择这三个`OfficeAssignment`存储过程 (请参阅以下屏幕截图），然后单击**完成**。 （这些存储的过程时，已在数据库中下载或创建其使用的脚本。）

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

右键单击`OfficeAssignment`实体，然后选择**存储过程映射**。

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

设置**插入**，**更新**，并**删除**函数使用其相应存储过程。 有关`OrigTimestamp`的参数`Update`函数中，设置**属性**到`Timestamp`，然后选择**使用原始值**选项。

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

当实体框架调用`UpdateOfficeAssignment`存储的过程，它将通过的原始值`Timestamp`中的列`OrigTimestamp`参数。 存储的过程使用此参数在其`Where`子句：

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

存储的过程还将选择的新值`Timestamp`更新后的列，以便实体框架可以保留`OfficeAssignment`与相应的数据库行同步已在内存中的实体。

(请注意，用于删除办公室分配的存储的过程不会具有`OrigTimestamp`参数。 因此，实体框架无法验证实体不删除它之前变。）

保存并关闭数据模型。

### <a name="adding-officeassignment-methods-to-the-dal"></a>添加对 DAL OfficeAssignment 方法

打开*ISchoolRepository.cs*并添加以下的 CRUD 方法`OfficeAssignment`实体集：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

添加到以下新方法*SchoolRepository.cs*。 在中`UpdateOfficeAssignment`方法，调用本地`SaveChanges`方法而不是`context.SaveChanges`。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

在测试项目中，打开*MockSchoolRepository.cs*并添加以下`OfficeAssignment`集合和 CRUD 方法。 （mock 存储库必须实现存储库接口，或该解决方案将不会编译）。

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>将 OfficeAssignment 方法添加到 BLL

在主项目中，打开*SchoolBL.cs*并添加以下的 CRUD 方法`OfficeAssignment`实体设置为它：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>创建 OfficeAssignments Web 页

创建新的 web 页，使用*Site.Master*母版页并将其命名*OfficeAssignments.aspx*。 添加到以下标记`Content`名为控件`Content2`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

请注意，在`DataKeyNames`属性，该标记指定`Timestamp`属性，以及记录密钥 (`InstructorID`)。 指定属性中的`DataKeyNames`属性会导致控件将它们保存在控件状态 （这是类似于视图状态），因此在回发处理过程中的原始值来提供。

如果您没有保存`Timestamp`值，实体框架不会为它`Where`子句的 sql`Update`命令。 因此不会找到要更新。 因此，实体框架会引发开放式并发异常每次`OfficeAssignment`更新实体。

打开*OfficeAssignments.aspx.cs*并添加以下`using`数据访问层的语句：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

以下代码添加到`Page_Init`方法，使动态数据功能。 此外将添加以下处理程序`ObjectDataSource`控件的`Updated`事件，以检查是否有并发错误：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>在 OfficeAssignments 上测试乐观并发

运行*OfficeAssignments.aspx*页。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

单击**编辑**行中，将在值更改**位置**列。

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

打开新浏览器窗口并运行页再次 （复制到第二个浏览器窗口中的第一个浏览器窗口的 URL）。

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

单击**编辑**在同一行，之前编辑和更改**位置**为其他值。

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

在第二个浏览器窗口中，单击**更新**。

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

切换到第一个浏览器窗口，然后单击**更新**。

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

你看到一条错误消息和**位置**值已更新以显示在第二个浏览器窗口中更改到的值。

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource 控件具有处理并发

`EntityDataSource`控件包括识别数据模型中的并发设置的内置逻辑，并处理更新和相应地删除操作。 但是，与所有异常，则必须处理`OptimisticConcurrencyException`异常自己以提供用户友好的错误消息。

接下来，将配置*Courses.aspx*页面 (使用`EntityDataSource`控件) 允许更新和删除操作并显示一条错误消息，如果发生并发冲突。 `Course`实体不具有跟踪列，因此您将使用相同的方法，就像处理并发`Department`实体： 跟踪所有非键属性的值。

打开*SchoolModel.edmx*文件。 非键属性的`Course`实体 (`Title`， `Credits`，和`DepartmentID`)，将**并发模式**属性设置为`Fixed`。 然后保存并关闭数据模型。

打开*Courses.aspx*页上并进行以下更改：

- 在中`CoursesEntityDataSource`控件中，添加`EnableUpdate="true"`和`EnableDelete="true"`属性。 现在，该控件的开始标记类似于下面的示例：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- 在中`CoursesGridView`控件，更改`DataKeyNames`属性值为`"CourseID,Title,Credits,DepartmentID"`。 然后添加`CommandField`元素`Columns`显示的元素**编辑**并**删除**按钮 (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`)。 `GridView`控件现在类似于下面的示例：

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

运行页面并与你之前在部门页中创建冲突的情况。 在两个浏览器窗口中运行页上，单击**编辑**在相同行在每个窗口中，并在每个使不同的更改。 单击**更新**在一个窗口，然后单击**更新**在其他窗口中。 当您单击**更新**第二个时，你看到错误页面，得到的未处理的并发异常。

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

处理此错误的方式非常类似于如何处理它的`ObjectDataSource`控件。 打开*Courses.aspx*页上，然后在`CoursesEntityDataSource`控件中，指定的处理程序`Deleted`和`Updated`事件。 现在，该控件的开始标记类似于下面的示例：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

之前`CoursesGridView`控件中，添加以下`ValidationSummary`控件：

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

在中*Courses.aspx.cs*，添加`using`语句`System.Data`命名空间中，添加一个方法来检查并发异常，并添加的处理程序`EntityDataSource`控件的`Updated`和`Deleted`处理程序。 该代码将如下所示：

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

此代码，并且你对之间的唯一区别`ObjectDataSource`控件是，在这种情况下并发异常处于`Exception`属性的事件参数对象而不是在该异常`InnerException`属性。

运行页面，然后再次创建并发冲突。 此时会显示一条错误消息：

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

处理并发冲突已介绍完毕。 下一教程将提供有关如何提高性能的 web 应用程序使用 Entity Framework 中的指导。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [下一页](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
