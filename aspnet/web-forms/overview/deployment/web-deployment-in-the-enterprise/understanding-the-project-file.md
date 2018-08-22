---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 了解项目文件 |Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) 项目文件位于生成和部署过程的核心。 本主题开头为 MSBuild 的概念性概述...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 114dd21002ef41627f3a101c0197a85fd5208887
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824424"
---
<a name="understanding-the-project-file"></a>了解项目文件
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft Build Engine (MSBuild) 项目文件位于生成和部署过程的核心。 本主题开头的 MSBuild 和项目文件的概念性概述。 它描述当您使用的项目文件，其效果通过举例说明如何使用项目文件来部署实际的应用程序时将遇到的关键组件。
> 
> 你将学习：
> 
> - MSBuild 如何使用 MSBuild 项目文件来生成项目。
> - 如何 MSBuild 集成与部署技术，如 Internet 信息服务 (IIS) Web 部署工具 （Web 部署）。
> - 如何了解项目文件的关键组件。
> - 如何使用项目文件生成和部署复杂的应用程序。


## <a name="msbuild-and-the-project-file"></a>MSBuild 和项目文件

当你创建并在 Visual Studio 中生成解决方案时，Visual Studio 使用 MSBuild 生成解决方案中的每个项目。 每个 Visual Studio 项目包含一个 MSBuild 项目文件，反映项目的类型的文件扩展名与&#x2014;例如，C# 项目 (.csproj)、 Visual Basic.NET 项目 (.vbproj) 或数据库项目 (.dbproj)。 若要生成项目时，MSBuild 必须处理与项目关联的项目文件。 项目文件是包含所有信息和说明 MSBuild 需生成项目，如要包括平台要求、 版本控制信息、 web 服务器或数据库服务器设置的内容的 XML 文档和必须执行的任务。

MSBuild 项目文件基于[MSBuild XML 架构](https://msdn.microsoft.com/library/5dy88c2e.aspx)，因此生成过程是完全开放和透明。 此外，您不需要安装 Visual Studio 才能使用 MSBuild 引擎&#x2014;MSBuild.exe 可执行文件是.NET Framework 的一部分，可以从命令提示符下运行。 作为开发人员，您可以编写您自己的 MSBuild 项目文件，使用 MSBuild XML 架构，来实施复杂的细化控制如何生成和部署你的项目。 这些自定义项目文件的工作方式与 Visual Studio 会自动生成的项目文件完全相同。

> [!NOTE]
> 此外可以与 Team Build 服务 Team Foundation Server (TFS) 中使用 MSBuild 项目文件。 例如，在持续集成 (CI) 方案中的项目文件可用于自动部署到测试环境时签入新代码。 有关详细信息，请参阅[用于自动执行 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。


### <a name="project-file-naming-conventions"></a>项目文件命名约定

在创建您自己的项目文件时，可以使用任何您喜欢的文件扩展名。 但是，若要使他人可以轻松地了解你的解决方案，应使用这些常见约定：

- 创建生成的项目的项目文件时，请使用.proj 扩展。
- 在创建要导入到其他项目文件的可重用的项目文件时，请使用.targets 扩展名。 文件扩展名为.targets 通常不生成任何内容本身，而是只需包含可以导入到.proj 文件的说明。

### <a name="integration-with-deployment-technologies"></a>与部署技术的集成

如果您使用过 ASP.NET web 应用程序和 ASP.NET MVC web 应用程序，如 web 应用程序项目在 Visual Studio 2010 中，您就知道这些项目包括用于打包和部署到目标环境的 web 应用程序的内置支持。 **属性**页这些项目包括**打包/发布 Web**并**打包/发布 SQL**可用于配置的选项卡如何的组件在打包和部署应用程序。 下面的示例演示**打包/发布 Web**选项卡：

![](understanding-the-project-file/_static/image1.png)

这些功能背后的基础技术称为 Web 发布管道 (WPP) 作为。 WPP 实质上是将 MSBuild 和[Web 部署](https://go.microsoft.com/?linkid=9805122)一起，以 web 应用程序提供完整的生成、 包和部署过程。

好消息是您可以充分利用 WPP 提供创建 web 项目的自定义项目文件时的集成点。 可以在项目文件中，可用于生成项目、 创建 web 部署包，并通过单个项目文件和 MSBuild 的单个调用远程服务器上安装这些包包含部署说明。 作为生成过程的一部分，你还可以调用任何其他可执行文件。 例如，可以运行 VSDBCMD.exe 命令行工具来部署数据库架构文件。 本主题的过程中，你将看到如何，您可以充分利用这些功能，以满足您的企业部署方案的要求。

> [!NOTE]
> Web 应用程序部署过程的工作原理的详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698.aspx)。


## <a name="the-anatomy-of-a-project-file"></a>项目文件的剖析

查看更多详细信息中的生成过程之前，它是值得花一些时间来熟悉 MSBuild 项目文件的基本结构。 本部分提供查看、 编辑或创建项目文件时，将会遇到的常见元素的概述。 具体而言，你将学习：

- 如何使用*属性*管理生成过程的变量。
- 如何使用*项*来确定生成过程的输入，这类似于代码文件。
- 如何使用*目标*并*任务*以便执行指令到 MSBuild，使用*属性*并*项*中其他位置定义项目文件中。

这显示了一个 MSBuild 项目文件中的主要元素之间的关系：

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>Project 元素

[项目](https://msdn.microsoft.com/library/bcxfsh87.aspx)元素是每个项目文件的根元素。 除了标识项目文件的 XML 架构**项目**元素可以包含特性来指定生成过程的入口点。 例如，在[联系人管理器示例解决方案](the-contact-manager-solution.md)，则*Publish.proj*文件指定生成应该通过调用名为目标来启动**FullPublish**。


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a>属性和条件

项目文件通常需要提供了大量的信息，以便成功地生成和部署你的项目的不同部分。 这条信息可能包括服务器名称、 连接字符串、 凭据、 生成配置、 源和目标文件路径和想要包括支持自定义的任何其他信息。 在项目文件中，属性必须定义内[PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)元素。 MSBuild 属性包括键-值对。 内**PropertyGroup**元素，元素名称定义的属性键和元素内容定义的属性值。 例如，可以定义名为的属性**ServerName**并**ConnectionString**来存储静态服务器名称和连接字符串。


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


若要检索的属性值，则使用格式<strong>$(</strong><em>PropertyName</em><strong>)</strong><em>。</em>例如，若要检索的值<strong>ServerName</strong>属性，你需要键入：


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> 你将看到示例说明了如何以及何时使用本主题后面的属性值。


在项目文件中嵌入的静态属性形式的信息并不总是理想的方法来管理生成过程。 在很多情况下，你将想要从其他源中获取信息或鼓励用户提供命令提示符中的信息。 MSBuild，可作为命令行参数指定任何属性值。 例如，用户可以提供的值**ServerName**时他或她 MSBuild.exe 从命令行运行。


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> 有关参数和可用于 MSBuild.exe 的开关的详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。


可以使用相同的属性语法以获取环境变量和内置项目属性的值。 许多常用的属性的定义，并且它们通过包括相关参数名称使用你的项目文件。 例如，若要检索的当前项目平台&#x2014;例如 **x86** 或 **AnyCpu**&#x2014;可以包括 **$(Platform)** 中的属性引用你的项目文件。 有关详细信息，请参阅[用于生成命令和属性的宏](https://msdn.microsoft.com/library/c02as0cs.aspx)，[常用的 MSBuild 项目属性](https://msdn.microsoft.com/library/bb629394.aspx)，并[保留属性](https://msdn.microsoft.com/library/ms164309.aspx)。

属性通常用于结合*条件*。 支持大多数 MSBuild 元素**条件**属性，它允许您指定 MSBuild 应在其评估该元素的条件。 例如，考虑此属性定义：


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


当 MSBuild 处理此属性定义时，它首先会检查以查看是否 **$(OutputRoot)** 属性值为可用。 如果属性值为空&#x2014;换而言之，用户未为此属性提供值&#x2014;条件计算结果为 **true** 和属性值设置为 **...\Publish\Out** 。如果用户已为此属性提供一个值，该条件计算结果为**false**和不使用静态属性值。

可以在其中指定条件的不同方式的详细信息，请参阅[MSBuild 条件](https://msdn.microsoft.com/library/7szfhaft.aspx)。

### <a name="items-and-item-groups"></a>项目和项组

重要的项目文件的角色之一是定义生成过程的输入。 通常情况下，这些输入是文件&#x2014;的代码文件、 配置文件、 命令文件和任何其他需要处理或将作为复制的文件生成过程的一部分。 在 MSBuild 项目架构中，由这些输入[项](https://msdn.microsoft.com/library/ms164283.aspx)元素。 在项目文件中，项目必须定义内[ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)元素。 就像**属性**元素，您可以命名**项**元素你的喜好。 但是，必须指定**Include**属性标识的文件或项所表示的通配符。


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


通过指定多个**项**具有相同名称的元素，要有效地创建的资源的命名的列表。 若要了解此操作的好方法是若要查看在 Visual Studio 将创建的项目文件之一。 例如， *ContactManager.Mvc.csproj*示例解决方案文件中的包括大量的项组，每个都有多个具有相同的名称**项**元素。


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


这样一来，在项目文件指示 MSBuild 构造需要相同的方式处理的文件的列表&#x2014;**引用**列表包含必须在位置，以便成功生成程序集**编译**列表包括必须编译的代码文件和**内容**列表提供一些资源，必须复制不变。 我们将介绍如何生成过程引用和使用本主题后面的这些项。

此外可以包含项元素[ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx)子元素。 这是用户定义的键 / 值对，实质上是表示特定于该项目的属性。 例如，大量**编译**项目文件中的项元素包括**DependentUpon**子元素。


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> 除了用户创建的项元数据，在创建的各种常见元数据分配的所有项。 有关详细信息，请参阅[常见项元数据](https://msdn.microsoft.com/library/ms164313.aspx)。


您可以创建**ItemGroup**根级别中的元素**项目**元素或在特定于**目标**元素。 **ItemGroup**元素还支持**条件**，你可以定制根据项目配置或平台等条件生成过程的输入的属性。

### <a name="targets-and-tasks"></a>目标和任务

在 MSBuild 架构中，[任务](https://msdn.microsoft.com/library/77f2hx1s.aspx)元素表示的各个生成指令 （或任务）。 MSBuild 包括大量预定义的任务。 例如：

- **复制**任务将文件复制到新位置。
- **Csc**任务调用 Visual C# 编译器。
- **Vbc**任务调用 Visual Basic 编译器。
- **Exec**任务运行指定的程序。
- **消息**任务将一条消息写入到一个记录器。

> [!NOTE]
> 现成可用的任务的完整详细信息，请参阅[MSBuild 任务参考](https://msdn.microsoft.com/library/7z253716.aspx)。 有关详细信息的任务，包括如何创建您自己的自定义任务，请参阅[MSBuild 任务](https://msdn.microsoft.com/library/ms171466.aspx)。


任务必须始终包含在[目标](https://msdn.microsoft.com/library/t50z2hka.aspx)元素。 一个**目标**元素是一组按顺序执行的一个或多个任务和项目文件可以包含多个目标。 当你想要运行一个任务或一组任务时，请调用包含它们的目标。 例如，假设您有一个简单的项目文件，将消息记录。


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


你可以通过调用从命令行中，目标 **/t** 开关指定目标。


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


或者，可以添加**DefaultTargets**归于**项目**元素，指定你想要调用的目标。


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


在这种情况下，您不必指定命令行中的目标。 您可以只需指定项目文件中，并调用 MSBuild **FullPublish**为您的目标。


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


目标和任务可以包括**条件**属性。 在这种情况下，您可以选择忽略整个目标或单个任务，如果满足某些条件时。

通常情况下，当您创建有用的任务和目标，将需要对属性和已在项目文件中其他位置定义的项，请参阅：

- 若要使用的属性值，请键入<strong>$(</strong><em>PropertyName</em><strong>)</strong>，其中<em>PropertyName</em>的名称<strong>属性</strong>元素或参数的名称。
- 若要使用的项，请键入<strong>@(</strong><em>ItemName</em><strong>)</strong>，其中<em>ItemName</em>的名称<strong>项</strong>元素。

> [!NOTE]
> 请记住，是否具有相同名称创建多个项，你正在生成列表。 与此相反，如果具有相同名称创建多个属性，您提供的最后一个属性值将覆盖任何以前的属性具有相同名称&#x2014;属性可以仅包含单个值。


例如，在*Publish.proj*文件中的示例解决方案中，看一看**BuildProjects**目标。


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


在此示例中，您可以观察这些关键点：

- 如果**BuildingInTeamBuild**参数指定了和的值为**true**，此目标中的任务都不会执行。
- 目标包含的单一实例[MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)任务。 此任务可以生成其他 MSBuild 项目。
- **ProjectsToBuild**项传递给任务。 此项可以表示项目或解决方案文件，所有已定义的一系列**ProjectsToBuild**项的项组中的元素。 在这种情况下， **ProjectsToBuild**项引用的单一解决方案文件。

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- 属性值传递给**MSBuild**任务包括参数名为**OutputRoot**并**配置**。 如果未为如果它们提供参数值或静态属性值设置。

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

您还可以看到**MSBuild**任务调用名为的目标**生成**。 这是一个广泛应用于 Visual Studio 项目文件，并且可以向你在自定义项目文件，如的几个内置目标**构建**，**清理**，**重新生成**，并**发布**。 您将学习有关使用目标和任务，来控制生成过程中，以及有关的详细信息**MSBuild**任务具体而言，本主题中的更高版本。

> [!NOTE]
> 在目标上的详细信息，请参阅[MSBuild 目标](https://msdn.microsoft.com/library/ms171462.aspx)。


## <a name="splitting-project-files-to-support-multiple-environments"></a>拆分项目文件，以支持多个环境

假设你想要能够将解决方案部署到多个环境，如测试服务器、 过渡平台和生产环境。 配置可能差别很大这些环境之间&#x2014;不只是根据服务器名称、 连接字符串等，但也可能会在凭据、 安全设置和其他因素的很多方面。 如果需要定期执行此操作，不真正便利，若要编辑项目文件中的多个属性，每次切换目标环境。 也不是一个理想的解决方案需要的属性值提供给生成过程的无限列表。

幸运的是一种替代方法。 MSBuild，可跨多个项目文件拆分生成配置。 若要查看此工作原理，在示例解决方案中，请注意，有两个自定义项目文件：

- *Publish.proj*，它包含属性、 项和普遍适用于所有环境的目标是。
- *Env Dev.proj*，其中包含特定于开发人员环境的属性。

现在请注意， *Publish.proj*文件包含[导入](https://msdn.microsoft.com/library/92x05xfs.aspx)元素中的，紧跟在左括号下方**项目**标记。


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


**导入**元素用于将另一个 MSBuild 项目文件的内容导入当前的 MSBuild 项目文件。 在这种情况下， **TargetEnvPropsFile**参数提供了你想要导入的项目文件的文件名。 运行 MSBuild 时，可以为此参数提供值。


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


这有效地将两个文件的内容合并到单个项目文件。 使用此方法，可以创建一个项目文件包含通用的生成配置和多个包含特定于环境的属性的补充项目文件。 因此，只需运行命令的不同参数值，你可以将你的解决方案部署到不同环境。

![](understanding-the-project-file/_static/image3.png)

拆分项目文件以这种方式是遵循一个好办法。 它允许开发人员通过运行单个命令，同时避免了重复的通用生成属性跨多个项目文件将部署到多个环境。

> [!NOTE]
> 有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[配置目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。


## <a name="conclusion"></a>结束语

本主题提供对 MSBuild 项目文件的常规介绍，并介绍了如何创建您自己的自定义项目文件来控制生成过程。 它还引入了将项目文件拆分为通用生成说明和特定于环境的生成属性，以轻松地生成并部署到多个目标的项目的概念。

下一主题[了解构建过程](understanding-the-build-process.md)，提供了更详细地了解如何通过引导您完成实际的复杂性级别部署的解决方案使用为控件生成和部署的项目文件。

## <a name="further-reading"></a>其他阅读材料

项目文件和 WPP 的更深入介绍，请参阅[内部 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](setting-up-the-contact-manager-solution.md)
> [下一页](understanding-the-build-process.md)
