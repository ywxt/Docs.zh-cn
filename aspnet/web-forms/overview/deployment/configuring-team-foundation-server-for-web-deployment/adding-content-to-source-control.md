---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 将内容添加到源代码管理 |Microsoft Docs
author: jrjlee
description: 本主题说明如何将内容添加到源代码管理在 Team Foundation Server (TFS) 2010年。 它介绍了如何将解决方案和项目添加到团队项目...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 2119705a75d0717d05d4a7db69b3f5d38b1cdd45
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834123"
---
<a name="adding-content-to-source-control"></a>将内容添加到源代码管理
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题说明如何将内容添加到源代码管理在 Team Foundation Server (TFS) 2010年。 它介绍了如何将解决方案和项目添加到团队项目在 TFS 中，并介绍如何将等框架或程序集的外部依赖项添加到源代码管理。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

## <a name="task-overview"></a>任务概述

在大多数情况下，每个开发人员团队成员应能够将内容添加到源代码管理。 若要将解决方案添加到 TFS 中的源控件，您将需要完成以下高级步骤：

- 连接到团队项目。
- 将在服务器上的团队项目文件夹结构映射到在本地计算机上的文件夹结构。
- 将解决方案及其内容添加到源代码管理。
- 添加到源代码管理的任何外部依赖关系。

本主题将演示如何执行这些过程。

任务和本主题中的演练假定，您已创建一个新的 TFS 团队项目来管理内容。 创建新的团队项目的详细信息，请参阅[在 TFS 中创建团队项目](creating-a-team-project-in-tfs.md)。

### <a name="who-performs-these-procedures"></a>谁将执行以下步骤？

在大多数情况下，每个开发人员团队成员应能够添加和修改特定团队项目中的内容。

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>连接到团队项目并创建的文件夹映射

在添加到源代码管理的任何内容之前，需要连接到团队项目并在本地计算机上创建的服务器上的文件夹结构和文件系统之间的映射。

**若要连接到团队项目，并将映射的本地路径**

1. 在开发人员工作站上打开 Visual Studio 2010。
2. 在 Visual Studio 中，在**团队**菜单上，单击**连接到 Team Foundation Server**。

    > [!NOTE]
    > 如果已配置 TFS 服务器的连接，则可以省略步骤 3-6。
3. 在中**连接到团队项目**对话框中，单击**服务器**。
4. 在中**添加/删除 Team Foundation Server**对话框中，单击**添加**。
5. 在中**添加 Team Foundation Server**对话框中，提供你的 TFS 实例的详细信息，然后单击**确定**。

    ![](adding-content-to-source-control/_static/image1.png)
6. 在中**添加/删除 Team Foundation Server**对话框中，单击**关闭**。
7. 在中**连接到团队项目**对话框中，选择你想要连接到，选择团队的 TFS 实例项目集合中，选择你想要添加到团队项目，单击**Connect**。

    ![](adding-content-to-source-control/_static/image2.png)
8. 在中**团队资源管理器**窗口中，展开你的团队项目，然后双击**源代码管理**。

    ![](adding-content-to-source-control/_static/image3.png)
9. 上**源控件资源管理器**选项卡上，单击**未映射**。

    ![](adding-content-to-source-control/_static/image4.png)
10. 在中**地图**对话框中**本地文件夹**框中，浏览到 （或创建） 的本地文件夹作为团队项目的根文件夹，然后单击**映射**。

    ![](adding-content-to-source-control/_static/image5.png)
11. 当系统提示要下载源代码文件时，单击**是**。

    ![](adding-content-to-source-control/_static/image6.png)

此时，已映射到开发人员工作站上的本地文件夹的团队项目的服务器端文件夹。 您已到本地文件夹结构从团队项目中下载的任何现有内容。 你现在可以开始将您自己的内容添加到源代码管理。

## <a name="add-projects-and-solutions-to-source-control"></a>添加到源代码管理项目和解决方案

若要添加到源代码管理项目和解决方案，首先需要在本地计算机上将它们移动到团队项目的映射文件夹。 然后，您可以签入要与服务器同步你添加的内容。

**若要将项目添加到源代码管理**

1. 开发人员工作站到团队项目的映射的文件夹结构中的相应位置中移动的项目和解决方案。

    > [!NOTE]
    > 许多组织会如何在源代码管理中组织项目和解决方案的首选的方法。 有关如何结构文件夹的指导，请参阅[How To： 结构在源代码管理文件夹，Team Foundation Server 中](https://msdn.microsoft.com/library/bb668992.aspx)。
2. 在 Visual Studio 2010 中打开的解决方案。
3. 在中**解决方案资源管理器**窗口中，右键单击解决方案，然后依次**将解决方案添加到源代码管理**。

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > 在某些情况下，具体取决于你的组织希望在 TFS 中，结构内容一无所知的状态可能需要将项目添加到源代码管理分别以提供更加精细地控制你的源代码的组织方式。
4. 确认**源控件资源管理器**选项卡显示已添加为团队项目的服务器文件夹结构中的内容。

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > **源控件资源管理器**选项卡显示你并无需再提示您，因为你的解决方案添加到本地文件系统上的映射文件夹进行的内容。 如果你的解决方案位于未映射的位置，请将提示您在 TFS 和你的本地文件系统中指定文件夹位置。
5. 上**源控件资源管理器**选项卡上，在**文件夹**窗格中，右键单击团队项目 (例如， **ContactManager**)，然后单击**签入挂起的更改**。
6. 在中**签入 – 源文件**对话框中，键入注释，然后依次**签入**。

    ![](adding-content-to-source-control/_static/image9.png)

此时已添加到 TFS 中的源代码管理你的解决方案。

## <a name="add-external-dependencies-to-source-control"></a>添加到源代码管理的外部依赖关系

到源代码管理添加项目或解决方案时，系统将还添加任何文件和你的项目或解决方案中的文件夹。 但是，在许多情况下，项目和解决方案也依赖于外部依赖项，如本地程序集，才能正常工作。 您需要添加到源代码管理，让 Team Build 和开发人员团队的其他成员的任何此类资源已成功生成你的代码。

例如，联系人管理器示例解决方案的文件夹结构包含名为包的文件夹。 这对于 ADO.NET Entity Framework 4.1 中包含的程序集以及各种支持资源。 包文件夹不属于 Contact Manager 解决方案，但没有它无法成功生成解决方案。 若要使 Team Build 生成解决方案，需要将包文件夹添加到源代码管理。

> [!NOTE]
> 包含的包文件夹是典型的实体框架或类似资源添加到你的解决方案使用适用于 Visual Studio 2010 NuGet 扩展时，会发生什么情况。


**若要将非项目内容添加到源代码管理**

1. 请确保想要添加它 （例如，包文件夹） 的项位于本地文件系统上的映射文件夹中的相应位置。
2. 在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目，然后双击**源代码管理**。

    ![](adding-content-to-source-control/_static/image10.png)
3. 上**源控件资源管理器**选项卡上，在**文件夹**窗格中，选择要添加的文件夹包含的项或项。
4. 单击**项目添加到文件夹**按钮。

    ![](adding-content-to-source-control/_static/image11.png)
5. 在中**添加到源代码管理**对话框框中，选择文件夹或多个你想要添加，，然后单击**下一步**。

    ![](adding-content-to-source-control/_static/image12.png)
6. 上**排除项**选项卡上，选择任何所需的项，已被自动排除 （例如程序集），然后单击**包括项**。

    ![](adding-content-to-source-control/_static/image13.png)
7. 上**要添加的项**选项卡上，验证你想要包括的所有文件列出，然后单击**完成**。

    ![](adding-content-to-source-control/_static/image14.png)
8. 在中**源控件资源管理器**窗口中，单击**签入**按钮。

    ![](adding-content-to-source-control/_static/image15.png)
9. 在中**签入 – 源文件**对话框中，键入注释，然后依次**签入**。

此时，具有外部依赖项为您的解决方案添加到源代码管理。

## <a name="conclusion"></a>结束语

本主题介绍了如何连接到团队项目，将映射的文件夹结构，并将内容添加到源代码管理。 有关如何使用源代码管理下的项的详细信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

下一主题[TFS 生成服务器配置用于 Web 部署](configuring-a-tfs-build-server-for-web-deployment.md)，介绍如何准备 TFS Team Build 的服务器，以生成和部署你的解决方案。

## <a name="further-reading"></a>其他阅读材料

有关使用 TFS 中的源控件的更全面信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。

> [!div class="step-by-step"]
> [上一页](creating-a-team-project-in-tfs.md)
> [下一页](configuring-a-tfs-build-server-for-web-deployment.md)
