---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 使 Web 应用程序脱机使用 Web 部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何采用脱机使用 Internet 信息服务 (IIS) Web 部署的自动部署期间的 web 应用程序...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: b8dc1ff26bbbe7dee1ee90fd929b2e98de5360db
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829510"
---
<a name="taking-web-applications-offline-with-web-deploy"></a>使 Web 应用程序脱机使用 Web 部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何获取 web 应用程序脱机使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 的自动部署持续时间。 浏览到 web 应用程序的用户将重定向到*应用程序\_offline.htm*文件之前部署已完成。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

在很多情况下，你将想要使 web 应用程序脱机时对相关的组件，如数据库或 web 服务进行更改。 通常情况下，在 IIS 和 ASP.NET 中，为此，将名为的文件置于*应用程序\_offline.htm* IIS 网站或 web 应用程序的根文件夹中。 *应用程序\_offline.htm*文件是标准的 HTML 文件，通常包含一种简单消息，通知用户该站点是否因维护而暂时不可用。 虽然*应用程序\_offline.htm*文件存在的网站的根文件夹中，IIS 会自动重的任何请求定向到文件。 完成后进行更新的操作后，删除*应用程序\_offline.htm*文件和网站继续像往常一样为请求提供服务。

当使用 Web 部署来执行自动或单步执行到目标环境的部署时，你可能想要合并添加和删除*应用程序\_offline.htm*文件到您的部署过程。 若要执行此操作，你将需要完成以下高级任务：

- 在 Microsoft Build Engine (MSBuild) 项目文件中用于控制部署过程中，创建 MSBuild 目标的复制*应用程序\_offline.htm*到目标服务器之前部署的任何任务的文件开始。
- 添加另一个删除的 MSBuild 目标*应用程序\_offline.htm*从目标服务器时完成了所有部署任务的文件。
- 在 web 应用程序项目中创建 *。 wpp.targets*文件，可确保*应用\_offline.htm* Web 部署调用时，将文件添加到部署包。

本主题将演示如何执行这些过程。 任务和本主题中的演练假定，您已创建一个解决方案，包含至少一个 web 应用程序项目，并使用自定义项目文件来控制部署过程中所述[中的 Web 部署企业](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 或者，可以使用[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案要遵循本主题中的示例。

## <a name="adding-an-appoffline-file-to-a-web-application-project"></a>将应用添加\_到 Web 应用程序项目的脱机文件

需要完成的第一个任务是将添加*应用程序\_脱机*文件到你的 web 应用程序项目：

- 若要防止文件干扰开发过程 （不希望永久脱机应用程序），您应将其称为以外*应用\_offline.htm*。 例如，可以命名该文件*应用程序\_脱机 template.htm*。
- 若要阻止该文件作为部署的是，应将生成操作设置为**None**。

**若要将应用添加\_到 web 应用程序项目的脱机文件**

1. 在 Visual Studio 2010 中打开你的解决方案。
2. 在中**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目，指向**添加**，然后单击**新项**。
3. 在中**添加新项**对话框中，选择**HTML 页**。
4. 在中**名称**框中，键入**应用\_脱机 template.htm**，然后单击**添加**。

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 添加一些简单的 HTML，以通知用户该应用程序已不可用，并保存该文件。 不包括任何服务器端标记 (例如，任何带有前缀的标记"asp:")。 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. 在中**解决方案资源管理器**窗口中，右键单击新文件，然后依次**属性**。
7. 在中**属性**窗口，请在**生成操作**行中，选中**None**。

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-appoffline-file"></a>部署和删除应用\_脱机文件

下一步是修改你部署的逻辑来将文件复制到目标服务器在部署过程的开始和结束时将其删除。

> [!NOTE]
> 下一步的过程假定，您使用自定义的 MSBuild 项目文件来控制您的部署过程中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 如果你正在部署直接从 Visual Studio，你将需要使用不同的方法。 Sayed Ibrahim Hashimi 描述中的一种方法[如何采用您 Web 应用脱机期间发布](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)。


若要部署*应用程序\_脱机*文件到目标的 IIS 网站，您需要调用 MSDeploy.exe 使用[Web 部署**contentPath**提供程序](https://technet.microsoft.com/library/dd569034(WS.10).aspx)。 **ContentPath**提供程序支持物理目录路径和 IIS 网站或应用程序路径，这使得同步 Visual Studio 项目文件夹和 IIS web 应用程序之间的文件的理想选择。 若要部署该文件，MSDeploy 命令应类似如下：


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]


若要从目标站点，在部署过程结束时删除该文件，MSDeploy 命令应类似如下：


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]


若要生成和部署过程的一部分自动运行这些命令，需要将其集成到自定义 MSBuild 项目文件。 下一步的过程描述如何执行此操作。

**若要部署和删除应用\_脱机文件**

1. 在 Visual Studio 2010 中，打开控制您的部署过程的 MSBuild 项目文件。 在中[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案，这是*Publish.proj*文件。
2. 在根目录**项目**元素中，创建一个新**PropertyGroup**元素存储为变量*应用\_脱机*部署：

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot**属性中其他位置定义*Publish.proj*文件。 它指示当前路径的相对路径的源内容的根文件夹的位置&#x2014;换而言之，相对于的位置*Publish.proj*文件。
4. **ContentPath**提供程序将不会接受相对文件路径，因此您需要先获取之前将其部署到您的源文件的绝对路径。 可以使用[ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx)任务来执行此操作。
5. 添加一个新**目标**名为元素**GetAppOfflineAbsolutePath**。 在此目标，使用**ConvertToAbsolutePath**任务来获取到的绝对路径*应用\_脱机模板*项目文件夹中的文件。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. 此目标使用到的相对路径*应用程序\_脱机模板*项目文件夹中的文件并将其保存到的绝对文件路径作为新的属性。 **BeforeTargets**属性指定您希望此目标之前执行**DeployAppOffline**目标，将在下一步中创建。
7. 添加名为的新目标**DeployAppOffline**。 在此目标中调用 MSDeploy.exe 命令部署你*应用程序\_脱机*到目标 web 服务器的文件。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. 在此示例中， **ContactManagerIisPath**属性在项目文件中其他位置定义。 这是只需中的 IIS 应用程序路径，在窗体 *[IIS 网站名称] / [应用程序名称]*。 在目标中包括条件使用户能够切换*应用程序\_脱机*部署打开或关闭通过更改属性值或提供一个命令行参数。
9. 添加名为的新目标**DeleteAppOffline**。 在此目标中调用 MSDeploy.exe 命令删除你*应用程序\_脱机*来自目标 web 服务器的文件。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 最后一个任务是在项目文件的执行过程中调用这些新目标在适当的位置。 可以以多种方式来执行此操作。 例如，在*Publish.proj*文件中， **FullPublishDependsOn**属性指定必须执行的目标的列表中进行排序时**FullPublish**默认调用目标。
11. 修改 MSBuild 项目文件来调用**DeployAppOffline**并**DeleteAppOffline**目标，请参阅在发布过程中相应点。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

自定义 MSBuild 项目文件中，运行时*应用程序\_脱机*文件将成功生成后立即部署到服务器。 它将然后会从服务器中删除所有部署任务完成后。

## <a name="adding-an-appoffline-file-to-deployment-packages"></a>将应用添加\_到部署包的脱机文件

根据配置您的部署方式，任何现有内容在目标 IIS web 应用程序&#x2014;等*应用\_offline.htm*文件&#x2014;时，可删除自动部署 web到目标的包。 若要确保*应用程序\_offline.htm*文件将留在原位部署期间，您需要部署直接的开头的文件除了包含自身的 web 部署包中的文件部署过程中。

- 如果已按照本主题中前面的任务，您将添加*应用程序\_offline.htm*对 web 应用程序项目在不同的文件名的文件 (我们使用了*应用\_脱机 template.htm*) 并将已设置生成操作为**None**。 这些更改所需防止干扰开发和调试该文件。 因此，你需要自定义的打包过程，请确保*应用程序\_offline.htm*文件包含在 web 部署包。

Web 发布管道 (WPP) 使用名为项列表**FilesForPackagingFromProject**来生成应包含 web 部署包中的文件的列表。 可以将自己的项添加到此列表自定义 web 包的内容。 若要执行此操作，需要完成以下高级步骤：

1. 创建一个名为的自定义项目文件 *[项目名称].wpp.targets*项目文件所在的文件夹中。

    > [!NOTE]
    > *。 Wpp.targets*文件需要在 web 应用程序项目文件所在的文件夹&#x2014;等*ContactManager.Mvc.csproj*&#x2014;而不是任何自定义所在的文件夹中用于控制生成和部署过程的项目文件。
2. 在中 *。 wpp.targets*文件中，创建新的 MSBuild 目标执行*之前* **CopyAllFilesToSingleFolderForPackage**目标。 这是生成要在包中包含的事项列表 WPP 目标。
3. 在新的目标中，创建**ItemGroup**元素。
4. 在中**ItemGroup**元素中，添加**FilesForPackagingFromProject**项，并指定*应用\_offline.htm*文件。

*。 Wpp.targets*文件应类似于下面：


[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]


这些是在此示例中需要注意的要点：

- **BeforeTargets**特性将插入它应在执行之前通过指定 WPP 到此目标**CopyAllFilesToSingleFolderForPackage**目标。
- **FilesForPackagingFromProject**项使用**DestinationRelativePath**元数据值将从文件重命名*应用\_脱机 template.htm*向*应用程序\_offline.htm*被添加到列表。

下一个过程演示如何添加这 *。 wpp.targets*到 web 应用程序项目文件。

**若要添加.wpp.targets 文件中的 web 部署包**

1. 在 Visual Studio 2010 中打开你的解决方案。
2. 在中**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目节点 (例如， **ContactManager.Mvc**)，指向**添加**，然后单击**新项**。
3. 在中**添加新项**对话框中，选择**XML 文件**模板。
4. 在 **名称** 框中，键入 *[项目名称]***.wpp.targets** (例如， **ContactManager.Mvc.wpp.targets**)，然后单击 **添加**.

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > 如果将新项添加到项目的根节点，在项目文件所在的同一文件夹中创建文件。 可以通过在 Windows 资源管理器中打开该文件夹对此进行验证。
5. 在文件中，添加前面所述的 MSBuild 标记。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. 保存并关闭 *[项目名称].wpp.targets*文件。

下一次你生成并打包你的 web 应用程序项目，将自动检测 WPP *。 wpp.targets*文件。 *应用程序\_脱机 template.htm*文件将作为生成的 web 部署包中包含*应用\_offline.htm*。

> [!NOTE]
> 如果你的部署失败，*应用程序\_offline.htm*文件将保持不变，并且你的应用程序将保持脱机状态。 这通常是所需的行为。 若要恢复应用程序的重新联机，您可以删除*应用程序\_offline.htm*文件从你的 web 服务器。 或者，如果更正任何错误，运行成功的部署，则*应用程序\_offline.htm*文件将被删除。


## <a name="conclusion"></a>结束语

本主题介绍了如何获取 web 应用程序脱机的部署，持续时间通过发布*应用程序\_offline.htm*到目标服务器的部署过程开始时文件，并将其在删除结束日期。 它还介绍了如何包括*应用程序\_offline.htm* web 部署包中的文件。

## <a name="further-reading"></a>其他阅读材料

打包和部署过程的详细信息，请参阅[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)，[用于 Web 包部署的配置参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)，和[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

如果发布 web 应用程序直接从 Visual Studio 中，而不使用这些教程中介绍的自定义 MSBuild 项目文件方法，您将需要使用略有不同的方法才能在发布期间应用程序脱机过程。 有关详细信息，请参阅[如何在发布期间采用 web 应用程序脱机](https://go.microsoft.com/?linkid=9805135)（博客文章）。

> [!div class="step-by-step"]
> [上一页](excluding-files-and-folders-from-deployment.md)
> [下一页](running-windows-powershell-scripts-from-msbuild-project-files.md)
