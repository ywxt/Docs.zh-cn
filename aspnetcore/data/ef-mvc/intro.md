---
title: "ASP.NET Core MVC 和 Entity Framework Core - 第 1 个教程，共 10 个教程"
author: tdykstra
description: 
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/intro
ms.openlocfilehash: 7de43a390ee0e11f6eda811b0774343ab330c53b
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-entity-framework-core-using-visual-studio-1-of-10"></a>ASP.NET Core MVC 和 Entity Framework Core 入门（使用 Visual Studio）（第 1 个教程，共 10 个）

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

[此处](xref:data/ef-rp/intro)提供了本教程的 Razor 页面版本。 Razor 页面版本更加通俗易懂，并介绍了更多 EF 功能。 建议阅读[本教程的 Razor 页面版本](xref:data/ef-rp/intro)。

Contoso University 示例 Web 应用程序演示如何使用 Entity Framework (EF) Core 2.0 和 Visual Studio 2017 创建 ASP.NET Core 2.0 MVC Web 应用程序。

该示例应用程序是一个虚构的 Contoso University 的网站。 其中包括学生录取、课程创建和讲师分配等功能。 本页是介绍如何从头开始生成 Contoso University 示例应用系列教程中的第一部分。

[下载或查看已完成的应用程序。](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

EF Core 2.0 是 EF 的最新版本，但尚不具有 EF 6.x 的所有功能。 有关选择 EF 6.x 还是 EF Core 的信息，请参阅 [比较 EF Core 和EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/)。 如果选择 EF 6.x，请参阅[本系列教程的上一版本](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

> [!NOTE]
> * 有关本教程的 ASP.NET Core 1.1 版本信息，请参阅 [本教程的 VS 2017 第 2 次更新版本（PDF 格式）](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/ef-mvc/intro/_static/efmvc1.1.pdf)。
> * 有关本教程的 Visual Studio 2015 版本，请参阅 [ ASP.NET Core 文档 VS 2015 版本的 PDF 文档](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf)。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a>疑难解答

如果遇到无法解决的问题，通常可以通过将自己的代码与[已完成项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)进行比较来寻找解决方案。 有关常见错误列表及其解决办法，请参阅[本系列最后一个教程的疑难解答部分](advanced.md#common-errors)。 如果在该处找不到所需内容，可以在 StackOverflow.com 上发表有关 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 或 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core) 的问题。

> [!TIP] 
> 本系列共 10 个教程，每个教程都以上一个教程为基础。 每次成功完成教程后，请考虑保存项目副本。 这样，如果遇到问题，便可以从上一教程重新开始，而无需从整个系列从头开始。

## <a name="the-contoso-university-web-application"></a>Contoso University Web 应用程序

将在这些教程中构建的应用程序是一个简单的大学网站。

用户可以查看和更新学生、课程和讲师信息。 以下是你将创建的几个屏幕。

![“学生索引”页](intro/_static/students-index.png)

![学生编辑页](intro/_static/student-edit.png)

该网站的 UI 样式与通过内置模板生成的 UI 样式十分接近，因此本教程主要着重介绍如何使用 Entity Framework。

## <a name="create-an-aspnet-core-mvc-web-application"></a>创建 ASP.NET Core MVC Web 应用程序

打开 Visual Studio 并创建名为“ContosoUniversity”的新 ASP.NET Core C# Web 项目。

* 从“文件”菜单中选择“新建”>“项目”。

* 从左窗格中依次选择“已安装”>“Visual C#”>“Web”。

* 选择“ASP.NET Core Web 应用程序”项目模板。

* 输入“ContosoUniversity”作为名称，然后单击“确定”。

  ![“新建项目”对话框](intro/_static/new-project.png)

* 等待“新建 ASP.NET Core Web 应用程序(.NET Core)”对话框显示出来

* 选择“ASP.NET Core 2.0”和“Web 应用程序（模型视图控制器）”模板。

  注意：本教程需要 ASP.NET Core 2.0 和 EF Core 2.0 或更高版本，确保未选择 ASP.NET Core 1.1。

* 确保将“身份验证”设置为“无身份验证”。

* 单击“确定” 

  ![“新建 ASP.NET 项目”对话框](intro/_static/new-aspnet.png)

## <a name="set-up-the-site-style"></a>设置网站样式

设置网站菜单、布局和主页时需作少量简单更改。

打开 Views/Shared/_Layout.cshtml 并进行以下更改：

* 将“ContosoUniversity”的每个匹配项都改为“Contoso University”。 共有三个匹配项。

* 添加 Students、Courses、Instructors 和 Departments 菜单项，并删除“联系人”菜单项。

突出显示所作更改。

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,30,36-39,48)]

在 Views/Home/Index.cshtml 中，将文件内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关本应用程序的文本：

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

按 Ctrl+F5 运行项目，或从菜单中依次选择“调试”>“开始执行(不调试)”。 随后将看到主页，主页中包含在这些教程中创建的页面标签。

![Contoso University 主页](intro/_static/home-page.png)

## <a name="entity-framework-core-nuget-packages"></a>Entity Framework Core NuGet 包

要为项目添加 EF Core 支持，请安装需要作为目标的数据库提供程序。 本教程使用 SQL Server，提供程序包为 [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)。 此包包含在 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 元包中，因此无需另外安装。

此包及其依赖项（`Microsoft.EntityFrameworkCore` 和 `Microsoft.EntityFrameworkCore.Relational`）为 EF 提供运行时支持。 之后将在[迁移](migrations.md)教程中添加工具包。 

有关为 Entity Framework Core 提供的其他数据库提供程序的信息，请参阅[数据库提供程序](https://docs.microsoft.com/ef/core/providers/)。

## <a name="create-the-data-model"></a>创建数据模型

接下来将创建 Contoso University 应用程序的实体类。 将从以下三个实体开始。

![Course-Enrollment-Student 数据模型关系图](intro/_static/data-model-diagram.png)

`Student` 和 `Enrollment` 实体之间存在一对多的关系，`Course` 和 `Enrollment` 实体之间存在一对多的关系。 换言之，一名学生可以登记任意数量的课程，一门课程可以包含任意数量的学生。

以下部分将为这几个实体中的每一个实体创建一个类。

### <a name="the-student-entity"></a>Student 实体

![Student 实体关系图](intro/_static/student-entity.png)

在 Models 文件夹中，创建名为 Student.cs 的类文件，并使用以下代码替换模板代码。

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

`ID` 属性将成为此类对应的数据库表的主键列。 默认情况下，Entity Framework 将名为 `ID` 或 `classnameID` 的属性视为主键。

`Enrollments` 属性是导航属性。 导航属性包含与此实体相关的其他实体。 在这种情况下，`Student entity` 的 `Enrollments` 属性将包含与该 `Student` 实体相关的所有 `Enrollment` 实体。 换言之，如果数据库中的给定 Student 行具有两个相关的 Enrollment 行（这两行的 StudentID 外键列包含该学生的外键值），该 `Student` 实体的 `Enrollments` 导航属性将包含这两个 `Enrollment` 实体。

如果导航属性可包含多个实体（如多对多或一对多关系），则其类型必须是可添加、可删除和可更新实体的列表，如 `ICollection<T>`。 可指定 `ICollection<T>` 或诸如 `List<T>` 或 `HashSet<T>` 的类型。 如果指定 `ICollection<T>`，EF 默认会创建一个 `HashSet<T>` 集合。

### <a name="the-enrollment-entity"></a>Enrollment 实体

![Enrollment 实体关系图](intro/_static/enrollment-entity.png)

在 Models 文件夹中，创建 Enrollment.cs，并使用以下代码替换现有代码：

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

`EnrollmentID` 属性将成为主键，正如在 `Student` 实体中看到的，此实体使用 `classnameID` 模式，而非 `ID`。 通常可选择一个模式，并将其用于整个数据模型。 变体说明可以使用任意模式。 [下一个教程](inheritance.md)将介绍如何使用不带类名的 ID，以便更轻松地在数据模型中实现继承。

`Grade` 属性为 `enum`。 `Grade` 类型声明后的问号表明 `Grade` 属性可为 NULL。 为 NULL 的年级与零年级不同，NULL 意味着该年级未知或尚未分配。

`StudentID` 属性是外键，其对应的导航属性为 `Student`。 `Enrollment` 实体与一个 `Student` 实体相关联，因此属性仅包含单个 `Student` 实体（而不像之前看到的 `Student.Enrollments` 导航属性，可包含多个 `Enrollment` 实体）。

`CourseID` 属性是外键，其对应的导航属性为 `Course`。 `Enrollment` 实体与一个 `Course` 实体相关联。

如果属性命名为 `<navigation property name><primary key property name>`，Entity Framework 会将其视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。 还可将外键属性简单命名为 `<primary key property name>`（例如可命名为 `CourseID`，因为 `Course` 实体的主键为 `CourseID`）。

### <a name="the-course-entity"></a>Course 实体

![Course 实体关系图](intro/_static/course-entity.png)

在 Models 文件夹中，创建 Course.cs 并使用以下代码替换现有代码：

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

`Enrollments` 属性是导航属性。 `Course` 实体可与任意数量的 `Enrollment` 实体相关。

本系列的[下一个教程](complex-data-model.md)将介绍 `DatabaseGenerated` 特性的更多相关信息。 基本上，此特性允许你输入课程的主键，而不是在数据库中生成该主键。

## <a name="create-the-database-context"></a>创建数据库上下文

数据库上下文类是为给定数据模型协调 Entity Framework 功能的主类。 将通过从 `Microsoft.EntityFrameworkCore.DbContext` 类派生的方式创建此类。 在代码中指定包含在数据模型中的实体。 还可以自定义特定 Entity Framework 行为。 在此项目中，类命名为 `SchoolContext`。

在项目文件夹中，创建一个名为 Data 的文件夹。

在 Data 文件夹中，创建名为 SchoolContext.cs 的新类文件，并使用以下代码替换模板代码：

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

此代码会为每个实体集创建一个 `DbSet` 属性。 在实体框架术语中，实体集通常与数据库表相对应，实体与表中的行相对应。

可能已省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 语句，但其效果相同。 Entity Framework 可能隐式包含了它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。

创建数据库时，EF 会创建名称与 `DbSet` 属性名相同的表。 集合的属性名通常为复数形式（Students 而非 Student），但开发者对表名是否应为复数意见不一。 在这些教程中，在 DbContext 中指定单数形式的表名将会覆盖默认行为。 要完成这一操作，请在最后的 DbSet 属性后添加以下突出显示的代码。

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a>通过依赖关系注入注册上下文

ASP.NET Core 默认实现[依赖关系注入](../../fundamentals/dependency-injection.md)。 服务（例如 EF 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。 需要这些服务（如 MVC 控制器）的组件通过构造函数提供相应服务。 可在本教程的后面部分了解获取上下文实例的控制器构造函数代码。

要将 `SchoolContext` 注册为服务，请打开 Startup.cs，并将突出显示的行添加到 `ConfigureServices` 方法。

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

通过调用 `DbContextOptionsBuilder` 对象上的方法，可将连接字符串的名称传递给上下文。 进行本地开发时，[ASP.NET Core 配置系统](xref:fundamentals/configuration/index)会从 appsettings.json 文件读取连接字符串。

为 `ContosoUniversity.Data` 和 `Microsoft.EntityFrameworkCore` 命名空间添加 `using` 语句，然后生成项目。

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

打开 appsettings.json 文件，并如以下示例所示添加连接字符串。

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

连接字符串指定 SQL Server LocalDB 数据库。 LocalDB 是轻型版本 SQL Server Express 数据库引擎，专门针对应用程序开发，而非生产使用。 LocalDB 按需启动并在用户模式下运行，因此没有复杂的配置。 默认情况下，LocalDB 会在 `C:/Users/<user>` 目录中创建 .mdf 数据库文件。

## <a name="add-code-to-initialize-the-database-with-test-data"></a>添加代码，以使用测试数据初始化该数据库

Entity Framework 将创建一个空数据库。 本部分中，创建数据库后，写入调用的方法，以使用测试数据填充该数据库。

此处，将使用 `EnsureCreated` 方法自动创建数据库。 [下一个教程](migrations.md)将介绍如何使用 Code First 迁移处理模型更改，以更改数据库架构而非丢弃或重新创建数据库。

在 Data 文件夹中，创建名为 DbInitializer.cs 的新类文件，使用以下代码替换模板代码，这会导致在需要时以及将测试数据加载到新数据库时创建数据库。

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

代码检查数据库中是否有任何学生，如果没有，则假定该数据库为新数据库，需填充测试数据。 它会将测试数据加载到数组中，而不是 `List<T>` 集合中，以便优化性能。

在 Program.cs 中，修改 `Main` 方法以在应用程序启动时执行以下操作：

* 从依赖关系注入容器获取数据库上下文实例。
* 调用 seed 方法，并将上下文传递给它。
* Seed 方法完成时释放上下文。

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

添加 `using` 语句：

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Usings)]

在旧版教程中，可以在 Startup.cs 中查看 `Configure` 方法的类似代码。 建议仅在设置请求管道时使用 `Configure` 方法。 应用程序启动代码属于 `Main` 方法。

首次运行应用程序时，会创建数据库，并为其填充测试数据。 任何时候想要更改数据模型，可删除数据库、更新 seed 方法，并以同样的方式重新启动新的数据库。 下一个教程将介绍如何在更改数据模型时修改该数据库，而不删除并重新创建该数据库。

## <a name="create-a-controller-and-views"></a>创建控制器和视图

接下来，将在 Visual Studio 中使用基架引擎添加 MVC 控制器和视图，以使用 EF 来查询和保存数据。

自动创建 CRUD 操作方法和视图的过程称为构架。 构架不同于生成代码，基架代码是可以根据自己需求修改的起点，而通常生成的代码是不能修改的。 需要自定义生成的代码时，使用分部类，或在情况发生变化时重新生成代码。

* 右键单击“解决方案资源管理器”中的 Controllers 文件夹，然后选择“添加”>“新基架项目”。

如果出现“添加 MVC 依赖项”对话框：
 
* [将 Visual Studio 更新到最新版本](https://www.visualstudio.com/downloads/)。 15.5 之前的 Visual Studio 版本显示此对话框。

* 如果无法更新，请选择“添加”，然后再次按照添加控制器步骤操作。

* 在“添加基架”对话框中：
  
  * 选中“视图使用 Entity Framework 的 MVC 控制器”。

  * 单击**添加**

* 在“添加控制器”对话框中：

  * 在“模型类”中选择“学生”。

  * 在“数据上下文类”中选择 SchoolContext。

  * 接受默认的 StudentsController 作为名称。

  * 单击**添加**


  ![构架 Student](intro/_static/scaffold-student.png)

  单击“添加”时，Visual Studio 基架引擎会创建 StudentsController.cs 文件和视图集（.cshtml 文件），以与控制器一同使用。

（如果没有如本教程前面部分介绍的那样事先手动创建数据库上下文，基架引擎还可帮助创建。 通过单击“数据上下文类”右侧的加号，可在“添加控制器”框中指定新的上下文类。  然后，Visual Studio 将创建 `DbContext` 类、控制器和视图。）

注意控制器将 `SchoolContext` 作为构造函数参数。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

ASP.NET 依赖关系注入负责将 `SchoolContext` 的实例传递到控制器中。 之前已在 Startup.cs 文件中进行过配置。

该控制器包含一个 `Index` 操作方法，该方法显示数据库中的所有学生。 该方法通过读取数据库上下文实例的 `Students` 属性从 Students 实体集获取学生列表：

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

本教程后面部分将介绍此代码中的异步编程元素。

Views/Students/Index.cshtml 视图在表中显示此列表：

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

按 Ctrl+F5 运行项目，或从菜单中依次选择“调试”>“开始执行(不调试)”。

单击“学生”选项卡以查看 `DbInitializer.Initialize` 方法插入的测试数据。 可以在页面顶部查看 `Student` 选项卡链接，或单击右上角的导航图标查看链接，具体取决于浏览器窗口的宽窄。

![Contoso University 主页宽窄](intro/_static/home-page-narrow.png)

![“学生索引”页](intro/_static/students-index.png)

## <a name="view-the-database"></a>查看数据库

启动应用程序时，`DbInitializer.Initialize` 方法调用 `EnsureCreated`。 如果 EF 检查到没有数据库时，它会创建一个数据库，然后 `Initialize` 方法代码的其他部分会使用数据填充数据库。 可以使用“SQL Server 对象资源管理器”(SSOX) 查看 Visual Studio 中的数据库。

关闭浏览器。

如果还没有打开 SSOX 窗口，可从 Visual Studio 中的“视图”菜单中选择 SSOX 窗口。

在 SSOX 中，单击“(localdb)\MSSQLLocalDB”>“数据库”，然后单击 appsettings.json 文件中连接字符串中的数据库名条目。

展开“表”节点，查看数据库中的表。

![SSOX 中的表](intro/_static/ssox-tables.png)

右键单击 Student 表，然后单击“查看数据”，以查看创建的列和插入到表中的行。

![SSOX 中的 Student 表](intro/_static/ssox-student-table.png)

.mdf 和 .ldf 数据库文件位于 C:\Users\<yourusername> 文件夹中。

由于在应用启动时运行的初始化方法中调用 `EnsureCreated`，现在可对 `Student` 类作出更改，删除数据库，然后再运行应用程序，数据库将自动重新创建以匹配作出的更改。 例如，如果向 `Student` 类添加 `EmailAddress` 属性，可以在重新创建的表中看到新的 `EmailAddress` 列。

## <a name="conventions"></a>约定

因为约定的使用或 Entity Framework 所做的假设，为使 Entity Framework 能够创建一个完整的数据库，必须写入的代码数量是最少的。

* 使用 `DbSet` 属性的名称作为表名。 若是未被 `DbSet` 属性引用的实体，则使用实体类名作为表名。

* 使用实体属性名作为列名。

* 以 ID 或 classnameID 命名的实体属性被视为主键属性。

* 如果属性命名为 <navigation property name><primary key property name>，将视为外键属性（例如 `Student` 导航属性的 `StudentID`，因为 `Student` 实体的主键为 `ID`）。 还可将外键属性简单命名为 <primary key property name>（例如可命名为 `EnrollmentID`，因为 `Enrollment` 实体的主键为 `EnrollmentID`）。

可以重写常规行为。 例如，可以按照本教程前面部分所述，明确指定表名。 或如本系列[下一个教程](complex-data-model.md)中介绍的，设置列名，并将任何属性设置为主键或外键。

## <a name="asynchronous-code"></a>异步代码

异步编程是 ASP.NET Core 和 EF Core 的默认模式。

Web 服务器可用的线程数量有限，在高负载情况下，所有可用的线程可能都正在使用。 在这种情况下，线程释放之前，服务器无法处理新的请求。 若使用同步代码，许多线程在等待 I/O 完成时实际上并未执行任何操作，但仍被占用。 若使用异步代码，进程在等待 I/O 完成时其线程会被释放，以便服务器用于处理其他请求。 因此，使用异步代码可以更有效地利用服务器资源，并且可以让服务器在没有延迟的情况下处理更多流量。

异步代码在运行时会引入少量的开销，流量较低时，对性能的影响可以忽略不计，但流量较高时，潜在的性能改善非常显著。

在以下代码中，`async` 关键字、`Task<T>` 返回值、`await` 关键字和 `ToListAsync` 方法让代码异步执行。

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* `async` 关键字通知编译器为方法主体部分生成回调，并自动创建返回的 `Task<IActionResult>` 对象。

* 返回类型 `Task<IActionResult>` 表示正在进行的工作，其结果是 `IActionResult` 类型。

* `await` 关键字让编译器将该方法拆分为两个部分。 第一部分以异步方式启动的操作结束。 第二部分被放入一个回调方法中，当操作完成时调用。

* `ToListAsync` 是 `ToList` 扩展方法的异步版本。

编写使用 Entity Framework 的异步代码时需要注意的一些事项：

* 只会异步执行导致查询或命令被发送到数据库的语句。 这包括，例如，`ToListAsync``SingleOrDefaultAsync` 和 `SaveChangesAsync`。 不包括只会更改 `IQueryable` 的语句，例如 `var students = context.Students.Where(s => s.LastName == "Davolio")`。

* EF 上下文并非线程安全：请勿尝试并行执行多个操作。 调用任何异步 EF 方法时，都始终使用 `await` 关键字。

* 如果想利用异步代码的性能优势，请确保正在使用的任何库程序包（如用于分页）也使用异步（如果它们调用任何导致查询发送到数据库的 Entity Framework 方法）。
有关在 .NET 异步编程的详细信息，请参阅[异步概述](https://docs.microsoft.com/dotnet/articles/standard/async)。
有关在 .NET 中进行异步编程的详细信息，请参阅[异步概述](https://docs.microsoft.com/dotnet/articles/standard/async)。

## <a name="summary"></a>总结

现在已创建了一个使用 Entity Framework Core 和 SQL Server Express LocalDB 来存储和显示数据的简单应用程序。 下一个教程将介绍如何执行基本的 CRUD（创建、读取、更新、删除）操作。

>[!div class="step-by-step"]
[下一篇](crud.md)  
