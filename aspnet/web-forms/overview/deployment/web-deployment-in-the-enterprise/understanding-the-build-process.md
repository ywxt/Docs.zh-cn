---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 了解生成过程 |Microsoft Docs
author: jrjlee
description: 本主题提供了企业范围内生成和部署过程的演练。 本主题中介绍的方法使用自定义 Microsoft 生成 Engin...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 581b7e996bf5aa4c76a6bf3d55a758677c0bf897
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804311"
---
<a name="understanding-the-build-process"></a>了解生成过程
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题提供了企业范围内生成和部署过程的演练。 本主题中介绍的方法使用自定义 Microsoft Build Engine (MSBuild) 项目文件以提供对过程的每个方面进行精细控制。 在项目文件中，自定义 MSBuild 目标用于运行 Internet 信息服务 (IIS) Web 部署工具 (MSDeploy.exe) 等部署实用程序和数据库部署实用工具 VSDBCMD.exe。
> 
> > [!NOTE]
> > 上一个主题[了解项目文件](understanding-the-project-file.md)、 所述的 MSBuild 项目文件的关键组件和引入了拆分项目文件，以支持部署到多个目标环境的概念。 如果您是不熟悉这些概念，则应该查看[了解项目文件](understanding-the-project-file.md)工作通读本主题之前。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="build-and-deployment-overview"></a>生成和部署概述

在中[Contact Manager 解决方案](the-contact-manager-solution.md)，三个文件控制的生成和部署过程：

- 一个*通用项目文件*(*Publish.proj*)。 这包含生成和部署目标环境之间没有更改的说明。
- *特定于环境的项目文件*(*Env Dev.proj*)。 这包含特定于特定的目标环境的生成和部署设置。 例如，可以使用*Env Dev.proj*文件以提供用于开发人员或测试环境的设置，并创建一个名为的备用文件*Env Stage.proj*来提供设置过渡环境环境。
- 一个*命令文件*(*发布 Dev.cmd*)。 此文件包含用于指定你的项目文件命令想要执行的 MSBuild.exe。 可以创建命令文件的每个目标环境，其中的每个文件都包含用于指定不同的特定于环境的项目文件的 MSBuild.exe 命令。 这使开发人员只需通过运行相应的命令文件将部署到不同的环境。

在示例解决方案中，可以找到这三个文件发布解决方案文件夹中。

![](understanding-the-build-process/_static/image1.png)

查看更多详细信息中的这些文件之前，让我们看一看在使用此方法时，整个生成过程的工作方式。 在高级别，如下所示的生成和部署过程：

![](understanding-the-build-process/_static/image2.png)

第一件事是两个项目文件&#x2014;一个包含通用的生成和部署说明，其中包含特定于环境的设置的另一个&#x2014;将合并到单个项目文件。 MSBuild 随后会处理通过项目文件中的说明。 它将构建每个解决方案，为每个项目使用项目文件中的项目。 它然后调用 Web Deploy (MSDeploy.exe) 等其他工具，并且在 VSDBCMD 实用程序将你的 web 内容和数据库部署到目标环境。

从开始到结束，生成和部署过程执行以下任务：

1. 它删除输出目录，以准备新的生成的内容。
2. 生成解决方案中的每个项目：

    1. Web 项目的&#x2014;在这种情况下，ASP.NET MVC web 应用程序和 WCF web 服务&#x2014;生成进程创建的每个项目的 web 部署包。
    2. 数据库项目的生成过程创建的每个项目的部署清单 （.deploymanifest 文件）。
3. 它使用 VSDBCMD.exe 实用程序来部署每个数据库项目在解决方案中，使用项目文件中的各种属性&#x2014;目标连接字符串和数据库名称&#x2014;以及.deploymanifest 文件。
4. 它使用 MSDeploy.exe 实用程序来部署解决方案，使用项目文件中的各种属性来控制部署过程中每个 web 项目。

示例解决方案可用于跟踪此过程的更多详细信息。

> [!NOTE]
> 有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。


## <a name="invoking-the-build-and-deployment-process"></a>调用的生成和部署过程

若要将 Contact Manager 解决方案部署到开发人员的测试环境，开发人员在运行*发布 Dev.cmd*命令文件。 这将调用 MSBuild.exe，指定*Publish.proj*作为要执行的项目文件并*Env Dev.proj*作为参数值。


[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]


> [!NOTE]
> **/Fl**切换 (的缩写 **/fileLogger**) 将生成输出记录到名为的文件*msbuild.log*当前目录中。 有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。


此时，MSBuild 开始运行，加载*Publish.proj*文件，并开始处理其中的说明。 第一个指令告知 MSBuild 导入项目文件**TargetEnvPropsFile**参数指定。


[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]


**TargetEnvPropsFile**参数指定*Env Dev.proj*文件，因此 MSBuild 将的内容合并*Env Dev.proj*文件到*Publish.proj*文件。

MSBuild 遇到合并的项目文件中的下一个元素是属性组。 在文件中出现的顺序处理属性。 MSBuild 创建键-值对的每个属性，提供满足任何指定的条件。 更高版本的文件中定义的属性将覆盖具有相同名称的文件中之前定义的任何属性。 例如，考虑**OutputRoot**属性。


[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]


当 MSBuild 处理第一个**OutputRoot**元素，提供类似的命名参数未提供，它设置的值**OutputRoot**属性设置为 **...\Publish\Out**。当遇到第二个**OutputRoot**元素，如果条件计算结果为**true**，它将覆盖的值**OutputRoot**具有的值的属性**OutDir**参数。

MSBuild 遇到下一个元素是包含名为的单个项组**ProjectsToBuild**。


[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]


MSBuild 的生成名为项列表来处理此指令**ProjectsToBuild**。 在这种情况下，项列表包含单个值&#x2014;的路径和文件名的解决方案文件。

此时，剩余的元素是目标。 目标的处理方式不同属性和项从&#x2014;实质上，目标不会处理除非显式将它们由用户指定或由另一个项目文件中的构造调用。 请记住，左括号**项目**标记包括**DefaultTargets**属性。


[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]


这会指示 MSBuild 来调用**FullPublish**目标，如果目标不是指定何时调用 MSBuild.exe。 **FullPublish**目标不包含任何任务; 而是只需指定依赖项的列表。


[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]


此依赖项告知 MSBuild，为了执行**FullPublish**目标，它需要调用此列表中提供的顺序的目标：

1. 它必须调用**清理**目标。
2. 它必须调用**BuildProjects**目标。
3. 它必须调用**GatherPackagesForPublishing**目标。
4. 它必须调用**PublishDbPackages**目标。
5. 它必须调用**PublishWebPackages**目标。

### <a name="the-clean-target"></a>清理目标

**清理**目标基本上删除输出目录及其所有内容，在准备进行新的生成。


[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]


请注意，目标包含**ItemGroup**元素。 定义属性或中的项时**目标**元素中，你要创建*动态*属性和项。 换而言之，属性或项不被处理，直到执行该目标。 输出目录可能不存在，或者包含任何文件，直到生成过程开始，因此无法生成 **\_FilesToDelete**为静态项列表; 你必须等待，直到执行正在进行。 在这种情况下，在目标内的动态项作为生成该列表。

> [!NOTE]
> 在这种情况下，因为**清理**目标是要执行的第一个，因此没有真正需要使用动态项组。 但是，最好在这种情况下，使用动态属性和项作为可能想要在某个时候不同的顺序执行的目标。  
> 您还应避免将声明将永远不使用的项的目标。 如果必须将仅供特定目标的项，请考虑将它们放置在要删除任何不必要的开销的生成过程的目标。


动态项之外，**清理**目标是非常简单，并且使用内置**消息**，**删除**，和**RemoveDir**任务：

1. 将消息发送到记录器。
2. 生成的要删除的文件的列表。
3. 删除的文件。
4. 删除输出目录。

### <a name="the-buildprojects-target"></a>BuildProjects 目标

**BuildProjects**目标就可以建立在示例解决方案中的所有项目。


[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]


此目标在上一主题中，某些详细信息中所述[了解项目文件](understanding-the-project-file.md)，来说明如何任务和目标引用属性和项。 此时，您有兴趣主要**MSBuild**任务。 此任务可用于生成多个项目。 该任务不会创建 MSBuild.exe; 的新实例它使用当前正在运行的实例来构建每个项目。 在此示例中的要点是部署属性：

- **DeployOnBuild**属性指示 MSBuild 在项目设置中运行部署的说明进行操作，每个项目的生成完成时。
- **DeployTarget**属性标识你想要调用后生成项目的目标。 在这种情况下，**包**目标生成项目输出打包到可部署 web 包。

> [!NOTE]
> **包**目标调用 Web 发布管道 (WPP)，它提供 MSBuild 和 Web 部署之间的集成。 如果你想要看一看的内置目标 WPP 提供，评审*Microsoft.Web.Publishing.targets* %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。


### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing 目标

如果您研究一下**GatherPackagesForPublishing**目标，您会注意到，它实际上并不包含任何任务。 相反，它包含定义三个动态的项的单个项组。


[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]


这些项指时创建的部署包**BuildProjects**执行目标时。 您无法定义这些项以静态方式在项目文件中，因为项引用的文件不存在直到**BuildProjects**执行目标。 相反，项必须动态中定义的目标，则不会调用直到后**BuildProjects**执行目标。

此目标中未使用项&#x2014;此目标只是生成的项和每个项值关联的元数据。 这些元素的处理，一旦**PublishPackages**项将包含两个值的路径*ContactManager.Mvc.deploy.cmd*文件和路径*ContactManager.Service.deploy.cmd*文件。 Web 部署的每个项目的 web 包的过程中创建这些文件和这些是您必须调用的文件以将包部署在目标服务器上。 如果您打开这些文件之一，您基本上将看到包含各种特定于生成的参数值的 MSDeploy.exe 命令。

**DbPublishPackages**项将包含单个值的路径*ContactManager.Database.deploymanifest*文件。

> [!NOTE]
> 生成数据库项目，并作为一个 MSBuild 项目文件使用相同的架构时，会生成一个.deploymanifest 文件。 它包含部署的数据库，包括数据库架构 (.dbschema) 的位置和任何预先部署和后期部署脚本的详细信息所需的所有信息。 有关详细信息，请参阅[概述的数据库生成和部署](https://msdn.microsoft.com/library/aa833165.aspx)。


您将了解有关如何创建和使用在部署包和数据库部署清单进行签名的详细信息[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)并[部署数据库项目](deploying-database-projects.md)。

### <a name="the-publishdbpackages-target"></a>PublishDbPackages 目标

简要说到， **PublishDbPackages**目标调用 VSDBCMD 实用程序来部署**ContactManager**数据库到目标环境。 配置数据库部署涉及大量的决策和细微差别，并将了解有关此信息的详细信息[部署数据库项目](deploying-database-projects.md)和[将数据库部署自定义为多个环境](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md). 在本主题中，我们将重点介绍此目标的实际函数。

首先，请注意，开始标记包含**输出**属性。


[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]


这是一种*目标批处理*。 在 MSBuild 项目文件中，批处理是一种循环访问集合的方法。 值**输出**属性中， **"%(DbPublishPackages.Identity)"**，是指**标识**元数据属性**DbPublishPackages**项列表。 此表示法，**Outputs=%***(ItemList.ItemMetadataName)*，将被转换为：

- 拆分中的项**DbPublishPackages**为包含相同的项目的多个批**标识**元数据值。
- 执行一次每个批处理的目标。

> [!NOTE]
> **标识**是之一[内置元数据值](https://msdn.microsoft.com/library/ms164313.aspx)分配给在创建的每个项。 它引用的值**Include**属性中**项**元素&#x2014;换而言之的路径和文件名的项。


在这种情况下，由于应永远不会有多个项具有相同的路径和文件名，因此我们实质上正在使用的一个批次大小。 对于每个数据库包执行一次目标。

您可以看到中的类似表示法 **\_Cmd**属性，用于生成具有适当的开关的 VSDBCMD 命令。


[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]


在这种情况下， **%(DbPublishPackages.DatabaseConnectionString)**， **%(DbPublishPackages.TargetDatabase)**，并 **%(DbPublishPackages.FullPath)** 全都引用元数据值的**DbPublishPackages**项集合。 **\_Cmd**属性由**Exec**任务中，调用命令。


[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]


由于此表示法，而**Exec**任务将创建唯一组合的基于批次**DatabaseConnectionString**， **TargetDatabase**，以及**FullPath**元数据值和该任务将执行一次的每个批。 这是一种*任务批处理*。 但是，因为目标级别批处理已划分为单个项的批，我们项集合**Exec**任务将运行每个迭代的目标仅一次。 换而言之，此任务将调用一次针对解决方案中每个数据库包 VSDBCMD 实用程序。

> [!NOTE]
> 目标和任务批处理的详细信息，请参阅 MSBuild[批处理](https://msdn.microsoft.com/library/ms171473.aspx)，[目标批处理中的项元数据](https://msdn.microsoft.com/library/ms228229.aspx)，并[任务批处理中的项元数据](https://msdn.microsoft.com/library/ms171474.aspx)。


### <a name="the-publishwebpackages-target"></a>PublishWebPackages 目标

通过目前为止，已调用**BuildProjects**目标，生成示例解决方案中的每个项目的 web 部署包。 伴随每个包会*deploy.cmd*文件，其中包含将包部署到目标环境所需的 MSDeploy.exe 命令，和一个*SetParameters.xml*文件，它指定必需的目标环境的详细信息。 您已调用**GatherPackagesForPublishing**目标，生成一个项集合，其中包含*deploy.cmd*你感兴趣的文件。 从根本上来说， **PublishWebPackages**目标执行这些功能：

- 它处理*SetParameters.xml*对于每个包包含为目标环境中，正确的详细信息的文件使用**XmlPoke**任务。
- 它将调用*deploy.cmd*文件对于每个包，使用适当的开关。

就像**PublishDbPackages**目标**PublishWebPackages**目标使用目标批处理来确保为每个 web 包一次执行该目标。


[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]


在目标内**Exec**任务用于运行*deploy.cmd*为每个 web 包文件。


[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]


有关配置 web 程序包的部署的详细信息，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

## <a name="conclusion"></a>结束语

本主题逐步讲解了如何使用拆分项目文件来控制从开始到结束的联系人管理器示例解决方案的生成和部署过程。 使用此方法允许你运行复杂的企业级部署在单个、 可重复执行步骤中，只需通过运行特定于环境的命令文件。

## <a name="further-reading"></a>其他阅读材料

项目文件和 WPP 的更深入介绍，请参阅[内部 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](understanding-the-project-file.md)
> [下一页](building-and-packaging-web-application-projects.md)
