---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署到生产环境-7 / 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: 26a832fd336f886ba1ddfb1682930afa4df56c58
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383631"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署到生产环境-7 / 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

在本教程中，将设置与宿主提供程序帐户和部署您的 ASP.NET web 应用程序到生产环境中使用 Visual Studio 一键式发布功能。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="selecting-a-hosting-provider"></a>选择托管提供商

对于 Contoso 大学应用程序和本系列教程，您需要 ASP.NET 4 和 Web 部署支持的提供程序。 特定的托管公司选择是为了让这些教程无法说明部署到实时网站的完整的体验。 每个托管公司提供不同的功能，并将部署到他们的服务器的体验上略有不同。 但是，在本教程中所述的过程是典型的整个过程。 用于本教程中，Cytanium.com，宿主提供程序是一个许多可用，并在本教程中的使用它不构成认可或推荐。

若要选择托管提供商准备就绪后，您可以比较功能和中的价格[提供程序库](https://www.microsoft.com/web/hosting)Microsoft.com/web 站点上。

## <a name="creating-an-account"></a>创建帐户

在你所选的提供程序上创建一个帐户。 如果支持完整的 SQL Server 数据库添加了额外，不需要为本教程中，选择它，但您将需要它[迁移到 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)本系列后面的教程。

对于这些教程，您无需注册一个新的域名。 您可以进行测试以使用提供程序分配给站点的临时 URL 来验证成功的部署。

创建帐户后，您通常收到欢迎电子邮件，其中包含为部署和管理你的网站所需的所有信息。 托管提供商向你发送的信息将类似于此处显示的内容。 将发送到新帐户所有者的 Cytanium 欢迎电子邮件包括以下信息：

- 提供程序的控件面板站点，您可以为您的网站管理设置的 URL。 在欢迎电子邮件，以方便参考的此部分包含 ID 和你指定的密码。 （同时具有已更改为下图演示值。）

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 默认.NET Framework 版本和有关如何对其进行更改的信息。 许多托管站点默认值为 2.0，适用于 ASP.NET 应用程序面向.NET Framework 2.0、 3.0 或 3.5。 但是 Contoso University 是.NET Framework 4 的应用程序，因此需要更改此设置。 （为 ASP.NET 4.5 应用程序将使用.NET 4.0 设置。）

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- 临时 URL 可用于访问你的网站。 在创建此帐户后，"contosouniversity.com"输入与现有域的名称。 因此临时 URL 是`http://contosouniversity.com.vserver01.cytanium.com`。

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- 若要了解如何设置数据库，并对其进行访问所需的连接字符串：

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- 有关工具和部署你的网站的设置的信息。 （从 Cytanium 电子邮件还提到 WebMatrix，此处省略了。）

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>设置.NET Framework 版本

Cytanium 欢迎电子邮件包含指向说明如何更改.NET Framework 的版本。 这些说明解释了，这可以通过 Cytanium 控制面板。 其他提供商拥有控件面板站点看起来相同，或者它们可能指示您要执行此操作以不同方式。

请转到控制面板 URL。 登录后你的用户名和密码，您将看到控制面板。

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

在中**承载空格**，将指针拖过 Web 图标，并选择**网站**菜单中。

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

在中**网站**框中，单击**contosouniversity.com** （在创建帐户时使用的站点名称）。

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

在中**的 Web 站点属性**框中，选择**扩展**选项卡。

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

更改从 ASP.NET **2.0 集成的管道**到**4.0 （集成管道）**，然后单击**更新**。

## <a name="publishing-to-the-hosting-provider"></a>发布到宿主提供程序

从宿主提供程序的欢迎电子邮件包括所有所需发布该项目的设置和您可以手动输入该信息到发布配置文件。 但将使用一种更简单和更少出错的方法来配置部署到提供程序： 你将下载 *.publishsettings*文件，并将其导入发布配置文件。

在浏览器中，转到 Cytanium 控制面板并选择**Web** ，然后选择**Web 站点。**

![选择网站的控制面板](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

选择**contosouniversity.com** web 站点。

![选择 contosouniversity.com 控制面板](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

选择**Web 发布**选项卡。

![控件面板 Web 发布选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

创建要用于 web 发布通过输入用户名和密码凭据。 您可以输入用于登录到控制面板上的相同凭据。 然后单击**启用**。

![控制面板创建发布凭据](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

单击**下载发布配置文件添加为此网站**。

![控件面板下载发布配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

当系统提示打开或保存该文件时，请将其保存。

![保存发布配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

在中**解决方案资源管理器**在 Visual Studio 中，右键单击 ContosoUniversity 项目，然后选择**发布**。 **发布 Web**上打开对话框**预览**选项卡具有**测试**选择，因为这是你使用的最后一个配置文件的配置文件。

选择**配置文件**选项卡，然后单击**导入**。

![发布 Web 向导导入按钮](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

在中**导入发布设置**对话框中，选择 *.publishsettings*文件，下载，然后单击**打开**。 向导将转到连接选项卡使用的所有字段填充。

![发布 Web 向导连接选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

.Publishsettings 文件会将该站点的计划内永久 URL 放在目标 URL 框中，但如果未尚未购买的域，将值替换为临时的 URL。 对于此示例中，URL 是 *[ http://contosouniversity.com.vserver01.cytanium.com ](http://contosouniversity.com.vserver01.cytanium.com)。* 此框的唯一用途是指定的 URL，浏览器将打开到自动后已成功部署后。 如果将其留空，唯一后果是在浏览器不会自动启动部署后。

单击**验证连接**以验证是否设置正确无误，并可以连接到服务器。 如上文所，绿色复选标记验证连接成功。

当你单击验证连接时，可能会看到**证书错误**对话框。 如果这样做，请验证服务器名称是你期望的内容。 如果是，则选择**Visual Studio 的将来会话保存此证书**然后单击**接受**。 （此错误表示宿主提供程序已选择以避免购买 SSL 证书部署到的 url 的费用。 如果想要通过使用有效的证书建立安全连接，请联系你托管提供商。）

![证书错误](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

单击 **“下一步”**。

在中**数据库**一部分**设置**选项卡上，输入相同的测试输入值，发布配置文件。 在下拉列表中，您会发现所需的连接字符串。

- 在连接字符串中的**SchoolContext，** 选择 `Data Source=|DataDirectory|School-Prod.sdf`
- 下**SchoolContext**，选择**应用 Code First 迁移**。
- 在连接字符串中的**DefaultConnection**，选择 `Data Source=|DataDirectory|aspnet-Prod.sdf`
- 下**DefaultConnection**，将保留**更新数据库**清除。

![发布 Web 向导设置选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

单击 **“下一步”**。

在中**预览版**选项卡上，单击**开始预览**以查看将复制的文件的列表。 请参阅上文时在本地计算机上部署到 IIS 的同一列表。

在发布之前，更改配置文件的名称，以便将应用你 Web.Production.config 转换文件。 选择**配置文件**选项卡，单击**管理配置文件**。

![发布 Web 向导管理配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

在中**编辑 Web 发布配置文件**对话框框中，选择生产配置文件，单击**重命名**，并将配置文件名称更改为生产环境。 然后单击**关闭**。

![Web 发布配置文件编辑对话框](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

单击“发布” 。

应用程序发布到宿主提供程序。 结果显示在**输出**窗口。

![部署后的输出窗口](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

在浏览器会自动打开指向中输入的 URL**目标 URL**框**连接**选项卡**发布 Web**向导。 你看到相同的主页上为 Visual Studio 中运行站点但现在没有"（测试）"或"（开发）"的标题栏中的环境指示器。 这表示环境指示器*Web.config*转换工作正常。

> [!NOTE]
> 如果你仍看到标题中的"（测试）"，删除*obj*文件夹从 ContosoUniversity 项目并重新部署。 在软件的预发布版本，以前应用的转换文件 (Web.Test.config) 可能会获得应用再次尽管你使用的生产配置文件。


[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

在运行将导致数据库访问的页面之前，请确保 Elmah 能够记录出现的任何错误。

## <a name="setting-folder-permissions-for-elmah"></a>Elmah 的设置文件夹权限

本系列教程以前一教程，您还记得，您必须确保应用程序在应用程序中 Elmah 存储错误日志文件的文件夹的写入权限。 当您部署到 IIS 本地计算机上时，手动设置这些权限。 在本部分中，将了解如何以在 Cytanium 设置权限。 （某些宿主提供程序，则可能无法为此，他们可能会提供一个或多个预定义的文件夹具有写权限。 在这种情况下你将需要修改应用程序以使用指定的文件夹。）

Cytanium 控制面板中，可以设置文件夹权限。 请转到该控件面板 URL 并选择**文件管理器**。

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

在中**文件管理器**框中，选择**contosouniversity.com** ，然后**wwwrooot**若要查看应用程序的根文件夹。 单击挂锁图标旁边**Elmah**。

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

在中**文件**/**文件夹权限**窗口中，选择**读取**并**编写**对应的复选框**contosouniversity.com**然后单击**设置的权限**。

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

请确保 Elmah 具有写入访问权限*Elmah*从而导致错误，然后显示 Elmah 错误报告的文件夹。 请求无效的 URL，如*Studentsxxx.aspx*。 正如之前一样，您看到*GenericErrorPage.aspx*页。 单击**注销**链接，然后再运行*Elmah.axd*。 您获得**日志中**首先，页验证*Web.config*转换已成功添加 Elmah 授权。 在你登录后，您将看到显示只是导致该错误的报表。

[![Elmah.axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>在生产环境中测试

运行**学生**页。 应用程序尝试访问 School 数据库第一次，这会触发代码优先迁移来创建数据库。 在该页面将显示一段时间延迟后，可看到没有任何学生。

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

运行**讲师**页以验证种子数据已成功在数据库中插入讲师数据。

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

与你在测试环境中，你想要验证数据库更新在生产环境中工作，但你通常不希望插入您的生产数据库输入测试数据。 对于本教程，将使用相同的方法在测试中一样。 但在实际的应用程序可能想要查找的方法，用于验证该数据库的更新，以成功而不会引入到生产数据库的测试数据。 在某些应用程序，可能会不切实际中添加了内容并将其删除。

添加一名学生，然后查看输入中的数据**学生**页后，可以验证是否可以更新数据库中的数据。

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

验证授权规则正常工作，可以通过选择**更新信用额度**从**课程**菜单。 **日志中**显示页。 输入你的管理员帐户凭据，请单击**日志中**，并**更新信用额度**显示页。

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

如果登录成功，**更新信用额度**显示页。 这表示已成功部署 ASP.NET 成员资格数据库 （使用单一的管理员帐户）。

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

你现在已成功部署和测试你的站点，它可公开通过 Internet。

## <a name="creating-a-more-reliable-test-environment"></a>创建更可靠的测试环境

中所述[部署到测试环境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程中，最可靠的测试环境是在只需像生产帐户托管提供商的第二个帐户。 这将是比作为测试环境中，使用本地 IIS，因为您将不得不注册第二个托管帐户开销更大。 但如果它会阻止生产站点错误或服务中断，可能会决定，因此有必要的成本。

用于创建和部署到测试帐户过程中的大部分是类似于什么已经设置部署到生产环境：

- 创建*Web.config*转换文件。
- 在托管提供商创建一个帐户。
- 创建新的发布配置文件并将部署到测试帐户。

### <a name="preventing-public-access-to-the-test-site"></a>测试站点中阻止公共访问权限

测试帐户的重要考虑事项是它将实时 Internet 上，但你不希望使用它的公共。 若要保持专用站点可以使用一个或多个以下方法：

- 请联系托管提供商设置仅允许访问到测试的站点将用于测试的 IP 地址的防火墙规则。
- 伪装 URL，以便它不是类似于公共站点的 URL。
- 使用*robots.txt*文件以确保，搜索引擎不会爬网测试站点和报表链接到它在搜索结果中。

第一种方法是显然最安全的但为此，该过程是特定于每个宿主提供程序并不将在本教程中介绍。 如果执行排列通过托管提供商以允许仅你的 IP 地址浏览到测试帐户 URL，您从理论上无需担心如何搜索引擎对其进行爬网。 但即使在这种情况下，部署*robots.txt*文件作为备份是一个好主意，以防意外关闭的防火墙规则。

*Robots.txt*文件出现在项目文件夹中，应在其中具有以下文本：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent`一行告诉文件中的规则适用于所有搜索引擎 web 爬网程序 （机器人） 的搜索引擎和`Disallow`行指定应在站点上的任何页已爬网。

您可能希望搜索引擎目录生产站点，因此您需要从生产部署中排除此文件。 若要执行此操作，请参阅**可以排除特定文件或文件夹从部署？** 中[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)。 请确保仅对生产发布配置文件指定排除。

创建第二个托管帐户是一种方法使用的测试环境不是必需的但可能需要额外的费用。 在以下教程中，您将继续为将 IIS 用作你的测试环境。

在下一步的教程中，将更新应用程序代码，并将所做的更改部署到测试和生产环境。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
