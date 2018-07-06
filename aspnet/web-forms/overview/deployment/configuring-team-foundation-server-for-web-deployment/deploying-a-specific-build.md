---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定生成 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何部署 web 包和数据库脚本从特定的上一个生成到新的目标，如过渡或生产环境的流程图...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 312cd6f42463722b76996a3a848102946e0ca265
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832463"
---
<a name="deploying-a-specific-build"></a>部署特定生成
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何部署 web 包和数据库脚本从特定的上一个生成到新的目标，如过渡或生产环境。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

到目前为止，本教程系列中的主题有侧重于如何构建、 打包和部署 web 应用程序和数据库的单步执行一部分或过程自动化。 但是，在某些常见的情况下，你将想要从生成中的放置文件夹的列表中选择了你部署的资源。 换而言之，最新版本可能不是你想要部署的生成。

请考虑在前一个主题中所述的持续集成 (CI) 场景[创建生成定义，支持部署](creating-a-build-definition-that-supports-deployment.md)。 你已在 Team Foundation Server (TFS) 2010年创建生成定义。 每次一名开发人员将代码签入 TFS，Team Build 将生成代码、 创建 web 包和数据库脚本作为生成过程的一部分，运行任何单元测试，并将资源部署到测试环境。 具体取决于在创建生成定义时配置的保留策略，TFS 将保留一定数量的上一生成。

![](deploying-a-specific-build/_static/image1.png)

现在，假设您执行了验证和验证测试针对其中一种生成在测试环境中，并已准备好应用程序部署到过渡环境。 在此期间，开发人员可能签入新代码。 不想要重新生成解决方案并将其部署到过渡环境中，并且你不想要将最新版本部署到过渡环境。 相反，你想要部署的特定生成的已验证，并在测试服务器上进行验证。

若要实现此目的，需要告知 Microsoft Build Engine (MSBuild) 若要查找的 web 包和特定生成的生成的数据库脚本的位置。

## <a name="overriding-the-outputroot-property"></a>重写 OutputRoot 属性

在中[示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)，则*Publish.proj*文件声明一个名为属性**OutputRoot**。 顾名思义，这是包含的生成过程生成的所有内容的根文件夹。 在中*Publish.proj*文件，您所见， **OutputRoot**属性指的是部署的所有资源的根位置。

> [!NOTE]
> **OutputRoot**是常用的属性名称。 Visual C# 和 Visual Basic 项目文件还声明此属性来存储所有生成输出的根位置。


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


如果你想在项目文件来部署 web 包和数据库从不同位置的脚本&#x2014;像上一个 TFS 生成的输出&#x2014;只需重写**OutputRoot**属性。 在 Team Build 服务器上，您应设置为相关生成文件夹的属性值。 如果从命令行运行 MSBuild，可以指定的值**OutputRoot**作为命令行参数：


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


在实践中，但是，您还想要跳过**构建**目标&#x2014;就不必在构建您的解决方案，如果不打算使用生成输出。 通过指定想要从命令行执行的目标，无法执行此操作：


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


但是，在大多数情况下，你将想要为 TFS 生成定义，生成你的部署逻辑。 这使用户与**生成排队**触发到 TFS 服务器通过连接任何 Visual Studio 安装中的部署的权限。

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>创建生成定义以部署特定生成

下一个过程介绍如何创建生成定义，使用户触发器部署到过渡环境使用单个命令。

在这种情况下，不想要实际生成的任何内容的生成定义&#x2014;不仅希望其在你的自定义项目文件中执行的部署逻辑。 *Publish.proj*文件包含将跳过的条件逻辑**生成**如果在 Team Build 中运行该文件为目标。 这是通过评估内置**BuildingInTeamBuild**属性，它将自动设置为**true**如果您在 Team Build 中运行你的项目文件。 因此，你可以跳过生成过程，只需运行要部署的现有生成的项目文件。

**若要创建生成定义，若要手动触发部署**

1. 在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目节点，右键单击**生成**，然后单击**新建生成定义**。

    ![](deploying-a-specific-build/_static/image2.png)
2. 上**常规**选项卡上，为生成定义指定一个名称 (例如， **DeployToStaging**) 和可选描述。
3. 上**触发器**选项卡上，选择**手动-签入不会触发新的生成**。
4. 上**生成默认值**选项卡上，在**生成输出复制到以下放置文件夹**框中，键入 drop 文件夹的通用命名约定 (UNC) 路径 (例如，  **\\TFSBUILD\Drops**)。

    ![](deploying-a-specific-build/_static/image3.png)
5. 上**进程**选项卡上，在**生成过程文件**下拉列表中，保留**DefaultTemplate.xaml**选定。 这是添加到所有新的团队项目的默认生成过程模板之一。
6. 在中**生成过程参数**表中，单击在**生成的项**行，然后依次**省略号**按钮。

    ![](deploying-a-specific-build/_static/image4.png)
7. 在中**生成的项**对话框中，单击**添加**。
8. 在中**类型的项**下拉列表中选择**MSBuild 项目文件**。
9. 浏览到与其控件部署过程中，选择的文件，然后单击的自定义项目文件的位置**确定**。

    ![](deploying-a-specific-build/_static/image5.png)
10. 在中**生成的项**对话框中，单击**确定**。
11. 在中**生成过程参数**表中，展开**高级**部分。
12. 在中**MSBuild 参数**行，指定特定于环境的项目文件的位置并为生成文件夹的位置添加一个占位符：

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > 你将需要重写**OutputRoot**值每次对生成进行排队。 下一过程中对此进行了。
13. 单击“保存” 。

当触发生成时，你需要更新**OutputRoot**属性以指向要部署的生成。

**若要部署特定生成的生成定义中**

1. 在中**团队资源管理器**窗口中，右键单击生成定义，然后单击**使新生成入队**。

    ![](deploying-a-specific-build/_static/image7.png)
2. 在中**使生成入队**对话框中，在**参数**选项卡上，展开**高级**部分。
3. 在中**MSBuild 参数**行中，将的值为**OutputRoot**生成文件夹的位置的属性。 例如：

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > 请务必包括尾部反斜杠生成文件夹的路径的末尾。
4. 单击**队列**。

当对生成进行排队、 项目文件将部署的数据库脚本和 web 包从生成放置文件夹中指定**OutputRoot**属性。

## <a name="conclusion"></a>结束语

本主题介绍了如何将发布部署资源，如 web 包和数据库脚本、 从上一个特定的生成使用拆分项目文件的部署模型。 本文介绍了如何重写**OutputRoot**属性以及如何将部署逻辑合并到 TFS 生成定义。

## <a name="further-reading"></a>其他阅读材料

创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)并[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。 生成排队的更多指导，请参阅[对生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。

> [!div class="step-by-step"]
> [上一页](creating-a-build-definition-that-supports-deployment.md)
> [下一页](configuring-permissions-for-team-build-deployment.md)
