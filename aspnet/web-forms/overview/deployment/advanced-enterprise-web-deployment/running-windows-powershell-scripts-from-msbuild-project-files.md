---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: 运行 MSBuild 项目文件中的 Windows PowerShell 脚本 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何生成和部署过程的一部分运行的 Windows PowerShell 脚本。 你可以在本地运行脚本 (换而言之，在 b...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: faedcee480b6c50dc560055206fedbe7af4d5f67
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803144"
---
<a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>运行 MSBuild 项目文件中的 Windows PowerShell 脚本
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何生成和部署过程的一部分运行的 Windows PowerShell 脚本。 可以本地运行脚本 （即，在生成服务器上） 或远程，如数据库服务器或目标 web 服务器上。
> 
> 有很多你可能想要运行部署后 Windows PowerShell 脚本的原因。 例如，你可能希望：
> 
> - 将自定义事件源添加到注册表。
> - 生成上传的文件系统目录。
> - 清理生成目录。
> - 向自定义日志文件中写入条目。
> - 发送电子邮件邀请到新预配的 web 应用程序的用户。
> - 创建具有相应权限的用户帐户。
> - 配置 SQL Server 实例之间进行复制。
> 
> 本主题将演示如何从 Microsoft Build Engine (MSBuild) 项目文件中的自定义目标本地和远程运行 Windows PowerShell 脚本。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

若要运行的 Windows PowerShell 脚本自动化或单步执行部署过程的一部分，你将需要完成以下高级任务：

- 将 Windows PowerShell 脚本添加到你的解决方案和源代码管理。
- 创建调用 Windows PowerShell 脚本的命令。
- 在命令中任何保留的 XML 字符进行转义。
- 自定义 MSBuild 项目文件中创建一个目标并使用**Exec**任务来运行你的命令。

本主题将演示如何执行这些过程。 任务和本主题中的演练假定您已经熟悉 MSBuild 目标和属性，并确保你了解如何使用自定义的 MSBuild 项目文件来驱动生成和部署过程。 有关详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

## <a name="creating-and-adding-windows-powershell-scripts"></a>创建并添加 Windows PowerShell 脚本

本主题中的任务使用名为 Windows PowerShell 脚本示例**LogDeploy.ps1**是为了说明如何从 MSBuild 运行脚本。 **LogDeploy.ps1**脚本包含单个行项写入日志文件的简单函数：


[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]


**LogDeploy.ps1**脚本接受两个参数。 第一个参数表示你想要添加一个条目的日志文件的完整路径和第二个参数表示你想要在日志文件中记录的部署目标。 当您运行该脚本时，它将行添加到此格式中的日志文件：


[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]


若要使**LogDeploy.ps1**可用到 MSBuild 的脚本，你需要：

- 将脚本添加到源代码管理。
- 将脚本添加到你在 Visual Studio 2010 中的解决方案。

您不必将与你解决方案的内容，而不考虑你是否计划在生成服务器或远程计算机上运行该脚本的脚本部署。 一种方法是将脚本添加到解决方案文件夹。 在联系人管理器示例中，因为你想要使用 Windows PowerShell 脚本作为部署过程中，最好将脚本添加到发布解决方案文件夹。

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

解决方案文件夹中的内容复制到生成服务器作为源材料。 但是，它们构成任何项目输出中的任何部分。

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>在生成服务器上执行的 Windows PowerShell 脚本

在某些情况下，你可能想要生成你的项目在计算机上运行 Windows PowerShell 脚本。 例如，可能会使用 Windows PowerShell 脚本来清理生成文件夹或将条目写入到自定义日志文件。

根据语法，从一个 MSBuild 项目文件运行 Windows PowerShell 脚本是相同的常规的命令提示符下运行的 Windows PowerShell 脚本。 需要调用 powershell.exe 可执行文件并使用 **– 命令**交换机以提供你想要运行的 Windows PowerShell 的命令。 (在 Windows PowerShell v2，可以使用 **– 文件**切换)。 该命令应采取以下格式：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]


例如：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]


如果您的脚本的路径包含空格，需要将文件路径括在单引号前面加 &。 不能使用双引号引起来，因为你已使用过它们括起命令：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]


在调用此命令从 MSBuild 时，有一些额外的注意事项。 首先，应包括 **– NonInteractive**标志来确保安静地执行脚本。 接下来，应包括 **– ExecutionPolicy**具有相应的自变量值的标志。 这将指定 Windows PowerShell 将应用于您的脚本，并允许你重写默认执行策略，这可能会阻止脚本执行的执行策略。 你可以从这些自变量值中进行选择：

- 值为**Unrestricted**将允许 Windows PowerShell 执行脚本，而不考虑是否签名脚本。
- 值为**RemoteSigned**将允许 Windows PowerShell 执行未签名的脚本在本地计算机上创建的。 但是，已在其他位置创建的脚本必须进行签名。 （在实践中，您创建的 Windows PowerShell 脚本本地生成服务器上不太可能）。
- 值为**AllSigned**将允许 Windows PowerShell 执行签名的脚本。

默认执行策略是**Restricted**，以防止 Windows PowerShell 运行所有脚本文件。

最后，您需要在 Windows PowerShell 命令中发生任何保留的 XML 字符进行转义：

- 将使用单引号**&amp;apos;**
- 将使用双引号**&amp;quot;**
- 将使用 & **&amp;amp;**

- 当您进行这些更改时，您的命令将与此类似：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]


在自定义 MSBuild 项目文件中，您可以创建新的目标并使用**Exec**任务才能运行此命令：


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]


在此示例中，请注意:

- 任何变量，如参数值和 Windows PowerShell 可执行文件的位置被声明为 MSBuild 属性。
- 条件包括以使用户能够重写这些值从命令行。
- **MSDeployComputerName**项目文件中其他位置声明属性。

在此目标执行生成过程的一部分时，Windows PowerShell 将运行你的命令和日志条目写入指定的文件。

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>在远程计算机上执行的 Windows PowerShell 脚本

Windows PowerShell 是能够通过远程计算机上运行脚本[Windows 远程管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)(WinRM)。 若要执行此操作，您需要使用[Invoke-command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet。 这样可以执行您的脚本对一个或多个远程计算机，而不将该脚本复制到远程计算机。 任何结果返回到你从中运行该脚本在本地计算机。

> [!NOTE]
> 在使用之前**Invoke-command** cmdlet 来执行 Windows PowerShell 脚本在远程计算机上，您需要配置 WinRM 侦听器以接受远程消息。 您可以执行此操作通过运行命令**winrm quickconfig**远程计算机上。 有关详细信息，请参阅[安装和配置适用于 Windows 远程管理的](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)。


从 Windows PowerShell 窗口中，将使用此语法来运行**LogDeploy.ps1**远程计算机上的脚本：


[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]


> [!NOTE]
> 使用的各种其他方式**Invoke-command**运行脚本文件，但这种方法是最简单需要提供参数值和管理包含空格的路径。


当从命令提示符中运行它时，需要调用 Windows PowerShell 可执行文件并使用 **– 命令**参数来提供您的说明：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]


根据之前，需要提供一些其他开关，并对任何保留的 XML 字符进行转义 MSBuild 中运行命令时：


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]


最后，与之前一样，您可以使用**Exec**内用于执行命令的自定义 MSBuild 目标的任务：


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]


在此目标执行生成过程的一部分时，Windows PowerShell 将在指定的计算机上运行脚本 **– computername**参数。

## <a name="conclusion"></a>结束语

本主题介绍了如何从一个 MSBuild 项目文件运行 Windows PowerShell 脚本。 这种方法可用于以自动或单步执行生成和部署过程的一部分运行的 Windows PowerShell 脚本，本地或远程计算机上。

## <a name="further-reading"></a>其他阅读材料

有关 Windows PowerShell 脚本签名和管理执行策略的指南，请参阅[运行 Windows PowerShell 脚本](https://technet.microsoft.com/library/ee176949.aspx)。 有关从远程计算机运行 Windows PowerShell 命令的指导，请参阅[运行远程命令](https://technet.microsoft.com/library/dd819505.aspx)。

使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

> [!div class="step-by-step"]
> [上一页](taking-web-applications-offline-with-web-deploy.md)
> [下一页](troubleshooting-the-packaging-process.md)
