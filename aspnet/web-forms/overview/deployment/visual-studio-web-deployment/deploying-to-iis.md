---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署到测试 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
ms.date: 03/23/2015
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 6bfd1399c9e627839005fa27086c90bc0cc049e5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826363"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>使用 Visual Studio 的 ASP.NET Web 部署： 部署到测试
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

本教程演示如何以 ASP.NET web 应用程序部署到 IIS 在本地计算机上。

开发的应用程序，您通常进行测试的 Visual Studio 中运行。 默认情况下，在 Visual Studio 2012 中的 web 应用程序项目使用 IIS Express 用作开发 web 服务器。 IIS Express 表现得更像与 Visual Studio 开发服务器 (也称为 Cassini)，默认情况下使用 Visual Studio 2010 的完整 IIS。 但既不开发 web 服务器的工作方式完全相同 IIS。 因此，就可以，当应用程序时对其进行测试在 Visual Studio 中，但失败部署到 IIS 时，将正确运行。

你可以在以下方面更可靠地测试应用程序：

1. 通过使用相同的过程的更高版本将使用它来将其部署到生产环境部署到 IIS 在开发计算机上的应用程序。 可以配置 Visual Studio 以使用 IIS 时运行 web 项目中，但执行该操作不会测试您的部署过程。 此方法验证部署过程除了验证你的应用程序将在 IIS 下正确运行。
2. 应用程序部署到测试环境与生产环境几乎相同。 由于这些教程在生产环境是 Azure 应用服务中的 Web 应用，因此非常适合测试环境是在 Azure 应用服务中创建的其他 web 应用。 将此第二个 web 应用仅用于测试，但将设置为生产 web 应用的相同方法。

选项 2 是最可靠的方法，若要测试，并且如果这样做，您不一定需要执行操作的选项 1。 但是，如果要部署到第三方托管提供程序选项 2 可能不可行，或可能开销很大，因此本系列教程演示这两种方法。 在提供了选项 2 的指导[部署到生产环境](deploying-to-production.md)教程。

有关在 Visual Studio 中使用 web 服务器的详细信息，请参阅[对于 ASP.NET Web 项目的 Visual Studio 中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。

## <a name="install-iis"></a>安装 IIS

若要在开发计算机上部署到 IIS，必须具有 IIS 和 Web 部署安装。 使用 Visual Studio 中，默认情况下安装 web 部署，但 IIS 未包含在默认 Windows 8 或 Windows 7 配置。 如果已安装了 IIS 和默认应用程序池已设置为.NET 4，请跳到[下一步部分](#sqlexpress)。

1. 使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是首选的方法来安装 IIS 和 Web 部署，因为 Web 平台安装程序为 IIS 安装建议的配置，并且它会自动安装 IIS 和 Web 的先决条件如有必要部署。

    若要运行 Web 平台安装程序来安装 IIS 和 Web 部署，请使用以下链接。 如果你已安装 IIS、 Web 部署或任何其所需的组件，Web 平台安装程序安装只缺少的内容。

   - [安装 IIS 和 Web 部署使用 WebPI](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

     可以看到，该值指示将安装 IIS 7 的消息。 链接的工作原理适用于 Windows 8 中的 IIS 8，但 Windows 8 确保 ASP.NET 4.5 安装，请执行以下步骤：

   - 打开**Control Panel**，**程序和功能**，**打开或关闭打开的 Windows 功能**。
   - 展开**Internet 信息服务**，**万维网服务**，并**应用程序开发功能**。
   - 请确保**ASP.NET 4.5**处于选中状态。

      ![选择 ASP.NET 4.5](deploying-to-iis/_static/image1.png)

安装 IIS 后，运行**IIS 管理器**以确保.NET Framework 版本 4 分配给默认应用程序池。

1. 按 WINDOWS + R 打开**运行**对话框。

    (或在 Windows 8 中输入"运行"**启动**页上，或在 Windows 7 中选择**运行**从**启动**菜单。 如果**运行**不在**启动**菜单中，右键单击任务栏中，单击**属性**，选择 **「 开始 」 菜单**选项卡上，单击**自定义**，然后选择**运行命令**。)
2. 输入"inetmgr"，然后单击**确定**。
3. 在中**连接**窗格中，展开服务器节点，然后选择**应用程序池**。 在中**应用程序池**窗格中，如果**DefaultAppPool**是分配给.NET framework 版本 4 所示，跳到下一节。

    [![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)
4. 如果您看到只有两个应用程序池，并且这两个值设置为.NET Framework 2.0，您必须在 IIS 中安装 ASP.NET 4。

    有关 Windows 8 中，请参阅在前面的说明部分已安装并确保该 ASP.NET 4.5，或请参阅[此知识库文章](https://support.microsoft.com/kb/2736284)。 对于 Windows 7 中，打开命令提示符窗口，请右键单击**命令提示符**在 Windows 中**启动**菜单并选择**以管理员身份运行**。 然后运行[aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中，使用以下命令安装 ASP.NET 4。 （在 32 位系统中，将为"Framework64"与"框架"。）

    [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

    此命令将为.NET Framework 4 中，创建新的应用程序池，但仍将被默认应用程序池设置为 2.0。 您要部署应用程序面向.NET 4 到该应用程序池，因此您必须将应用程序池更改为.NET 4。
5. 如果您关闭**IIS 管理器**再次运行中，展开服务器节点，单击**应用程序池**以显示**应用程序池**再次窗格。
6. 在中**应用程序池**窗格中，单击**DefaultAppPool**，然后在**操作**窗格中，单击**基本设置**。

    [![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)
7. 在中**编辑应用程序池**对话框中，更改 **.NET Framework 版本**到 **.NET Framework v4.0.30319**然后单击**确定**。

    [![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)

IIS 现在已准备就绪，发布 web 应用程序，但您可以执行的之前必须在测试环境中创建将使用的数据库。

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>安装 SQL Server Express

LocalDB 不设计用于处理在 IIS 中，因此对于你的测试环境需要已安装 SQL Server Express。 如果使用的 Visual Studio 2010 SQL Server Express 已安装默认情况下。 如果正在使用 Visual Studio 2012，您必须安装它。

若要安装 SQL Server Express，请安装它从[Download Center: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062)通过单击[ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe)或[ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe)。 如果选择了错误为您的系统，它将无法安装，并且您可以尝试另一个。

SQL Server 安装中心的第一页，单击**新的 SQL Server 独立安装或向现有安装添加功能**，并按照说明进行操作，接受默认选项。 在安装向导中，接受默认设置。 有关安装选项的详细信息，请参阅[从安装向导 （安装程序） 中安装 SQL Server 2012](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>创建 SQL Server Express 数据库的测试环境

Contoso 大学应用程序有两个数据库： 成员资格数据库和应用程序数据库。 可以将这些数据库部署到两个独立数据库或单个数据库。 你可能想要将它们合并为了简化应用程序数据库和成员资格数据库之间的数据库联接。 如果要部署到第三方托管提供商，托管计划可能会提供的原因要将它们合并。 例如，托管提供商可能会收取多个数据库的详细信息，或可能甚至不允许多个数据库。

在本教程中，你将部署到测试环境中的两个数据库和过渡和生产环境中的一个数据库。

从**视图**在 Visual Studio 中，选择菜单**服务器资源管理器**(**数据库资源管理器**在 Visual Web Developer)，然后右键单击**数据连接** ，然后选择**创建新的 SQL Server 数据库**。

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

在中**创建新的 SQL Server 数据库**对话框框中，输入"。 \SQLExpress"在**服务器名称**框和"aspnet-ContosoUniversity"中**新的数据库名称**框，然后单击**确定**。

![创建 aspnet ContosoUniversity](deploying-to-iis/_static/image9.png)

请按照相同的过程来创建一个名为"ContosoUniversity"的新 SQL Server Express School 数据库。

**服务器资源管理器**现在将显示两个新数据库。

![在服务器资源管理器中的新数据库](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>创建新的数据库授予脚本

当在开发计算机上在 IIS 中运行的应用程序时，该应用程序使用的默认应用程序池的凭据访问数据库。 但是，默认情况下，应用程序池标识没有权限打开的数据库。 因此您必须运行一个脚本，以授予该权限。 在本部分中，您将创建将运行更高版本以确保在 IIS 中运行时，该应用程序可以打开数据库的脚本。

右键单击该解决方案 （而不是项目的），然后单击**添加新项**，然后创建一个新**SQL 文件**名为*Grant.sql*。 将以下 SQL 命令复制到文件，然后保存并关闭文件：

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

> [!NOTE]
> 此脚本用于处理与 SQL Server Express 2012 和 Windows 8 或 Windows 7 中的 IIS 设置，如在本教程中指定了。 如果使用不同版本的 SQL Server 或 Windows，或您设置 IIS 计算机上以不同的方式，可能需要对此脚本的更改。 有关 SQL Server 脚本详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。


> [!NOTE] 
> 
> **安全说明**此脚本将向提供 db\_所有者在运行时，这是您在生产环境中必须访问数据库的用户的权限。 在某些情况下您可能想要指定具有完整的数据库架构更新部署中，权限和指定的运行时具有的权限仅读取和写入数据的不同用户的用户。 有关详细信息，请参阅[评审 Code First 迁移自动 Web.config 更改](#reviewingmigrations)在本教程中更高版本。


<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>运行应用程序数据库中授予脚本

你可以配置要运行授予脚本成员资格数据库中，在部署期间因为该数据库的部署使用 dbDacFx 提供程序的发布配置文件。 在 Code First 迁移部署，这是你要如何部署应用程序数据库期间，无法运行脚本。 因此，必须手动运行应用程序数据库中的部署前的脚本。

1. 在 Visual Studio 中打开*Grant.sql*前面创建的文件。
2. 单击“连接” 。 

    ![连接按钮](deploying-to-iis/_static/image11.png)
3. 在中**连接到服务器**对话框框中，输入 *。 \SQLExpress*作为**服务器名称**，然后单击**Connect**。
4. 在数据库下拉列表中选择**ContosoUniversity**，然后单击**Execute**。 

    ![](deploying-to-iis/_static/image12.png)

现在，默认应用程序池标识代码优先迁移来创建数据库表，该应用程序运行时在应用程序数据库中具有足够的权限。

## <a name="publish-to-iis"></a>将发布到 IIS

有几种方法可以将它们部署到 IIS，使用 Visual Studio 和 Web 部署：

- 使用一键式发布的 Visual Studio。
- 从命令行发布。
- 创建*部署包*和使用 IIS 管理器 UI 安装它。 部署包组成 *.zip*文件，其中包含所有文件和在 IIS 中安装站点所需的元数据。
- 创建部署包并将其使用命令行安装。

已在前面的教程，要将 Visual Studio 设置为自动执行部署任务适用于所有这些方法的过程。 在这些教程将使用这些方法的前两个。 有关使用部署包的信息，请参阅[web 应用程序部署通过创建和安装 web 部署包](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)for Visual Studio 和 ASP.NET Web 部署内容映射中。

发布前，请确保在管理员模式下运行 Visual Studio。 如果没有看到 **（管理员）** 在标题栏中，关闭 Visual Studio。 在 Windows 8**启动**页上或 Windows 7**启动**菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择**以管理员身份运行**。 管理员模式下是发布仅当您要发布到 IIS 在本地计算机上所必需的。

### <a name="create-the-publish-profile"></a>创建发布配置文件

1. 在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目 （而不是 ContosoUniversity.DAL 项目），然后选择**发布**。

    **发布 Web**向导显示。

    ![发布 Web 向导配置文件选项卡](deploying-to-iis/_static/image13.png)
2. 在下拉列表中，选择**&lt;新建...&gt;**. (安装了最新 Visual Studio 更新，没有任何下拉列表中，而且单击以从头开始创建新的配置文件按钮**自定义**。)
3. 在中**新的配置文件**对话框中，输入"Test"，然后单击**确定**。

    该向导将自动前进到**连接**选项卡。
4. 在中**服务 URL**框中，输入*localhost*。
5. 在中**站点/应用程序**框中，输入*默认 Web 站点/ContosoUniversity*
6. 在中**目标 URL**框中，输入 `http://localhost/ContosoUniversity`

    **目标 URL**设置不需要。 完成 Visual Studio 部署应用程序后，它会自动打开默认浏览器访问此 URL。 如果不想要在部署后自动打开浏览器，将此框留空。
7. 单击**验证连接**以验证是否设置正确无误，并可以在本地计算机上连接到 IIS。

    绿色复选标记验证连接成功。

    ![发布 Web 向导连接选项卡](deploying-to-iis/_static/image14.png)
8. 单击**下一步**转到**设置**选项卡。
9. **配置**下拉列表框指定要部署的生成配置。 将其设置为发布的默认值。 不会将在本教程中部署了调试版本。
10. 展开**文件发布选项**，然后选择**排除将应用程序中的文件\_Data 文件夹**。

    在测试环境中应用程序将访问本地 SQL Server Express 实例中创建的数据库，不.mdf 文件中*应用程序\_数据*文件夹。
11. 将保留**在发布期间预编译**并**删除目标处的其他文件**清除复选框。

    ![设置选项卡中的文件发布选项](deploying-to-iis/_static/image15.png)

    预编译是主要用于非常大的站点; 一个选项它可以减少页面第一次请求页面时，将站点发布后的启动时间。

    不需要由于这是你第一次部署，也不会有任何文件的目标文件夹中尚未删除的其他文件。

    > [!NOTE] 
    > 
    > [!CAUTION]
    > 如果选择**删除的其他文件**对于到相同站点的后续部署，请确保你使用的预览功能，以便你提前看到在部署之前，将删除哪些文件。 预期的行为是，Web 部署会删除已在项目中删除目标服务器上的文件。 但是，在源和目标文件夹下的整个文件夹结构进行比较，并在某些情况下 Web 部署可能会删除不想要删除的文件。
    > 
    > 例如，如果在服务器上的子文件夹中没有的 web 应用程序项目部署到的根文件夹时，将删除子文件夹。 你可能在 contoso.com 的主站点的一个项目，并在 contoso.com/blog 博客的另一个项目。 博客应用程序是一个子文件夹中。 如果您选择删除目标位置的其他文件，在将主站点时，将删除博客应用程序。
    > 
    > 有关其他示例，您的应用程序\_数据文件夹可能会意外删除。 某些数据库，例如 SQL Server Compact 数据库文件存储在应用\_数据文件夹。 在初始部署之后不想要保留将数据库文件复制在后续部署中，因此选择排除应用\_打包/发布 Web 选项卡上的数据。在执行操作，如果你已删除所选目标位置的其他文件、 数据库文件和应用程序之后\_的下次发布时都将删除数据文件夹本身。

### <a name="configure-deployment-for-the-membership-database"></a>配置成员资格数据库部署

以下步骤适用于**DefaultConnection**数据库中**数据库**对话框的一节。

1. 在中**远程连接字符串**框中，输入以下指向新的 SQL Server Express 成员资格数据库的连接字符串。

    [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

    由于部署过程会将此连接字符串放在已部署的 Web.config 文件中**在运行时使用此连接字符串**处于选中状态。

    此外可以获取的连接字符串**服务器资源管理器**。 在中**服务器资源管理器**，展开**数据连接**，然后选择 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**数据库，然后从**属性**窗口中复制**连接字符串**值。 连接字符串将具有一个可以删除的其他设置： `Pooling=False`。
2. 选择**更新数据库**。

    这会导致要在部署过程中创建目标数据库中的数据库架构。 以下步骤中指定您需要运行其他脚本： 一个用于授予对默认应用程序池，一个用于部署数据的数据库访问权限。
3. 单击**配置数据库更新**。
4. 在中**配置数据库更新**对话框中，单击**添加 SQL 脚本**，然后导航到*Grant.sql*之前保存在解决方案文件夹中的脚本。
5. 重复此过程以添加*aspnet 数据 dev.sql*脚本。

    ![为成员资格数据库配置数据库更新](deploying-to-iis/_static/image16.png)
6. 单击 **“关闭”**。

### <a name="configure-deployment-for-the-application-database"></a>配置应用程序数据库的部署

当 Visual Studio 检测到实体框架`DbContext`类，它创建中的条目**数据库**节，其中包含**执行 Code First 迁移**复选框，而不是**更新数据库**复选框。 对于本教程将使用该复选框来指定 Code First 迁移部署。

在某些情况下，你可能使用`DbContext`数据库，但想要使用 dbDacFx 提供程序而不是迁移部署数据库。 在这种情况下，请参阅[如何将 Code First 数据库而无需迁移的部署？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) MSDN 上的 ASP.NET Web 部署常见问题解答中。

以下步骤适用于**SchoolContext**数据库中**数据库**对话框的一节。

1. 在中**远程连接字符串**框中，输入以下指向新的 SQL Server Express 应用程序数据库的连接字符串。

    [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

    由于部署过程会将此连接字符串放在已部署的 Web.config 文件中**在运行时使用此连接字符串**处于选中状态。

    此外可以获取的应用程序数据库连接字符串**服务器资源管理器**相同的方式获得成员身份数据库连接字符串。
2. 选择**执行 Code First 迁移 （应用程序启动时运行）**。

    此选项将导致部署过程，配置已部署的 Web.config 文件，以指定`MigrateDatabaseToLatestVersion`初始值设定项。 此初始值设定项自动更新数据库的最新版本时该应用程序部署后首次访问数据库。

### <a name="configure-publish-profile-transforms"></a>配置发布配置文件转换

1. 单击**关闭**，然后单击**是**当系统询问你是否要保存更改。
2. 在中**解决方案资源管理器**，展开**属性**，展开**PublishProfiles**。
3. Rright 键单击*Test.pubxml，* ，然后单击**添加配置转换**。

    ![添加配置转换菜单](deploying-to-iis/_static/image17.png)

    Visual Studio 将创建*Web.Test.config*转换文件并将其打开。
4. 在中*Web.Test.config*转换文件中，打开后立即插入以下代码配置标记。

    [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    当使用测试发布配置文件时，此转换设置为"Test"的环境指示器。 在已部署的站点将在"Contoso University"H1 标题后看到"（测试）"。
5. 保存并关闭文件。
6. 右键单击*Web.Test.config*文件，并单击**预览版转换**以确保您编码的转换生成预期的更改。

    **Web.config 预览版**窗口中显示结果应用同时*Web.Release.config*转换并*Web.Test.config*转换。

### <a name="preview-the-deployment-updates"></a>预览的部署更新

1. 打开**发布 Web**再次向导 (右键单击 ContosoUniversity 项目，然后单击**发布**)。
2. 在中**预览版**选项卡上，请确保**测试**配置文件，并且仍然选择，然后单击**开始预览**以查看将复制的文件的列表。

    ![预览按钮](deploying-to-iis/_static/image18.png)

    ![发布预览](deploying-to-iis/_static/image19.png)

    此外可以单击**预览版数据库**链接可查看将在成员资格数据库中运行的脚本。 （没有运行脚本对于 Code First 迁移部署，因此没有要预览的应用程序数据库。）
3. 单击“发布” 。

    如果 Visual Studio 不是在管理员模式下，可能会收到一个错误消息，指示权限错误。 在这种情况下，关闭 Visual Studio，在管理员模式下打开并尝试再次发布。

    在管理员模式下，Visual Studio 是否**输出**窗口报告成功生成和发布。

    ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

    如果输入中的 URL**目标 URL**上的发布配置文件框**连接**选项卡上，浏览器会自动打开指向本地计算机上在 IIS 中运行 Contoso University 主页上。

## <a name="test-in-the-test-environment"></a>在测试环境中测试

请注意，环境指示器，显示"（测试）"而不是"（开发）"，其中显示*Web.config*环境指示器的转换是否成功。

运行**讲师**页以验证 Code First 种子讲师数据的数据库。 当选中此页时，可能需要几分钟才能加载，因为 Code First 创建数据库并运行`Seed`方法。 （它没有这样做时，因为该应用程序不尝试尚未访问的数据库都在主页上。）

单击**学生**选项卡以验证是否已部署的数据库具有任何学生。

选择**添加学生**从**学生**菜单中，添加一名学生，，然后查看中的新学生**学生**页以验证是否可以成功写入到数据库.

从**课程**菜单中，选择**更新信用额度**。 **更新信用额度**页面需要管理员权限，因此**Log In**显示页。 输入创建早期 （"admin"和"devpwd"） 的管理员帐户凭据。 **更新信用额度**显示页面时，用于验证在上一教程中创建的管理员帐户已正确部署到测试环境。

确认*Elmah*文件夹中存在*c:\inetpub\wwwroot\ContosoUniversity*的占位符文件将在其中的文件夹。

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>查看自动 Web.config 更改的 Code First 迁移

打开*Web.config*文件中的已部署应用程序*C:\inetpub\wwwroot\ContosoUniversity* ，可以看到部署过程会自动配置 Code First 迁移到其中更新到最新版本的数据库。

![](deploying-to-iis/_static/image21.png)

部署过程还创建新的连接字符串的代码优先迁移来更新数据库架构的以独占方式使用：

![Database_Publish 连接字符串](deploying-to-iis/_static/image22.png)

通过此附加的连接字符串，您可以指定一个用户帐户对数据库架构更新，以及用于数据访问应用程序的不同用户帐户。 例如，可将分配**db\_所有者**到 Code First 迁移角色和**db\_datareader**并**db\_datawriter**向应用程序角色。 这是一种常用的深度防御模式阻止潜在的恶意代码应用程序更改数据库架构。 （例如，可能发生此错误在成功的 SQL 注入式攻击。）这些教程不使用此模式。 如果你想要在你的方案中实现此模式，可以通过执行以下步骤操作即可：

1. 在中**设置**选项卡**发布 Web**向导中，输入具有完整的数据库架构更新权限，指定的用户的连接字符串，并清除**使用此连接字符串在运行时**复选框。 在已部署的 Web.config 文件中，这将成为`DatabasePublish`连接字符串。
2. 创建 Web.config 文件转换为你想要在运行时使用的应用程序的连接字符串。

## <a name="summary"></a>总结

现在已在开发计算机上部署到 IIS 应用程序，并对其进行存在测试。

![在测试中的主页](deploying-to-iis/_static/image23.png)

这将验证部署过程将应用程序的内容复制到正确的位置 （不包括不想部署的文件），并还该 Web 部署 IIS 正确配置在部署过程。 在下一步的教程中，你将运行一个测试，以发现尚未完成的部署任务： 上设置文件夹权限*Elmah*文件夹。

## <a name="more-information"></a>详细信息

在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：

- [IIS Express 概述](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)IIS.net 站点上。
- [引入了 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的博客上。
- [Web 服务器在 Visual Studio 中的，对 ASP.NET Web 项目](https://msdn.microsoft.com/library/58wxa9w5.aspx)。
- [核心区别之间 IIS 和 ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 站点上。

在中等信任环境中运行应用程序时，可能出现什么问题的信息，请参阅[承载 ASP.NET 应用程序在中等信任](http://www.4guysfromrolla.com/articles/100307-1.aspx)上 Rolla 站点中的 4 个专家。

> [!div class="step-by-step"]
> [上一页](project-properties.md)
> [下一页](setting-folder-permissions.md)
