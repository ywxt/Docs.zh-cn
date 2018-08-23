---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: 配置目标环境的部署属性 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置特定于环境的属性，以便将示例 Contact Manager 解决方案部署到特定的目标环境...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 1486cc7d8f25e823481dfab109d18c407c2d8063
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832264"
---
<a name="configuring-deployment-properties-for-a-target-environment"></a>配置目标环境的部署属性
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置特定于环境的属性，以便将示例 Contact Manager 解决方案部署到特定的目标环境。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="process-overview"></a>过程概述

将用于生成和部署 Contact Manager 解决方案的项目文件拆分为两个物理文件中：

- 一个包含通用生成设置和说明 ( *Publish.proj*文件)。
- 一个包含特定于环境的生成设置 (*Env Dev.proj*， *Env Stage.proj*，依此类推)。

在生成时，相应的特定于环境的项目文件合并到通用*Publish.proj*文件以形成一组完整的生成说明。 可以通过创建或自定义特定于环境的项目文件的描述部署方案的设置来配置部署到特定的目标环境。

许多这些值由目标环境的配置方式&#x2014;具体而言，是否在目标 web 服务器配置为使用 Web 部署代理服务 （远程代理） 或 Web 部署处理程序。 这些方法的详细信息并选择自己的环境的正确方法的指导，请参阅[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)。

[联系人管理器方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)需要两个特定于环境的项目文件：

- 向开发人员测试环境部署 (*Env Dev.proj*)。 开发人员测试环境配置为接受使用远程代理的远程部署，如中所述[方案： 配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。 此文件需要终结点地址，以及特定于位置的设置，例如连接字符串和服务终结点提供远程代理。
- 部署到过渡环境 (*Env Stage.proj*)。 在过渡环境配置为接受远程部署使用 Web 部署处理程序，如中所述[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。 此文件需要提供 Web 部署处理程序终结点地址以及类似于连接字符串的特定于位置的设置和服务终结点。

务必要注意特定于环境的项目文件中配置的设置不会影响 web 包本身的内容&#x2014;相反，它们控制如何部署包和包时提供哪些参数值提取。 要导入 web 包到生产环境中所述手动[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)并[手动安装 Web 程序包](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)，因此它并不重要哪些设置中使用了特定于环境的项目文件生成包时。 Internet 信息服务 (IIS) 管理器将提示您输入任何参数化值，如连接字符串和服务终结点时将包导入。

若要将 Contact Manager 解决方案部署到目标环境，可以自定义此文件或可以将其用作模板，并创建你自己的文件。

**若要配置特定于环境的部署设置 Contact Manager 解决方案**

1. 在 Visual Studio 2010 中打开 ContactManager WCF 解决方案。
2. 在中**解决方案资源管理器**窗口中，展开**发布**文件夹中，展开**EnvConfig**文件夹，然后再双击**Env Dev.proj**.

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. 替换中的属性值*Env Dev.proj*测试环境的正确值的文件。

    > [!NOTE]
    > 此过程后面的表提供有关每个属性的详细信息。
4. 保存您的工作，，然后关闭*Env Dev.proj*文件。

## <a name="choosing-the-right-deployment-properties"></a>选择正确的部署属性

此表描述了在示例特定于环境的项目文件中，每个属性的用途*Env Dev.proj*，并应提供的值提供一些指导。


|                                                        属性名                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        详细信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>MSDeployComputerName</strong>目标 web 服务器或服务终结点的名称。               |                                                                                                                                                                                                                                              如果你正在部署到目标 web 服务器上的远程代理服务，则可以指定目标计算机名称 (例如， <strong>TESTWEB1</strong>或<strong>TESTWEB1.fabrikam.net</strong>)，也可以指定远程代理终结点 (例如， `http://TESTWEB1/MSDEPLOYAGENTSERVICE`)。 部署中每个用例的工作方式相同。 如果你正在部署到 Web 部署处理程序在目标 web 服务器上，你应指定服务终结点，并且包括作为查询字符串参数的 IIS 网站的名称 (例如， `https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`)。                                                                                                                                                                                                                                              |
|         <strong>MSDeployAuth</strong> Web 部署应使用对远程计算机进行身份验证的方法。          |                                                                                                                                                                                                                          这应设置为<strong>NTLM</strong>或<strong>基本</strong>。 通常情况下，将使用<strong>NTLM</strong>如果你正在部署到远程代理服务并<strong>基本</strong>如果正在部署到 Web 部署处理程序。 如果使用基本身份验证，还需要指定的用户名和密码才能执行部署应模拟 IIS Web 部署工具 （Web 部署）。 在此示例中，这些值通过提供<strong>MSDeployUsername</strong>并<strong>MSDeployPassword</strong>属性。 如果使用 NTLM 身份验证，可以忽略这些属性，或将其留空。                                                                                                                                                                                                                          |
| <strong>MSDeployUsername</strong>如果使用基本身份验证，Web 部署将使用此帐户在远程计算机上。  |                                                                                                                                                                                                                                                                                                                                                                                                                       这应采用以下形式<em>域</em>\*用户名 * (例如， <strong>FABRIKAM\matt</strong>)。 如果指定基本身份验证，则仅使用此值。 如果使用 NTLM 身份验证，则可以省略该属性。 如果提供一个值，则它将被忽略。                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong>如果使用基本身份验证，Web 部署将使用此密码在远程计算机上。 |                                                                                                                                                                                                                                                                                                                                                                                                                    这是在指定的用户帐户的密码<strong>MSDeployUsername</strong>属性。 如果指定基本身份验证，则仅使用此值。 如果使用 NTLM 身份验证，则可以省略该属性。 如果提供一个值，则它将被忽略。                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong>你想要部署的联系人管理器 MVC 应用程序的 IIS 路径。     |                                                                                                                                                                                                                                                                                                                                                                        这应是路径的形式显示在 IIS 管理器中，[<em>IIS 网站名称</em>] / [<em>web</em><em>应用程序名称</em>]。 请记住，需要部署应用程序之前存在的 IIS 网站。 例如，如果已创建名为 DemoSite 的 IIS 网站，你可以为 DemoSite/ContactManager 指定 MVC 应用程序的 IIS 路径。                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong>你想要部署的联系人管理器中的 WCF 服务的 IIS 路径。    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          例如，如果已创建名为 DemoSite 的 IIS 网站，您可以指定作为 WCF 服务的 IIS 路径<strong>DemoSite/ContactManagerService</strong>。                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>ContactManagerTargetUrl</strong>可访问的 WCF 服务的 URL。                   |                                                                                                                                                     这将需要在窗体 [<em>IIS 网站的根 URL</em>] / [<em>服务应用程序名称</em>] / [<em>服务终结点</em>]。 例如，如果已在端口 85 上创建的 IIS 网站，URL 将采用格式`http://localhost:85/ContactManagerService/ContactService.svc`。 请记住 MVC 应用程序和 WCF 服务部署到同一台服务器。 因此，从安装它的计算机只会访问此 URL。 因此，最好在 URL 中使用 localhost 或 IP 地址，而不是计算机名称或主机标头。 如果使用的计算机名称或主机标头[环回检查](https://go.microsoft.com/?linkid=9805131)在 IIS 中的安全功能可能会阻止 URL 并返回<strong>HTTP 401.1-未经授权的</strong>错误。                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong>数据库服务器的连接字符串。                  | 连接字符串确定这两个凭据 VSDBCMD 将用来连接到数据库服务器和创建数据库和 web 服务器应用程序池将使用与数据库服务器联系，并与数据库交互的凭据。 实质上是此处有两个选择。 可以指定<strong>集成安全性 = true</strong>，在这种情况下使用集成的 Windows 身份验证：<strong>数据源 = TESTDB1; Integrated Security = true</strong>在这种情况下，将使用创建数据库运行可执行文件，VSDBCMD 的用户和应用程序的凭据，将访问数据库使用的 web 服务器计算机帐户标识。 或者，可以指定用户名和 SQL Server 帐户的密码。 VSDBCMD 创建数据库和要与数据库交互的应用程序池，在这种情况下，使用 SQL Server 凭据：<strong>数据源 = TESTDB1;用户 Id = ASqlUser;密码 = Pa$ $w0rd</strong>本主题中的演练假定您将使用集成的 Windows 身份验证。 |
|        <strong>CmTargetDatabase</strong>你想要为数据库服务器，您将创建的数据库的名称。        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     此处提供的值作为参数添加到 VSDBCMD 命令。 此外可用于构建 web 服务器上的应用程序池可用于与数据库交互的完整连接字符串。                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

以下示例演示如何配置这些属性对于特定部署方案。

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>示例 1&#x2014;部署到远程代理服务

在此示例中：

- 要部署到 TESTWEB1 上的远程代理服务。
- 则会指示 Web 部署可以使用 NTLM 身份验证。 Web 部署将使用用于调用 Microsoft Build Engine (MSBuild) 的凭据运行。
- 使用集成身份验证来部署**ContactManager** TESTDB1 到数据库。 数据库会使用用于调用 MSBuild 的凭据进行部署。


[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]


### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>示例 2&#x2014;部署到 Web 部署处理程序终结点

在此示例中：

- 要部署到 STAGEWEB1 上的 Web 部署处理程序服务终结点。
- 则会指示 Web 部署可以使用基本身份验证。
- 指定 Web 部署应模拟的 FABRIKAM\stagingdeployer 帐户在远程计算机上。
- 使用 SQL Server 身份验证来部署**ContactManager** STAGEDB1 到数据库。


[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]


## <a name="conclusion"></a>结束语

此时，项目文件被完全配置为生成并部署到一个或多个目标环境的 Contact Manager 解决方案。

若要单步执行、 可重复部署过程的一部分使用这些项目文件，您需要执行*Publish.proj*文件使用 MSBuild，并传入作为参数的特定于环境的项目文件的位置。 可以以多种方式来执行此操作：

- MSBuild 和自定义项目文件的简介的概述，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。
- 有关如何构建用于执行自定义项目文件的 MSBuild 命令的信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。
- 有关如何将 MSBuild 命令合并到单步执行、 可重复部署的命令文件的信息，请参阅[创建和运行部署命令文件](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)。
- 有关如何从 Team Build 执行自定义项目文件的信息，请参阅[创建该支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

> [!div class="step-by-step"]
> [上一篇](creating-a-server-farm-with-the-web-farm-framework.md)
