---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 迁移到 SQL Server-10 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: bc0bca18d2f6e4cdbb527ab75952e9a50eb49b20
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827350"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 迁移到 SQL Server-10 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

本教程演示如何从 SQL Server Compact 迁移到 SQL Server。 你可能想要执行此操作的原因之一是利用 SQL Server Compact 不支持，如存储的过程、 触发器、 视图或复制的 SQL Server 功能。 有关 SQL Server Compact 和 SQL Server 之间的差异的详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>SQL Server Express，而不是完整的 SQL Server 进行开发

一旦您已决定升级到 SQL Server，你可能想要在开发和测试环境中使用 SQL Server 或 SQL Server Express。 工具支持在和中的数据库引擎功能的差异，除了有提供程序实现中 SQL Server Compact 与其他版本的 SQL Server 之间的差异。 这些差异可能会导致相同的代码生成不同的结果。 因此，如果您决定要保留 SQL Server Compact 与开发数据库，，应全面测试您的站点在 SQL Server 或 SQL Server Express 中每个部署到生产环境之前测试环境中。

与 SQL Server Compact 不同 SQL Server Express 是实质上是相同的数据库引擎和作为完整的 SQL Server 使用相同的.NET 提供程序。 当测试与 SQL Server Express 时，您可以确信的获得相同的结果也将与 SQL Server。 可以使用 SQL Server Express 的 SQL Server 可以使用使用大部分相同的数据库工具 (值得注意的例外正在[SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx))，并支持的 SQL Server 存储的过程、 视图、 触发器等其他功能和复制。 （您通常需要在生产网站中，但是使用完整的 SQL Server。 SQL Server Express 可以在共享宿主环境中运行，但它不是为此，请和很多宿主提供程序不支持它。）

如果正在使用 Visual Studio 2012，则通常选择 SQL Server Express LocalDB 在开发环境因为这是默认情况下使用 Visual Studio 安装的内容。 但是，在 IIS 中，因此您必须使用 SQL Server 或 SQL Server Express 为您的测试环境时，不会将 LocalDB 起作用。

### <a name="combining-databases-versus-keeping-them-separate"></a>而不保留它们单独存放数据库

Contoso 大学应用程序有两个 SQL Server Compact 数据库： 成员资格数据库 (*aspnet.sdf*) 和应用程序数据库 (*School.sdf*)。 迁移时，您可以将这些数据库迁移到两个独立数据库或单个数据库。 你可能想要将它们合并为了简化应用程序数据库和成员资格数据库之间的数据库联接。 托管计划还可能提供的原因要将它们合并。 例如，托管提供商可能会收取多个数据库的详细信息，或可能甚至不允许多个数据库。 这是与 Cytanium Lite 承载用于本教程中，这样只有一个 SQL Server 数据库的帐户的情况。

在本教程中，你会将两个数据库迁移这种方式：

- 迁移到开发环境中的两个 LocalDB 数据库。
- 迁移到测试环境中的两个 SQL Server Express 数据库。
- 迁移到一个组合完整 SQL Server 数据库在生产环境中。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="installing-sql-server-express"></a>安装 SQL Server Express

Visual Studio 2010 中，默认情况下会自动安装 SQL Server Express，但默认情况下它不随一起安装 Visual Studio 2012。 若要安装 SQL Server 2012 Express，请单击以下链接

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

选择*简体中文/x64/SQLEXPR\_x64\_ENU.exe*或*简体中文/x86/SQLEXPR\_x86\_ENU.exe*，并在安装向导中，接受默认值设置。 有关安装选项的详细信息，请参阅[从安装向导 （安装程序） 中安装 SQL Server 2012](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>对于测试环境中创建 SQL Server Express 数据库

下一步是创建的 ASP.NET 成员资格和 School 数据库。

从**视图**菜单中选择**服务器资源管理器**(**数据库资源管理器**在 Visual Web Developer)，然后右键单击**数据连接**，然后选择**创建新的 SQL Server 数据库**。

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

在中**创建新的 SQL Server 数据库**对话框框中，输入"。 \SQLExpress"在**服务器名称**框和"aspnet-测试"中**新的数据库名称**，然后单击**确定**。

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

请按照相同的过程来创建一个名为"学校-Test"的新 SQL Server Express School 数据库。

（要追加"Test"到这些数据库名因为稍后需要创建开发环境中，每个数据库的其他实例，并且需要能够以区分两个组数据库。）

**服务器资源管理器**现在将显示两个新数据库。

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>创建新的数据库授予脚本

当在开发计算机上在 IIS 中运行的应用程序时，该应用程序使用的默认应用程序池的凭据访问数据库。 但是，默认情况下，应用程序池标识没有权限打开的数据库。 因此您必须运行一个脚本，以授予该权限。 在本部分中，您将创建将运行更高版本以确保在 IIS 中运行时，该应用程序可以打开数据库的脚本。

在解决方案中*SolutionFiles*中创建的文件夹[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中，创建名为的新 SQL 文件*Grant.sql*。 将以下 SQL 命令复制到文件，然后保存并关闭文件：

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> 此脚本用于处理与 SQL Server 2008 和 Windows 7 中的 IIS 设置，如在本教程中指定了。 如果使用不同版本的 SQL Server 或 Windows，或您设置 IIS 计算机上以不同的方式，可能需要对此脚本的更改。 有关 SQL Server 脚本详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。


> [!NOTE] 
> 
> **安全说明**此脚本将向提供 db\_所有者在运行时，这是您在生产环境中必须访问数据库的用户的权限。 在某些情况下您可能想要指定具有完整的数据库架构更新部署中，权限和指定的运行时具有的权限仅读取和写入数据的不同用户的用户。 有关详细信息，请参阅**评审 Code First 迁移自动 Web.config 更改**中[作为测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)。


## <a name="configuring-database-deployment-for-the-test-environment"></a>配置测试环境的数据库部署

接下来，您将配置 Visual Studio，以便它将执行以下任务，以便每个数据库：

- 生成 SQL 脚本，在目标数据库中创建源数据库的结构 （表、 列、 约束等）。
- 生成 SQL 脚本，将源数据库的数据插入到目标数据库中的表。
- 运行生成的脚本，并创建目标数据库中授予脚本。

打开**项目属性**窗口，然后选择**打包/发布 SQL**选项卡。

请确保**处于活动状态 （发布）** 或**发行**中选择**配置**下拉列表。

单击**启用此页**。

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

**打包/发布 SQL**因为它指定旧部署方法，通常会禁用选项卡。 大多数情况下，应配置中的数据库部署**发布 Web**向导。 从 SQL Server Compact 迁移到 SQL Server 或 SQL Server Express 是一种特殊情况，此方法是一个不错的选择。

单击**从 Web.config 导入**。

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio 将查找连接字符串*Web.config*文件中，查找另一个用于成员资格数据库，一个用于 School 数据库，并将行对应于每个连接字符串中添加**数据库条目**表。 对于现有的 SQL Server Compact 数据库，是它找到的连接字符串和下一步就是要配置方式和位置来部署这些数据库。

输入中的数据库部署设置**数据库项详细信息**以下部分**数据库条目**表。 中所示的设置**数据库项详细信息**部分适用于二者中的一行**数据库条目**选择表，如下图中所示。

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>配置部署设置的成员资格数据库

选择**DefaultConnection 部署**中的一行**数据库条目**表中以配置应用于成员资格数据库的设置。

在中**目标数据库的连接字符串**，输入指向新的 SQL Server Express 成员资格数据库的连接字符串。 可以获取从所需的连接字符串**服务器资源管理器**。 在中**服务器资源管理器**，展开**数据连接**，然后选择**aspnetTest**数据库，然后从**属性**窗口复制**连接字符串**值。

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

此处重现相同的连接字符串：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

复制并粘贴到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。

请确保**抽取数据和/或从现有数据库架构**处于选中状态。 这是哪些因素会导致 SQL 脚本来自动生成并运行目标数据库中。

**源数据库的连接字符串**从提取值*Web.config*文件，指向开发 SQL Server Compact 数据库。 这是将用于生成将在目标数据库中更高版本运行的脚本的源数据库。 由于你想要部署生产版本的数据库，更改"aspnet Dev.sdf"为"aspnet Prod.sdf"。

更改**数据库脚本选项**从**仅限架构**到**架构和数据**，因为要从中复制数据 （用户帐户和角色） 以及数据库结构。

若要配置部署运行之前创建的授予脚本，必须将其添加到**数据库脚本**部分。 单击**添加脚本**，然后在**添加 SQL 脚本**对话框框中，导航到你在其中存储授予脚本的文件夹 （这是包含您的解决方案文件的文件夹）。 选择名为的文件*Grant.sql*，然后单击**打开**。

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

设置**DefaultConnection 部署**中的一行**数据库条目**现在如以下插图所示：

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>配置部署设置的 School 数据库

接下来，选择**SchoolContext 部署**中的一行**数据库条目**若要配置的 School 数据库部署设置的表。

可以使用你之前用来获取新的 SQL Server Express 数据库的连接字符串的相同方法。 将复制到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

请确保**抽取数据和/或从现有数据库架构**处于选中状态。

**源数据库的连接字符串**从提取值*Web.config*文件，指向开发 SQL Server Compact 数据库。 将"学校 Dev.sdf"更改为"学校-Prod.sdf"若要部署生产版本的数据库。 (在应用中永远不会创建学校 Prod.sdf 文件\_Data 文件夹中，因此会将该文件从测试环境复制到应用\_ContosoUniversity 项目文件夹更高版本中的数据文件夹。)

更改**数据库脚本选项**到**架构和数据**。

您还想要运行脚本，以授予读取和写入应用程序池标识此数据库的权限，因此添加*Grant.sql*之前用于成员资格数据库的脚本文件。

完成后，设置**SchoolContext 部署**中的一行**数据库条目**如以下插图所示：

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

保存对更改**打包/发布 SQL**选项卡。

复制*学校 Prod.sdf*文件从*c:\inetpub\wwwroot\ContosoUniversity\App\_数据*文件夹*应用\_数据*文件夹中在 ContosoUniversity 项目中。

### <a name="specifying-transacted-mode-for-the-grant-script"></a>为授予脚本指定事务的模式

部署过程生成脚本来部署数据库架构和数据。 默认情况下，这些脚本在事务中运行。 但是，默认情况下 （如 grant 脚本中） 的自定义脚本不能在事务中运行。 如果部署过程包含事务模式，在部署期间运行的脚本时可能遇到超时错误。 在本部分中，若要配置自定义脚本来运行在事务中编辑项目文件。

在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，然后选择**卸载项目**。

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

然后再次右键单击项目并选择**编辑 ContosoUniversity.csproj**。

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio 编辑器中显示项目文件的 XML 的内容。 请注意，有几条`PropertyGroup`元素。 (在图中的内容，`PropertyGroup`省略了元素。)

![项目文件编辑器窗口](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

第一个，不具有`Condition`属性，而不考虑应用的设置生成配置的。 一个`PropertyGroup`元素仅适用于调试生成配置 (请注意`Condition`属性)、 一个仅适用于发布生成配置，并且其中一个仅适用于测试生成配置。 内`PropertyGroup`元素中的为发布生成配置，你将看到`PublishDatabaseSettings`上输入的包含设置元素**打包/发布 SQL**选项卡。没有`Object`对应于每个授权脚本的元素的指定的 （请注意，这两个实例"Grant.sql"）。 默认情况下`Transacted`的属性`Source`元素为每个授予脚本`False`。

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

更改的值`Transacted`的属性`Source`元素`True`。

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

保存并关闭项目文件中，并右键单击项目中的**解决方案资源管理器**，然后选择**重新加载项目**。

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>设置连接字符串的 Web.Config 转换

连接字符串的新的 SQL Express 数据库输入**打包/发布 SQL**选项卡上通过 Web 部署仅用于在部署期间更新目标数据库。 您仍必须设置*Web.config*转换，以便在已部署中的连接字符串*Web.config*文件指向新的 SQL Server Express 数据库。 (当你使用**打包/发布 SQL**选项卡上，无法在发布配置文件中配置连接字符串。)

打开*Web.Test.config*和替换`connectionStrings`具有元素`connectionStrings`下面的示例中的元素。 （请确保你仅将复制 connectionStrings 元素，而不是如下所示提供上下文的周围的代码。）

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

此代码会导致`connectionString`并`providerName`每个属性`add`要被替换元素中已部署*Web.config*文件。 这些连接字符串不是你在中输入相同**打包/发布 SQL**选项卡。设置"MultipleActiveResultSets = True"具有已添加到它们，因为它具有所需的实体框架和通用提供程序。

## <a name="installing-sql-server-compact"></a>安装 SQL Server Compact

SqlServerCompact NuGet 包提供 SQL Server Compact 数据库引擎的 Contoso 大学应用程序的程序集。 但现在它不是应用程序，但 Web 部署，必须能够读取 SQL Server Compact 数据库中，若要创建在 SQL Server 数据库中运行脚本。 若要启用 Web 部署可以读取 SQL Server Compact 数据库，请安装 SQL Server Compact 在开发计算机上使用以下链接： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。

## <a name="deploying-to-the-test-environment"></a>部署到测试环境

若要发布到测试环境，您必须创建配置为使用的发布配置文件**打包/发布 SQL**数据库发布而不发布配置文件数据库设置的选项卡。

首先，删除现有的测试配置文件。

在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。

选择**配置文件**选项卡。

单击**管理配置文件**。

选择**测试**，单击**删除**，然后单击**关闭**。

关闭**发布 Web**向导以保存此更改。

接下来，创建新的测试配置文件，并使用它来发布该项目。

在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。

选择**配置文件**选项卡。

选择**&lt;新...&gt;** 从下拉列表中，并输入"Test"作为配置文件名称。

在中**服务 URL**框中，输入*localhost*。

在中**站点/应用程序**框中，输入*默认 Web 站点/ContosoUniversity*。

在中**目标 URL**框中，输入 `http://localhost/ContosoUniversity/` 。

单击 **“下一步”**。

**设置**选项卡会发出警告，**打包/发布 SQL**已经配置了选项卡上，并且它使你有机会来覆盖它们通过单击启用新的数据库发布的改进。 为此部署，不想要重写**打包/发布 SQL**选项卡上设置，因此只需单击**下一步**。

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

中的消息**预览版**选项卡指示**没有数据库选择发布**，但这只意味着未在发布配置文件中配置数据库发布。

单击“发布” 。

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio 部署应用程序，并在测试环境中的站点的主页上浏览器中打开。 运行讲师页以查看它显示您在前面看到的相同数据。 运行**添加学生**页上，添加新学生，然后查看中的新学生**学生**页。 这将验证你可以更新数据库。 选择**更新信用额度**（需要登录） 的页以验证是否已部署成员资格数据库并有权访问它。

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>对于生产环境中创建 SQL Server 数据库

现在，已部署到测试环境，你准备好设置部署到生产环境。 在开始之前用于测试环境中，通过创建要部署到的数据库。 您还记得概述，Cytanium Lite 托管计划将仅允许单个 SQL Server 数据库，因此将只有一个数据库，不是两个设置。 所有表和成员身份和学校 SQL Server Compact 数据库中的数据将部署到生产环境中的一个 SQL Server 数据库中。

转到 Cytanium 控件面板[ http://panel.cytanium.com ](http://panel.cytanium.com)。 将鼠标悬停**数据库**，然后单击**SQL Server 2008**。

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

在中**SQL Server 2008**页上，单击**Create Database**。

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

命名数据库"学校"，然后单击**保存**。 （页上会自动添加前缀"contosou"，因此有效的名称将是"contosouSchool"。）

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

在同一页上，单击**Create User**。 在 Cytanium 的服务器，而不是使用集成的 Windows 安全性，并让应用程序池标识，打开你的数据库，你将创建有权打开你的数据库用户。 你将转到生产环境中的连接字符串添加用户的凭据*Web.config*文件。 在此步骤中创建这些凭据。

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

填写必填字段**SQL 用户属性**页：

- 输入"ContosoUniversityUser"作为名称。
- 输入密码。
- 选择**contosouSchool**作为默认数据库。
- 选择**contosouSchool**复选框。

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>在生产环境的配置数据库部署

现在您已准备好设置中的数据库部署设置**打包/发布 SQL**选项卡，如之前在测试环境。

打开**项目属性**窗口中，选择**打包/发布 SQL**选项卡，并确保选中**处于活动状态 （发布）** 或者**版本**是在所选**配置**下拉列表。

在配置部署设置为每个数据库时，你的生产和测试环境所执行的操作的主要区别是如何配置连接字符串中。 对于测试环境中输入不同的目标数据库连接字符串，但是对于生产环境目标连接字符串将是相同的两个数据库。 这是因为这两个数据库部署到生产环境中的一个数据库。

### <a name="configuring-deployment-settings-for-the-membership-database"></a>配置部署设置的成员资格数据库

若要配置将应用于成员资格数据库的设置，请选择**DefaultConnection 部署**中的一行**数据库条目**表。

在中**目标数据库的连接字符串**，输入指向刚创建的新生产 SQL Server 数据库的连接字符串。 可以从欢迎使用电子邮件来获取连接字符串。 电子邮件的相关部分包含以下示例连接字符串：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

替换为三个变量后，您需要的连接字符串看起来如下例所示：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

复制并粘贴到此连接字符串**目标数据库的连接字符串**中**打包/发布 SQL**选项卡。

请确保**抽取数据和/或从现有数据库架构**仍然选择，且**数据库脚本选项**仍**架构和数据**。

在中**数据库脚本**框中，清除 Grant.sql 脚本旁边的复选框。

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>配置部署设置的 School 数据库

接下来，选择**SchoolContext 部署**中的一行**数据库条目**表中以配置 School 数据库设置。

将复制到相同的连接字符串**目标数据库的连接字符串**复制到此字段中的成员资格数据库。

请确保**抽取数据和/或从现有数据库架构**仍然选择，且**数据库脚本选项**仍**架构和数据**。

在中**数据库脚本**框中，清除 Grant.sql 脚本旁边的复选框。

保存对更改**打包/发布 SQL**选项卡。

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>设置 Web.Config 转换为对生产数据库的连接字符串

接下来，你将设置*Web.config*转换，以便在已部署中的连接字符串*Web.config*文件以指向新的生产数据库。 输入的连接字符串**打包/发布 SQL** Web 部署可以使用选项卡是与应用程序需要使用，除了添加一个相同`MultipleResultSets`选项。

打开*Web.Production.config*和替换`connectionStrings`具有元素`connectionStrings`元素，如以下示例所示。 (仅复制`connectionStrings`元素中，不提供要显示的上下文的周围的标记。)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

有时，您看到建议，告诉你始终加密中的连接字符串*Web.config*文件。 这可能是如果你已部署到你自己的公司网络上的服务器。 时要部署到共享宿主环境中，不过，将信任托管提供商的安全做法并不是必需的或实际加密连接字符串。

## <a name="deploying-to-the-production-environment"></a>部署到生产环境

现在你已准备好部署到生产。 Web 部署将在项目中的 SQL Server Compact 数据库中读取*应用程序\_数据*文件夹，然后重新创建其所有表和生产 SQL Server 数据库中的数据。 若要通过使用发布**打包/发布 Web**选项卡设置，则必须创建新的发布配置文件用于生产。

首先，删除现有的生产配置文件，如之前所做的测试配置文件。

在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。

选择**配置文件**选项卡。

单击**管理配置文件**。

选择**生产**，单击**删除**，然后单击**关闭**。

关闭**发布 Web**向导以保存此更改。

接下来，创建新的生产配置文件，并使用它来发布该项目。

在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目中，然后单击**发布**。

选择**配置文件**选项卡。

单击**导入**，并选择前面下载的.publishsettings 文件。

上**连接**选项卡上，更改**目标 URL**到正确的临时 URL，在此示例是 http://contosouniversity.com.vserver01.cytanium.com 。

重命名到生产环境的配置文件。 (选择**配置文件**选项卡，单击**管理配置文件**若要执行此操作)。

关闭**发布 Web**向导将保存所做的更改。

在实际的应用程序在其中正在更新数据库在生产环境中，您将执行两个附加步骤现在在发布之前：

1. 上传*应用程序\_offline.htm*，如下所示[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。
2. 使用**文件管理器**Cytanium 控件面板要复制的功能*aspnet Prod.sdf*并*学校 Prod.sdf*文件从生产站点复制到*应用程序\_数据*ContosoUniversity 项目文件夹。 这可确保要部署到新的 SQL Server 数据库的数据包括最新的更新所做的生产网站。

在中**Web 单键发布**工具栏中，请确保**生产**配置文件已选中，然后单击**发布**。

如果上传<em>应用程序\_offline.htm</em>发布前，您必须使用<strong>文件管理器</strong>实用程序在要删除的 Cytanium 控件面板<em>应用\_脱机。</em>htm 然后再测试。 你还可以在同一时间删除<em>.sdf</em>文件从<em>应用\_数据</em>文件夹。

你现在可以打开浏览器并转到您的个人网站的 URL 以测试应用程序相同的方式部署到测试环境之后。

## <a name="switching-to-sql-server-express-localdb-in-development"></a>切换到开发中的 SQL Server Express LocalDB

如概述中所述，它是通常最好在测试和生产环境中使用的开发中使用相同的数据库引擎。 （请记住在开发中使用 SQL Server Express 的优势是，数据库仍将可用开发、 测试和生产环境中）。在本部分中您将设置为 ContosoUniversity 项目从 Visual Studio 运行应用程序时使用 SQL Server Express LocalDB。

若要执行此迁移的最简单方法是让代码优先和成员资格系统为你创建这两个新的开发数据库。 使用此方法将迁移需要三个步骤：

1. 更改连接字符串以指定新的 SQL Express LocalDB 数据库。
2. 运行网站管理工具以创建管理员用户。 这将创建成员资格数据库。
3. 使用 Code First 迁移更新数据库命令来创建和设置应用程序数据库的种子。

### <a name="updating-connection-strings-in-the-webconfig-file"></a>正在更新 Web.config 文件中的连接字符串

打开*Web.config*文件，然后替换`connectionStrings`元素使用以下代码：

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>创建成员资格数据库

在中**解决方案资源管理器**，选择 ContosoUniversity 项目，然后单击**ASP.NET 配置**中**项目**菜单。

选择安全选项卡。

单击**创建或管理角色**，然后创建**管理员**角色。

返回到安全选项卡。

单击**创建用户**，然后选择**管理员**复选框，并创建名为管理员的用户

关闭**网站管理工具**。

### <a name="creating-the-school-database"></a>创建 School 数据库

打开包管理器控制台窗口。

在中**默认项目**下拉列表中，选择 ContosoUniversity.DAL 项目。

输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First 迁移应用的初始迁移创建数据库，然后应用 AddBirthDate 迁移，然后运行 Seed 方法。

通过按控件 F5 运行该站点。 与用于测试和生产环境一样，运行**添加学生**页上，添加新学生，然后查看中的新学生**学生**页。 这将验证 School 数据库已创建并初始化和你已阅读并向其中写入访问权限。

选择**更新信用额度**页上，然后登录以验证成员资格数据库已部署并且有权访问它。 如果未迁移的用户帐户，创建一个管理员帐户，然后选择**更新信用额度**页后，可以验证它是否正常工作。

## <a name="cleaning-up-sql-server-compact-files"></a>清除 SQL Server Compact 文件

您不再需要的文件和已包含在内以支持 SQL Server Compact 的 NuGet 包。 如果你想 （此步骤不需要），你可以清理不需要的文件和引用。

在中**解决方案资源管理器**，删除 *.sdf*从文件*应用\_数据*文件夹和*amd64*和*x86*从文件夹*bin*文件夹。

在中**解决方案资源管理器**，右键单击该解决方案 （而不是项目的），并单击**为解决方案管理 NuGet 包**。

在左窗格中**管理 NuGet 包**对话框中，选择**已安装的包**。

选择**EntityFramework.SqlServerCompact**程序包，再单击**管理**。

在中**选择项目**对话框中，选择这两个项目。 若要卸载这两个项目中的包，请清除这两个复选框，然后单击**确定**。

在询问您是否也卸载依赖的包的对话框中，单击不可以。 其中一种是您必须保留的实体框架包。

请按照相同的过程来卸载**SqlServerCompact**包。 (必须按以下顺序卸载包，因为**EntityFramework.SqlServerCompact**程序包依赖于**SqlServerCompact**包。)

你现在已成功迁移到 SQL Server Express 和完整的 SQL Server。 在下一个教程将使另一个数据库更改，并将了解如何测试和生产数据库使用 SQL Server Express 和完整的 SQL Server 时部署数据库更改。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
