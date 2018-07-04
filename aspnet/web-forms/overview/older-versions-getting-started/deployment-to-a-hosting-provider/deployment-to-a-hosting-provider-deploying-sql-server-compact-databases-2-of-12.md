---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server Compact 数据库-2 的 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: d52a8b8555f2f4accd628a5e24f2e1705fe8d9aa
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364771"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server Compact 数据库-2 的 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

本教程演示如何设置两个 SQL Server Compact 数据库和用于部署的数据库引擎。

用于数据库访问，Contoso 大学应用程序需要以下软件，因为它不包含在.NET Framework 必须与应用程序部署：

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) （数据库引擎）。
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) （启用 ASP.NET 成员资格系统，以使用 SQL Server Compact）
- [实体框架 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)（代码首次进行迁移）。

数据库结构和一些 （并非所有） 的应用程序的两个中的数据还必须部署数据库。 通常情况下，开发应用程序，您不想要将部署到实时站点的数据库中输入测试数据。 但是，您还可以输入一些要部署的生产数据。 在本教程中将配置 Contoso University 项目，以便在部署时，所需的软件和正确的数据将包括在内。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="sql-server-compact-versus-sql-server-express"></a>与 SQL Server Express 的 SQL Server Compact

示例应用程序使用 SQL Server Compact 4.0。 此数据库引擎是网站; 对于相对较新的选项早期版本的 SQL Server Compact 在 web 托管环境中无效。 SQL Server Compact 提供了与使用 SQL Server Express 进行开发和部署到完整的 SQL Server 的较常见的方案相比的几个优点。 具体取决于您选择托管提供商的情况下，SQL Server Compact 可能更便宜，若要部署，因为有些提供商会收取额外支持完整的 SQL Server 数据库。 因为您可以作为 web 应用程序的一部分部署的数据库引擎本身没有 SQL Server Compact 的无需额外付费。

但是，您还应了解其限制。 SQL Server Compact 不支持存储的过程、 触发器、 视图或复制。 (不支持的 SQL Server Compact 的 SQL Server 功能的完整列表，请参阅[差异之间 SQL Server Compact 和 SQL Server](https://msdn.microsoft.com/library/bb896140.aspx)。)此外，一些可用于处理架构和 SQL Server Express 和 SQL Server 数据库中的数据的工具不起作用 SQL Server Compact。 例如，您不能使用 SQL Server Management Studio 或 SQL Server Data Tools 在 Visual Studio 中使用 SQL Server Compact 数据库。 必须使用 SQL Server Compact 数据库的其他选项：

- 在 Visual Studio 中，为 SQL Server Compact 提供了有限的数据库操作功能，可以使用服务器资源管理器。
- 可以使用的数据库操作功能[WebMatrix](https://www.microsoft.com/web/webmatrix/)，其中包含多个功能比服务器资源管理器。
- 可以使用相对全功能的第三方或开源工具，如[SQL Server Compact Toolbox](https://github.com/ErikEJ/SqlCeToolbox)并[SQL Compact 数据和架构脚本实用程序](https://github.com/ErikEJ/SqlCeToolbox)。
- 可以编写和运行自己的 DDL （数据定义语言） 脚本来处理数据库架构。

你可以开始使用 SQL Server Compact，然后再升级随着需求的发展更高版本。 本系列教程的后续教程演示如何将到 SQL Server Express 和 SQL Server 迁移 SQL Server Compact 中。 但是，如果要创建新的应用程序并希望在不久的将来需要 SQL Server，则可能最好使用 SQL Server 或 SQL Server Express 启动。

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>配置用于部署的 SQL Server Compact 数据库引擎

通过安装以下 NuGet 包添加了 Contoso 大学应用程序中的数据访问所需的软件：

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.Web.Providers](http://nuget.org/List/Packages/System.Web.Providers) （ASP.NET 通用提供程序）
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework.SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

链接指向当前版本的这些包，这可能是比本教程中下载的初学者项目中安装的内容。 对于向宿主提供程序的部署，请确保您使用实体框架 5.0 或更高版本。 早期版本的 Code First 迁移需要完全信任权限，并在许多主机托管提供商应用程序将运行于中等信任级别。 中等信任级别的详细信息，请参阅[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程。

NuGet 包安装通常负责将部署应用程序使用此软件所需的所有内容。 在某些情况下，这涉及到任务，例如更改 Web.config 文件并添加 PowerShell 脚本，每当您生成解决方案时运行。 **如果你想要不使用 NuGet 添加对任何这些功能 （如 SQL Server Compact 和实体框架） 的支持，请确保您了解 NuGet 包安装，以便您可以手动执行相同的工作的用途。**

是一个例外，NuGet 不小心谨慎地所要做，才能确保成功部署的所有内容。 SqlServerCompact NuGet 包添加到项目，用于将复制到本机程序集的后期生成脚本*x86*并*amd64*项目下的子文件夹*bin*文件夹中，但该脚本不在项目中包括这些文件夹。 因此，Web 部署将不将它们复制到目标网站除非手动将其包含在项目中。 （此行为会导致从默认部署配置; 另一个选项，不会使用这些教程中，将更改控制此行为的设置。 您可以更改的设置是**仅运行该应用程序所需的文件**下**要部署的项**上**打包/发布 Web**选项卡**项目属性**窗口。 更改此设置通常建议不要因为它可能会导致许多其他文件部署到生产环境不是那里需要。 有关替代项的详细信息，请参阅[配置项目属性](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)教程。)

生成项目，然后在**解决方案资源管理器**单击**显示所有文件**如果尚未这样做。 您可能还需要单击**刷新**。

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

展开**bin**文件夹，以查看**amd64**并**x86**文件夹，然后选择这些文件夹，右键单击，并选择**包括在项目**.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

文件夹图标更改为显示该文件夹已包含在项目。

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>配置应用程序数据库部署的 Code First 迁移

当您部署的应用程序数据库时，通常会不只需部署中它的数据的所有开发数据库到生产环境，因为很多的数据有可能仅用于测试目的。 例如，一个测试数据库中的学生名是虚构的。 但是，你通常不能部署只中它不包含数据的数据库结构根本。 某些测试数据库中的数据可能是真实数据，用户可以开始使用应用程序时，必须有为。 例如，您的数据库可能具有包含有效级别值或实际部门名称的表。

若要模拟这种常见方案，你将配置代码第一个迁移 Seed 方法，将想要在生产环境中存在将数据插入到数据库。 此 Seed 方法不会插入测试数据，因为它将 Code First 在生产环境中创建数据库后在生产环境中运行。

在早期版本的 Code First 迁移发布之前，过去通常 Seed 方法来插入测试数据，此外，因为在开发过程中每个模型更改使用该数据库必须完全删除并重新创建从零开始。 使用 Code First 迁移测试数据保留数据库发生更改后，因此不需要包括 Seed 方法中的测试数据。 下载的项目使用初始值设定项类的 Seed 方法中包括的所有数据的预迁移方法。 在本教程中将禁用初始值设定项类，并启用迁移。 然后将更新迁移配置类的 Seed 方法，以便它将插入想要在生产环境中要插入的数据。

下图说明了应用程序数据库的架构：

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

对于这些教程，将假定`Student`和`Enrollment`首次部署站点时，表应为空。 其他表包含必须在应用程序上线时预加载的数据。

您将使用 Code First 迁移，因为不再需要使用**DropCreateDatabaseIfModelChanges** Code First 初始值设定项。 此初始值设定项的代码位于 SchoolInitializer.cs 文件 ContosoUniversity.DAL 项目中。 中的设置**appSettings** Web.config 文件的元素会导致应用程序尝试首次访问数据库时运行此初始值设定项：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

打开应用程序 Web.config 文件，移除指定的 appSettings 元素中的 Code First 初始值设定项类的元素。 AppSettings 元素现在如下所示：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 若要指定一个初始值设定项类的另一种方法是执行此操作通过调用`Database.SetInitializer`中`Application_Start`中的方法*Global.asax*文件。 如果要使用该方法来指定初始值设定项的项目中启用迁移，删除该代码行。


接下来，启用 Code First 迁移。

第一步是确保 ContosoUniversity 项目设置为启动项目。 在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目并选择**设为启动项目**。 Code First 迁移将查找要查找的数据库连接字符串的启动项目中。

从**工具**菜单上，单击**库程序包管理器**，然后**程序包管理器控制台**。

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

在顶部**程序包管理器控制台**窗口中选择作为默认项目，并在 ContosoUniversity.DAL`PM>`提示符处输入"启用迁移"。

![enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

此命令将创建*Configuration.cs*文件中的新*迁移*ContosoUniversity.DAL 项目文件夹中的。

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

您选择 DAL 项目，因为必须在包含的第一个代码的上下文类的项目中执行"enable-migrations"命令。 在类库项目中的类时，Code First 迁移查找解决方案的启动项目中的数据库连接字符串。 在 ContosoUniversity 解决方案中，web 项目具有已设置为启动项目。 （如果你没有不想要指定有连接字符串为启动项目在 Visual Studio 中的项目，您可以指定启动项目中 PowerShell 命令。 若要查看 enable-migrations 命令的命令语法，您可以输入命令"获取帮助 enable-migrations"。）

打开 Configuration.cs 文件，将为中的注释`Seed`方法使用以下代码：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

对引用`List`已在其下的红色波浪线，因为你没有`using`尚未为其命名空间语句。 右键单击其中一个的实例`List`然后单击**解决**，然后单击**using System.Collections.Generic**。

![解决与 using 语句](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

此菜单选项将添加到下面的代码`using`语句接近文件顶部。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> 将代码添加到`Seed`方法是可以固定的数据插入到数据库的许多方式之一。 一种替代方法是将代码添加到`Up`和`Down`迁移的每个类的方法。 `Up`和`Down`方法包含实现数据库更改的代码。 您将看到示例中为它们[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程。
> 
> 您还可以编写通过使用执行 SQL 语句的代码`Sql`方法。 例如，如果您已将 Department 表向添加预算列并希望将所有部门的预算为 1,000.00 美元都初始化为迁移的一部分，您可以添加到代码的以下行`Up`迁移方法：
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 此示例中所示为本教程使用`AddOrUpdate`中的方法`Seed`方法的 Code First 迁移`Configuration`类。 代码优先迁移调用`Seed`方法后每个迁移，且此方法将更新具有已插入，或将其插入，如果它们尚不存在的行。 `AddOrUpdate`方法可能不是你的方案的最佳选择。 有关详细信息，请参阅[负责与 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)Julie Lerman 的博客上。


按 CTRL-SHIFT-B 以生成项目。

下一步是创建`DbMigration`类适用于初始迁移。 您希望此迁移，以创建新的数据库，因此您必须删除已存在的数据库。 SQL Server Compact 数据库中包含 *.sdf*中的文件*应用\_数据*文件夹。 在中**解决方案资源管理器**，展开*应用\_数据*ContosoUniversity 项目，以查看两个 SQL Server Compact 数据库，在其中由 *.sdf*文件。

右键单击*School.sdf*文件，并单击**删除**。

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

在中**程序包管理器控制台**窗口中，输入命令"add-migration Initial"若要创建初始迁移并将其命名为"初始"。

![add-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 迁移创建另一个类文件中的*迁移*文件夹中，并且此类包含创建数据库架构的代码。

在中**程序包管理器控制台**，输入命令"更新数据库"以创建数据库并运行**种子**方法。

![update-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(如果收到一个错误，指示表已存在，无法创建，则可能是因为删除了该数据库后，您在执行前运行应用程序`update-database`。 这种情况下，删除*School.sdf*再次文件，然后重试`update-database`命令。)

运行该应用程序。 现在学生页面为空，但讲师页包含讲师。 这是什么则会在生产环境中部署应用程序之后。

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

现在项目已准备好部署*学校*数据库。

## <a name="creating-a-membership-database-for-deployment"></a>为部署创建成员资格数据库

Contoso 大学应用程序使用 ASP.NET 成员资格系统和窗体身份验证用户进行身份验证和授权。 只有管理员才能访问其页面之一。 若要查看此页上，运行该应用程序，并选择**更新信用额度**下飞出式菜单**课程**。 应用程序将显示**日志中**页上，因为只有管理员才有权使用**更新信用额度**页。

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

以"管理员"使用密码"Pa$ w0rd"（请注意数字零来代替"w0rd"中的字母"o"）。 您登录后**更新信用额度**显示页。

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

将站点部署第一次，时，往往会排除大部分或全部创建用于测试的用户帐户。 在这种情况下，你将部署的管理员帐户和任何用户帐户。 而不是手动删除的测试帐户，将创建具有仅需要在生产环境中的一个管理员用户帐户的新成员资格数据库。

> [!NOTE]
> 成员资格数据库将存储帐户密码的哈希值。 若要部署从一台计算机到另一个帐户，必须确保哈希例程不生成目标服务器上的不同哈希值不是它们在源计算机上执行。 它们会生成相同的哈希时使用了 ASP.NET 通用提供程序，只要不更改默认的算法。 默认的算法是 HMACSHA256 和中指定**验证**的属性**[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** Web.config 文件中的元素。


成员资格数据库不由 Code First 迁移，维护并且没有使用测试帐户数据库种子 （因为没有为 School 数据库） 没有自动初始值设定项。 因此，要保持可用的测试数据将使测试数据库的副本之前创建一个新。

在中**解决方案资源管理器**，重命名*aspnet.sdf*文件中*应用\_数据*到的文件夹*aspnet Dev.sdf*。 (不复制，只需将其重命名，将在一段时间中创建新的数据库。)

在中**解决方案资源管理器**，请确保选中 web 项目 （ContosoUniversity、 不 ContosoUniversity.DAL）。 然后在**项目**菜单中，选择**ASP.NET 配置**若要运行**网站管理工具**(WAT)。

选择**安全**选项卡。

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

单击**创建或管理角色**并添加**管理员**角色。

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

导航回到**安全**选项卡上，单击**Create User**，并以管理员身份添加用户"admin"。 在单击之前**Create User**按钮**Create User**页上，确保你选择**管理员**复选框。 在本教程中所用的密码已"Pa$ w0rd"，并且您可以输入任何电子邮件地址。

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

关闭浏览器。 在中**解决方案资源管理器**，单击刷新按钮以查看新*aspnet.sdf*文件。

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

右键单击**aspnet.sdf** ，然后选择**包括在项目**。

## <a name="distinguishing-development-from-production-databases"></a>区分从生产数据库开发

在本部分中，你将重命名数据库，以便开发版本是学校 Dev.sdf，aspnet Dev.sdf 和生产版本是学校 Prod.sdf 和 aspnet Prod.sdf。 这不是有必要，但这样做因此有助于使你获取的数据库的测试和生产版本相混淆。

在中**解决方案资源管理器**，单击**刷新**和扩展该应用程序\_数据文件夹，请参阅前面创建的 School 数据库，右键单击它并选择**包括在项目**.

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

重命名*aspnet.sdf*到*aspnet Prod.sdf*。

重命名*School.sdf*到*学校 Dev.sdf*。

当不想要使用的 Visual Studio 中运行应用程序 *-Prod*版本的数据库文件中，你想要使用 *-Dev*版本。 因此您需要更改 Web.config 文件中的连接字符串，以便它们指向 *-Dev*数据库版本。 （尚未创建的 School Prod.sdf 文件，但这是确定，因为 Code First 将创建该数据库中有运行你的应用的第一个生产时间。）

打开应用程序 Web.config 文件，并找到连接字符串：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

将"aspnet.sdf"更改为"aspnet-Dev.sdf"，并将"School.sdf"更改为"学校 Dev.sdf":

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

SQL Server Compact 数据库引擎和这两个数据库现已准备好进行部署。 在以下教程，将自动设置*Web.config*文件必须是不同的开发、 测试和生产环境中的设置的转换。 （在必须更改设置之间的连接字符串，但您将设置所做的更改更高版本创建的发布配置文件时。）

## <a name="more-information"></a>详细信息

有关 NuGet 的详细信息，请参阅[使用 NuGet 管理项目库](https://msdn.microsoft.com/magazine/hh547106.aspx)并[NuGet 文档](http://docs.nuget.org/docs/start-here/overview)。 如果不想要使用 NuGet，您需要了解如何分析 NuGet 包，以确定它的作用时安装它。 (例如，可以配置*Web.config*转换，配置 PowerShell 脚本以运行在生成时，等等。)若要了解有关 NuGet 的工作原理的详细信息，请参阅尤其[创建和发布包](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)并[配置文件和源代码转换](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [下一页](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
