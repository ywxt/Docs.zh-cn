---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 配置 Web 服务器的 Web 部署发布 （离线部署） |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置 IIS web 服务器以支持脱机 web 发布和部署。 当你处理的 Internet Information Services (我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: 555b4b3c79d8efc641b1c179482993371735dbe2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397572"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a>配置用于 Web 部署发布 （离线部署） 的 Web 服务器
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置 IIS web 服务器以支持脱机 web 发布和部署。
> 
> 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取你的应用程序或 web 服务器上的站点。 你可以：
> 
> - 使用*Web 部署远程代理服务*。 这种方法需要较少配置 web 服务器，但您需要提供的本地服务器管理员凭据才能将任何内容部署到服务器。
> - 使用*Web 部署处理程序*。 这种方法更复杂，需要更多的初始工作来设置 web 服务器。 但是，在使用此方法时，你可以配置 IIS 以允许非管理员用户来执行部署。 Web 部署处理程序只是在 IIS 7 或更高版本中可用。
> - 使用*离线部署*。 这种方法需要 web 服务器的最低配置，但服务器管理员必须手动复制到服务器上的 web 包并将其导入通过 IIS 管理器。
> 
> 主要功能、 优势和一种方法的缺点的详细信息，请参阅[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)。


是，如果你的网络基础结构或安全限制阻止远程部署。 这是最有可能出现这种情况在 web 服务器是独立的面向 Internet 的生产环境中，&#x2014;以物理方式或通过防火墙和子网&#x2014;服务器基础结构的其余部分。

显然，此方法变得不够理想，如果 web 应用程序会定期更新。 如果您的基础结构允许，可能想要启用远程部署，请考虑使用 Web 部署处理程序或 Web 部署远程代理服务。

## <a name="task-overview"></a>任务概述

若要配置 web 服务器以支持脱机导入和部署 web 包，您将需要：

- 安装 IIS 7.5 和 IIS 7 建议的配置。
- 安装 Web 部署 2.1 或更高版本。
- 创建一个 IIS 网站来承载部署的内容。
- 禁用 Web 部署代理服务。

若要专门托管示例解决方案，还需要为：

- 安装.NET Framework 4.0。
- 安装 ASP.NET MVC 3。

本主题将演示如何执行每个这些过程。 任务和本主题中的演练假定您正在使用运行 Windows Server 2008 R2 的全新服务器内部版本。 在继续之前，请确保：

- 安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。
- 服务器已加入域。
- 在服务器具有静态 IP 地址。

> [!NOTE]
> 有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。


## <a name="install-products-and-components"></a>安装的产品和组件

本部分将指导您完成在 web 服务器上安装所需的产品和组件。 在开始之前，一个好的做法是运行 Windows 更新，以确保你的服务器是完全保持最新。

在这种情况下，你需要安装以下事项：

- **IIS 7 推荐配置**。 这使得**Web 服务器 (IIS)** 角色在 web 服务器上的和安装的 IIS 模块和托管的 ASP.NET 应用程序所需的组件组。
- **.NET framework 4.0**。 这是运行此版本的.NET Framework 生成的应用程序所需要的。
- **Web 部署工具 2.1 或更高版本**。 这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。 Web 部署与 IIS 集成，并允许您导入和导出 web 包。
- **ASP.NET MVC 3**。 这会安装您需要运行 MVC 3 应用程序的程序集。

> [!NOTE]
> 本演练介绍如何使用 Web 平台安装程序来安装和配置各种组件。 尽管不一定要使用 Web 平台安装程序，它通过简化了安装过程会自动检测的依赖关系以及确保始终获得最新的产品版本。 有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。


**若要安装必需的产品和组件**

1. 下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。
2. 安装完成后，Web 平台安装程序将自动启动。

    > [!NOTE]
    > 现在可以在任何时候从启动 Web 平台安装程序**启动**菜单。 为此，请在**启动**菜单上，单击**所有程序**，然后单击**Microsoft Web 平台安装程序**。
3. 在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。
4. 在左侧和右侧的窗口中，在导航窗格中，单击**框架**。
5. 在中**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，单击**添加**。

    > [!NOTE]
    > 你可能已安装.NET Framework 4.0 到 Windows 更新。 如果已安装的产品或组件，Web 平台安装程序将此信息指示通过替换**外**按钮，其文本**已安装**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. 在中**ASP.NET MVC 3 (Visual Studio 2010)** 行中，单击**添加**。
7. 在导航窗格中，单击**Server**。
8. 在 **IIS 7 建议配置** 行中，单击 **添加** 。
9. 在中**Web 部署工具 2.1**行中，单击**添加**。
10. 单击“安装” 。 Web 平台安装程序将显示产品列表&#x2014;以及任何关联的依赖关系&#x2014;安装，并将提示你接受许可条款。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. 查看许可条款，如果同意条款，单击**我接受**。
12. 安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。

如果在安装 IIS 之前安装.NET Framework 4.0，您将需要运行[ASP.NET IIS 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)(aspnet\_regiis.exe) 若要向 IIS 注册 ASP.NET 的最新版本。 如果不这样做，您会发现 IIS 将 （如 HTML 文件） 中提供静态内容没有任何问题，但它将返回**HTTP 错误 404.0-未找到**尝试浏览到 ASP.NET 内容时。 下一步过程可用于确保在注册 ASP.NET 4.0。

**若要向 IIS 注册 ASP.NET 4.0**

1. 单击**启动**，然后键入**命令提示符下**。
2. 在搜索结果中，右键单击**命令提示符**，然后单击**以管理员身份运行**。
3. 在命令提示符窗口中， 导航到 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目录。
4. 键入以下命令，然后按 Enter:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. 如果计划托管 64 位 web 应用程序，任何时候，则应该向 IIS 注册 ASP.NET 的 64 位版本。 为此，请在命令提示符窗口中，导航到 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目录。
6. 键入以下命令，然后按 Enter:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

很好的做法是，Windows 更新再次使用此时若要下载并安装新的产品和组件已安装所有可用更新。

## <a name="configure-the-iis-website"></a>配置 IIS 网站

可以将 web 内容部署到你的服务器之前，您需要创建和配置 IIS 网站来承载的内容。 Web 部署可以仅将 web 包部署到现有 IIS 网站;它不能为您创建的网站。 在高级别中，将需要完成以下任务：

- 在文件系统来托管你的内容上创建一个文件夹。
- 创建 IIS 网站提供内容，并将其与本地文件夹关联。
- 授予读取权限的本地文件夹上的应用程序池标识。

尽管没有什么措施可以阻止您从内容部署到 IIS 中的默认网站，但不建议使用此方法用于测试或演示方案之外的任何内容。 若要模拟生产环境中，应使用特定于应用程序的要求的设置创建新的 IIS 网站。

**若要创建和配置 IIS 网站**

1. 在本地文件系统上创建一个文件夹以存储你的内容 (例如， **C:\DemoSite**)。
2. 上**启动**菜单，依次指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**。
3. 在 IIS 管理器中，在**连接**窗格中，展开服务器节点 (例如， **PROWEB1**)。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. 右键单击**站点**节点，并单击**添加网站**。
5. 在中**站点名称**框中，键入为 IIS 网站的名称 (例如， **DemoSite**)。
6. 在中**物理路径**框中，键入 （或浏览到） 到本地文件夹的路径 (例如， **C:\DemoSite**)。
7. 在中**端口**框中，键入你想要托管网站的端口号 (例如， **85**)。

    > [!NOTE]
    > 标准端口号是 80 用于 HTTP 和 HTTPS 的 443。 但是，如果托管该网站在端口 80 上的，你需要停止默认网站，然后才能访问你的站点。
8. 将保留**主机名**框保留为空，除非你想要配置该网站的域名系统 (DNS) 记录，然后单击**确定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > 在生产环境中，你将很可能想要托管你的网站在端口 80 上并配置主机标头，以及匹配的 DNS 记录。 在 IIS 7 中配置主机标头的详细信息，请参阅[为网站 (IIS 7) 配置主机标头](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[DNS 服务器概述](https://technet.microsoft.com/en-gb/library/cc770392.aspx)并[DNS 服务器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在中**操作**窗格下**编辑站点**，单击**绑定**。
10. 在中**站点绑定**对话框中，单击**添加**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. 在中**添加网站绑定**对话框中，将**IP 地址**并**端口**以匹配您现有的站点配置。
12. 在中**主机名**框中，键入你的 web 服务器的名称 (例如， **PROWEB1**)，然后单击**确定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > 第一个站点绑定使你可以访问站点使用的 IP 地址和端口在本地或`http://localhost:85`。 第二个站点绑定使你可以使用计算机名称在域上的其他计算机访问站点 (例如， http://proweb1:85)。
13. 在中**站点绑定**对话框中，单击**关闭**。
14. 在中**连接**窗格中，单击**应用程序池**。
15. 在中**应用程序池**窗格中，右键单击你的应用程序池的名称，然后单击**基本设置**。 默认情况下，应用程序池的名称将与你的网站的名称匹配 (例如， **DemoSite**)。
16. 在 **.NET Framework 版本** 列表中，选择 **.NET Framework v4.0.30319** ，然后单击 **确定** 。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > 示例解决方案需要.NET Framework 4.0。 这不是必需的 Web 部署一般情况下。

为了使你的网站提供内容，应用程序池标识必须具有读取存储内容的本地文件夹的权限。 在 IIS 7.5 应用程序池以运行唯一的应用程序池标识 （与以前版本的 IIS，其中应用程序池通常运行使用网络服务帐户） 默认情况下。 应用程序池标识不是真实的用户帐户和未出现在任何用户或组的列表&#x2014;相反，它动态启动时创建的应用程序池。 每个应用程序池标识添加到本地**IIS\_IUSRS**隐藏项的安全组。

若要授予对文件或文件夹上的应用程序池标识的权限，您有两个选项：

- 将权限分配给应用程序池标识直接，使用格式<strong>IIS AppPool\</strong ><em>[应用程序池名称]</em>(例如， <strong>IIS AppPool\DemoSite</strong>).
- 向其分配权限**IIS\_IUSRS**组。

最常用的方法是将权限分配给本地**IIS\_IUSRS**组，因为这种方法允许您更改应用程序池，而无需重新配置的文件系统权限。 下一个过程中使用此基于组的方法。

> [!NOTE]
> 在 IIS 7.5 的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。


**若要配置 IIS 网站的文件夹权限**

1. 在 Windows 资源管理器，浏览到本地文件夹的位置。
2. 右键单击文件夹，然后依次**属性**。
3. 上**安全**选项卡上，单击**编辑**，然后单击**添加**。
4. 单击**位置**。 在中**位置**对话框中，选择本地服务器，然后单击**确定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. 在中**选择用户或组**对话框中，键入**IIS\_IUSRS**，单击**检查名称**，然后单击**确定**。
6. 在中<strong>的权限</strong><em>[文件夹名称]</em>对话框中，请注意，新的组已分配<strong>读取&amp;执行</strong>，<strong>列出文件夹内容</strong>，并<strong>读取</strong>默认情况下的权限。 保留此保持不变，然后单击<strong>确定</strong>。
7. 单击<strong>确定</strong>以关闭<em>[文件夹名称]</em><strong>属性</strong>对话框。

## <a name="disable-the-remote-agent-service"></a>禁用远程代理服务

在安装 Web Deploy，Web 部署代理服务安装，并自动启动。 此服务可以部署和发布远程位置中的 web 包。 您不会使用的远程部署功能在此方案中，因此应停止并禁用服务。

> [!NOTE]
> 不需要停止远程代理服务才能导入和手动部署 web 包。 但是，它是停止和禁用服务，如果不打算使用它的好办法。


可以停止和禁用某项服务在多个方面，使用各种命令行实用程序或 Windows PowerShell cmdlet。 此过程介绍了简单的基于 UI 的方法。

**若要停止并禁用远程代理服务**

1. 在“开始”  菜单上，指向“管理工具” ，然后单击“服务” 。
2. 在服务控制台中，找到**Web 部署代理服务**行。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. 右键单击**Web 部署代理服务**，然后单击**属性**。
4. 在中**Web 部署代理服务属性**对话框中，单击**停止**。
5. 在中**启动类型**列表中，选择**禁用**，然后单击**确定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a>结束语

此时，你的 web 服务器是脱机 web 包部署已准备就绪。 在尝试导入到 IIS 网站的 web 包之前，你可能想要检查这些关键点：

- 已向 IIS 注册 ASP.NET 4.0？
- 没有应用程序池标识具有读取访问权限的源文件夹的你的网站？
- 已停止 Web 部署代理服务？

> [!div class="step-by-step"]
> [上一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [下一页](configuring-a-database-server-for-web-deploy-publishing.md)
