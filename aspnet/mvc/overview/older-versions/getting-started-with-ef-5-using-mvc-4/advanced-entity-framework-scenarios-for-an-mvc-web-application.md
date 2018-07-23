---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC Web 应用程序 (10 / 10) 的高级 Entity Framework 方案 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5a75d85140a40660314ab267fdd74a8058d791fc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832670"
---
<a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>高级的 Entity Framework 方案 MVC Web 应用程序 (10 / 10)
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


上一教程中实现的存储库和工作单元模式。 本教程涵盖以下主题：

- 执行原始 SQL 查询。
- 执行非跟踪查询。
- 检查查询发送到数据库。
- 使用代理类。
- 禁用自动检测更改。
- 保存时禁用验证更改。
- [错误和解决方法](#errors)

对于大多数这些主题，您将使用已创建的页。 若要使用原始 SQL 执行批量更新将创建新页面的更新的数据库中的所有课程的可修读人数：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

并使用非跟踪查询会将新的验证逻辑添加到院系编辑页：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>原始 SQL 的查询

实体框架 Code First API 包括使您能够直接向数据库传递 SQL 命令的方法。 有下列选项：

- 使用`DbSet.SqlQuery`返回实体类型的查询方法。 返回的对象必须是预期的类型的`DbSet`对象，并且它们会自动跟踪的数据库上下文除非关闭跟踪。 (参见下一节`AsNoTracking`方法。)
- 使用`Database.SqlQuery`方法的返回类型不是实体的查询。 数据库上下文不会跟踪返回的数据，即使你使用该方法来检索实体类型也是如此。
- 使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx)非查询命令。

使用 Entity Framework 的优点之一是它可避免你编写跟数据库过于耦合的代码 它会自动生成 SQL 查询和命令，使得你无需自行编写。 当您需要运行的手动创建，特定 SQL 查询时有一些特殊情况，但这些方法使你能够处理此类异常。

在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。 一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。 在本教程中，将用户输入集成到查询中时会使用参数化查询。

### <a name="calling-a-query-that-returns-entities"></a>调用一个查询返回实体

假设你想`GenericRepository`类以提供附加的筛选和排序的灵活性而无需通过其他方法创建派生的类。 若要实现此目的的一种方法是添加接受 SQL 查询的方法。 然后，可以指定任何类型的筛选或排序你想在控制器中，如`Where`取决于联接或子查询的子句。 在本部分中将了解如何实现此类方法。

创建`GetWithRawSql`方法通过添加以下代码*GenericRepository.cs*:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

在中*CourseController.cs*，调用新方法从`Details`方法，如以下示例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

您可以在这种情况下使用`GetByID`使用的方法，但您`GetWithRawSql`方法来验证`GetWithRawSQL`方法的工作原理。

运行验证 select 查询的工作原理的详细信息页 (选择**课程**选项卡，然后**详细信息**面向一门课程)。

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>调用一个查询返回其他类型的对象

之前你在“关于”页面创建了一个学生统计信息网格，显示每个注册日期的学生数量。 此代码*HomeController.cs*使用 LINQ:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

假设你想要编写检索此数据直接在 SQL，而不是使用 LINQ 中的代码。 若要执行此操作需要运行的查询返回实体对象以外的内容，这意味着您需要使用`Database.SqlQuery`方法。

在中*HomeController.cs*，将 LINQ 语句中的为`About`方法使用以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

运行关于页面。 显示的数据和之前一样。

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>调用更新查询

假设 Contoso 大学管理员想要能够在数据库中，如更改的每个课程的可修读人数执行大容量更改。 如果该大学有大量的课程，检索所有实体并单独更改会降低效率。 在本部分中，你将实施允许用户指定的要更改所有课程的可修读人数因子的 web 页面并将通过执行 SQL 中进行更改`UPDATE`语句。 页面外观类似于下图：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

在上一教程中使用泛型存储库读取和更新`Course`中的实体`Course`控制器。 对于此大容量更新操作，需要创建不是泛型存储库中的新存储库方法。 为此，你将创建一个专用`CourseRepository`派生的类`GenericRepository`类。

在中*DAL*文件夹中，创建*CourseRepository.cs*和现有代码替换为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

在中*UnitOfWork.cs*，更改`Course`存储库类型从`GenericRepository<Course>`到 `CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

在中*CourseContoller.cs*，添加`UpdateCourseCredits`方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

此方法将使用两个`HttpGet`和`HttpPost`。 当`HttpGet``UpdateCourseCredits`方法运行`multiplier`变量将为 null，并且视图将显示一个空文本框和一个提交按钮上, 图中所示。

当**更新**单击按钮和`HttpPost`方法运行`multiplier`会在文本框中输入的值。 然后，代码调用该存储库`UpdateCourseCredits`方法，返回的受影响的行，并且该值存储在`ViewBag`对象。 当视图收到中受影响的行数`ViewBag`对象，则显示该编号而不是在文本框中，并提交按钮，如下图中所示：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

创建中的视图*Views\Course*更新课程学分页上的文件夹：

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

在中*Views\Course\UpdateCourseCredits.cshtml*，模板代码替换为以下代码：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

通过选择**Courses**选项卡运行`UpdateCourseCredits`方法，然后在浏览器地址栏中 URL 的末尾添加"/ UpdateCourseCredits"到 (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。 在文本框中输入数字：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

单击**Update**。 你会看到受影响的行数：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

单击**Back To List**可以看到课程列表，其中可修读人数已经替换成修改后的数字。

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

有关原始 SQL 查询的详细信息，请参阅[原始 SQL 查询](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)Entity Framework 团队博客上。

## <a name="no-tracking-queries"></a>非跟踪查询

当数据库上下文检索数据库行，并创建表示它们的实体对象时，默认情况下它跟踪的内存中的实体是否保持同步，在数据库中的内容。 更新实体时，内存中的数据充当缓存并使用该数据。 在 Web 应用程序中，此缓存通常是不必要的，因为上下文实例通常生存期较短（创建新的实例并用于处理每个请求），并且通常在再次使用该实体之前处理读取实体的上下文。

您可以指定是否将上下文跟踪的查询的实体对象使用`AsNoTracking`方法。 可能想要执行的典型方案包括以下操作：

- 该查询将检索此类大型的数据量关闭跟踪可能会显著提高性能。
- 你想要附加一个实体来更新它，但前面要检索同一实体用于其他目的。 由于数据库上下文已跟踪了该实体，因此无法附加要更改的实体。 若要避免这种情况发生的一种方法是使用`AsNoTracking`与以前的查询选项。

在本部分中将实现说明了这些方案中的第二个的业务逻辑。 具体而言，将强制实施业务规则，规定一名讲师，不能为多个部门的管理员。

在中*DepartmentController.cs*，添加新的方法可从调用`Edit`和`Create`方法以确保没有两个部门都具有相同的管理员：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

将代码中的添加`try`块`HttpPost``Edit`方法来调用这种新方法，如果没有任何验证错误。 `try`块现在看起来如下例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

运行院系编辑页面并尝试将某个部门的管理员更改为一名讲师人员已经是另一个部门的管理员。 获取预期的错误消息：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

现在运行院系编辑页面再次和此变更**预算**量。 当您单击**保存**，您将看到一个错误页面：

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

异常错误消息是"`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`"由于以下一系列事件将发生这种情况：

- `Edit`方法调用`ValidateOneAdministratorAssignmentPerInstructor`方法，检索所有具有他们的管理员为 Kim Abercrombie 的部门。 它使英语系时要读取。 因为这是正在编辑的部门，不会报告错误。 由于此读取操作，但是，从数据库读取的英语系实体是现在跟踪数据库上下文。
- `Edit`方法尝试设置`Modified`标志在英语版 department 实体创建的 MVC 模型联编程序，但该失败，因为上下文已跟踪英语系的实体。

此问题的一种解决方案是为了防止上下文跟踪内存中的部门实体验证查询来检索。 这样做，因为你不会更新该实体或从其缓存在内存中受益的方式再次读取它没有缺点。

在中*DepartmentController.cs*，请在`ValidateOneAdministratorAssignmentPerInstructor`方法中，不指定任何跟踪，如在下面的示例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

重复尝试编辑**预算**院系的量。 这一次操作成功，并在站点返回预期的院系索引页上，显示修改后的预算值。

## <a name="examining-queries-sent-to-the-database"></a>检查发送到数据库的查询

有时能够以查看发送到数据库的实际 SQL 查询对于开发者来说是很有用的。 若要执行此操作，可以检查在调试器中的查询变量，或调用查询的`ToString`方法。 若要试用此项，将看看简单查询并再看会发生什么情况向其添加此类预先加载、 筛选和排序选项。

在中*控制器/CourseController*，将为`Index`方法使用以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

现在中设置断点*GenericRepository.cs*上`return query.ToList();`并且`return orderBy(query).ToList();`语句的`Get`方法。 在调试模式下运行该项目并选择课程索引页。 当代码到达该断点时，检查`query`变量。 可以看到发送到 SQL Server 的查询。 它是一个简单`Select`语句：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

查询可以是太长，无法在 Visual Studio 中调试窗口中显示。 若要查看整个查询，可以复制变量值并将其粘贴到文本编辑器中：

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

现在将向课程索引页添加下拉列表，以便用户可以筛选为特定部门。 您将对课程进行排序的标题，并且你将指定预先加载`Department`导航属性。 在中*CourseController.cs*，将为`Index`方法使用以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

该方法接收的下拉列表中所选的值`SelectedDepartment`参数。 如果未选择任何项，则此参数将为 null。

一个`SelectList`集合，其中包含所有部门的下拉列表将传递给视图。 参数传递给`SelectList`构造函数指定值字段名称、 文本字段名称和所选的项。

有关`Get`方法`Course`存储库中，代码将指定的筛选器表达式、 排序顺序和预先加载`Department`导航属性。 筛选器表达式始终返回`true`如果未选择下拉列表中 (即，`SelectedDepartment`为 null)。

在中*Views\Course\Index.cshtml*，打开之前立即`table`标记中，添加以下代码以创建下拉列表和一个提交按钮：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

以及中仍保持设置的断点`GenericRepository`类中，运行课程索引页。 继续操作，代码命中断点的行，第一次两次，以便将在浏览器中显示的页。 从下拉列表中选择一个部门，然后单击**筛选器**:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

这一次第一个断点将在下拉列表的部门查询。 跳过该步骤，并查看`query`变量下一次代码达到断点才能看到什么`Course`查询现在如下所示。 你将看到类似于以下内容：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

您可以看到查询现`JOIN`加载的查询`Department`数据以及`Course`数据，并且必须包含`WHERE`子句。

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>使用代理类

当 Entity Framework 创建实体实例 （例如，当执行查询时） 时，它通常创建其作为动态生成的派生类型的代理的实体的实例。 此代理将覆盖要插入挂钩，以便访问属性时自动执行的操作的实体的某些虚拟属性。 例如，这种机制用于支持延迟加载的关系。

大多数情况下无需注意此使用代理服务器，但有例外情况：

- 在某些情况下您可能想要阻止实体框架创建代理实例。 例如，序列化非代理实例可能比序列化代理实例更高效。
- 当您实例化实体类使用`new`运算符，别让代理实例。 这意味着不会功能，如延迟加载和自动更改跟踪。 这通常是好了;您通常不需要延迟加载，因为您将创建新的实体不在数据库中，且通常无需更改跟踪，如果您显式标记为实体`Added`。 但是，如果您需要延迟加载，并且你需要更改跟踪，您可以创建新实体实例与使用的代理`Create`方法的`DbSet`类。
- 你可能想要从代理类型中获取的实际实体类型。 可以使用`GetObjectType`方法的`ObjectContext`类，以获取代理类型实例的实际实体类型。

有关详细信息，请参阅[使用代理](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)Entity Framework 团队博客上。

## <a name="disabling-automatic-detection-of-changes"></a>禁用自动检测更改

Entity Framework 通过比较的实体的当前值与原始值来判断更改实体的方式 （因此需要发送更新到数据库）。 如果实体已查询或附加，存储的原始值。 如下方法会导致自动脏值：

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

如果正在跟踪大量实体，并且你调用下列方法之一很多时候在循环中，您可能会显著的性能改进，通过暂时关闭自动更改检测使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)属性。 有关详细信息，请参阅[自动检测更改](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。

## <a name="disabling-validation-when-saving-changes"></a>保存时禁用验证更改

当您调用`SaveChanges`方法中，默认情况下，实体框架中已更改的所有实体的所有属性的数据之前验证更新数据库。 如果你已更新大量实体和已验证了数据，这项工作是不必要和无法使保存的过程所做的更改通过暂时关闭验证需要更少的时间。 您可以执行操作，使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)属性。 有关详细信息，请参阅[验证](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。

## <a name="summary"></a>总结

这样就完成这一系列的 ASP.NET MVC 应用程序中使用实体框架的教程。 其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

有关如何部署 web 应用程序后已生成的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)MSDN 库中。

有关相关的 MVC 中，例如身份验证和授权，其他主题的信息，请参阅[MVC 的推荐资源](../../getting-started/recommended-resources-for-mvc.md)。

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>鸣谢

- Tom Dykstra 编写本教程中的原始版本和是 Microsoft Web 平台和工具内容团队的资深编程作家。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 合著了本教程和大多数更新对 EF 5 和 MVC 4 的工作的操作一样。 Rick 是 Microsoft 将重点放在 Azure 和 MVC 的资深编程作家。
- [Rowan Miller](http://www.romiller.com)和实体框架团队的其他成员协助代码评审和帮助调试与我们正在 EF 5 更新本教程时出现的迁移的许多问题。

## <a name="vb"></a>VB

当最初生成在本教程时，我们提供已完成的下载项目的 C# 和 VB 的版本。 利用此更新中，我们将向每一章，以使其更轻松地在系列中，但由于时间限制，我们已经不为 vb。 这样做了其他优先任意位置开始的 C# 可下载项目 如果您构建使用这些教程为 VB 项目，并愿意与他人共享的请让我们知道。

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>错误和解决方法

### <a name="cannot-createshadow-copy"></a>无法创建/卷影副本

错误消息：

*无法创建/卷影副本 DotNetOpenAuth.OpenId 该文件已存在时。*

解决方案：

等待几秒钟，并刷新页面。

### <a name="update-database-not-recognized"></a>更新数据库无法识别

错误消息：

*术语更新数据库未识别为 cmdlet、 函数、 脚本文件或可操作程序的名称。检查名称的拼写或如果已包含路径，验证路径正确，然后重试。*(从*`Update-Database`* PMC 命令。)

解决方案：

退出 Visual Studio。 重新打开项目，然后重试。

### <a name="validation-failed"></a>验证失败

错误消息：

*对一个或多个实体的验证失败。请参阅 EntityValidationErrors 属性的更多详细信息。* (从*`Update-Database`* PMC 命令。)

解决方案：

此问题的一个原因是验证错误时`Seed`方法运行。 请参阅[种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)有关调试的提示`Seed`方法。

### <a name="http-50019-error"></a>HTTP 500.19 错误

错误消息：

*不能访问 HTTP 错误 500.19-内部服务器错误，请求的页面，因为该页的相关的配置数据无效。*

解决方案：

出现此错误的一种方法是从拥有多个解决方案，它们使用相同的端口号的每个副本。 通常可以通过退出的 Visual Studio 中，所有实例，然后重新启动该项目上的工作来解决此问题。 如果这不起作用，请尝试更改端口号。 右键单击项目文件，然后单击属性。 选择**Web**选项卡，然后将更改中的端口号**项目 Url**文本框。

### <a name="error-locating-sql-server-instance"></a>定位 SQL Server 实例出错

错误消息：

*建立与 SQL Server 的连接时发生与网络相关或特定于实例的错误。未找到或无法访问服务器。验证实例名称正确以及 SQL Server 配置为允许远程连接。(提供程序： SQL 网络接口，错误： 26-定位指定服务器/实例时)*

解决方案：

检查连接字符串。 如果你已手动删除数据库，更改构造字符串中的数据库的名称。

> [!div class="step-by-step"]
> [上一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [下一页](building-the-ef5-mvc4-chapter-downloads.md)
