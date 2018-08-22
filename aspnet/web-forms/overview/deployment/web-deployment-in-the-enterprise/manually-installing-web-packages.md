---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手动安装 Web 程序包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何手动导入 web 部署包到 Internet 信息服务 (IIS)。 主题构建和打包 Web 应用程序...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: ca85db5cfb30bc06d6d3b94001a3668088461b87
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830673"
---
<a name="manually-installing-web-packages"></a>手动安装 Web 程序包
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何手动导入 web 部署包到 Internet 信息服务 (IIS)。
> 
> 本主题[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)所述 IIS Web 部署工具 （Web 部署），与 Microsoft Build Engine (MSBuild) 和 Web 发布管道 (WPP) 结合使用，可以如何打包应用web 应用程序项目转换单个 zip 文件。 此文件中，通常称为 web 部署包 （或只需部署包），包含需要 IIS，以便重新创建 web 应用程序的 web 服务器上的所有内容和配置信息。
> 
> 一旦你创建 web 部署包，可以将其发布到 IIS 服务器以各种方式。 在很多情况下，你将想要充分利用 MSBuild、 WPP，和 Web 部署可以创建和自动或单步执行生成和部署过程的一部分的远程安装 web 程序包之间的集成点。 此过程所述[部署 Web 包](deploying-web-packages.md)。 但是，这并不总是可行。 假设你想要部署 web 应用程序到面向 Internet 的生产环境。 出于安全原因，生产环境中此类是在非常最不可能是独立于生成服务器，在外围网络 （也称为 DMZ、 外围安全区域和外围子网） 中的子网防火墙后面。 在很多情况下，在生产环境将在单独的域或以物理方式隔离网络上。
> 
> 在这些情况下，唯一的选项可能是端口到目标服务器上的 web 包，并手动将其导入 IIS。 尽管这种方法可以阻止自动的部署，但它仍是一种 web 应用程序发布的高效方法&#x2014;只需将单个 zip 文件复制到你的 web 服务器并使用向导来引导您完成导入过程。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

## <a name="task-overview"></a>任务概述

你将需要完成以下高级任务，以导入 IIS web 部署包：

- 创建使用 MSBuild 命令行、 Team Build 或 Visual Studio 2010 web 部署包。
- 将 web 包复制到目标 web 服务器。
- 使用导入应用程序包向导在 IIS 管理器安装的 web 包并为变量，如连接字符串和服务终结点提供的值。

本主题将演示如何执行这些过程。 任务和本主题中的演练假定您已经熟悉 web 包、 Web 部署和 WPP 背后的概念。 有关详细信息，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

> [!NOTE]
> 本主题最适合使用结合[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)，其中解释了如何安装所需的组件，并为程序包导入准备的 IIS 网站。


## <a name="create-a-web-deployment-package"></a>创建 Web 部署包

第一个任务是创建你想要部署的 web 应用程序的 web 部署包。 可以在不同的方式来创建 web 包。

**方法 1： 使用 Visual Studio 创建生成过程的一部分的包**

您可以将 web 应用程序项目配置为通过每次生成后创建 web 部署包**打包/发布 Web**项目属性页上的选项卡。 此过程所述[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

**方法 2： 使用 MSBuild 创建生成过程的一部分的包**

如果您在 web 应用程序项目使用 MSBuild 生成直接通过自定义的 MSBuild 项目文件或从命令行中，您可以创建 web 部署包生成过程的一部分通过包括**DeployOnBuild = true**并**DeployTarget = 包**在命令中的属性。 此过程所述[了解构建过程](understanding-the-build-process.md)。

**方法 3： 在 Visual Studio 中按需创建包**

可以随时在 Visual Studio 2010 中创建 web 应用程序项目的 web 部署包。 若要执行此操作，在**解决方案资源管理器**窗口中，右键单击 web 应用程序项目，然后依次**生成部署包**。

![](manually-installing-web-packages/_static/image1.png)

**方法 4： 按需从命令行创建包**

可以从命令行创建 web 部署包，通过调用**包**上 web 应用程序项目使用 MSBuild 目标。 该命令应类似如下：


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


无论何种方法使用，最终结果相同。 WPP 为 zip 文件，以及各种支持资源，你的 web 应用程序项目的输出文件夹中创建 web 部署包。

![](manually-installing-web-packages/_static/image2.png)

您计划手动导入 web 包，即是要求只有 zip 文件。 将此文件复制到目标 web 服务器，可以开始导入过程。

## <a name="import-a-web-package-into-iis"></a>将 Web 包导入 IIS

下一步过程可用于从本地文件系统的 web 部署包导入 IIS 网站。 执行此过程之前，请确保您有：

- 复制到 web 服务器的 web 部署包。
- 配置 IIS web 服务器以承载应用程序。

有关配置 IIS web 服务器以支持 web 部署包的详细信息，请参阅[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。

**若要导入使用 IIS 管理器的 web 部署包**

1. 在 IIS 管理器中，在**连接**窗格中，右键单击你的 IIS 网站，依次指向**部署**，然后单击**导入应用程序**。

    ![](manually-installing-web-packages/_static/image3.png)
2. 在导入应用程序的包向导中，在**选择的包**页上，浏览到 web 部署包的位置，然后单击**下一步**。
3. 上**选择包的内容**页上，清除任何内容，您不需要，然后单击**下一步**。

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 在许多情况下，您可能不想要导入的所有操作与 web 部署包。 例如，可能不想要允许 Web 部署可以替换为关联的数据库。  
    > **授予的权限**条目设置目标文件系统，以确保应用程序池标识可以访问存储网站内容的物理文件夹的权限。 此外，匿名身份验证用户授予读取到的文件夹的权限允许应用程序提供多用途 Internet 邮件扩展 (MIME) 类型的文件。 如果您愿意，可以删除这些条目，并手动配置的权限。
4. 上**输入应用程序包信息**页上，提供所需的信息。

    ![](manually-installing-web-packages/_static/image5.png)
5. 当创建 web 包时，WPP 分析你的应用程序的配置文件，并检测任何变量，如连接字符串和服务终结点。 这种情况下：

    1. **应用程序路径**是你想要安装应用程序的 IIS 路径。 此设置是通用的 WPP 创建的所有部署包。
    2. **ContactService 服务终结点地址**是应用程序应使用与已部署的 WCF 服务进行通信的地址。 此设置对应于中的条目*web.config*文件。
    3. 第一个**连接字符串**设置是 Web 部署应使用来部署应用程序 （在这种情况下 ASP.NET 成员资格数据库中） 与关联的数据库的连接字符串。 此设置对应于上的设置**打包/发布 SQL** Visual Studio 中的选项卡。
    4. 第二个**连接字符串**设置是你的应用程序实际上将用于启动和运行时与数据库通信的连接字符串。 这对应于在一个连接字符串条目*web.config*文件。

        > [!NOTE]
        > 有关这些参数是从哪里来的详细信息，请参阅[为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)。
6. 单击 **“下一步”**。
7. 如果这不是已部署到此网站的应用程序第一次，将提示您指定是否要删除在安装之前的所有现有内容。 选择适合于您的需求，然后依次**下一步**。

    ![](manually-installing-web-packages/_static/image6.png)
8. 完成 IIS 已安装的包，请单击**完成**。

    ![](manually-installing-web-packages/_static/image7.png)

此时，已成功发布到 IIS web 应用程序。

## <a name="conclusion"></a>结束语

本主题介绍了如何将 web 部署包导入为使用 IIS 管理器中的 IIS 网站。 安全或基础结构限制使得远程部署，不可能或不需要时相应 web 应用程序发布到这种方法。

## <a name="further-reading"></a>其他阅读材料

有关如何配置 IIS web 服务器以支持手动导入 web 包的指南，请参阅[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 有关部署 web 包的更多常规指南，请参阅[演练： 部署 Web 应用程序项目使用 Web 部署包 (第 1 部分，共 4 部分)](https://msdn.microsoft.com/library/dd483479.aspx)。

> [!div class="step-by-step"]
> [上一篇](creating-and-running-a-deployment-command-file.md)
