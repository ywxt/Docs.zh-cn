---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 使用 Visual Studio 的 ASP.NET Web 部署： 准备数据库部署 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: 67f44d9f23a2fe83c48e68328b1dee739056e32f
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912379"
---
<a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>使用 Visual Studio 的 ASP.NET Web 部署： 准备数据库部署
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

本教程演示如何获取该项目数据库部署已准备就绪。 数据库结构和一些 （并非所有） 的应用程序的两个中的数据必须将数据库部署到测试、 过渡和生产环境。

通常情况下，开发应用程序，您不想要将部署到实时站点的数据库中输入测试数据。 但是，你可能还有一些要部署的生产数据。 在本教程将 Contoso University 项目配置，准备 SQL 脚本，以便在部署时，不包含正确数据。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

示例应用程序使用 SQL Server Express LocalDB。 SQL Server Express 是免费版本的 SQL Server。 它通常用于在开发过程中由于基于相同的数据库引擎作为完整版本的 SQL Server。 您可以使用 SQL Server Express 进行测试，并确保该应用程序的表现与在生产中，但有少数例外的 SQL Server 版本而异的功能相同。

LocalDB 是 SQL Server Express，使你能够使用作为数据库的特殊执行模式 *.mdf*文件。 通常情况下，LocalDB 数据库文件保存在*应用程序\_数据*web 项目的文件夹。 在 SQL Server Express 用户实例功能还使您可以使用 *.mdf*文件，但用户实例功能已弃用; 因此，用于处理建议 LocalDB *.mdf*文件。

通常 SQL Server Express 不用于生产 web 应用程序。 LocalDB 具体而言不是建议用于生产 web 应用程序因为它不旨在与 IIS 配合使用。

在 Visual Studio 2012 中，默认情况下，使用 Visual Studio 安装 LocalDB。 在 Visual Studio 2010 和早期版本中，在使用 Visual Studio; 默认情况下安装 SQL Server Express （而不是 LocalDB)就是为什么它作为安装中的先决条件之一[此系列中的第一个教程](introduction.md)。

有关 SQL Server 版本的详细信息，包括 LocalDB，请参阅以下资源[使用 SQL Server 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)。

## <a name="entity-framework-and-universal-providers"></a>实体框架和通用提供程序

用于数据库访问，Contoso 大学应用程序需要以下软件，因为它不包含在.NET Framework 必须与应用程序部署：

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) （启用 ASP.NET 成员资格系统，以使用 Azure SQL 数据库）
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

由于此软件包括在 NuGet 包，以便所需的程序集部署与该项目已设置项目。 （指向这些包，这可能是比本教程中下载的初学者项目中安装的内容的当前版本的链接）。

如果您要部署到第三方托管提供程序而不是 Azure，请确保您使用实体框架 5.0 或更高版本。 早期版本的 Code First 迁移需要完全信任权限，并且大多数托管提供程序将在中等信任中运行你的应用程序。 中等信任级别的详细信息，请参阅[部署到 IIS 作为测试环境](deploying-to-iis.md)教程。

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>为应用程序数据库部署配置 Code First 迁移

Contoso University 应用程序数据库由 Code First，将使用 Code First 迁移部署它。 通过使用 Code First 迁移的数据库部署的概述，请参阅[此系列中的第一个教程](introduction.md)。

当您部署的应用程序数据库时，通常会不只需部署中它的数据的所有开发数据库到生产环境，因为很多的数据有可能仅用于测试目的。 例如，一个测试数据库中的学生名是虚构的。 但是，你通常不能部署只中它不包含数据的数据库结构根本。 某些测试数据库中的数据可能是真实数据，用户可以开始使用应用程序时，必须有为。 例如，您的数据库可能具有包含有效级别值或实际部门名称的表。

若要模拟这种常见方案，你将配置 Code First 迁移`Seed`将想要在生产环境中存在将数据插入到数据库的方法。 这`Seed`方法不应插入测试数据，因为它将 Code First 在生产环境中创建数据库后在生产环境中运行。

在早期版本的 Code First 迁移发布之前，它为常见的`Seed`方法来插入测试数据还，因为在开发过程中每个模型更改使用该数据库必须完全删除并重新创建从零开始。 使用 Code First 迁移，数据库发生更改后保留数据的测试，因此包括中的测试数据`Seed`方法不是必需。 下载的项目使用的方法包括中的所有数据`Seed`初始值设定项类的方法。 在本教程中将禁用该初始值设定项类和`enable Migrations. Then you'll update the `种子中的迁移配置的方法的类，使它插入只想要在生产环境中要插入的数据。

下图说明了应用程序数据库的架构：

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

对于这些教程，将假定`Student`和`Enrollment`首次部署站点时，表应为空。 其他表包含必须在应用程序上线时预加载的数据。

### <a name="disable-the-initializer"></a>禁用初始值设定项

由于使用 Code First 迁移，无需使用`DropCreateDatabaseIfModelChanges`Code First 初始值设定项。 此初始值设定项的代码位于*SchoolInitializer.cs* ContosoUniversity.DAL 项目文件中的。 中的设置`appSettings`的元素*Web.config*文件会导致应用程序尝试首次访问数据库时运行此初始值设定项：

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

打开应用程序*Web.config*文件，并删除或注释掉`add`指定 Code First 初始值设定项类的元素。 `appSettings`元素现在如下所示：

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 若要指定一个初始值设定项类的另一种方法是执行此操作通过调用`Database.SetInitializer`中`Application_Start`中的方法*Global.asax*文件。 如果要使用该方法来指定初始值设定项的项目中启用迁移，删除该代码行。

> [!NOTE]
> 如果正在使用 Visual Studio 2013，添加步骤 2 和 3 之间的以下步骤: (a) 在 PMC 输入"更新包 entityframework-版本 6.1.1"若要获取 EF 的当前版本。 然后 (b) 生成项目以获取生成错误的列表，并修复它们。 删除不再存在，右键单击并单击解析以添加 using 语句他们需要的命名空间的 using 语句并将出现的 System.Data.EntityState 更改为 System.Data.Entity.EntityState。

### <a name="enable-code-first-migrations"></a>启用 Code First 迁移

1. 请确保为 ContosoUniversity 项目 (而不是 ContosoUniversity.DAL) 设置为启动项目。 在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目并选择**设为启动项目**。 Code First 迁移将查找要查找的数据库连接字符串的启动项目中。
2. 从**工具**菜单中，选择**NuGet 包管理器** > **包管理器控制台**。

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. 在顶部**程序包管理器控制台**窗口中选择作为默认项目，并在 ContosoUniversity.DAL`PM>`提示符处输入"启用迁移"。

    ![enable-migrations 命令](preparing-databases/_static/image4.png)

    (如果收到错误消息，指出*启用迁移*不识别该命令中，输入命令*更新 EntityFramework 的重新安装*，然后重试。)

    此命令将创建*迁移*ContosoUniversity.DAL 项目和该文件夹中的将该文件夹中两个文件： *Configuration.cs*文件，可以用来配置迁移，以及*InitialCreate.cs*文件创建数据库的初始迁移。

    ![Migrations 文件夹](preparing-databases/_static/image5.png)

    选择中的 DAL 项目**默认项目**的下拉列表**程序包管理器控制台**因为`enable-migrations`必须包含代码优先的项目中执行命令上下文类。 在类库项目中的类时，Code First 迁移查找解决方案的启动项目中的数据库连接字符串。 在 ContosoUniversity 解决方案中，web 项目具有已设置为启动项目。 如果不想要指定有连接字符串为启动项目在 Visual Studio 中的项目，您可以在 PowerShell 命令中指定启动项目。 若要查看命令语法，请输入命令`get-help enable-migrations`。

    `enable-migrations`命令自动创建第一次迁移，因为数据库已存在。 一种替代方法是让迁移在创建数据库。 若要执行此操作，请使用**服务器资源管理器**或**SQL Server 对象资源管理器**删除 ContosoUniversity 数据库，然后再启用迁移。 启用迁移后，第一次迁移手动创建通过输入命令"添加迁移 InitialCreate"。 然后可以通过输入命令"更新数据库"创建数据库。

### <a name="set-up-the-seed-method"></a>设置种子方法

对于本教程将添加固定的数据，通过将代码添加到`Seed`Code First 迁移方法`Configuration`类。 代码优先迁移调用`Seed`每个迁移后的方法。

由于`Seed`方法运行每个迁移后，已存在数据的表中后第一次迁移。 若要处理这种情况下，将使用`AddOrUpdate`方法来更新具有已插入，或如果它们尚不存在插入这些行。 `AddOrUpdate`方法可能不是你的方案的最佳选择。 有关详细信息，请参阅[负责与 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)Julie Lerman 的博客上。

1. 打开*Configuration.cs*文件，然后替换中的注释`Seed`方法使用以下代码：

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 对引用`List`已在其下的红色波浪线，因为你没有`using`尚未为其命名空间语句。 右键单击其中一个的实例`List`然后单击**解决**，然后单击**using System.Collections.Generic**。

    ![解决与 using 语句](preparing-databases/_static/image6.png)

    此菜单选项将添加到下面的代码`using`语句接近文件顶部。

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. 按 CTRL-SHIFT-B 以生成项目。

现在项目已准备好部署*ContosoUniversity*数据库。 在部署应用程序，第一次运行它，并导航到的页访问数据库之后, Code First 将创建数据库并运行此`Seed`方法。

> [!NOTE]
> 将代码添加到`Seed`方法是可以固定的数据插入到数据库的许多方式之一。 一种替代方法是将代码添加到`Up`和`Down`迁移的每个类的方法。 `Up`和`Down`方法包含实现数据库更改的代码。 您将看到示例中为它们[部署数据库更新](deploying-a-database-update.md)教程。
> 
> 您还可以编写通过使用执行 SQL 语句的代码`Sql`方法。 例如，如果您已将 Department 表向添加预算列并希望将所有部门的预算为 1,000.00 美元都初始化为迁移的一部分，您可以添加到代码的以下行`Up`迁移方法：
> 
> `Sql("UPDATE Department SET Budget = 1000");`


## <a name="create-scripts-for-membership-database-deployment"></a>创建成员资格数据库部署的脚本

Contoso 大学应用程序使用 ASP.NET 成员资格系统和窗体身份验证用户进行身份验证和授权。 **更新信用额度**页是仅供管理员角色中的用户访问。

运行应用程序，然后单击**课程**，然后单击**更新信用额度**。

![单击更新信用额度](preparing-databases/_static/image7.png)

**登录**页将显示，因为**更新信用额度**页需要管理权限。

输入*管理员*作为用户名并*devpwd*作为密码，然后单击**登录**。

![登录页](preparing-databases/_static/image8.png)

**更新信用额度**页将出现。

![更新信用额度页](preparing-databases/_static/image9.png)

用户和角色的信息位于*aspnet ContosoUniversity*由指定的数据库**DefaultConnection**中的连接字符串*Web.config*文件。

此数据库不受 Entity Framework Code First，因此无法使用迁移来将其部署。 您将使用 dbDacFx 提供程序部署数据库架构，并将配置发布配置文件以运行会将初始数据插入数据库表的脚本。

> [!NOTE]
> 使用 Visual Studio 2013 引入了新的 ASP.NET 成员资格系统 （现在名为 ASP.NET 标识）。 新系统，您可以将应用程序和成员资格表保留在同一个数据库，并可以使用 Code First 迁移部署同时。 示例应用程序使用不能通过使用 Code First 迁移部署早期 ASP.NET 成员资格系统。 用于将此成员资格数据库部署的过程也适用于你的应用程序需要部署不由 Entity Framework Code First 创建的 SQL Server 数据库的任何其他方案。


此处，您通常不希望在生产环境中开发中相同的数据。 将站点部署第一次，时，往往会排除大部分或全部创建用于测试的用户帐户。 因此，已下载的项目有两个成员身份数据库： *aspnet ContosoUniversity.mdf*与开发用户并*aspnet ContosoUniversity Prod.mdf*与生产用户。 对于本教程中的用户名称是相同的两个数据库中：*管理员*并*nonadmin*。 这两个用户具有的密码*devpwd*中开发数据库和*prodpwd*生产数据库中。

将对在测试环境和生产用户到过渡和生产部署开发用户。 为此，你将在本教程中，一个用于开发，一个用于生产环境中，创建两个 SQL 脚本，并在更高版本的教程中，你将配置发布过程来运行它们。

> [!NOTE]
> 成员资格数据库将存储帐户密码的哈希值。 若要部署从一台计算机到另一个帐户，必须确保哈希例程不生成目标服务器上的不同哈希值不是它们在源计算机上执行。 它们会生成相同的哈希时使用了 ASP.NET 通用提供程序，只要不更改默认的算法。 默认的算法是 HMACSHA256 和中指定**验证**的属性 **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** Web.config 文件中的元素。


使用 SQL Server Management Studio (SSMS)，或使用第三方工具，可以手动创建数据部署脚本。 本教程的余下内容将显示如何在 SSMS 中，但如果不想要安装并使用 SSMS 可以从项目的完整版本获取脚本并跳到您的解决方案文件夹中将其存储的部分。

若要安装 SSMS，请安装它从[Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062)通过单击[ENU\x64\SQLManagementStudio\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe)或[ENU\x86\SQLManagementStudio\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)。 如果选择了错误为您的系统，它将无法安装，并且您可以尝试另一个。

（请注意，这是一个 600 兆字节下载。 可能需要很长时间到安装，并且需要重新启动您的计算机。)

SQL Server 安装中心的第一页，单击**新的 SQL Server 独立安装或向现有安装添加功能**，并按照说明进行操作，接受默认选项。

### <a name="create-the-development-database-script"></a>创建开发数据库脚本

1. SSMS 中运行。
2. 在中**连接到服务器**对话框框中，输入 *(localdb) \v11.0*作为**服务器名称**，将保留**身份验证**设置为**Windows 身份验证**，然后单击**Connect**。

    ![SSMS 连接到服务器](preparing-databases/_static/image10.png)
3. 在中**对象资源管理器**窗口中，展开**数据库**，右键单击**aspnet ContosoUniversity**，单击**任务**，然后单击**生成脚本**。

    ![SSMS 生成脚本](preparing-databases/_static/image11.png)
4. 在中**生成和发布脚本**对话框中，单击**设置脚本编写选项**。

    可以跳过**选择对象**步骤，因为默认值是**编写整个数据库及所有数据库对象的脚本**和要执行的操作。
5. 单击 **“高级”**。

    ![SSMS 脚本编写选项](preparing-databases/_static/image12.png)
6. 在中**高级脚本编写选项**对话框中，向下滚动到**的数据的脚本类型**，然后单击**仅限数据**下拉列表中的选项。
7. 更改**编写 USE DATABASE 脚本**到**False**。 使用语句不是有效的 Azure SQL 数据库和测试环境中部署到 SQL Server Express 时不需要。

    ![SSMS 数据仅限脚本，USE 语句](preparing-databases/_static/image13.png)
8. 单击 **“确定”**。
9. 在中**生成和发布脚本**对话框中，**文件名**框指定将创建脚本的位置。 将路径更改为解决方案文件夹 （ContosoUniversity.sln 文件的文件夹） 和文件名*aspnet 数据 dev.sql*。
10. 单击**下一步**若要转到**摘要**选项卡，然后依次**下一步**再次以创建脚本。

    ![创建的 SSMS 脚本](preparing-databases/_static/image14.png)
11. 单击 **“完成”**。

### <a name="create-the-production-database-script"></a>创建生产数据库脚本

由于尚未与生产数据库来运行该项目，它不是尚未附加到 LocalDB 实例。 因此需要进行第一次附加数据库。

1. 在 SSMS**对象资源管理器**，右键单击**数据库**然后单击**附加**。

    ![SSMS 将附加](preparing-databases/_static/image15.png)
2. 在中**附加数据库**对话框中，单击**添加**，然后导航到*aspnet ContosoUniversity Prod.mdf*中的文件*应用\_数据*文件夹。

     ![SSMS 添加附加.mdf 文件](preparing-databases/_static/image16.png)
3. 单击 **“确定”**。
4. 按照你之前用来创建用于生产文件的脚本的相同过程。 脚本文件命名*aspnet 数据 prod.sql*。

## <a name="summary"></a>总结

这两个数据库现已准备好部署并解决方案文件夹中有两个数据部署脚本。

![数据部署脚本](preparing-databases/_static/image17.png)

以下教程中配置项目设置影响部署，并设置自动*Web.config*文件必须在已部署应用程序中不同的设置的转换。

## <a name="more-information"></a>详细信息

有关 NuGet 的详细信息，请参阅[使用 NuGet 管理项目库](https://msdn.microsoft.com/magazine/hh547106.aspx)并[NuGet 文档](http://docs.nuget.org/docs/start-here/overview)。 如果不想要使用 NuGet，您需要了解如何分析 NuGet 包，以确定它的作用时安装它。 (例如，可以配置*Web.config*转换，配置 PowerShell 脚本以运行在生成时，等等。)若要了解有关 NuGet 的工作原理的详细信息，请参阅[创建和发布包](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)并[配置文件和源代码转换](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一页](introduction.md)
> [下一页](web-config-transformations.md)
