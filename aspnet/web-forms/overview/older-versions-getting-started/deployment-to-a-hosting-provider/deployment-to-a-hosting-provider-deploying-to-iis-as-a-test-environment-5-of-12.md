---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署到 IIS 作为测试环境-5 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 46d986aad52b0ab5a235eade2e17b0cf9f8cdb9f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835196"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 作为测试环境-5 12 部署到 IIS
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

本教程演示如何以 ASP.NET web 应用程序部署到 IIS 在本地计算机上。

开发的应用程序，您通常进行测试的 Visual Studio 中运行。 默认情况下，这意味着你正在使用 Visual Studio 开发服务器 (也称为 Cassini)。 Visual Studio 开发服务器可以轻松地在 Visual Studio 中，开发过程中测试，但它不能与 IIS 完全相同。 因此，就可以，当应用程序时对其进行测试在 Visual Studio 中，但失败到 IIS 部署在宿主环境中时，将正确运行。

你可以在以下方面更可靠地测试应用程序：

1. 使用 IIS Express 或完整 IIS 而不是 Visual Studio 开发服务器时在 Visual Studio 中测试在开发过程。 此方法通常会模拟更准确地说您的网站在 IIS 下运行的方式。 但是，此方法不测试您的部署过程或验证部署过程的结果将正常运行。
2. 通过使用相同的过程的更高版本将使用它来将其部署到生产环境部署到 IIS 在开发计算机上的应用程序。 此方法验证部署过程除了验证你的应用程序将在 IIS 下正确运行。
3. 应用程序部署到尽可能接近生产环境的测试环境。 由于这些教程在生产环境是第三方托管提供商，非常适合测试环境会为具有托管提供商的第二个帐户。 将此第二个帐户仅用于测试，但它会设置生产帐户一样。

本教程演示了选项 2 的步骤。 选项 3 指南提供的末尾[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中，并且在本教程末尾有指向资源的选项 1。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="configuring-the-application-to-run-in-medium-trust"></a>在中等信任中配置为运行应用程序

之前安装 IIS，并且部署到它，你将以便在站点运行更像它在典型的共享宿主环境中将会更改 Web.config 文件设置。

主机托管提供商通常在运行您的网站*中等信任*，这意味着它不允许执行某些功能。 例如，应用程序代码不能访问 Windows 注册表和无法读取或写入应用程序的文件夹层次结构之外的文件。 默认情况下你的应用程序运行*高信任*上本地计算机，这意味着应用程序可能能够执行操作时将其部署到生产环境会失败。 因此，若要使测试环境的详细信息能准确地反映生产环境，将配置要在中等信任中运行的应用程序。

在应用程序 Web.config 文件中添加**信任**中的元素**system.web**元素，在此示例中所示。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

甚至在本地计算机上，现在在 IIS 中的中等信任应用程序将运行。 此设置使你的应用程序代码来执行某些操作会导致生产失败来尽早发现任何尝试。

> [!NOTE]
> 如果使用的 Entity Framework Code First 迁移，请确保具有版本 5.0 或更高版本安装。 在实体框架版本 4.3，迁移以更新数据库架构需要完全信任。


## <a name="installing-iis-and-web-deploy"></a>安装 IIS 和 Web 部署

若要在开发计算机上部署到 IIS，必须具有 IIS 和 Web 部署安装。 此外，默认 Windows 7 配置中不会包含这些信息。 如果你安装了 IIS 和 Web 部署，请跳至下一节。

使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是首选的方法来安装 IIS 和 Web 部署，因为 Web 平台安装程序为 IIS 安装建议的配置，并且它会自动安装 IIS 和 Web 的先决条件如有必要部署。

若要运行 Web 平台安装程序来安装 IIS 和 Web 部署，请使用以下链接。 如果你已安装 IIS、 Web 部署或任何其所需的组件，Web 平台安装程序安装只缺少的内容。

- [安装 IIS 和 Web 部署使用 WebPI](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>将默认应用程序池设置为.NET 4

安装 IIS 后，运行**IIS 管理器**以确保.NET Framework 版本 4 分配给默认应用程序池。

从 Windows**启动**菜单中，选择**运行**，输入"inetmgr"，然后单击**确定**。 (如果**运行**命令不在你**启动**菜单中，可以按 Windows 键和 R，以将其打开。 或者右键单击任务栏中单击**属性**，选择**开始菜单**选项卡上，单击**自定义**，然后选择**运行命令**。)

在中**连接**窗格中，展开服务器节点，然后选择**应用程序池**。 在中**应用程序池**窗格中，如果**DefaultAppPool**是分配给.NET framework 版本 4 所示，跳到下一节。

[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

如果您看到只有两个应用程序池，并且这两个值设置为.NET Framework 2.0，您必须在 IIS 中安装 ASP.NET 4:

- 通过右键单击打开命令提示符窗口**命令提示符**在 Windows 中**启动**菜单并选择**以管理员身份运行**。 然后运行[aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中，使用以下命令安装 ASP.NET 4。 （在 64 位系统中，将为"框架"与"Framework64"）。

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP.NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    此命令将为.NET Framework 4 中，创建新的应用程序池，但仍将被默认应用程序池设置为 2.0。 您要部署应用程序面向.NET 4 到该应用程序池，因此您必须将应用程序池更改为.NET 4。

如果您关闭**IIS 管理器**再次运行中，展开服务器节点，单击**应用程序池**以显示**应用程序池**再次窗格。

在中**应用程序池**窗格中，单击**DefaultAppPool**，然后在**操作**窗格中，单击**基本设置**。

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

在中**编辑应用程序池**对话框中，更改 **.NET Framework 版本**到 **.NET Framework v4.0.30319**然后单击**确定**。

[![Selecting_.NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

现在您就可以将发布到 IIS。

## <a name="publishing-to-iis"></a>发布到 IIS

有几种方法可以部署使用 Visual Studio 2010 和 Web 部署：

- 使用一键式发布的 Visual Studio。
- 创建*部署包*和使用 IIS 管理器 UI 安装它。 部署包组成 *.zip*文件，其中包含所有文件和在 IIS 中安装站点所需的元数据。
- 创建部署包并将其使用命令行安装。

已在前面的教程，要将 Visual Studio 设置为自动执行部署任务适用于所有这三种方法的过程。 在这些教程将使用第一种方法。 有关使用部署包的信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。

发布前，请确保在管理员模式下运行 Visual Studio。 (在 Windows 7**启动**菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择**以管理员身份运行**。)管理员模式下是发布仅当您要发布到 IIS 在本地计算机上所必需的。

在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目 （而不是 ContosoUniversity.DAL 项目），然后选择**发布**。

**发布 Web**向导显示。

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

在下拉列表中，选择**&lt;新建...&gt;**.

在中**新的配置文件**对话框中，输入"Test"，然后单击**确定**。

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

此名称是与 Web.Test.config 中间节点相同转换先前创建的文件。 这种对应关系是哪些因素会导致 Web.Test.config 转换时使用此配置文件发布应用。

该向导将自动前进到**连接**选项卡。

在中**服务 URL**框中，输入*localhost*。

在中**站点/应用程序**框中，输入*默认 Web 站点/ContosoUniversity*。

在中**目标 URL**框中，输入`http://localhost/ContosoUniversity`。

**目标 URL**设置不需要。 完成 Visual Studio 部署应用程序后，它会自动打开默认浏览器访问此 URL。 如果不想要在部署后自动打开浏览器，将此框留空。

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

单击**验证连接**以验证是否设置正确无误，并可以在本地计算机上连接到 IIS。

绿色复选标记验证连接成功。

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

单击**下一步**转到**设置**选项卡。

**配置**下拉列表框指定要部署的生成配置。 默认值为版本中，这是你想。

将保留**删除目标处的其他文件**清除复选框。 由于这是你第一次部署，也不会有任何文件的目标文件夹中尚未。

在中**数据库**部分中，为连接字符串框中输入以下值**SchoolContext**:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

由于部署过程会将此连接字符串放在已部署的 Web.config 文件中**在运行时使用此连接字符串**处于选中状态。

此外，在**SchoolContext**，选择**应用 Code First 迁移**。 此选项将导致部署过程，配置已部署的 Web.config 文件，以指定`MigrateDatabaseToLatestVersion`初始值设定项。 此初始值设定项自动更新数据库的最新版本时该应用程序部署后首次访问数据库。

在连接字符串中的**DefaultConnection**，输入以下值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

将保留**更新数据库**清除。 将通过复制在应用中的.sdf 文件来部署成员资格数据库\_数据，而您不希望部署过程以执行任何其他与此数据库操作。

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

单击**下一步**转到**预览**选项卡。

在中**预览版**选项卡上，单击**开始预览**以查看将复制的文件的列表。

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

单击“发布” 。

如果 Visual Studio 不是在管理员模式下，可能会收到一个错误消息，指示权限错误。 在这种情况下，关闭 Visual Studio，在管理员模式下打开并尝试再次发布。

在管理员模式下，Visual Studio 是否**输出**窗口报告成功生成和发布。

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

在浏览器会自动打开指向本地计算机上在 IIS 中运行 Contoso University 主页上。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>在测试环境中测试

请注意，环境指示器，显示"（测试）"而不是"（开发）"，其中显示*Web.config*环境指示器的转换是否成功。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

运行**学生**页后，可以验证是否已部署的数据库具有任何学生。 选择此页时可能需要几分钟才能加载，因为 Code First 创建数据库并运行`Seed`方法。 （它没有这样做时，因为该应用程序不尝试尚未访问的数据库都在主页上。）

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

运行**讲师**页以验证，Code First 设定数据库种子的讲师数据：

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

选择**添加学生**从**学生**菜单中，添加一名学生，，然后查看中的新学生**学生**页以验证是否可以成功写入到数据库:

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

从**课程**菜单中，选择**更新信用额度**。 **更新信用额度**页面需要管理员权限，因此**Log In**显示页。 输入创建早期 （"admin"和"Pa$ w0rd"） 的管理员帐户凭据。 **更新信用额度**显示页面时，用于验证在上一教程中创建的管理员帐户已正确部署到测试环境。

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

确认*Elmah*文件夹是否存在与仅在它的占位符文件。

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>评审 Code First 迁移自动 Web.config 更改

打开*Web.config*文件中的已部署应用程序*C:\inetpub\wwwroot\ContosoUniversity* ，可以看到部署过程会自动配置 Code First 迁移到其中更新到最新版本的数据库。

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

部署过程还创建新的连接字符串的代码优先迁移来更新数据库架构的以独占方式使用：

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

通过此附加的连接字符串，您可以指定一个用户帐户对数据库架构更新，以及用于数据访问应用程序的不同用户帐户。 例如，您也可以将 db\_到 Code First 迁移和 db 所有者角色\_datareader 和 db\_datawriter 角色添加至应用程序。 这是一种常用的深度防御模式阻止潜在的恶意代码应用程序更改数据库架构。 （例如，可能发生此错误在成功的 SQL 注入式攻击。）这些教程不使用此模式。 它不适用于 SQL Server Compact，并在本系列后面的教程中迁移到 SQL Server 时不适用。 Cytanium 站点提供了一个访问在 Cytanium 创建的 SQL Server 数据库的用户帐户。 如果能够在你的方案中实现此模式，可以通过执行以下步骤操作即可：

1. 在中**设置**选项卡**发布 Web**向导中，输入具有完整的数据库架构更新权限，指定的用户的连接字符串，并清除**使用此连接字符串在运行时**复选框。 在已部署的 Web.config 文件中，这将成为`DatabasePublish`连接字符串。
2. 创建 Web.config 文件转换为你想要在运行时使用的应用程序的连接字符串。

现在已在开发计算机上部署到 IIS 应用程序，并对其进行存在测试。 这将验证部署过程将应用程序的内容复制到正确的位置 （不包括不想部署的文件），并还该 Web 部署 IIS 正确配置在部署过程。 在下一步的教程中，你将运行一个测试，以发现尚未完成的部署任务： 上设置文件夹权限*Elmah*文件夹。

## <a name="more-information"></a>详细信息

在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：

- [IIS Express 概述](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview)IIS.net 站点上。
- [引入了 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的博客上。
- [如何： 为 Visual Studio 中的 Web 项目指定 Web 服务器](https://msdn.microsoft.com/library/ms178108.aspx)。
- [核心区别之间 IIS 和 ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 站点上。
- [在 30 秒内测试你的 ASP.NET MVC 或 Web 窗体应用程序在 IIS 7](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) Rick Anderson 的博客上。 此条目提供为何使用 Visual Studio 开发服务器 (Cassini) 进行测试不是作为测试在 IIS Express 中，可靠和为什么测试在 IIS Express 中是不可靠作为测试在 IIS 中的示例。

在中等信任环境中运行应用程序时，可能出现什么问题的信息，请参阅[承载 ASP.NET 应用程序在中等信任](http://www.4guysfromrolla.com/articles/100307-1.aspx)上 Rolla 站点中的 4 个专家。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [下一页](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
