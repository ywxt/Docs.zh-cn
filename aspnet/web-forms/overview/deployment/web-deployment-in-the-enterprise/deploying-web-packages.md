---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: 部署 Web 包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在您可以发布 web 部署包到远程服务器通过使用 Internet 信息服务 (IIS) Web 部署工具 (Web...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 44c3772263cbebaf03e1393542fda32467a97cd8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825260"
---
<a name="deploying-web-packages"></a>部署 Web 程序包
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在您可以发布 web 部署包到远程服务器使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0。
> 
> 有两种主要方式，您可以在其中部署到远程服务器的 web 包：
> 
> - 可以直接使用 MSDeploy.exe 命令行实用程序。
> - 你可以运行 *[项目名称].deploy.cmd*生成过程生成的文件。
> 
> 最终结果是不管哪种方法使用相同的。 从根本上来说，所有 *。 deploy.cmd*文件是运行 MSDeploy.exe 与一些预先确定的值，以便无需为了部署包提供尽可能多的信息。 这简化了部署过程。 另一方面，直接使用 MSDeploy.exe 可以更灵活地通过完全在包的部署方式。
> 
> 您使用哪种方法将取决于多种因素，您需要对部署过程包括多大控制，并且您面向的 Web 部署远程代理服务或 Web 部署处理程序。 本主题说明如何使用每种方法，并标识适合每种方法时。
> 
> 任务和本主题中的演练假设：
> 
> - 你已生成并打包 web 应用程序，如中所述[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。
> - 在你修改*SetParameters.xml*文件中所述为你的目标环境，提供正确的参数值[用于 Web 包部署的配置参数](configuring-parameters-for-web-package-deployment.md)。


运行 [*项目名称*]*。 deploy.cmd*文件是最简单的方法来部署 web 包。 具体而言，使用 *。 deploy.cmd*文件可提供通过直接使用 MSDeploy.exe 以下优势：

- 您无需指定 web 部署包的位置&#x2014; *。 deploy.cmd*文件已经知道其所在位置。
- 无需指定的位置*SetParameters.xml*文件&#x2014; *。 deploy.cmd*文件已经知道其所在位置。
- 无需指定源和目标 MSDeploy 提供程序&#x2014; *。 deploy.cmd*文件已经知道要使用哪些值。
- 无需指定 MSDeploy 操作设置&#x2014; *。 deploy.cmd*文件将通常所需的值自动添加到 MSDeploy.exe 命令。

在使用之前 *。 deploy.cmd*文件来部署 web 包，您应该确保：

- *。 Deploy.cmd*文件中，[*项目名称*]。*SetParameters.xml*文件和 web 包 ([*项目名称*]。*zip*) 位于同一文件夹中。
- Web Deploy (MSDeploy.exe) 安装在运行的计算机上 *。 deploy.cmd*文件。

*。 Deploy.cmd*文件支持各种命令行选项。 在命令提示符下运行该文件时，这是基本语法：


[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]


您必须指定这两 **/T**标志或 **/Y**标志，以指示您是否要分别执行一次测试运行或在实时部署 （请勿使用这两个标志在同一命令中）。 下表解释了每个标记的用途。

| Flag | 描述 |
| --- | --- |
| **/T** | 调用与 MSDeploy.exe **– whatif**标志以指示一次测试运行。 而不是将包部署，它创建一份如果未将部署包，会发生什么情况。 |
| **/Y** | 调用 MSDeploy.exe，而无需 **– whatif**标志。 这将包部署到本地计算机或指定的目标服务器。 |
| **/M** | 指定目标服务器名称或服务 URL。 你可以在此处提供的值的详细信息，请参阅**终结点注意事项**本主题中的部分。 如果省略 **/M**标志，包将部署到本地计算机。 |
| **/A** | 指定应使用 MSDeploy.exe 来执行部署的身份验证类型。 可能的值为**NTLM**并**基本**。 如果省略 **/A**标志，身份验证类型默认值为**NTLM**部署到 Web 部署远程代理服务和**基本**上部署的 Web 部署处理程序。 |
| **/U** | 指定用户名称。 这仅适用于使用基本身份验证。 |
| **/P** | 指定密码。 这仅适用于使用基本身份验证。 |
| **/L** | 指示包应部署到本地 IIS Express 实例。 |
| **/G** | 指定使用部署包[tempAgent 提供程序设置](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。 如果省略 **/G**标志，则该值默认为**false**。 |

> [!NOTE]
> 每次生成过程创建一个 web 包，它还会创建名为的文件 *[项目名称].deploy readme.txt*来解释这些部署选项。


除了这些标志，还可以指定 Web 部署操作设置为其他 *。 deploy.cmd*参数。 您指定的任何其他设置只被传递到基础 MSDeploy.exe 命令。 有关这些设置的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。

假设你想要将 ContactManager.Mvc web 应用程序项目部署到测试环境中，通过运行 *。 deploy.cmd*文件。 在测试环境配置为使用 Web 部署远程代理服务，如中所述[Web 服务器配置用于 Web 部署发布 （远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。 若要部署 web 应用程序，需要完成后续步骤。

**若要部署 web 应用程序使用。 deploy.cmd 文件**

1. 生成并打包 web 应用程序项目，如中所述[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。
2. 修改*ContactManager.Mvc.SetParameters.xml*文件，以包含测试环境中，正确的参数值，如中所述[用于 Web 包部署的配置参数](configuring-parameters-for-web-package-deployment.md)。
3. 打开命令提示符窗口并导航到的位置*ContactManager.Mvc.deploy.cmd*文件。
4. 键入以下命令，然后按 Enter:

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

在此示例中：

- **/Y**标志指示你想要实际部署包，而不是执行一个试用版运行。
- **/M**标志指示你想要将包部署到名为 TESTWEB1 的服务器。 此值，从 MSDeploy.exe 将尝试将包部署到 Web 部署远程代理服务在 http://TESTWEB1/MSDeployAgentService 。
- **/A**标志指示你想要使用 NTLM 身份验证。 在这种情况下，您不必指定用户名和密码。

为了说明如何使用 *。 deploy.cmd*文件简化了部署过程，看一看 MSDeploy.exe 命令执行运行时，获取生成*ContactManager.Mvc.deploy.cmd*使用上面所示的选项。


[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]


有关使用的详细信息 *。 deploy.cmd*文件来部署 web 包，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。

## <a name="using-msdeployexe"></a>使用 MSDeploy.exe

尽管使用 *。 deploy.cmd*文件通常可简化部署过程中，有某些情况下时最好直接使用 MSDeploy.exe。 例如：

- 如果你想要将部署到 Web 部署处理程序中以非管理员用户，则无法使用 *。 deploy.cmd*文件。 这是由于 Web Deploy 2.0 中的 bug 所述**终结点注意事项**。
- 如果你想要手动切换不同*SetParameters.xml*不同位置中的文件，您可能更倾向于直接使用 MSDeploy.exe。
- 如果你想要重写几个 MSDeploy.exe 命令行参数，您可能更愿意直接使用 MSDeploy.exe。

使用 MSDeploy.exe，需要提供三个关键信息：

- 一个 **– 源**参数，指示你的数据的来源。
- 一个 **– dest**参数，指示其中数据转到。
- 一个 **– 谓词**参数，用于指示[操作](https://technet.microsoft.com/library/dd568989(WS.10).aspx)你想要执行。

依赖于 MSDeploy.exe [Web Deploy 提供程序](https://technet.microsoft.com/library/dd569040(WS.10).aspx)处理源和目标数据。 Web 部署包括许多提供程序表示它就能使用的应用程序和数据源的范围中的&#x2014;例如，有 SQL Server 数据库、 IIS web 服务器、 证书、 全局程序集缓存 (GAC) 程序集，提供程序各种不同的配置文件和大量其他类型的数据。 这两个 **– 源**参数和 **– dest**参数必须指定提供程序，在窗体 **– 源**: [*providerName*] = [*位置*]。 当您要将 web 包部署到 IIS 网站时，应使用以下值：

- **– 源**提供程序是始终[包](https://technet.microsoft.com/library/dd569019(WS.10).aspx)。 例如：

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest**提供程序是始终[自动](https://technet.microsoft.com/library/dd569016(WS.10).aspx)。例如：

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **– 谓词**始终**同步**。

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

此外，你将需要指定各种其他[特定于提供程序的设置](https://technet.microsoft.com/library/dd569001(WS.10).aspx)和常规[操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 例如，假设你想要部署到过渡环境 ContactManager.Mvc web 应用程序。 部署 Web 部署处理程序为目标，并且必须使用基本身份验证。 若要部署 web 应用程序，需要完成后续步骤。

**使用 MSDeploy.exe 的 web 应用程序部署**

1. 生成并打包 web 应用程序项目，如中所述[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。
2. 修改*ContactManager.Mvc.SetParameters.xml*文件，以包含在过渡环境的正确的参数值，如中所述[用于 Web 包部署的配置参数](configuring-parameters-for-web-package-deployment.md)。
3. 打开命令提示符窗口并浏览到 MSDeploy.exe 的位置。 这通常是在 %PROGRAMFILES%\IIS\Microsoft Web 部署 V2\msdeploy.exe。
4. 键入此命令，然后按 Enter （忽略换行）：

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

在此示例中：

- **– 源**参数指定**包**提供程序，并指示 web 包的位置。
- **– Dest**参数指定**自动**提供程序。 **ComputerName**设置目标服务器上提供 Web 部署处理程序的服务 URL。 **Authtype**设置指示你想要使用基本身份验证，并且这种情况下，你需要提供**用户名**和一个**密码**。 最后， **includeAcls ="False"** 设置表示您不希望将访问控制列表 (Acl) 的文件复制到目标服务器在源 web 应用程序中。
- **– 谓词： 同步**参数指示要复制的目标服务器上的源内容。
- **-DisableLink**参数指示不想复制应用程序池、 虚拟目录配置或在目标服务器上的安全套接字层 (SSL) 证书。 有关详细信息，请参阅[Web 部署链接扩展](https://technet.microsoft.com/library/dd569028(WS.10).aspx)。
- **– SetParamFile**参数提供的位置*SetParameters.xml*文件。
- **– AllowUntrusted**开关指示 Web 部署应接受不受信任的证书颁发机构颁发的 SSL 证书。 如果你正在部署到 Web 部署处理程序，并且你已使用自签名的证书保护的服务 URL，您需要包含此开关。

## <a name="automating-web-package-deployment"></a>自动执行 Web 包部署

在很多企业方案，你将想要将 web 包部署为更大的单步或自动的部署的一部分。 无论你选择要将 web 包部署通过运行 *。 deploy.cmd*文件，或者通过直接使用 MSDeploy.exe，可以将命令参数化，并调用它们从 Microsoft 生成引擎 (MSBuild) 中的目标项目文件。

在联系人管理器示例解决方案中，看一看**PublishWebPackages**中的 target *Publish.proj*文件。 此目标运行一次为每个 *。 deploy.cmd*由名为项列表的文件**PublishPackages**。 目标使用属性和项元数据来构建一套完整的参数值的每个 *。 deploy.cmd*文件，然后使用**Exec**任务来运行命令。


[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]


> [!NOTE]
> 示例解决方案中与常规中的自定义项目文件的简介中的项目文件模型的更广泛概述，请参阅[了解项目文件](understanding-the-project-file.md)并[了解生成过程](understanding-the-build-process.md)。


## <a name="endpoint-considerations"></a>终结点的注意事项

无论通过运行来部署 web 包是否 *。 deploy.cmd*文件，或者通过直接使用 MSDeploy.exe，您需要指定计算机名称或你的部署的服务终结点。

如果目标 web 服务器配置为使用 Web 部署远程代理服务的部署，你会指定为目标的目标服务 URL。


[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]


或者，您可以单独的服务器名称指定为目标，和 Web 部署将推断远程代理服务 URL。


[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]


如果目标 web 服务器配置为使用 Web 部署处理程序的部署，您需要的 IIS Web 管理服务 (WMSvc) 的终结点地址指定为目标。 默认情况下，此形式：


[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]


你可以面向任何使用这些终结点 *。 deploy.cmd*文件或直接 MSDeploy.exe。 但是，如果你想要作为非管理员用户，将部署到 Web 部署处理程序中所述[Web 服务器配置用于 Web 部署发布 （Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)，需要将查询字符串添加到服务终结点地址。


[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]


这是因为非管理员用户不具有对 IIS; 服务器级访问权限他或她仅有权访问特定的 IIS 网站。 在撰写本文之际，由于存在 bug 中 Web 发布管道 (WPP)，而不能运行 *。 deploy.cmd*文件中使用的终结点地址，包括查询字符串。 在此方案中，您需要直接使用 MSDeploy.exe 部署 web 包。

> [!NOTE]
> Web 部署远程代理服务和 Web 部署处理程序的详细信息，请参阅[选择右方法对 Web 部署](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。 有关如何配置特定于环境的项目文件将部署到这些终结点的指导，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。


## <a name="authentication-considerations"></a>身份验证注意事项

无论通过运行来部署 web 包是否 *。 deploy.cmd*文件，或者通过直接使用 MSDeploy.exe，您需要指定身份验证类型。 Web 部署接受两个可能值： **NTLM**或**基本**。 如果指定基本身份验证，还需要提供用户名和密码。 有您需要注意当选择身份验证类型的各种因素：

- 如果要部署到 Web 部署远程代理服务，则必须使用 NTLM 身份验证。 远程代理服务不接受基本身份验证凭据。
- 如果你正在部署到 Web 部署处理程序，可以使用 NTLM 或基本身份验证。 默认设置为基本身份验证。 尽管基本身份验证依赖于用户名和密码以纯文本形式传输，但你的凭据会受到保护，因为 Web 部署处理程序始终使用 SSL 加密。
- 如果 web 包包括一个数据库，并且 web 服务器和数据库服务器在单独的计算机，你将无法使用部署数据库由于 NTLM 身份验证[NTLM"双跃点"限制](https://go.microsoft.com/?linkid=9805120)。 您需要在你部署的连接字符串中使用 SQL Server 凭据或提供对 Web 部署的基本身份验证凭据。 中更详细地介绍了此问题[的成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

## <a name="conclusion"></a>结束语

本主题介绍如何部署 web 包通过运行 *。 deploy.cmd*文件或直接使用 MSDeploy.exe。 它介绍了在每种方法可能比较适合，并描述了如何参数化并作为更大的单步执行或自动生成过程的一部分运行的部署命令。

## <a name="further-reading"></a>其他阅读材料

有关如何创建和参数化 web 部署包的指南，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)并[用于 Web 包部署的配置参数](configuring-parameters-for-web-package-deployment.md)。 有关如何生成和部署 web 包从 Team Foundation Server (TFS) 实例的指导，请参阅[用于自动执行 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 有关如何自定义和部署过程故障排除的信息，请参阅[不包括文件和文件夹从部署](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一页](configuring-parameters-for-web-package-deployment.md)
> [下一页](deploying-database-projects.md)
