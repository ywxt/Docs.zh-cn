---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署到生产 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: a91feedb9ac09b2a70ca256c72d312a1e78ecbc8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827872"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>使用 Visual Studio 的 ASP.NET Web 部署： 部署到生产
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

在本教程中，设置 Microsoft Azure 帐户、 创建过渡和生产环境和部署 ASP.NET web 应用程序到过渡环境和生产环境通过使用 Visual Studio 一键式发布功能。

如果您愿意，您可以将其部署到第三方托管提供商。 在本教程中所述的过程的大部分都是相同的宿主提供程序或适用于 Azure，只不过每个提供程序有其自己的帐户和 web 站点管理的用户界面。 您可以找到在托管提供商[库的提供程序](https://www.microsoft.com/web/hosting)Microsoft.com 网站上。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查本系列教程中的故障排除页。

## <a name="get-a-microsoft-azure-account"></a>获取 Microsoft Azure 帐户

如果还没有 Azure 帐户，可以只需几分钟内创建一个免费试用帐户。 有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。

## <a name="create-a-staging-environment"></a>创建过渡环境

> [!NOTE]
> 由于在撰写本教程时，Azure 应用服务将添加用于自动执行多个用于创建过渡和生产环境的进程的新功能。 请参阅[设置过渡环境中 Azure 应用服务 web 应用的](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。


中所述[部署到测试环境教程](deploying-to-iis.md)、 最可靠的测试环境是在只需像生产网站上的托管提供商的网站。 在许多主机托管提供商，您将不得不权衡与大量其他成本的优势，但在 Azure 中，您可以创建其他免费的 web 应用作为过渡应用。 您还需要一个数据库，并为此，通过创建生产数据库的费用的额外费用将为无或最小。 所使用的数据库存储量，而不是为每个数据库，在 Azure 中需要付费，你将在过渡环境中使用的额外存储量将是最小。

中所述[部署到测试环境教程](deploying-to-iis.md)、 过渡和生产环境并打算将两个数据库部署到一个数据库中。 如果你想要将它们分开，过程将相同只不过将创建用于每个环境的其他数据库，并且在创建发布配置文件时，将选择每个数据库的正确的目标字符串。

在本教程的本部分将创建 web 应用和数据库要用于过渡环境中，并将部署到过渡环境和在创建和部署到生产环境之前存在测试。

> [!NOTE]
> 以下步骤说明如何使用 Azure 管理门户在 Azure 应用服务中创建 web 应用。 在 Azure SDK 的最新版本，您还可以执行这无需离开 Visual Studio 中，通过使用服务器资源管理器。 在 Visual Studio 2013 中，还可以直接从发布对话框中创建 web 应用。 有关详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)


1. 在中[Azure 管理门户](https://manage.windowsazure.com/)，单击**网站**，然后单击**新建**。
2. 单击**网站**，然后单击**自定义创建**。

    **新建网站-自定义创建**向导随即打开。 **自定义创建**向导，可在同一时间创建网站和数据库。
3. 在中**创建网站**步骤的向导中，输入中的字符串**URL**框，以用作你的应用程序的唯一 URL 的过渡环境。 例如，输入 ContosoUniversity staging123 （包括末尾的随机数字，使其成为唯一执行 ContosoUniversity 过渡的情况下）。

    完整的 URL 将包含的在此处输入和文本框旁边看到的后缀。
4. 在中**区域**下拉列表中，选择离你最近的区域。

    此设置指定你的 web 应用将运行在哪个数据中心。
5. 在中**数据库**下拉列表中，选择**创建新的 SQL 数据库**。
6. 在中**数据库连接字符串名称**框中，保留默认值为*DefaultConnection*。
7. 单击向右框底部的箭头。

    如下图所示**创建网站**对话框，其中包含在其中的示例值。 将不同的 URL 和您输入的区域。

    ![创建网站的步骤](deploying-to-production/_static/image1.png)

    该向导将前进到**指定数据库设置**步骤。
8. 在中**名称**框中，输入*ContosoUniversity*加上随机的编号，以使之成为唯一的例如*ContosoUniversity123*。
9. 在中**服务器**框中，选择**新建 SQL 数据库服务器**。
10. 输入管理员名称和密码。

    不要输入现有名称和密码在此处。 应输入新名称和你现在定义，以后访问数据库时使用的密码。
11. 在中**区域**框中，选择你为 web 应用选择的同一区域。

    将 web 服务器和数据库服务器放置在同一个区域提供最佳性能，并尽量减少费用。
12. 单击底部的框以指示你已完成的复选标记。

    如下图所示**指定数据库设置**对话框，其中包含在其中的示例值。 你输入的值可能不同。

    ![数据库设置步骤使用数据库向导创建的新网站-](deploying-to-production/_static/image2.png)

    管理门户返回到网站页面，并**状态**列显示正在创建 web 应用。 （通常不到一分钟），一段时间后**状态**列显示已成功创建 web 应用。 在左侧的导航栏中的 web 应用帐户中有数会显示下一步**网站**旁边显示图标，而数据库数量**SQL 数据库**图标。

    ![管理门户中，创建网站的网站页面](deploying-to-production/_static/image3.png)

    Web 应用名称将不同于在图中的示例应用。

## <a name="deploy-the-application-to-staging"></a>部署到过渡环境的应用程序

现在，已创建 web 应用和过渡环境的数据库，可以将项目部署到它。

> [!NOTE]
> 这些说明介绍了如何通过下载来创建发布配置文件 *.publishsettings*文件，它仅适用于不 Azure 还为第三方主机托管提供商。 最新 Azure SDK 还可直接连接到 Azure 从 Visual Studio 中，并从你有在 Azure 帐户中的 web 应用的列表中选择。 在 Visual Studio 2013 中，你可以登录到 Azure 从**Web 发布**对话框中或从**服务器资源管理器**窗口。 有关详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。


### <a name="download-the-publishsettings-file"></a>下载.publishsettings 文件

1. 单击刚刚创建的 web 应用的名称。

    ![单击要转到仪表板的站点](deploying-to-production/_static/image4.png)
2. 下**速览**中**仪表板**选项卡上，单击**下载发布配置文件**。

    ![下载发布配置文件链接](deploying-to-production/_static/image5.png)

    此步骤下载包含所有将部署到 web 应用的应用程序所需的设置的文件。 这样就不必手动输入此信息，将导入 Visual Studio 的此文件。
3. 保存 *.publishsettings*可以从 Visual Studio 访问的文件夹中的文件。

    ![保存.publishsettings 文件](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 安全性- *.publishsettings*文件包含用于管理你的 Azure 订阅和服务的凭据 （未编码）。 此文件的安全最佳做法是将其暂时存储 （例如在 Libraries\Documents 文件夹中），在源目录的外部，然后完成导入后删除它。 恶意用户获得访问权 *.publishsettings*文件可以编辑、 创建和删除 Azure 服务。

### <a name="create-a-publish-profile"></a>创建发布配置文件

1. 在 Visual Studio 中，右键单击中的 ContosoUniversity 项目**解决方案资源管理器**，然后选择**发布**从上下文菜单。

    **发布 Web**向导随即打开。
2. 单击**配置文件**选项卡。
3. 单击“导入” 。
4. 导航到 *.publishsettings*你之前已下载文件，然后单击**打开**。

    ![导入发布设置对话框](deploying-to-production/_static/image7.png)
5. 在中**连接**选项卡上，单击**验证连接**以确保设置正确无误。

    当已验证的连接时，旁边会出现一个绿色复选标记**验证连接**按钮。

    对于某些宿主提供程序，当您单击时**验证连接**，你可能会看到**证书错误**对话框。 如果这样做，请验证服务器名称是你期望的内容。 如果服务器名称正确无误，请选择**Visual Studio 的将来会话保存此证书**然后单击**接受**。 （此错误表示宿主提供程序已选择以避免购买 SSL 证书部署到的 url 的费用。 如果想要通过使用有效的证书建立安全连接，请联系你托管提供商。）
6. 单击 **“下一步”**。

    ![连接成功图标和连接选项卡中的下一步按钮](deploying-to-production/_static/image8.png)
7. 在中**设置**选项卡上，展开**文件发布选项**，然后选择**将应用程序中排除文件\_Data 文件夹**。

    有关下的其他选项的信息**文件发布选项**，请参阅[部署到 IIS](deploying-to-iis.md)教程。 屏幕截图数据库配置步骤结束时的此步骤和以下数据库配置步骤的结果是该显示。
8. 下**DefaultConnection**中**数据库**部分中，配置成员资格数据库的数据库部署。
9. 1. 选择**更新数据库**。

        **远程连接字符串**框下方**DefaultConnection**使用.publishsettings 文件中的连接字符串填充。连接字符串包含存储在以纯文本中的 SQL Server 凭据 *.pubxml*文件。 如果不想将它们永久存在存储，可以部署数据库后，则会删除其从发布配置文件，并将其存储在 Azure 中。 有关详细信息，请参阅[如何保护您的 ASP.NET 数据库连接字符串从源部署到 Azure 时](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx)Scott Hanselman 的博客上。
      2. 单击**配置数据库更新**。
      3. 在中**配置数据库更新**对话框中，单击**添加 SQL 脚本**。
      4. 在中**添加 SQL 脚本**框中，导航到*aspnet 数据 prod.sql*脚本，您之前保存在解决方案文件夹，然后单击**打开**。
      5. 关闭**配置数据库更新**对话框。
10. 下**SchoolContext**中**数据库**部分中，选择**执行 Code First 迁移 （应用程序启动时运行）**。

    Visual Studio 将显示**执行 Code First 迁移**而不是**更新数据库**为`DbContext`类。 如果你想要使用 dbDacFx 提供程序而不是迁移部署使用访问数据库`DbContext`类，请参阅[如何将 Code First 数据库而无需迁移的部署？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)在 Visual Studio Web 部署常见问题和 MSDN 上的 ASP.NET。

    **设置**选项卡现在看起来如下例所示：

    ![过渡环境的设置选项卡](deploying-to-production/_static/image9.png)
11. 执行以下步骤以保存配置文件并对其重命名*过渡*:

    1. 单击**配置文件**选项卡，然后依次**管理配置文件**。
    2. 导入创建两个新配置文件，一个用于 FTP，一个用于 Web 部署。 配置 Web 部署配置文件： 重命名为此配置文件*过渡*。

        ![重命名到过渡环境的配置文件](deploying-to-production/_static/image10.png)
    3. 关闭**编辑 Web 发布配置文件**对话框。
    4. 关闭**发布 Web**向导。

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>配置发布配置文件转换为环境的指示符

> [!NOTE]
> 本部分演示如何设置 Web.config 转换为环境的指示符。 因为指示器位于`<appSettings>`元素，必须在部署到 Azure 应用服务时指定该转换的另一种方法。 有关详细信息，请参阅[在 Azure 中的指定 Web.config 设置](web-config-transformations.md#watransforms)。


1. 在中**解决方案资源管理器**，展开**属性**，然后展开**PublishProfiles**。
2. 右键单击*Staging.pubxml*，然后单击**添加配置转换**。

    ![用于临时添加配置转换](deploying-to-production/_static/image11.png)

    Visual Studio 将创建*Web.Staging.config*转换文件并将其打开。
3. 在中*Web.Staging.config*转换文件中，打开后立即插入以下代码`configuration`标记。

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    当使用过渡发布配置文件时，此转换将设置为"Prod"环境指示器。 在已部署的 web 应用中，不会在"Contoso University"H1 标题后看到任何后缀，例如"（开发）"（测试）"。
4. 右键单击*Web.Staging.config*文件，并单击**预览版转换**以确保您编码的转换生成预期的更改。

    **Web.config 预览版**窗口中显示结果应用同时*Web.Release.config*转换并*Web.Staging.config*转换。

### <a name="prevent-public-use-of-the-test-app"></a>防止公共使用的测试应用

过渡应用的重要考虑事项是它将实时 Internet 上，但你不希望使用它的公共。 若要最大程度减少人将查找并使用它的可能性，可以使用一个或多个以下方法：

- 设置访问过渡应用仅允许使用来测试暂存的 IP 地址的防火墙规则。
- 使用不可能猜到的经过模糊处理的 URL。
- 创建*robots.txt*文件以确保，搜索引擎不会爬网测试应用程序和报表链接到它在搜索结果中。

第一种方法是最有效的但因为它可能要求你将部署到 Azure 云服务而不是 Azure 应用服务未涵盖在本教程中。 有关云服务的详细信息和在 Azure 中的 IP 限制，请参阅[计算托管选项提供的 Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)并[阻止特定 IP 地址访问 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。 如果要部署到第三方托管提供商，请联系提供商联系以了解如何实现 IP 限制。

对于本教程中，将创建*robots.txt*文件。

1. 在中**解决方案资源管理器**，右键单击 ContosoUniversity 项目，然后单击**添加新项**。
2. 创建一个新**文本文件**名为*robots.txt*，并将它置于以下文本：

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent`一行告诉文件中的规则适用于所有搜索引擎 web 爬网程序 （机器人） 的搜索引擎和`Disallow`行指定应在站点上的任何页已爬网。

    您希望搜索引擎目录生产应用，因此您需要从生产部署中排除此文件。 若要执行操作，你将配置在生产环境中的设置发布配置文件时创建它。

### <a name="deploy-to-staging"></a>部署到过渡环境

1. 打开**发布 Web**右键单击 Contoso University 项目并单击向导**发布**。
2. 请确保**过渡**选择配置文件。
3. 单击“发布” 。

    **输出**窗口将显示已执行的部署操作并报告成功完成部署。 默认浏览器会自动打开指向已部署的 web 应用的 URL。

## <a name="test-in-the-staging-environment"></a>在过渡环境中测试

请注意，该环境标记是不存在 (没有"（测试）"或"（开发）"H1 标题，显示后*Web.config*环境指示器的转换是否成功。

![主页上的过渡环境](deploying-to-production/_static/image12.png)

运行**学生**页后，可以验证是否已部署的数据库具有任何学生。

运行**讲师**页以验证，Code First 设定数据库种子的讲师数据：

选择**添加学生**从**学生**菜单中，添加一名学生，，然后查看中的新学生**学生**页以验证是否可以成功写入到数据库.

从**课程**页上，单击**更新信用额度**。 **更新信用额度**页面需要管理员权限，因此**Log In**显示页。 输入创建早期 （"admin"和"prodpwd"） 的管理员帐户凭据。 **更新信用额度**显示页面时，用于验证在上一教程中创建的管理员帐户已正确部署到测试环境。

请求了无效的 URL 以产生错误 ELMAH 将跟踪，然后请求 ELMAH 错误报告。 如果要部署到第三方托管提供商，您可能会发现报表同样为空上一教程中为空。 必须使用托管提供商的帐户管理工具来配置启用 ELMAH 要写入的日志文件夹的文件夹权限。

现在就像将用于生产的 web 应用中在云中运行您创建的应用程序。 由于一切正常运行下, 一步是部署到生产环境。

## <a name="deploy-to-production"></a>部署到生产环境

创建生产 web 应用和部署到生产环境的过程与过渡环境，相同，只不过需要排除*robots.txt*从部署。 若要执行此操作将编辑发布配置文件。

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>创建生产环境和生产发布配置文件

1. 在 Azure 中，用于过渡的相同过程创建的生产 web 应用和数据库。

    创建数据库时，可以选择将其放在同一台服务器之前，创建或创建新的服务器。
2. 下载 *.publishsettings*文件。
3. 通过导入生产环境创建发布配置文件 *.publishsettings*文件，用于过渡的相同过程。

    别忘了配置数据部署脚本下的**DefaultConnection**中**数据库**一部分**设置**选项卡。
4. 重命名为发布配置文件*生产*。
5. 配置发布配置文件转换为环境的指示符，用于过渡的相同过程...

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>编辑要排除 robots.txt 的.pubxml 文件

发布配置文件的文件命名&lt;profilename&gt;*.pubxml*并位于*PublishProfiles*文件夹。 *PublishProfiles*文件夹位于*属性*文件夹中的 C# web 应用程序项目，在*我的项目*在 VB web 应用程序项目中，或在文件夹*应用程序\_数据*文件夹中的 web 应用程序项目。 每个 *.pubxml*文件包含应用于一个设置发布配置文件。 在发布 Web 向导中输入的值存储在这些文件，并可以编辑它们以便创建或更改不会在 Visual Studio UI 中提供的设置。

默认情况下 *.pubxml*文件包含在项目中创建发布配置文件，但您可以从项目中排除它们和 Visual Studio 仍将使用它们时。 Visual Studio 查找*PublishProfiles*文件夹 *.pubxml*文件，而不管这些数据是否包括在项目中。

每个 *.pubxml*文件有 *.pubxml 用户*文件。 *.Pubxml 用户*文件包含加密的密码，如果选择了**保存密码**选项，并且默认情况下会从项目中排除。

一个 *.pubxml*文件包含与特定的发布配置文件相关的设置。 如果你想要配置应用于所有配置文件的设置，则可以创建 *。 wpp.targets*文件。 生成过程将导入到这些文件 *.csproj*或 *.vbproj*项目文件中，因此可以在这些文件中配置大多数设置都可以在项目文件中配置。 有关详细信息 *.pubxml*文件并 *。 wpp.targets*文件，请参阅[如何： 编辑发布配置文件 (.pubxml) 文件中的部署设置和。 wpp.targets Visual Studio 中的文件Web 项目](https://msdn.microsoft.com/library/ff398069.aspx)。

1. 在中**解决方案资源管理器**，展开**属性**展开**PublishProfiles**。
2. 右键单击*Production.pubxml*然后单击**打开**。

    ![打开.pubxml 文件](deploying-to-production/_static/image13.png)
3. 右键单击*Production.pubxml*然后单击**打开**。
4. 添加以下行之前结束`PropertyGroup`元素：

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    .Pubxml 文件现在看起来如下例所示：

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    有关如何排除文件和文件夹的详细信息，请参阅[可以排除特定文件或文件夹从部署？](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)中**Visual Studio 和 ASP.NET 的 Web 部署常见问题解答**MSDN 上。

### <a name="deploy-to-production"></a>部署到生产环境

1. 打开**发布 Web**向导，确保**生产**发布配置文件已选择，然后单击**开始预览**上**预览**选项卡，确认*robots.txt*文件不会复制到生产应用。

    ![文件发布到生产环境的预览](deploying-to-production/_static/image14.png)

    查看将复制的文件的列表。 您会发现其中的所有 *.cs*文件，其中包括 *。 aspx.cs*， *。 aspx.designer.cs*， *Master.cs*，和*Master.designer.cs*省略文件。 所有这些代码已编译到*ContosoUniversity.dll*并*ContosUniversity.pdb*您会发现中的文件*bin*文件夹。 因为仅 *.dll*需要向运行该应用程序，以及你前面指定应部署仅运行该应用程序所需的文件，则不 *.cs*文件已复制到目标环境。 *Obj*文件夹并*ContosoUniversity.csproj*并 *。 csproj.user*文件省略出于同样的原因。

    单击**发布**将部署到生产环境。
2. 在生产环境，用于过渡的相同过程中进行测试。

    所有内容都是相同 URL 除外的过渡环境和缺少*robots.txt*文件。

## <a name="summary"></a>总结

你现在已成功部署和测试你的 web 应用，它可公开通过 Internet。

![主页生产](deploying-to-production/_static/image15.png)

在下一步的教程中，将更新应用程序代码，将更改部署到测试、 过渡和生产环境。

> [!NOTE]
> 在生产环境中使用你的应用程序时您应实现的恢复计划。 即，应该定期备份的数据库从生产应用到一个安全存储位置，并应保留多个代的此类备份。 更新数据库时，应进行更改之前立即从备份副本。 然后，如果您有误并部署到生产环境后不发现它之前，您将仍将能够将数据库恢复到其损坏之前的状态。 有关详细信息，请参阅[Azure SQL 数据库备份和还原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。
> 
> 
> [!NOTE]
> 在本教程中 SQL Server 要部署到的版本是 Azure SQL 数据库。 类似于其他版本的 SQL Server 部署过程时，实际的生产应用程序可能在某些情况下为 Azure SQL 数据库需要特殊的代码。 有关详细信息，请参阅[使用 Azure SQL 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)并[SQL Server 和 Azure SQL 数据库之间进行选择](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。
> 
> [!div class="step-by-step"]
> [上一页](setting-folder-permissions.md)
> [下一页](deploying-a-code-update.md)
