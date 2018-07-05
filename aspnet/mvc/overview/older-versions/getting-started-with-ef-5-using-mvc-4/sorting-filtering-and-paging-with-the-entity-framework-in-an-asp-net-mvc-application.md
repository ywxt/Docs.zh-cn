---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 排序、 筛选和分页与实体框架在 ASP.NET MVC 应用程序 (10 的 3) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: c2b53c5f35b0d7cd519ab3fdcb57c39463c40a8a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401219"
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>排序、 筛选和分页与 ASP.NET MVC 应用程序 (10 的 3) 中的实体框架
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


上一教程中实现一组基本的 CRUD 操作执行的 web 页面`Student`实体。 在本教程将添加排序、 筛选和分页功能**学生**索引页。 同时，还将创建一个执行简单分组的页面。

下图展示了完成操作后的页面外观。 列标题是用户可以单击以按该列排序的链接。 重复单击列标题可在升降排序顺序之间切换。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>向学生索引页添加列排序链接

若要添加到学生索引页进行排序，你将更改`Index`方法`Student`控制器并将代码添加到`Student`索引视图。

### <a name="add-sorting-functionality-to-the-index-method"></a>添加排序功能，到 Index 方法

在中*Controllers\StudentController.cs*，将为`Index`方法使用以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此代码接收来自 URL 中的查询字符串的 `sortOrder` 参数。 ASP.NET MVC 提供查询字符串值作为操作方法的参数。 该参数将是一个字符串，可为“Name”或“Date”，可选择后跟下划线和字符串“desc”来指定降序。 默认排序顺序为升序。

首次请求索引页时，没有任何查询字符串。 学生显示按升序排序依据`LastName`，这是默认设置，如在 fall-through 事例所建立`switch`语句。 当用户单击列标题超链接时，查询字符串中会提供相应的 `sortOrder` 值。

这两个`ViewBag`使用变量，以便该视图可以配置与相应的查询字符串值的列标题超链接：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

这些是三元语句。 第一个指定，如果`sortOrder`参数为 null 或为空，`ViewBag.NameSortParm`应设置为"名称\_desc"; 否则为它应设置为空字符串。 通过这两个语句，视图可如下设置列标题超链接：

| 当前排序顺序 | 姓氏超链接 | 日期超链接 |
| --- | --- | --- |
| 姓氏升序 | descending | ascending |
| 姓氏降序 | ascending | ascending |
| 日期升序 | ascending | descending |
| 日期降序 | ascending | ascending |

该方法使用[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)指定要作为排序依据的列。 该代码会创建[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)变量之前`switch`语句，将修改在`switch`语句，并调用`ToList`方法之后`switch`语句。 当创建和修改 `IQueryable` 变量时，不会向数据库发送任何查询。 您将转换之前未执行查询`IQueryable`对象通过调用一个方法，如集合`ToList`。 因此，此代码导致直到才执行单个查询`return View`语句。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>添加列标题超链接到学生索引视图

在中*Views\Student\Index.cshtml*，替换`<tr>`和`<th>`的标题行的突出显示的代码元素：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

此代码使用中的信息`ViewBag`属性具有相应查询的超链接设置字符串值。

运行页面，然后单击**姓氏**并**注册日期**列标题以验证排序是否工作。

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

单击后**姓氏**标题下方，学生显示按降序姓氏的顺序。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>向学生索引页添加搜索框

要向学生索引页添加筛选功能，需将文本框和提交按钮添加到视图，并在 `Index` 方法中做出相应的更改。 在文本框中输入一个字符串以在名字和姓氏字段中进行搜索。

### <a name="add-filtering-functionality-to-the-index-method"></a>向 Index 方法添加筛选功能

在中*Controllers\StudentController.cs*，将为`Index`用下面的代码 （所做的更改会突出显示） 的方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

已向 `Index` 方法添加 `searchString` 参数。 你还向 LINQ 语句添加`where`clausethat 仅选择的学生的名字或姓氏中包含搜索字符串。 从将添加到索引视图的文本框中接收搜索字符串值。添加的语句[其中](https://msdn.microsoft.com/library/bb535040.aspx)子句执行仅当没有要搜索的值。

> [!NOTE]
> 在许多情况下可以对实体框架实体集或作为内存中集合上的扩展方法调用相同的方法。 结果通常都是相同，但在某些情况下可能会不同。 例如，.NET Framework 实现`Contains`方法将空字符串传递给它，而 SQL Server Compact 4.0 的实体框架提供程序返回空字符串零行，则返回所有行。 因此该示例中的代码 (将放`Where`内的语句`if`语句) 可确保对于所有版本的 SQL Server 获得相同的结果。 此外，.NET Framework 实现`Contains`方法默认情况下，执行区分大小写比较，但实体框架 SQL Server 提供程序默认情况下执行不区分大小写的比较。 因此，调用`ToUpper`使测试显式不区分大小写的方法可确保结果不更改时更改代码更高版本以使用存储库，它将返回`IEnumerable`而不是集合`IQueryable`对象。 （在 `IEnumerable` 集合上调用 `Contains` 方法时，将获得 .NET Framework 实现；当在 `IQueryable` 对象上调用它时，将获得数据库提供程序实现。）


### <a name="add-a-search-box-to-the-student-index-view"></a>向“学生索引”视图添加搜索框

在中*Views\Student\Index.cshtml*，添加打开之前立即突出显示的代码`table`若要创建标题栏、 文本框中，标记和一个**搜索**按钮。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

运行页上，输入搜索字符串，然后单击**搜索**以验证筛选是否正常工作。

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

请注意，URL 不包含"an"搜索字符串，这意味着，如果此页加入书签，您不会获得筛选的列表，当您使用书签。 将更改**搜索**按钮，本教程的后面使用筛选器条件的查询字符串。

## <a name="add-paging-to-the-students-index-page"></a>向学生索引页添加分页

若要向学生索引页添加分页，首先你将安装**PagedList.Mvc** NuGet 包。 然后你将进行中的其他更改`Index`方法并添加分页链接到`Index`视图。 **PagedList.Mvc**是许多很好的分页和排序的 ASP.NET MVC 中，包之一，此处使用旨在仅作为示例，不为相对于其他选择为其建议。 下图显示了分页链接。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>安装 PagedList.MVC NuGet 包

NuGet **PagedList.Mvc**会自动安装包**PagedList**包作为依赖项。 **PagedList**打包安装`PagedList`的集合类型和扩展方法`IQueryable`和`IEnumerable`集合。 扩展方法创建单个页面中的数据`PagedList`共集合您`IQueryable`或`IEnumerable`，和`PagedList`集合提供了一些属性和方法的简化分页。 **PagedList.Mvc**包将安装的分页帮助器显示分页按钮。

从**工具**菜单中，选择**库程序包管理器**，然后**为解决方案管理 NuGet 包**。

在中**管理 NuGet 包**对话框中，单击**联机**在左侧选项卡，然后在搜索框中输入"分页"。 当您看见**PagedList.Mvc**包，单击**安装**。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在中**选择项目**框中，单击**确定**。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>向 Index 方法添加分页功能

在中*Controllers\StudentController.cs*，添加`using`语句`PagedList`命名空间：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

将 `Index` 方法替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

此代码将添加`page`参数、 当前的排序顺序参数和当前的筛选器参数向方法签名，如下所示：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

第一次显示页面时，或者如果用户没有单击分页或排序链接，所有参数都将为 NULL。 如果单击分页链接后，`page`变量将包含要显示的页码。

`A ViewBag` 属性提供了与当前的排序顺序中，视图，因为此值必须包含在分页链接为了保持排序顺序都分页时相同：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

另一个属性， `ViewBag.CurrentFilter`，视图提供当前筛选器字符串。 此值必须包含在分页链接中，以便在分页过程中保持筛选器设置，并且在页面重新显示时必须将其还原到文本框中。 如果在分页过程中搜索字符串发生变化，则页面必须重置为 1，因为新的筛选器会导致显示不同的数据。 在文本框中输入值并按下提交按钮，则会更改搜索字符串。 在这种情况下，`searchString`参数不为 null。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

该方法的末尾`ToPagedList`学生的扩展方法`IQueryable`对象将学生查询转换为支持分页的集合类型中的学生的单个页。 该单个学生页面然后传递给视图：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 方法需要一个页码。 两个问号表示[null 合并运算符](https://msdn.microsoft.com/library/ms173224.aspx)。 NULL 合并运算符为可为 NULL 的类型定义默认值；表达式 `(page ?? 1)` 表示如果 `page` 有值，则返回该值，如果 `page` 为 NULL，则返回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>向学生索引视图添加分页链接

在中*Views\Student\Index.cshtml*，现有代码替换为以下代码：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

页面顶部的 `@model` 语句指定视图现在获取的是 `PagedList` 对象，而不是 `List` 对象。

`using`语句`PagedList.Mvc`，访问 MVC 帮助程序的分页按钮。

该代码使用的重载[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) ，它指定允许[FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

默认值[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)提交表单数据对于 POST，这意味着，参数将 HTTP 消息正文中而不是在 URL 作为查询字符串传递。 当指定 HTTP GET 时，表单数据作为查询字符串在 URL 中传递，从而使用户能够将 URL 加入书签。 [使用 HTTP GET 的 W3C 指南](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定操作不会导致更新时应使用 GET。

单击新页面时可以看到当前的搜索字符串，将使用当前搜索字符串初始化文本框。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

列标题链接使用查询字符串向控制器传递当前搜索字符串，以便用户可以在筛选结果中进行排序：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

显示当前页和总页数。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

如果没有要显示的页面，会显示"的 0 页 0"。 (在这种情况下页面数大于页计数因为`Model.PageNumber`为 1，和`Model.PageCount`为 0。)

通过显示分页按钮`PagedListPager`帮助程序：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`帮助器提供多种可自定义，包括 Url 和样式设置的选项。 有关详细信息，请参阅[TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 站点上。

运行页。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

单击不同排序顺序的分页链接，以确保分页正常工作。 然后输入一个搜索字符串并再次尝试分页，以验证分页也可以正确地进行排序和筛选。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>创建有关页面，其中显示学生统计信息

对于 Contoso 大学网站的一页，将显示每个注册日期注册学生的数量。 这需要对组进行分组和简单计算。 若要完成此操作，需要执行以下操作：

- 为需要传递给视图的数据创建一个视图模型类。
- 修改`About`中的方法`Home`控制器。
- 修改`About`视图。

### <a name="create-the-view-model"></a>创建视图模型

创建*Viewmodel*文件夹。 在该文件夹中，将类文件添加*EnrollmentDateGroup.cs*和现有代码替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改主控制器

在中*HomeController.cs*，添加以下`using`语句的文件的顶部：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

类的左大括号后立即添加数据库上下文的类变量：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

将 `About` 方法替换为以下代码：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 语句按注册日期对学生实体进行分组，计算每组中实体的数量，并将结果存储在 `EnrollmentDateGroup` 视图模型对象的集合中。

添加`Dispose`方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改“关于”视图

中的代码替换*Views\Home\About.cshtml*文件使用以下代码：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

运行应用并单击**有关**链接。 表格中会显示每个注册日期的学生计数。

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>可选： 将应用部署到 Windows Azure

到目前为止应用程序已运行本地 IIS Express 中在开发计算机上。 若要使其可供其他人通过 Internet 使用，必须将其部署到 web 宿主提供程序。 在本教程的此可选部分会将其部署到 Windows Azure 网站。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>使用 Code First 迁移部署数据库

若要部署的数据库将使用 Code First 迁移。 在创建发布配置文件，用于从 Visual Studio 部署的配置设置时，将选择一个复选框，将标记为**执行 Code First 迁移 （应用程序启动时运行）**。 此设置会导致部署过程会自动配置应用程序*Web.config*文件在目标服务器上，以便使用 Code First`MigrateDatabaseToLatestVersion`初始值设定项类。

Visual Studio 不会不执行任何操作与数据库在部署过程。 当部署的应用程序部署后首次访问数据库时，Code First 自动创建数据库或更新数据库架构到最新版本。 如果应用程序实现迁移`Seed`方法，方法运行后创建的数据库或更新的模式。

迁移`Seed`方法插入测试数据。 如果在部署到生产环境，您将必须更改`Seed`方法，使其仅插入想要插入到您的生产数据库的数据。 例如，在当前数据模型中可能想要开发数据库中具有真实的课程，但虚构的学生。 您可以编写`Seed`方法负载皆在开发中，并在部署到生产环境之前然后注释虚构的学生。 也可以编写`Seed`方法加载仅课程，并通过使用应用程序的 UI 手动测试数据库中输入虚构的学生。

### <a name="get-a-windows-azure-account"></a>获取 Windows Azure 帐户

你将需要 Windows Azure 帐户。 如果你还没有一个，可以在几分钟即可完成创建一个免费试用帐户。 有关详细信息，请参阅[Windows Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>在 Windows Azure 中创建网站和 SQL 数据库

Windows Azure 网站将运行在共享宿主环境中，这意味着它与其他 Windows Azure 客户端共享的虚拟机 (Vm) 上运行。 共享宿主环境是开始在云中低成本方法。 更高版本，如果你的 web 流量的增加，应用程序可以缩放以满足的需求的专用 Vm 上运行。 如果您需要更复杂的体系结构，则可以迁移到 Windows Azure 云服务。 云服务可以根据需要配置的专用 Vm 上运行。

Windows Azure SQL 数据库是基于 SQL Server 技术构建的基于云的关系数据库服务。 工具和适用于 SQL Server 的应用程序还可用于 SQL 数据库。

1. 在中[Windows Azure 管理门户](https://manage.windowsazure.com/)，单击**网站**在左侧选项卡，然后单击**新建**。

    ![管理门户中的新按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. 单击**自定义创建**。

    ![使用管理门户中的数据库链接创建](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **新建网站-自定义创建**向导随即打开。
3. 在中**新的 Web 站点**步骤的向导中，输入中的字符串**URL**框，以用作你的应用程序的唯一 URL。 完整的 URL 将包含的在此处输入和文本框旁边看到的后缀。 图中显示了"ConU"，但该 URL 是可能因此必须另外选择一个。

    ![使用管理门户中的数据库链接创建](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. 在中**区域**下拉列表中，选择离你近的区域。 此设置指定你的网站将运行在哪个数据中心。
5. 在中**数据库**下拉列表中，选择**创建免费的 20 MB SQL 数据库**。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. 在中**数据库连接字符串名称**，输入*SchoolContext*。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 单击向右框底部的箭头。 该向导将前进到**数据库设置**步骤。
8. 在中**名称**框中，输入*ContosoUniversityDB*。
9. 在中**服务器**框中，选择**新建 SQL 数据库服务器**。 或者，如果你之前创建一个服务器，您可以从下拉列表中选择该服务器。
10. 输入管理员**登录名**并**密码**。 如果所选**新的 SQL 数据库服务器**不要输入现有名称和密码在此处，应输入新名称和密码，你现在定义以后访问数据库时使用。 如果你选择之前创建的服务器，您将为该服务器输入凭据。 对于本教程中，不会选择***高级***复选框。 ***高级***选项使您可以将数据库设置为[排序规则](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。
11. 选择相同**区域**与你为网站选择。
12. 单击右下角的框以指示你已完成的复选标记。   
  
    ![数据库设置步骤使用数据库向导创建的新 Web 站点中的](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    下图显示了使用现有的 SQL Server 和登录名。   
  
    ![数据库设置步骤使用数据库向导创建的新 Web 站点中的](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    管理门户返回到网站页中，并**状态**列显示正在创建网站。 （通常不到一分钟），一段时间后**状态**列显示已成功创建网站。 在左侧导航栏中，你的帐户中的站点数会显示旁边**网站**旁边显示图标，而数据库数量**SQL 数据库**图标。

## <a name="deploy-the-application-to-windows-azure"></a>部署到 Windows Azure 应用程序

1. 在 Visual Studio 中，右键单击该项目中的**解决方案资源管理器**，然后选择**发布**从上下文菜单。  
  
    ![在项目上下文菜单中发布](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. 在中**配置文件**选项卡**发布 Web**向导中，单击**导入**。  
  
    ![导入发布设置](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. 如果之前未添加您的 Windows Azure 订阅在 Visual Studio 中，执行以下步骤。 在这些步骤，添加你的订阅，以便列表下的下拉列表**从 Windows Azure 网站导入**将包括您的网站。

    a. 在中**导入发布配置文件**对话框中，单击**从 Windows Azure 网站导入**，然后单击**添加 Windows Azure 订阅**。

    ![添加 Windows Azure 订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. 在中**导入 Windows Azure 订阅**对话框中，单击**下载订阅文件**。

    ![下载订阅文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 在浏览器窗口中，保存 *.publishsettings*文件。

    ![下载的.publishsettings 文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 安全性- *publishsettings*文件包含用于管理你的 Windows Azure 订阅和服务的凭据 （未编码）。 此文件的安全最佳做法是将其暂时存储在源目录的外部 (例如在*Libraries\Documents*文件夹)，然后将其导入完成后删除。 恶意用户获得访问权`.publishsettings`文件可以编辑、 创建和删除 Windows Azure 服务。

    d. 在中**导入 Windows Azure 订阅**对话框中，单击**浏览**，并导航到 *.publishsettings*文件。

    ![下载订阅](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. 单击“导入” 。

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. 在中**导入发布配置文件**对话框中，选择**从 Windows Azure 网站导入**，从下拉列表中，选择你的网站，然后单击**确定**。  
  
    ![导入发布配置文件](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. 在中**连接**选项卡上，单击**验证连接**以确保设置正确无误。  
  
    ![验证连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 当已验证的连接时，旁边会出现一个绿色复选标记**验证连接**按钮。 单击 **“下一步”**。  
  
    ![已成功验证的连接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. 打开**远程连接字符串**下拉列表下的**SchoolContext** ，然后选择你创建的数据库的连接字符串。
8. 选择**执行 Code First 迁移 （应用程序启动时运行）**。
9. 取消选中**在运行时使用此连接字符串**有关**UserContext (DefaultConnection)**，因为此应用程序不使用成员资格数据库。   
  
    ![设置选项卡](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. 单击 **“下一步”**。
11. 在中**预览版**选项卡上，单击**开始预览**。  
  
    ![在预览选项卡中的开始预览按钮](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    该选项卡显示将复制到服务器的文件的列表。 显示预览不需要发布应用程序，但是需要注意的一个有用的函数。 在这种情况下，不需要使用显示的文件列表执行任何操作。 下一次部署此应用程序，只有已更改的文件会出现在此列表中。  
  
    ![开始预览文件输出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. 单击“发布” 。  
    Visual Studio 开始执行将文件复制到 Windows Azure 服务器的过程。
13. **输出**窗口将显示已执行的部署操作并报告成功完成部署。  
  
    ![报告部署成功的输出窗口](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 成功完成部署后的默认浏览器会自动打开指向已部署的 web 站点的 URL。  
    您创建的应用程序现在在云中运行。 单击学生选项卡。  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

此时您*SchoolContext*已在 Windows Azure SQL 数据库中创建了数据库因为所选**执行 Code First 迁移 （在应用启动时运行）**。 *Web.config*已部署的 web 站点中的文件已更改，以便[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项将运行你的代码读取或写入数据库中的数据的第一个时间 (所选时发生**学生**选项卡):

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

部署过程还创建了新的连接字符串 *(SchoolContext\_DatabasePublish*) 的代码优先迁移来更新数据库架构和数据库的种子设定使用。

![Database_Publish 连接字符串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection*连接字符串是成员资格数据库 （其中我们不使用在本教程中）。 *SchoolContext*连接字符串是为 ContosoUniversity 数据库。

您可以找到在计算机上的 Web.config 文件的已部署的版本*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*。您可以访问已部署*Web.config*文件本身通过使用 FTP。 有关说明，请参阅[使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 按照说明开头的"若要使用 FTP 工具，需要以下三项： FTP URL、 用户名和密码。"

> [!NOTE]
> Web 应用不会实现安全性，以便找到 URL 的任何人可以更改的数据。 有关如何保护网站上的说明，请参阅[包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Windows Azure 网站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 可以阻止其他人使用该站点，通过 Windows Azure 管理门户或**服务器资源管理器**Visual Studio 可停止站点中。


![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>代码的第一个初始值设定项

在部署部分中看到[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项正在使用。 代码首先还提供您可以使用，包括其他初始值设定项[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （默认值）， [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx)和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways`初始值设定项也可用于设置单元测试的条件。 您还可以编写您自己初始值设定项，并且如果不想等待，直到应用程序从读取或写入数据库，您可以显式调用初始值设定项。 初始值设定项的完整说明，请参阅一书的第 6 章[Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan Miller。

## <a name="summary"></a>总结

在本教程中已了解如何创建数据模型并实现基本的 CRUD，排序、 筛选、 分页和分组功能。 在下一教程将开始通过展开数据模型来查看更高级的主题。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [下一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
