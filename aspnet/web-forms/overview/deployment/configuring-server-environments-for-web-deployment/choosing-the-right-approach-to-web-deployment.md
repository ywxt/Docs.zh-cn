---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 选择 Web 部署的适当方法 |Microsoft Docs
author: jrjlee
description: 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: f1c3a09d9e960a53a25e0dd0b953224204a9ba7b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367740"
---
<a name="choosing-the-right-approach-to-web-deployment"></a>选择 Web 部署的适当方法
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取已打包的 web 应用程序到 web 服务器上。 您可以：
> 
> - 将从远程位置应用程序部署通过面向*Web 部署代理服务*（也称为"远程代理"） 在目标服务器上。
> - 部署中使用 Web 部署按需 （也称为"临时代理"） 的远程位置的应用程序。
> - 将从远程位置应用程序部署通过面向*IIS Web 部署处理程序*目标服务器上。
> - 将应用程序部署手动将 web 包复制到目标服务器并将其导通过 IIS 管理器。
> 
> 配置目标 web 服务器的方式取决于你想要使用哪种部署的方法。 本主题将帮助您决定哪种部署的方法是最适合你。


此表显示的主要优点和缺点的每个部署方法，以及通常最适合每种方法的方案。

| 方法 | 优点 | 缺点 | 典型的方案 |
| --- | --- | --- | --- |
| 远程代理 | 它很容易设置。 它是适用于 web 应用程序和内容的常规更新。 | 用户必须是目标服务器上的管理员。 用户不能提供备用凭据。 | 开发环境。 测试环境。 |
| 临时代理 | 没有必要在目标计算机上安装 Web 部署。 自动使用最新版本的 Web 部署。 | 用户必须是目标服务器上的管理员。 用户不能提供备用凭据。 | 开发环境。 测试环境。 |
| Web 部署处理程序 | 非管理员用户可以将内容部署。 它是适用于 web 应用程序和内容的常规更新。 | 它是更复杂，无法设置。 | 过渡环境。 Intranet 生产环境。 托管的环境。 |
| 离线部署 | 它是非常容易设置。 它是适用于隔离环境。 | 服务器管理员必须手动复制并导入 web 包每次。 | 面向 Internet 的生产环境。 隔离的网络环境。 |
  

## <a name="using-the-remote-agent"></a>使用远程代理

在安装 Web 部署使用默认设置在目标服务器上时，Web 部署代理服务 （"远程代理"） 自动安装并启动。 默认情况下，远程代理公开 HTTP 终结点在此地址：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> 您可以替换 [*server*] 与你的 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。


服务器管理员可以通过指定此终结点地址部署 web 包从开发人员的计算机或生成服务器等远程位置。 例如，假设在 Fabrikam，Inc.Matt 婷已在自己的开发人员计算机上生成 ContactManager.Mvc web 应用程序项目。 生成过程生成 web 包，连同 *。 deploy.cmd*安装包所需的文件，其中包含 Web 部署命令。 如果 Matt TESTWEB1 服务器上的服务器管理员，他可以通过他的开发人员计算机上运行以下命令部署到测试 web 服务器的 web 应用程序：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


在实际的这一事实，如果您提供计算机名称，因此 Matt 只需键入以下 Web 部署的可执行文件可以推断出远程代理的终结点地址：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> 有关 Web 部署命令行语法的详细信息和 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。


远程代理提供了简单方法以从远程位置，将内容部署，这种方法可以十分适用于一次单击或自动部署。 但是，运行部署命令的用户还必须是域管理员或目标服务器上的本地管理员组的成员。 此外，远程代理不支持基本身份验证，因此不能在命令行上传递其他凭据。

远程代理提供了在开发或测试方案，其中这并不常见的开发人员可以完全权限管理员控制测试服务器环境中，并且通常重新生成并重新部署非常的应用程序中部署的有用方法频繁。 但是，这种方法是通常不到可接受过渡或生产环境。

使用远程代理方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。

## <a name="using-the-temp-agent"></a>使用临时代理

部署的临时代理方法是与远程代理方法类似。 但是，与远程代理方法中，不需要在目标 web 服务器上安装 Web 部署。 相反，当您执行部署时，Web 部署将在目标服务器上安装 web 部署代理服务的临时版本并将使用此若要将内容部署到 IIS。 部署完成后，删除所有临时文件。

如果你想要使用临时代理提供程序设置中，添加 **/g**你部署的命令的标志：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> 不能使用临时代理如果目标计算机上安装 web 部署代理服务，则即使该服务未运行。


此方法的优点是，无需维护的 Web 部署在目标服务器上进行安装。 此外，不需要确保源和目标计算机正在运行相同版本的 Web 部署。 但是，此方法面临相同的主体限制远程代理方法，即，你必须在目标服务器上的本地管理员才能部署内容，并且支持仅 NTLM 身份验证。 临时代理方法还要求在目标环境的更多初始配置。

使用临时代理的详细信息，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)并[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

## <a name="using-the-web-deploy-handler"></a>使用 Web 部署处理程序

适用于 IIS 7 及更高版本，Web 部署提供了通过 IIS Web 部署处理程序采用其他部署方法。 与 IIS Web 管理服务 (WMSvc)，它旨在允许用户从远程位置管理 IIS 网站紧密地集成 Web 部署处理程序。

默认情况下，远程代理公开 HTTP 终结点在此地址：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> 您可以替换 [*server*] 与你的 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。


Web 部署处理程序通过远程代理和临时代理，其最大优点是，您可以配置 IIS 以允许非管理员用户将应用程序和内容部署到特定的 IIS 网站。 Web 部署处理程序还支持基本身份验证，因此可在 Web 部署命令中作为参数提供备用凭据。 主要缺点是，Web 部署处理程序是最初要设置和配置更复杂。

对于非管理员用户，Web 管理服务 (WMSvc) 将仅允许用户连接到 IIS 使用站点级别的连接，而不是服务器级连接。 若要访问特定站点，可以将特定于站点的查询字符串包含在终结点地址：


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


例如，假设生成过程配置为自动部署到过渡环境的 web 应用程序每次成功生成之后。 如果使用远程代理方法，您需要在目标服务器上进行的生成进程标识管理员。 与此相反，使用 Web 部署处理程序方法您可以授予非管理员用户&#x2014;**FABRIKAM\stagingdeployer**在这种情况下&#x2014;，特定的 IIS 网站和生成过程的权限可以提供这些若要将 web 包部署的凭据。


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 有关使用的详细信息 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。


Web 部署处理程序提供了部署在过渡环境、 宿主的环境和基于 intranet 的生产环境中，远程访问服务器可用但不是管理员凭据的有用方法。

使用 Web 部署处理程序方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

## <a name="using-offline-deployment"></a>使用离线部署

在某些情况下，不可能或可行，若要从远程位置将应用程序和内容部署到 IIS 网站。 例如，在源和目标计算机可能在隔离的网络或网络段或防火墙策略可能不允许远程访问。

在类似这样的情况下，您仍然可以使用打包和发布功能的 Web 部署;您只是不能使用它们从远程位置。 相反，目标服务器上的管理员必须复制到服务器上的 web 包并将其导入通过 IIS 管理器。

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

离线部署方法是在面向 Internet 的生产环境中，其中外围网络中的服务器可能会受到限制与内部网络中的计算机的连接通常很有用。

使用离线部署方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

## <a name="further-reading"></a>其他阅读材料

Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。 有关使用的详细信息 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。

可以在其中部署 web 包从远程计算机的不同方式的更多常规指南，请参阅[使用 Web 部署远程](https://technet.microsoft.com/library/ee461175(WS.10).aspx)。 使用 Web 按需部署的详细信息，请参阅[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。

> [!div class="step-by-step"]
> [上一页](configuring-server-environments-for-web-deployment.md)
> [下一页](scenario-configuring-a-test-environment-for-web-deployment.md)
