---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 生成和打包 Web 应用程序项目 |Microsoft Docs
author: jrjlee
description: 当你想要将 web 应用程序项目部署到远程服务器环境时，您的首要任务是生成项目并生成 web 部署 packa...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: ff8312d16dff2a9eec9ae909bca5e72d52f17094
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382603"
---
<a name="building-and-packaging-web-application-projects"></a>生成和打包 Web 应用程序项目
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 当你想要将 web 应用程序项目部署到远程服务器环境时，您的首要任务是生成项目并生成 web 部署包。 本主题介绍如何生成过程适用于 web 应用程序项目。 具体而言，它说明了：
> 
> - 如何 Web 发布管道 (WPP) 扩展生成过程以包含部署功能。
> - 如何 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 将 web 应用程序到部署包。
> - 如何生成和打包进程的工作原理和创建的文件的。


在 Visual Studio 2010 中，WPP 支持 web 应用程序项目的生成和部署过程。 WPP 提供一的组 Microsoft Build Engine (MSBuild) 目标，可以扩展 MSBuild 的功能并使其能够将 Web 部署与集成。 Visual Studio 中，可以在属性页上看到此扩展的功能，为 web 应用程序项目。 **打包/发布 Web**页上，一起**打包/发布 SQL**页上，使你能够配置生成过程完成后，为部署打包你的 web 应用程序项目是如何。

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP 是如何工作的？

如果您看一下项目文件的 C#-基于的 web 应用程序项目，您可以看到它将两个.targets 文件导入。


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]


第一个**导入**语句是普遍适用于所有 Visual C# 项目。 此文件中， *Microsoft.CSharp.targets*，包含目标和任务特定的 Visual C#。 例如，C# 编译器 (**Csc**) 此处调用任务。 *Microsoft.CSharp.targets*反过来文件导入*Microsoft.Common.targets*文件。 这将定义目标所共有的所有项目，如**构建**，**重新生成**，**运行**，**编译**，和**清理**. 第二个**导入**语句是特定于 web 应用程序项目。 *Microsoft.WebApplication.targets*反过来文件导入*Microsoft.Web.Publishing.targets*文件。 *Microsoft.Web.Publishing.targets*实质上是文件*是*WPP。 它定义了目标，如**包**并**MSDeployPublish**，调用 Web 部署来完成不同的部署任务。

若要了解如何使用这些其他目标，在联系人管理器示例解决方案中，打开*Publish.proj*文件，并看一看**BuildProjects**目标。


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]


此目标使用**MSBuild**任务可以生成各种项目。 请注意**DeployOnBuild**并**DeployTarget**属性：

- **DeployOnBuild = true**属性实质上意味着"我想要生成已成功完成时执行的其他目标。"
- **DeployTarget**属性标识所需时要执行的目标的名称**DeployOnBuild**属性等于**true**。 在这种情况下，指定你想要执行的 MSBuild**包**后生成项目目标。

**包**中定义目标*Microsoft.Web.Publishing.targets*文件。 从根本上来说，此目标中，将你的 web 应用程序项目的生成输出，并将其转换可以发布到 IIS web 服务器的 web 部署包。

> [!NOTE]
> 若要查看项目文件 (例如， <em>ContactManager.Mvc.csproj</em>) 在 Visual Studio 2010 中，首先需要卸载从你的解决方案项目。 在中<strong>解决方案资源管理器</strong>窗口中，右键单击项目节点，然后依次<strong>卸载项目</strong>。 再次右键单击项目节点，然后依次<strong>编辑</strong><em>[项目文件]</em>)。 项目文件将在其原始的 XML 格式打开。 请记住，完成后重新加载项目。  
> 有关详细信息 MSBuild 目标，任务，并<strong>导入</strong>语句，请参阅[了解项目文件](understanding-the-project-file.md)。 项目文件和 WPP 的更深入介绍，请参阅[内部 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。


## <a name="what-is-a-web-deployment-package"></a>Web 部署包是什么？

当生成和部署 web 应用程序项目中，通过使用 Visual Studio 2010 或直接使用 MSBuild 时，最终结果是通常*web 部署包*。 Web 部署包是一个.zip 文件。 它包含的所有内容，IIS 和 Web 部署需重新创建 web 应用程序，包括：

- 已编译的输出的 web 应用程序，包括内容、 资源文件、 配置文件、 JavaScript 和级联样式表 (CSS) 资源和等等。
- 程序集为 web 应用程序项目和任何引用你的解决方案中的项目。
- 若要生成要部署 web 应用程序与任何数据库的 SQL 脚本。

生成的 web 部署包之后, 可以将其发布到 IIS web 服务器以各种方式。 例如，通过面向 Web 部署远程代理服务或 Web 部署处理程序中的目标 web 服务器上，可以远程部署它也可以使用 IIS 管理器中手动导入目标 web 服务器上的包。 部署到这些方法的详细信息，请参阅[选择右方法对 Web 部署](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。

## <a name="how-does-the-build-process-work"></a>生成过程是如何工作的？

这将显示在生成和打包 web 应用程序项目时，会发生什么情况：

![](building-and-packaging-web-application-projects/_static/image2.png)

生成 web 应用程序项目时，生成过程将生成名为的文件 *[项目名称]。SourceManifest.xml*。 项目文件以及生成输出，这 *。SourceManifest.xml*文件告知 Web 部署它需要包含 web 部署包中。 使用这些输入，Web 部署生成名为 web 部署包 *[项目名称].zip*。

Web 部署包，以及生成过程会生成可帮助你使用的包的两个文件：

- *。 Deploy.cmd*文件包括一组将你的 web 部署包发布到远程 IIS web 服务器的 Web Deploy (MSDeploy.exe) 的参数化命令。 运行 *。 deploy.cmd*文件中，使用适当的参数，通常提供更快和更轻松地替代手动构造 MSDeploy.exe 命令自己。
- *SetParameters.xml*文件提供了一组到 MSDeploy.exe 命令的参数值。 这些值包括属性，如 IIS web 应用程序到你想要部署包的任何服务终结点的值和连接字符串中定义的名称*web.config*文件和任何部署属性在项目属性页上定义的值。

*SetParameters.xml*文件是管理部署过程的关键。 此文件是根据你的 web 应用程序项目的内容动态生成的。 例如，如果您添加的连接字符串您*web.config*文件，生成过程将自动检测连接字符串，相应地，参数化部署并创建中的条目*SetParameters.xml*文件，以便您可以修改连接字符串作为部署过程的一部分。 下一主题[为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)、 说明此文件中更多详细信息的角色，并描述在其中您可以修改它生成和部署过程的不同方式。

> [!NOTE]
> 在 Visual Studio 2010 中，WPP 不支持预编译之前打包的 web 应用程序中的页。 Visual Studio 和 WPP 的下一版本将包括预编译 web 应用程序作为一个打包选项的功能。


## <a name="conclusion"></a>结束语

本主题提供有关在 Visual Studio 2010 中的 web 应用程序项目生成和打包过程的概述。 它描述如何 WPP，可以调用 MSBuild，Web 部署命令，它介绍了如何生成和打包进程的工作原理。

一旦你创建 web 部署包下, 一步是将其部署。 有关这方面的详细信息，请参阅[为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)并[部署 Web 包](deploying-web-packages.md)。

## <a name="further-reading"></a>其他阅读材料

在本教程的下一个主题[为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)并[部署 Web 包](deploying-web-packages.md)，提供有关如何使用已创建的 web 包的指导。 本系列中的最后一个教程[高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)，提供有关如何自定义和打包过程故障排除指南。

项目文件和 WPP 的更深入介绍，请参阅[内部 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一页](understanding-the-build-process.md)
> [下一页](configuring-parameters-for-web-package-deployment.md)
