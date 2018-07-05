---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 创建生成定义支持部署 |Microsoft Docs
author: jrjlee
description: 如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，您需要创建你的团队项目中的生成定义。 此主题 des...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: d0220ee5c7c066d107311c1235949cec5049cc27
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370275"
---
<a name="creating-a-build-definition-that-supports-deployment"></a>创建生成定义支持部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，您需要创建你的团队项目中的生成定义。 本主题介绍如何在 TFS 中创建新的生成定义以及如何控制 web 部署作为 Team Build 中的生成过程的一部分。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

生成定义是控制如何以及何时在 TFS 中的团队项目进行生成的机制。 指定每个生成定义：

- 你想要生成 Visual Studio 解决方案文件或自定义 Microsoft Build Engine (MSBuild) 项目文件等操作。
- 确定何时生成应采取的条件放置，如手动触发器，持续集成 (CI) 或封闭签入。
- Team Build 应向其发送生成输出，其中包括像 web 包和数据库脚本的部署项目的位置。
- 应保留每个生成的时间量。
- 生成过程的各种其他参数。

> [!NOTE]
> 生成定义的详细信息，请参阅[定义在生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。


本主题将演示如何创建使用 CI，生成定义，以便开发人员签入新的内容时触发生成。 如果生成成功，生成服务在运行要将解决方案部署到测试环境的自定义项目文件。

当触发生成时，这些操作需要执行：

- 首先，Team Build 应生成解决方案。 作为此过程的一部分，Team Build 将调用 Web 发布管道 (WPP) 为每个解决方案中的 web 应用程序项目中生成 web 部署包。 Team Build 还将运行与解决方案关联的任何单元测试。
- 如果解决方案生成失败，Team Build 应采取任何进一步的操作。 应将单元测试失败视为生成失败。
- 如果解决方案生成成功，Team Build 应运行控制解决方案的部署的自定义项目文件。 作为此过程的一部分，Team Build 将调用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 在目标 web 服务器上安装打包的 web 应用程序，并且它会调用 VSDBCMD.exe 实用工具来运行数据库创建目标数据库服务器上的脚本。

这说明了该过程：

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案包括自定义 MSBuild 项目文件中， *Publish.proj*，可以从 MSBuild 或 Team Build 中运行。 如中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，此项目文件定义逻辑，用于将你的 web 包和数据库部署到目标环境。 该文件包含运行时将其在 Team Build，离开只需部署要运行的任务中省略的构建和打包过程的逻辑。 这是因为时自动执行这种方式中的部署，通常需要确保已成功生成解决方案并在部署过程开始之前，将传递任何单元测试。

下一部分介绍如何通过创建新的生成定义来实现此过程。

> [!NOTE]
> 此过程&#x2014;中一个自动执行过程会生成、 测试，并将解决方案部署&#x2014;很可能是最适合部署以供测试环境。 为过渡和生产环境，您更可能想要将内容从以前生成的已验证并验证在测试环境中部署。 这种方法下一主题中所述[部署特定生成](deploying-a-specific-build.md)。


### <a name="who-performs-this-procedure"></a>此过程的执行者是谁？

通常情况下，TFS 管理员执行此过程。 在某些情况下，开发人员团队负责人可能需要在 TFS 中的负责的团队项目集合。 若要创建新的生成定义，您需要的成员**项目集合生成管理员**组包含解决方案的团队项目集合。

## <a name="create-a-build-definition-for-ci-and-deployment"></a>创建 CI 和部署的生成定义

下一步的过程描述如何创建 CI 触发的生成定义。 如果生成成功，将解决方案部署的自定义 MSBuild 项目文件中使用的逻辑。

**若要创建的 CI 和部署的生成定义**

1. 在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目节点，右键单击**生成**，然后单击**新建生成定义**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. 上**常规**选项卡上，为生成定义指定一个名称 (例如， **DeployToTest**) 和可选描述。
3. 上**触发器**选项卡上，选择你想要触发新的生成的条件。 例如，如果你想要生成解决方案，每次一名开发人员签入新代码时，将部署到测试环境，选择**持续集成**。
4. 上**生成默认值**选项卡上，在**生成输出复制到以下放置文件夹**框中，键入 drop 文件夹的通用命名约定 (UNC) 路径 (例如，  **\\TFSBUILD\Drops**)。

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > 此放置位置存储多个生成，具体取决于你配置的保留策略。 当你想要发布到过渡或生产环境的部署项目从特定的生成时，这是您可以找到它们。
5. 上**进程**选项卡上，在**生成过程文件**下拉列表中，保留**DefaultTemplate.xaml**选定。 这是添加到所有新的团队项目的默认生成过程模板之一。
6. 在中**生成过程参数**表中，单击在**生成的项**行，然后依次**省略号**按钮。

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. 在中**生成的项**对话框中，单击**添加**。
8. 浏览到你的解决方案文件的位置，然后单击**确定**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. 在中**生成的项**对话框中，单击**添加**。
10. 在中**类型的项**下拉列表中选择**MSBuild 项目文件**。
11. 浏览到与其控件部署过程中，选择的文件，然后单击的自定义项目文件的位置**确定**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. **生成的项**对话框现在应显示两个项。 单击 **“确定”**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. 上**进程**选项卡上，在**生成过程参数**表中，展开**高级**部分。
14. 在中**MSBuild 参数**行中，添加任何 MSBuild 命令行自变量的*任一*项构建的需要。 在联系人管理器解决方案方案中，这些参数是必需的：

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. 在此示例中：

    1. **DeployOnBuild = true**并**DeployTarget = 包**时生成 Contact Manager 解决方案，是必需参数。 这会指示 MSBuild 创建 web 部署包后生成每个 web 应用程序项目，如中所述[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。
    2. **TargetEnvPropsFile**参数是必需的在生成时*Publish.proj*文件。 此属性指示的特定于环境的配置文件的位置，如中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。
16. 上**保留策略**选项卡上，配置想要根据需要保留每种类型的多少生成。
17. 单击“保存” 。

## <a name="queue-a-build"></a>将生成排入队列

此时，您已创建至少一个新的生成定义。 您定义的生成过程现在将根据你在生成定义中指定的触发器运行。

如果已配置生成定义，以使用 CI，可以通过两种方式来测试你的生成定义：

- 签入到团队项目，以触发自动生成的一些内容。
- 手动对生成进行排队。

**若要手动对生成进行排队**

1. 在中**团队资源管理器**窗口中，右键单击生成定义，然后单击**使新生成入队**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. 在中**使生成入队**对话框中，查看生成属性，然后单击**队列**。

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

若要查看进度和结果生成的&#x2014;而不考虑它是否触发手动或自动&#x2014;双击中的生成定义**团队资源管理器**窗口。 这将打开**生成资源管理器**选项卡。

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

在这里，可以排查生成失败。 如果您双击各个生成，可以查看摘要信息，并单击浏览详细的日志文件。

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

此信息可用于对生成失败进行故障排除和解决任何问题，然后再尝试另一个生成。

> [!NOTE]
> 执行部署逻辑生成很可能失败，直到已授予生成服务器中的目标环境所需的任何权限。 有关详细信息，请参阅[团队生成部署配置的权限](configuring-permissions-for-team-build-deployment.md)。


## <a name="monitor-the-build-process"></a>监视生成过程

TFS 提供范围广泛的功能来帮助你监视生成过程。 例如，TFS 可以向你发送一封电子邮件或在完成生成时在任务栏通知区域中显示警告。 有关详细信息，请参阅[运行并监视生成](https://msdn.microsoft.com/library/ms181721.aspx)。

## <a name="conclusion"></a>结束语

本主题介绍了如何在 TFS 中创建生成定义。 生成定义配置为使用 CI，因此，生成过程运行时开发人员签入到团队项目的内容。 生成定义执行自定义的 MSBuild 项目文件，以将 web 包和数据库脚本部署到目标服务器环境。

为了使自动部署成功完成生成过程的一部分，你将需要授予访问目标 web 服务器和目标数据库服务器上的生成服务帐户的适当权限。 在本教程的最后一个主题[团队生成部署配置的权限](configuring-permissions-for-team-build-deployment.md)，介绍如何标识和配置用于从 Team Build 服务器的自动部署所需的权限。

## <a name="further-reading"></a>其他阅读材料

创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)并[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。 生成排队的更多指导，请参阅[对生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。

> [!div class="step-by-step"]
> [上一页](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一页](deploying-a-specific-build.md)
