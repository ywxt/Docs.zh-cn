---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 为 ASP.NET MVC 应用程序 (1 / 10) 创建的实体框架数据模型 |Microsoft Docs
author: tdykstra
description: 本教程系列的较新版本不可用，Visual Studio 2013、 Entity Framework 6 和 MVC 5。 Contoso University 示例 web 应用程序详细信息
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 68b74d1e1d13aa4ee080913bfd8219d1a9189bb7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377215"
---
<a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>为 ASP.NET MVC 应用程序 (1 / 10) 创建的实体框架数据模型
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > 一个[本系列教程的较新版本](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)不可用，Visual Studio 2013、 Entity Framework 6 和 MVC 5。
> 
> 
> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 示例应用程序供一个虚构的 Contoso 大学网站使用。 它包括诸如学生入学、 课程创建和导师分配等功能。 此教程系列介绍了如何构建 Contoso University 示例应用程序。 你可以[下载完整的应用程序](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)。
> 
> ## <a name="code-first"></a>Code First
> 
> 有三种方法可以使用实体框架中的数据： *Database First*， *Model First*，并*Code First*。 本教程适用于第一个代码。 有关如何选择最适合你的方案指南这些工作流之间的差异信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="mvc"></a>MVC
> 
> 示例应用程序基于[ASP.NET MVC](../../../index.md)。 如果想要使用 ASP.NET Web 窗体模型，请参阅[模型绑定和 Web 窗体](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md)组成的系列教程并[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。
> 
> ## <a name="software-versions"></a>软件版本
> 
> | **本教程中所示** | **也可用于** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Web 的 visual Studio 2012 Express。 这会自动安装 Windows Azure sdk，如果没有 VS 2012 或 VS 2012 Express for Web。 应运行 visual Studio 2013，但本教程尚未经过测试，并且某些菜单选项和对话框不同。 [VS 2013 版本的 Windows Azure SDK](https://go.microsoft.com/fwlink/p/?linkid=323510)是 Windows Azure 部署所必需的。 |
> | .NET 4.5 | 大多数所示的功能将适用于.NET 4 中，但某些不会。 例如，在 EF 中的枚举支持需要.NET 4.5。 |
> | 实体框架 5 |  |
> | [Windows Azure SDK 2.1](https://go.microsoft.com/fwlink/p/?linkid=323511) | 如果您跳过 Windows Azure 部署步骤，则不需要 SDK。 当发布新版本的 SDK 时，该链接将安装较新版本。 在这种情况下，可能需要调整某些新 UI 和功能的说明进行操作。 |
> 
> ## <a name="questions"></a>问题
> 
> 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)，则[实体框架和 LINQ to 实体论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。
> 
> ## <a name="acknowledgments"></a>鸣谢
> 
> 请参阅有关系列中的最后一个教程[确认和有关 VB 注意](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)。
> 
> ## <a name="original-version-of-the-tutorial"></a>在本教程的原始版本
> 
> 本教程的原始版本现已推出[EF 4.1 / MVC 3 电子书](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)。


## <a name="the-contoso-university-web-application"></a>Contoso University Web 应用程序

你将在这些教程中学习构建一个简单的大学网站的应用程序。

用户可以查看和更新学生、 课程和教师信息。 以下是一些你即将创建的页面。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

本教程主要关注于如何使用 Entity Framework , 所以此站点的UI样式都是直接套用内置的模板。

## <a name="prerequisites"></a>系统必备

说明和屏幕快照，在本教程假定你使用的[Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads)或[Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)、 使用最新的更新和 Azure SDK for.NET 安装截至 7 月，2013。 你可以获取所有这些都可以通过以下链接：

[Azure SDK for.NET (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

如果已安装的 Visual Studio，上面的链接将安装所有缺少的组件。 如果未安装 Visual Studio，该链接将安装 Visual Studio 2012 Express for Web。 可以使用 Visual Studio 2013 中，但某些必需的过程和屏幕将有所不同。

## <a name="create-an-mvc-web-application"></a>创建 MVC Web 应用程序

打开 Visual Studio 并创建一个新 C# 项目名为"ContosoUniversity"使用**ASP.NET MVC 4 Web 应用程序**模板。 请确保针对 **.NET Framework 4.5** (你将使用[`enum`属性](https://msdn.microsoft.com/data/hh859576.aspx)，并且需要.NET 4.5)。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**模板。

将保留**Razor**查看引擎选择，并留下**创建单元测试项目**清除复选框。

单击 **“确定”**。

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>设置网站样式

通过几个简单的更改设置站点菜单、 布局和主页。

打开*views/shared\\_Layout.cshtml*，并使用下面的代码替换文件的内容。 突出显示所作更改。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

此代码会更改以下内容：

- 将"My ASP.NET MVC Application"和"your logo here"的模板实例替换为"Contoso University"。
- 添加本教程的后面将使用的多个操作链接。

在中*Views\Home\Index.cshtml*，该文件的内容替换为以下代码以消除有关 ASP.NET 和 MVC 模板段落：

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

在中*Controllers\HomeController.cs*，更改的值`ViewBag.Message`中`Index`到"欢迎使用 Contoso University ！"，如下面的示例中所示的操作方法：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

按 CTRL + F5 以运行该站点。 请参阅主页，其中主菜单。

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>创建数据模型

接下来你将创建 Contoso 大学应用程序的实体类。 首先将以下三个实体：

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` 和 `Enrollment`实体之间是一对多的关系，`Course` 和`Enrollment` 实体之间也是一个对多的关系。 换而言之，一名学生可以修读任意数量的课程, 并且某一课程可以被任意数量的学生修读。

接下来，你将创建与这些实体对应的类。

> [!NOTE]
> 如果您尝试编译项目，然后完成创建所有这些实体类，将收到编译器错误。


### <a name="the-student-entity"></a>Student 实体

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

在中*模型*文件夹中，创建*Student.cs*和现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 属性将成为对应于此类的数据库表中的主键。 名为的属性解释默认情况下，实体框架`ID`或*classname* `ID`为主键。

`Enrollments`属性是*导航属性*。 导航属性中包含与此实体相关的其他实体。 在这种情况下，`Enrollments`的属性`Student`实体将保留所有`Enrollment`实体相关的`Student`实体。 换而言之，如果给定`Student`数据库中的行具有两个相关`Enrollment`行 (包含该学生的主键的行中的值及其`StudentID`外键列)，则该`Student`实体的`Enrollments`导航属性将包含这两个`Enrollment`实体。

导航属性通常定义为`virtual`，以便它们可以充分利用 Entity Framework 的特定功能，如*延迟加载*。 (将解释延迟加载在后面[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列后面的教程。

如果导航属性可以具有多个实体 （如多对多或一对多关系），那么导航属性的类型必须是可以添加、 删除和更新条目的容器，如 `ICollection`。

### <a name="the-enrollment-entity"></a>Enrollment 实体

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在 *Models* 文件夹中，创建 *Enrollment.cs* 并且用以下代码替换现有代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Grade 属性是[枚举](https://msdn.microsoft.com/data/hh859576.aspx)。 问号后`Grade`类型声明指示`Grade`属性是[可以为 null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。 评级为 null 是不同于评级为零，null 表示一个等级未知或者尚未分配。

`StudentID` 属性是一个外键， `Student` 是与其对应的导航属性。 `Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含单个 `Student` 实体 (与前面所看到的 `Student.Enrollments` 导航属性不同后，`Student`中可以容纳多个 `Enrollment` 实体)。

`CourseID` 属性是一个外键， `Course` 是与其对应的导航属性。 `Enrollment` 实体与一个 `Course` 实体相关联。

### <a name="the-course-entity"></a>Course 实体

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

在中*模型*文件夹中，创建*Course.cs*，现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 属性是导航属性。 一个 `Course` 体可以与任意数量的 `Enrollment` 实体相关。

我们会说的详细信息 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)。无）] 属性在下一步的教程。 简单来说，此特性让你能自行指定主键，而不是让数据库自动指定主键。

## <a name="create-the-database-context"></a>创建数据库上下文

协调为给定的数据模型的实体框架功能的主类是*数据库上下文*类。 通过从派生来创建此类[System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)类。 在该类中你可以指定数据模型中包含哪些实体。 你还可以定义某些 Entity Framework 行为。 在此项目中将数据库上下文类命名为 `SchoolContext`。

创建名为的文件夹*DAL* （适用于数据访问层）。 在该文件夹中创建名为的新类文件*SchoolContext.cs*，和现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

此代码将创建[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)每个实体集的属性。 在实体框架术语中，*实体集*通常对应于数据库表和一个*实体*对应于表中的行。

`modelBuilder.Conventions.Remove`中的语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法会阻止表名正在变为复数形式。 如果不这样做，将命名为生成的表`Students`， `Courses`，和`Enrollments`。 相反，将表名`Student`， `Course`，和`Enrollment`。 开发者对表名称是否应为复数意见不一。 本教程使用单数形式，但重要的一点是，你可以选择任意窗体，您的首选，通过包括或省略这行代码。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)是 SQL Server Express 数据库引擎的按需启动并在用户模式下运行的轻型版本。 中的 SQL Server Express，使您可以使用数据库作为特殊执行模式运行 LocalDB *.mdf*文件。 通常情况下，LocalDB 数据库文件保存在*应用程序\_数据*web 项目的文件夹。 在 SQL Server Express 用户实例功能还使您可以使用 *.mdf*文件，但用户实例功能已弃用; 因此，用于处理建议 LocalDB *.mdf*文件。

通常 SQL Server Express 不用于生产 web 应用程序。 LocalDB 具体而言不是建议用于生产 web 应用程序因为它不旨在与 IIS 配合使用。

在 Visual Studio 2012 和更高版本中，默认情况下使用 Visual Studio 安装 LocalDB。 在 Visual Studio 2010 和早期版本中，在使用 Visual Studio; 默认情况下安装 SQL Server Express （而不是 LocalDB)必须手动安装它，如果您使用 Visual Studio 2010。

在本教程中你将使用 LocalDB，以便数据库可以存储在*应用程序\_数据*的文件夹 *.mdf*文件。 打开根*Web.config*文件，并添加到新的连接字符串`connectionStrings`集合，如下面的示例中所示。 (请确保更新*Web.config*根项目文件夹中的文件。 此外，还有*Web.config*文件位于*视图*无需更新的子文件夹。)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

默认情况下，实体框架将查找名为相同的连接字符串`DbContext`类 (`SchoolContext`此项目)。 已添加的连接字符串指定一个名为的 LocalDB 数据库*ContosoUniversity.mdf*位于*应用\_数据*文件夹。 有关详细信息，请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。

实际上不需要指定连接字符串。 如果不提供连接字符串，实体框架将为你创建一个;但是，数据库可能不是在*应用程序\_数据*您的应用程序的文件夹。 有关在其中创建数据库的信息，请参阅[到新数据库 Code First](https://msdn.microsoft.com/data/jj193542)。

`connectionStrings`集合还具有一个名为的连接字符串`DefaultConnection`用于成员资格数据库。 不会在本教程中使用了成员资格数据库。 两个连接字符串之间的唯一区别是数据库名称和名称属性值。

## <a name="set-up-and-execute-a-code-first-migration"></a>设置并执行代码的第一次迁移

当你首次开始开发的应用程序时，你的数据模型更改频繁，以及每次获取与数据库不同步的模型更改。 你可以配置实体框架会自动删除并重新创建每次更改数据模型的数据库。 这不是在开发初期的问题，因为测试数据很轻松地重新创建，但已将其部署到生产后通常需要更新数据库架构，而不删除数据库。 迁移功能，Code First 来更新数据库而无需删除并重新创建它。 在新的项目的开发周期的早期你可能想要使用[DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx)删除、 重新创建并重新设定数据库种子每当模型更改。 一个在准备好部署应用程序，您可以将其转换为的迁移方法。 本教程中将只使用迁移。 有关详细信息，请参阅[Code First 迁移](https://msdn.microsoft.com/data/jj591621)并[迁移截屏视频系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

### <a name="enable-code-first-migrations"></a>启用 Code First 迁移

1. 从**工具**菜单上，单击**库程序包管理器**，然后**程序包管理器控制台**。

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. 在`PM>`提示符处输入以下命令：

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![enable-migrations 命令](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    此命令将创建*迁移*文件夹中的 ContosoUniversity 项目中，在该文件夹中放入*Configuration.cs*可编辑以配置 Migrations 的文件。

    ![Migrations 文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration`类包括`Seed`时创建的数据库和每次更新后的数据模型更改时调用的方法。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    这样做的目的`Seed`方法是使您能够测试数据插入到数据库后 Code First 创建它，或对其进行更新。

### <a name="set-up-the-seed-method"></a>设置种子方法

[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法运行 Code First 迁移创建数据库和每次它将更新到最新的迁移数据库。 Seed 方法的目的是为了使您能够将数据插入到你的表之前应用程序将第一次访问数据库。

在早期版本的 Code First，发布迁移之前，它为常见的`Seed`插入测试数据，因为在开发过程中每个模型更改使用该数据库必须完全删除并重新创建从零开始的方法。 使用 Code First 迁移，数据库发生更改后保留数据的测试，因此包括中的测试数据[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法通常不是必需。 事实上，您不希望`Seed`方法插入测试数据，如果您将使用迁移来将数据库部署到生产环境，因为`Seed`方法将在生产环境中运行。 在这种情况下你想`Seed`方法只有你想要在生产环境中要插入的数据插入到数据库。 例如，可能想要包括在实际系名称的数据库`Department`表应用程序变得可用在生产环境中时。

对于本教程，你将在使用迁移部署，但你`Seed`方法将是否仍要插入测试数据，以使其更轻松地了解应用程序功能而无需手动插入大量数据的工作原理。

1. 内容替换为*Configuration.cs*文件使用以下代码，将测试数据加载到新数据库。 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法采用数据库上下文对象作为输入参数，并在方法中的代码使用该对象来将新实体添加到数据库。 对于每个实体类型，代码创建新实体的集合，将它们添加到适当[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)属性，然后单击保存到数据库的更改。 但并不需要调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)后的实体的每个组的方法，正如在这里，但这样做可帮助您找到问题的根源，如果向数据库写入代码时出现异常。

    某些插入数据的语句使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法来执行"upsert"操作。 因为`Seed`方法运行与每个迁移，您不能只是插入数据，因为你尝试添加的行已存在后将创建数据库的初始迁移。 "Upsert"操作可以防止当你尝试插入的行已存在，但它将会发生的错误***重写***对测试应用程序时可能已做的数据的任何更改。 使用测试数据的某些表中您可能不希望发生这种情况： 在某些情况下测试时更改数据时所需数据库更新后保留所做的更改。 在这种情况下想要执行条件插入操作： 插入行，仅当它尚不存在。 Seed 方法使用这两种方法。

    第一个参数传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法指定要用于检查行是否已存在的属性。 提供的，测试学生数据`LastName`属性可用于此目的，因为每个列表中的最后一个名称是唯一的：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    此代码假定最后一个名称唯一。 如果你手动添加的学生使用重复的最后一个名称，将得到以下异常执行迁移的下一个时间。

    序列包含多个元素

    有关详细信息`AddOrUpdate`方法，请参阅[负责使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)Julie Lerman 的博客上。

    添加的代码`Enrollment`实体不会使用`AddOrUpdate`方法。 它检查实体是否已存在并插入该实体，如果不存在。 此方法将会保留在运行迁移时，注册级所做的更改。 此代码循环访问的每个成员`Enrollment`[列表](https://msdn.microsoft.com/library/6sh2ey19.aspx)，如果在数据库中找不到注册，它将注册添加到数据库。 第一次更新数据库，数据库将为空，因此它会将添加每个注册。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    有关如何调试信息`Seed`方法以及如何处理冗余数据，例如两个学生命名为"Alexander Carson"，请参阅[进行种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)Rick Anderson 的博客上。
2. 生成项目。

### <a name="create-and-execute-the-first-migration"></a>创建和执行第一次迁移

1. 在包管理器控制台窗口中，输入以下命令： 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration`命令将添加到迁移文件夹 *[日期戳]\_InitialCreate.cs*文件，其中包含代码将创建数据库。 第一个参数 (`InitialCreate)`用于文件命名，可以是任何所需内容; 通常选择的单词或短语汇总了迁移做什么。 例如，你可能会命名为更高版本迁移&quot;AddDepartmentTable&quot;。

    ![使用初始迁移的 migrations 文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `Up`方法`InitialCreate`类创建与数据模型实体集相对应的数据库表和`Down`方法中删除它们。 迁移调用 `Up` 方法为迁移实现数据模型更改。 输入用于回退更新的命令时，迁移调用 `Down` 方法。 下面的代码演示的内容`InitialCreate`文件：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database`命令将运行`Up`方法来创建数据库，然后将它运行`Seed`方法来填充该数据库。

现在已为你的数据模型创建的 SQL Server 数据库。 数据库的名称是*ContosoUniversity*，并 *.mdf*文件是在项目的*应用\_数据*文件夹因为这是你在中指定你连接字符串。

你可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**(SSOX) 在 Visual Studio 中查看数据库。 对于本教程中，将使用**服务器资源管理器**。 在 Visual Studio Express 2012 for Web，**服务器资源管理器**称为**数据库资源管理器**。

1. 从**视图**菜单上，单击**服务器资源管理器**。
2. 单击**添加连接**图标。

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. 如果系统将提示您**选择数据源**对话框中，单击**Microsoft SQL Server**，然后单击**继续**。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. 在中**添加连接**对话框框中，输入 **(localdb) \v11.0**有关**服务器名称**。 下**选择或输入数据库名称**，选择**ContosoUniversity。**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. 单击“确定” 
6. 展开**SchoolContext** ，然后展开**表**。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. 右键单击**学生**表，然后单击**显示表数据**若要查看已创建的列和插入到表的行。

    ![Student 表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>创建一个学生控制器和视图

下一步是在应用程序可使用其中一个表中创建 ASP.NET MVC 控制器和视图。

1. 若要创建`Student`控制器中，右键单击**控制器**中的文件夹**解决方案资源管理器**，选择**添加**，然后单击**控制器**. 在中**添加控制器**对话框中，进行以下选择，然后单击**添加**: 

   - 控制器名称： **StudentController**。
   - 模板：**读/写操作和视图使用 Entity Framework 的 MVC 控制器**。
   - 模型类：**学生 (ContosoUniversity.Models)**。 （如果看不到下拉列表中的此选项，生成项目，然后重试。）
   - 数据上下文类： **SchoolContext (ContosoUniversity.Models)**。
   - 视图： **Razor (CSHTML)**。 （默认值。）

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio 将打开*Controllers\StudentController.cs*文件。 您看到类变量已经创建了实例化数据库上下文对象：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index`操作方法获取的学生列表*学生*实体集通过阅读`Students`数据库上下文实例的属性：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\Index.cshtml*视图的表中显示此列表：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. 按 Ctrl+F5 运行项目。

     单击**学生**选项卡以查看测试数据的`Seed`插入的方法。

     ![学生索引页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>约定

您必须在实体框架能够为您创建完整的数据库中编写的代码量很小的因为使用了*约定*，或使实体框架的假设。 其中一些已经指出：

- 复数的形式的实体类名称用作表名。
- 使用实体属性名作为列名。
- 命名的实体属性`ID`或*classname* `ID`被视为主键属性。

您已了解约定可以重写 （例如，您指定不应表名变为复数形式），你会学习有关约定以及如何重写中对其的详细信息[创建更多的复杂数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)教程稍后在此系列中。 有关详细信息，请参阅[Code First 约定](https://msdn.microsoft.com/data/jj679962)。

## <a name="summary"></a>总结

你现在已创建使用 Entity Framework 和 SQL Server Express 来存储和显示数据的简单应用程序。 在以下教程中，您将学习如何执行基本的 CRUD （创建、 读取、 更新、 删除） 操作。 可以将保留在此页底部的反馈。 请让我们知道你喜欢本教程的此部分的内容和我们如何改进它。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [下一篇](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
