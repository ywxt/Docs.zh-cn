---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 设置 Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何下载和配置 Contact Manager 解决方案开发人员工作站上本地运行。
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 479dbb8d2edbe9fb953ea9e1312ffb8fdbd3e2fe
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802126"
---
<a name="setting-up-the-contact-manager-solution"></a>设置 Contact Manager 解决方案
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何下载和配置 Contact Manager 解决方案开发人员工作站上本地运行。


## <a name="system-requirements"></a>系统要求

若要在本地运行 Contact Manager 解决方案并执行其他任务在本教程中所述，你将需要开发人员工作站上安装此软件：

- Visual Studio 2010 Service Pack 1、 Premium 或 Ultimate Edition
- Internet 信息服务 (IIS) 7.5 Express
- SQL Server Express 2008 R2
- IIS Web 部署工具 （Web 部署） 2.1 或更高版本
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

除了 Visual Studio 2010 中，您可以下载并安装最新版本的所有这些产品和组件[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。

## <a name="download-and-extract-the-solution"></a>下载并提取解决方案

您可以从 MSDN 代码库下载联系人管理器示例应用程序[此处](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)。

## <a name="configure-and-run-the-solution"></a>配置和运行解决方案

若要配置并在本地计算机上运行 Contact Manager 解决方案，你将需要执行以下高级步骤：

1. 如果你还没有，请使用启用的成员资格和角色管理功能创建本地 ASP.NET 应用程序服务数据库。
2. 编辑中的连接字符串*web.config*文件以指向本地 SQL Server Express 实例。
3. 从 Visual Studio 2010 运行解决方案。

本部分的其余部分提供有关如何完成这些任务的更多指导。

**若要创建应用程序服务数据库**

1. 打开 Visual Studio 2010 命令提示符。 为此，请在**启动**菜单，依次指向**所有程序**，单击**Microsoft Visual Studio 2010**，单击**Visual Studio Tools**，，然后单击**Visual Studio 命令提示符 (2010)**。
2. 在命令提示符下，键入以下命令，并按 Enter:

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. 使用 **– C**开关来指定你的数据库服务器的连接字符串。
    2. 使用 **– A**开关来指定应用程序服务想要向数据库添加的功能。 在这种情况下， **m**指示你想要添加的成员资格提供程序支持并**r**指示你想要添加对角色管理器的支持。
    3. 使用 **– d**开关来指定你的应用程序服务数据库的名称。 如果省略此开关，该实用工具将使用的默认名称创建数据库**aspnetdb**。
3. 已成功创建数据库，命令提示符会显示一条确认消息。

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> 有关详细信息 aspnet\_regsql 实用程序，请参阅[ASP.NET SQL Server 注册工具 (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。


下一步是确保 Contact Manager 解决方案中的连接字符串指向 SQL Server Express 的本地实例。

**若要更新连接字符串**

1. 在 Visual Studio 2010 中打开 Contact Manager 解决方案。
2. 在中**解决方案资源管理器**窗口中，展开**ContactManager.Mvc**项目，然后再双击**Web.config**节点。

    > [!NOTE]
    > ContactManager.Mvc 项目包含两个*web.config*文件。 您需要编辑项目级文件。

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. 在中**connectionStrings**元素中，验证连接字符串指定**ApplicationServices**指向您的本地 ASP.NET 应用程序服务数据库。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. 在中**解决方案资源管理器**窗口中，展开**ContactManager.Service**项目，然后再双击**Web.config**节点。

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. 在**connectionStrings**元素，在名为的连接字符串**ContactManagerContext**，验证**数据源**属性设置为本地的 SQL 实例Server Express。 不需要更改连接字符串中的其他部分。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. 保存所有打开的文件。

现在，应准备好在本地计算机上运行 Contact Manager 解决方案。

> [!NOTE]
> 如果按照这些步骤操作无需首先创建应用程序服务数据库，ASP.NET 将尝试创建一个用户首次创建数据库。 但是，手动创建数据库用户可更多地掌控你想要支持的应用程序服务功能集。


**若要运行 Contact Manager 解决方案**

1. 在 Visual Studio 2010 中，按 F5。
2. Internet Explorer 启动，并请求联系人管理器 ASP.NET MVC 3 应用程序的 URL。 默认情况下，应用程序将显示**所有联系人**页。

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. 添加几个联系人，并验证该应用程序按预期方式工作。

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. 浏览到`http://localhost:50114/Account/Register`（如果您正在托管不同的端口上的应用程序，则调整 URL）。 添加用户名、 电子邮件地址和密码，并验证您能够成功注册一个帐户。

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. 浏览到`http://localhost:50114/Account/LogOn`（如果您正在托管不同的端口上的应用程序，则调整 URL）。 验证您可以使用刚刚创建的帐户登录。

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. 关闭 Internet Explorer 以停止调试。

## <a name="conclusion"></a>结束语

此时，应完全配置 Contact Manager 解决方案为在本地计算机上运行。 在本教程中处理通过其他主题时，可以使用该解决方案作为参考。

下一主题[了解项目文件](understanding-the-project-file.md)，介绍了如何使用 Contact Manager 解决方案中的自定义 Microsoft Build Engine (MSBuild) 项目文件来控制部署过程。

> [!div class="step-by-step"]
> [上一页](the-contact-manager-solution.md)
> [下一页](understanding-the-project-file.md)
