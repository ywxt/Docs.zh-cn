---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 数据库服务器配置 web 部署发布 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何配置 SQL Server 2008 R2 数据库服务器以支持 web 部署和发布。 本主题中所述的任务都 co...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: a2340c0d561ed274e281b5f6d942af0a2027315a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="configuring-a-database-server-for-web-deploy-publishing"></a><span data-ttu-id="43c73-104">Web 部署发布更改为配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="43c73-104">Configuring a Database Server for Web Deploy Publishing</span></span>
====================
<span data-ttu-id="43c73-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="43c73-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="43c73-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="43c73-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="43c73-107">本主题介绍如何配置 SQL Server 2008 R2 数据库服务器以支持 web 部署和发布。</span><span class="sxs-lookup"><span data-stu-id="43c73-107">This topic describes how to configure a SQL Server 2008 R2 database server to support web deployment and publishing.</span></span>
> 
> <span data-ttu-id="43c73-108">本主题中所述的任务共有的每个部署方案&#x2014;不论你的 web 服务器配置为使用 IIS Web 部署工具 （Web 部署） 的远程代理服务、 Web 部署处理程序或脱机的部署并不重要或你运行应用程序的单个 web 服务器或服务器场。</span><span class="sxs-lookup"><span data-stu-id="43c73-108">The tasks described in this topic are common to every deployment scenario&#x2014;it doesn't matter whether your web servers are configured to use the IIS Web Deployment Tool (Web Deploy) Remote Agent Service, the Web Deploy Handler, or offline deployment or your application is running on a single web server or a server farm.</span></span> <span data-ttu-id="43c73-109">部署数据库的方式可能更改根据安全要求和其他注意事项。</span><span class="sxs-lookup"><span data-stu-id="43c73-109">The way you deploy the database may change according to security requirements and other considerations.</span></span> <span data-ttu-id="43c73-110">例如，你可能部署数据库或不包含示例数据，并可能部署用户角色映射，或在部署后手动配置。</span><span class="sxs-lookup"><span data-stu-id="43c73-110">For example, you might deploy the database with or without sample data, and you might deploy user role mappings or configure them manually after deployment.</span></span> <span data-ttu-id="43c73-111">但是，配置数据库服务器的方式保持不变。</span><span class="sxs-lookup"><span data-stu-id="43c73-111">However, the way you configure the database server remains the same.</span></span>


<span data-ttu-id="43c73-112">你无需安装任何其他产品或工具，配置要支持 web 部署的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="43c73-112">You don't have to install any additional products or tools to configuring a database server to support web deployment.</span></span> <span data-ttu-id="43c73-113">假设你的数据库服务器和 web 服务器运行在不同计算机上，你只需要：</span><span class="sxs-lookup"><span data-stu-id="43c73-113">Assuming that your database server and your web server run on different machines, you simply need to:</span></span>

- <span data-ttu-id="43c73-114">允许 SQL Server 以使用 TCP/IP 进行通信。</span><span class="sxs-lookup"><span data-stu-id="43c73-114">Permit SQL Server to communicate using TCP/IP.</span></span>
- <span data-ttu-id="43c73-115">允许 SQL Server 流量通过任何防火墙。</span><span class="sxs-lookup"><span data-stu-id="43c73-115">Allow SQL Server traffic through any firewalls.</span></span>
- <span data-ttu-id="43c73-116">为 web 服务器计算机帐户提供的 SQL Server 登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-116">Give the web server machine account a SQL Server login.</span></span>
- <span data-ttu-id="43c73-117">计算机帐户登录名映射到任何所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-117">Map the machine account login to any required database roles.</span></span>
- <span data-ttu-id="43c73-118">提供将运行部署 SQL Server 登录名和数据库创建者权限的帐户。</span><span class="sxs-lookup"><span data-stu-id="43c73-118">Give the account that will run the deployment a SQL Server login and database creator permissions.</span></span>
- <span data-ttu-id="43c73-119">若要支持重复的部署，将部署帐户登录名映射到**db\_所有者**数据库角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-119">To support repeat deployments, map the deployment account login to the **db\_owner** database role.</span></span>

<span data-ttu-id="43c73-120">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="43c73-120">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="43c73-121">任务和本主题中的演练假定你刚开始使用 Windows Server 2008 R2 上运行的 SQL Server 2008 R2 的默认实例。</span><span class="sxs-lookup"><span data-stu-id="43c73-121">The tasks and walkthroughs in this topic assume that you're starting with a default instance of SQL Server 2008 R2 running on Windows Server 2008 R2.</span></span> <span data-ttu-id="43c73-122">在继续之前，确保：</span><span class="sxs-lookup"><span data-stu-id="43c73-122">Before you continue, ensure that:</span></span>

- <span data-ttu-id="43c73-123">安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="43c73-123">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="43c73-124">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="43c73-124">The server is domain-joined.</span></span>
- <span data-ttu-id="43c73-125">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="43c73-125">The server has a static IP address.</span></span>
- <span data-ttu-id="43c73-126">安装 SQL Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="43c73-126">SQL Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>

<span data-ttu-id="43c73-127">SQL Server 实例仅需要包括**数据库引擎服务**角色，它自动包含在任何 SQL Server 安装。</span><span class="sxs-lookup"><span data-stu-id="43c73-127">The SQL Server instance only needs to include the **Database Engine Services** role, which is included automatically in any SQL Server installation.</span></span> <span data-ttu-id="43c73-128">但是，为了便于配置和维护，我们建议你包括**管理工具-基本**和**管理工具 – 完整**服务器角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-128">However, for ease of configuration and maintenance, we recommend that you include the **Management Tools – Basic** and **Management Tools – Complete** server roles.</span></span>

> [!NOTE]
> <span data-ttu-id="43c73-129">有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-129">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="43c73-130">有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-130">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="43c73-131">有关安装 SQL Server 的详细信息，请参阅[安装 SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-131">For more information on installing SQL Server, see [Installing SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx).</span></span>


## <a name="enable-remote-access-to-sql-server"></a><span data-ttu-id="43c73-132">启用对 SQL Server 的远程访问</span><span class="sxs-lookup"><span data-stu-id="43c73-132">Enable Remote Access to SQL Server</span></span>

<span data-ttu-id="43c73-133">SQL Server 使用 TCP/IP 与远程计算机通信。</span><span class="sxs-lookup"><span data-stu-id="43c73-133">SQL Server uses TCP/IP to communicate with remote computers.</span></span> <span data-ttu-id="43c73-134">如果你的数据库服务器和 web 服务器位于不同的计算机上，你需要：</span><span class="sxs-lookup"><span data-stu-id="43c73-134">If your database server and your web server are on different machines, you need to:</span></span>

- <span data-ttu-id="43c73-135">配置 SQL Server 网络设置，以允许通过 TCP/IP 进行通信。</span><span class="sxs-lookup"><span data-stu-id="43c73-135">Configure SQL Server networking settings to allow communication over TCP/IP.</span></span>
- <span data-ttu-id="43c73-136">将任何硬件或软件的防火墙允许 TCP 流量 （并在某些情况下用户数据报协议 (UDP) 流量） 上的 SQL Server 实例使用的端口的配置。</span><span class="sxs-lookup"><span data-stu-id="43c73-136">Configure any hardware or software firewalls to allow TCP traffic (and in some cases User Datagram Protocol (UDP) traffic) on the ports that the SQL Server instance uses.</span></span>

<span data-ttu-id="43c73-137">若要启用 SQL Server 通信通过 TCP/IP，请使用 SQL Server 配置管理器来更改您的 SQL Server 实例的网络配置。</span><span class="sxs-lookup"><span data-stu-id="43c73-137">To enable SQL Server to communicate over TCP/IP, use SQL Server Configuration Manager to change the network configuration for your SQL Server instance.</span></span>

<span data-ttu-id="43c73-138">**若要启用 SQL Server 以使用 TCP/IP 进行通信**</span><span class="sxs-lookup"><span data-stu-id="43c73-138">**To enable SQL Server to communicate using TCP/IP**</span></span>

1. <span data-ttu-id="43c73-139">上**启动**菜单上，指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，单击**配置工具**，然后单击**SQL Server 配置管理器**。</span><span class="sxs-lookup"><span data-stu-id="43c73-139">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, click **Configuration Tools**, and then click **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="43c73-140">在树视图窗格中，展开**SQL Server 网络配置**，然后单击**MSSQLSERVER 的协议**。</span><span class="sxs-lookup"><span data-stu-id="43c73-140">In the tree view pane, expand **SQL Server Network Configuration**, and then click **Protocols for MSSQLSERVER**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43c73-141">如果已安装多个 SQL Server 实例，你将看到<strong>协议</strong><em>[实例名称]</em>每个实例的项。</span><span class="sxs-lookup"><span data-stu-id="43c73-141">If you have installed multiple instances of SQL Server, you'll see a <strong>Protocols for</strong><em>[instance name]</em> item for each instance.</span></span> <span data-ttu-id="43c73-142">你需要配置网络设置基于实例的实例。</span><span class="sxs-lookup"><span data-stu-id="43c73-142">You need to configure network settings on an instance-by-instance basis.</span></span>
3. <span data-ttu-id="43c73-143">在细节窗格中，右键单击**TCP/IP**行，然后依次**启用**。</span><span class="sxs-lookup"><span data-stu-id="43c73-143">In the details pane, right-click the **TCP/IP** row, and then click **Enable**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. <span data-ttu-id="43c73-144">在**警告**对话框中，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="43c73-144">In the **Warning** dialog box, click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. <span data-ttu-id="43c73-145">你需要重新启动 MSSQLSERVER 服务，然后新的网络配置将会生效。</span><span class="sxs-lookup"><span data-stu-id="43c73-145">You need to restart the MSSQLSERVER service before your new network configuration will take effect.</span></span> <span data-ttu-id="43c73-146">从服务控制台中，或从 SQL Server Management Studio，你可以将在命令提示符下执行该操作。</span><span class="sxs-lookup"><span data-stu-id="43c73-146">You can do that at a command prompt, from the Services console, or from SQL Server Management Studio.</span></span> <span data-ttu-id="43c73-147">在此过程中，你将使用 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="43c73-147">In this procedure, you'll use SQL Server Management Studio.</span></span>
6. <span data-ttu-id="43c73-148">关闭 SQL Server 配置管理器。</span><span class="sxs-lookup"><span data-stu-id="43c73-148">Close SQL Server Configuration Manager.</span></span>
7. <span data-ttu-id="43c73-149">上**启动**菜单上，指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，然后单击**SQL Server Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="43c73-149">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
8. <span data-ttu-id="43c73-150">在**连接到服务器**对话框中，在**服务器名称**框中，键入数据库服务器的名称，然后单击**连接**。</span><span class="sxs-lookup"><span data-stu-id="43c73-150">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. <span data-ttu-id="43c73-151">在**对象资源管理器**窗格中，右键单击父服务器节点 (例如， **TESTDB1**)，然后单击**重新启动**。</span><span class="sxs-lookup"><span data-stu-id="43c73-151">In the **Object Explorer** pane, right-click the parent server node (for example, **TESTDB1**), and then click **Restart**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. <span data-ttu-id="43c73-152">在**Microsoft SQL Server Management Studio**对话框中，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="43c73-152">In the **Microsoft SQL Server Management Studio** dialog box, click **Yes**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. <span data-ttu-id="43c73-153">在重新启动该服务，已关闭 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="43c73-153">When the service has restarted, close SQL Server Management Studio.</span></span>

<span data-ttu-id="43c73-154">若要允许 SQL Server 流量通过防火墙，请首先需要知道您的 SQL Server 实例所使用的端口。</span><span class="sxs-lookup"><span data-stu-id="43c73-154">To allow SQL Server traffic through a firewall, you first need to know which ports your SQL Server instance is using.</span></span> <span data-ttu-id="43c73-155">这将取决于如何在 SQL Server 实例已在其中创建和配置：</span><span class="sxs-lookup"><span data-stu-id="43c73-155">This will depend on how the SQL Server instance was created and configured:</span></span>

- <span data-ttu-id="43c73-156">A*默认实例*的 SQL Server 侦听 （和响应） TCP 端口 1433年上的请求。</span><span class="sxs-lookup"><span data-stu-id="43c73-156">A *default instance* of SQL Server listens for (and responds to) requests on TCP port 1433.</span></span>
- <span data-ttu-id="43c73-157">A*命名实例*的 SQL Server 侦听 （和响应） 动态分配的 TCP 端口上的请求。</span><span class="sxs-lookup"><span data-stu-id="43c73-157">A *named instance* of SQL Server listens for (and responds to) requests on a dynamically assigned TCP port.</span></span>
- <span data-ttu-id="43c73-158">如果启用了 SQL Server Browser 服务，客户端可以查询 UDP 端口 1434 以查找要使用特定的 SQL Server 实例的 TCP 端口上的服务。</span><span class="sxs-lookup"><span data-stu-id="43c73-158">If the SQL Server Browser service is enabled, clients can query the service on UDP port 1434 to find out which TCP port to use for a particular SQL Server instance.</span></span> <span data-ttu-id="43c73-159">但是，出于安全原因通常禁用此服务。</span><span class="sxs-lookup"><span data-stu-id="43c73-159">However, this service is often disabled for security reasons.</span></span>

<span data-ttu-id="43c73-160">假设你正在使用的 SQL Server 的默认实例，你需要将防火墙配置为允许流量。</span><span class="sxs-lookup"><span data-stu-id="43c73-160">Assuming that you're using a default instance of SQL Server, you need to configure your firewall to allow traffic.</span></span>

| <span data-ttu-id="43c73-161">方向</span><span class="sxs-lookup"><span data-stu-id="43c73-161">Direction</span></span> | <span data-ttu-id="43c73-162">从端口</span><span class="sxs-lookup"><span data-stu-id="43c73-162">From Port</span></span> | <span data-ttu-id="43c73-163">到端口</span><span class="sxs-lookup"><span data-stu-id="43c73-163">To Port</span></span> | <span data-ttu-id="43c73-164">端口类型</span><span class="sxs-lookup"><span data-stu-id="43c73-164">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="43c73-165">入站</span><span class="sxs-lookup"><span data-stu-id="43c73-165">Inbound</span></span> | <span data-ttu-id="43c73-166">任意</span><span class="sxs-lookup"><span data-stu-id="43c73-166">Any</span></span> | <span data-ttu-id="43c73-167">1433</span><span class="sxs-lookup"><span data-stu-id="43c73-167">1433</span></span> | <span data-ttu-id="43c73-168">TCP</span><span class="sxs-lookup"><span data-stu-id="43c73-168">TCP</span></span> |
| <span data-ttu-id="43c73-169">出站</span><span class="sxs-lookup"><span data-stu-id="43c73-169">Outbound</span></span> | <span data-ttu-id="43c73-170">1433</span><span class="sxs-lookup"><span data-stu-id="43c73-170">1433</span></span> | <span data-ttu-id="43c73-171">任意</span><span class="sxs-lookup"><span data-stu-id="43c73-171">Any</span></span> | <span data-ttu-id="43c73-172">TCP</span><span class="sxs-lookup"><span data-stu-id="43c73-172">TCP</span></span> |
  

> [!NOTE]
> <span data-ttu-id="43c73-173">从技术上讲，客户端计算机将使用 1024年和 5000 之间随机分配的 TCP 端口进行通信使用 SQL Server，并且你可以相应地限制防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="43c73-173">Technically, a client computer will use a randomly assigned TCP port between 1024 and 5000 to communicate with SQL Server, and you can restrict your firewall rules accordingly.</span></span> <span data-ttu-id="43c73-174">SQL Server 端口和防火墙的详细信息，请参阅[to SQL 通过防火墙进行通信所需的 TCP/IP 端口号](https://go.microsoft.com/?linkid=9805125)和[如何： 配置服务器以侦听特定 TCP 端口 （SQL Server 配置管理器）](https://msdn.microsoft.com/library/ms177440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-174">For more information on SQL Server ports and firewalls, see [TCP/IP port numbers required to communicate to SQL over a firewall](https://go.microsoft.com/?linkid=9805125) and [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](https://msdn.microsoft.com/library/ms177440.aspx).</span></span>


<span data-ttu-id="43c73-175">在大多数 Windows Server 环境中，你可能需要在数据库服务器上配置 Windows 防火墙。</span><span class="sxs-lookup"><span data-stu-id="43c73-175">In most Windows Server environments, you'll likely have to configure Windows Firewall on the database server.</span></span> <span data-ttu-id="43c73-176">默认情况下，Windows 防火墙允许所有出站流量，除非规则专门禁止它。</span><span class="sxs-lookup"><span data-stu-id="43c73-176">By default, Windows Firewall allows all outbound traffic unless a rule specifically prohibits it.</span></span> <span data-ttu-id="43c73-177">若要启用你的 web 服务器来访问你的数据库，你需要配置 SQL Server 实例使用的端口号允许 TCP 流量的入站的规则。</span><span class="sxs-lookup"><span data-stu-id="43c73-177">To enable your web server to reach your database, you need to configure an inbound rule that allows TCP traffic on the port number that the SQL Server instance uses.</span></span> <span data-ttu-id="43c73-178">如果你正在使用的 SQL Server 的默认实例，可以使用下一个过程来配置此规则。</span><span class="sxs-lookup"><span data-stu-id="43c73-178">If you're using a default instance of SQL Server, you can use the next procedure to configure this rule.</span></span>

<span data-ttu-id="43c73-179">**若要配置 Windows 防火墙以允许与默认 SQL Server 实例的通信**</span><span class="sxs-lookup"><span data-stu-id="43c73-179">**To configure Windows Firewall to allow communication with a default SQL Server instance**</span></span>

1. <span data-ttu-id="43c73-180">在数据库服务器上，在**启动**菜单上，指向**管理工具**，然后单击**高级安全 Windows 防火墙**。</span><span class="sxs-lookup"><span data-stu-id="43c73-180">On the database server, on the **Start** menu, point to **Administrative Tools**, and then click **Windows Firewall with Advanced Security**.</span></span>
2. <span data-ttu-id="43c73-181">在树视图窗格中，单击**入站规则**。</span><span class="sxs-lookup"><span data-stu-id="43c73-181">In the tree view pane, click **Inbound Rules**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. <span data-ttu-id="43c73-182">在**操作**窗格中，在**入站规则**，单击**新规则**。</span><span class="sxs-lookup"><span data-stu-id="43c73-182">In the **Actions** pane, under **Inbound Rules**, click **New Rule**.</span></span>
4. <span data-ttu-id="43c73-183">在新入站规则向导中，在**规则类型**页上，选择**端口**，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="43c73-183">In the New Inbound Rule Wizard, on the **Rule Type** page, select **Port**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. <span data-ttu-id="43c73-184">上**协议和端口**页上，确保**TCP**选择，然后在**特定本地端口**框中，键入**1433年**，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="43c73-184">On the **Protocol and Ports** page, ensure that **TCP** is selected, and in the **Specific local ports** box, type **1433**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. <span data-ttu-id="43c73-185">上**操作**页上，保留**允许连接**选择和单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="43c73-185">On the **Action** page, leave **Allow the connection** selected and click **Next**.</span></span>
7. <span data-ttu-id="43c73-186">上**配置文件**页上，保留**域**选择，清除**私有**和**公共**复选框，并依次**下一步**。</span><span class="sxs-lookup"><span data-stu-id="43c73-186">On the **Profile** page, leave **Domain** selected, clear the **Private** and **Public** check boxes, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. <span data-ttu-id="43c73-187">上**名称**页上，为规则提供适当描述性名称 (例如， **SQL Server 默认实例 – 网络访问**)，然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="43c73-187">On the **Name** page, give the rule a suitably descriptive name (for example, **SQL Server default instance – network access**), and then click **Finish**.</span></span>

<span data-ttu-id="43c73-188">有关详细信息对于 SQL Server，配置 Windows 防火墙，尤其是当你需要通过非标准或动态端口与 SQL Server 进行通信，请参阅[如何： 为数据库引擎访问配置 Windows 防火墙](https://technet.microsoft.com/library/ms175043.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-188">For more information on configuring Windows Firewall for SQL Server, particularly if you need to communicate with SQL Server over non-standard or dynamic ports, see [How to: Configure a Windows Firewall for Database Engine Access](https://technet.microsoft.com/library/ms175043.aspx).</span></span>

## <a name="configure-logins-and-database-permissions"></a><span data-ttu-id="43c73-189">配置登录名和数据库权限</span><span class="sxs-lookup"><span data-stu-id="43c73-189">Configure Logins and Database Permissions</span></span>

<span data-ttu-id="43c73-190">在部署 web 应用程序到 Internet 信息服务 (IIS) 时，应用程序使用的应用程序池标识运行。</span><span class="sxs-lookup"><span data-stu-id="43c73-190">When you deploy a web application to Internet Information Services (IIS), the application runs using the identity of the application pool.</span></span> <span data-ttu-id="43c73-191">在域环境中，应用程序池标识使用在其上运行来访问网络资源的服务器的计算机帐户。</span><span class="sxs-lookup"><span data-stu-id="43c73-191">In a domain environment, application pool identities use the machine account of the server on which they run to access network resources.</span></span> <span data-ttu-id="43c73-192">计算机帐户采用以下形式<em>[域名]</em><strong>\</ g ><em>[计算机名称]</em><strong>$</strong>&#x2014;例如，<strong>FABRIKAM\TESTWEB1$</strong>。</span><span class="sxs-lookup"><span data-stu-id="43c73-192">Machine accounts take the form <em>[domain name]</em><strong>\</strong><em>[machine name]</em><strong>$</strong>&#x2014;for example, <strong>FABRIKAM\TESTWEB1$</strong>.</span></span> <span data-ttu-id="43c73-193">若要允许跨网络访问的数据库将 web 应用程序，你需要：</span><span class="sxs-lookup"><span data-stu-id="43c73-193">To allow your web application to access a database across the network, you need to:</span></span>

- <span data-ttu-id="43c73-194">将 web 服务器计算机帐户的登录名添加到 SQL Server 实例。</span><span class="sxs-lookup"><span data-stu-id="43c73-194">Add a login for the web server machine account to the SQL Server instance.</span></span>
- <span data-ttu-id="43c73-195">计算机帐户登录名映射到任何所需的数据库角色 (通常**db\_datareader**和**db\_datawriter**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-195">Map the machine account login to any required database roles (typically **db\_datareader** and **db\_datawriter**).</span></span>

<span data-ttu-id="43c73-196">如果在服务器场中，而不是一台服务器上运行 web 应用程序，你将需要重复执行这些过程，以服务器场中每个 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="43c73-196">If your web application is running on a server farm, rather than a single server, you'll need to repeat these procedures for every web server in the server farm.</span></span>

> [!NOTE]
> <span data-ttu-id="43c73-197">应用程序池标识和访问网络资源的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="43c73-197">For more information on application pool identities and accessing network resources, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="43c73-198">您可以达到这些任务以各种方式。</span><span class="sxs-lookup"><span data-stu-id="43c73-198">You can approach these tasks in various ways.</span></span> <span data-ttu-id="43c73-199">若要创建登录名，您可以：</span><span class="sxs-lookup"><span data-stu-id="43c73-199">To create the login, you can either:</span></span>

- <span data-ttu-id="43c73-200">使用 TRANSACT-SQL 或 SQL Server Management Studio 在数据库服务器上手动创建登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-200">Create the login manually on the database server, using Transact-SQL or SQL Server Management Studio.</span></span>
- <span data-ttu-id="43c73-201">使用 SQL Server 2008 服务器项目在 Visual Studio 中创建和部署该登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-201">Use a SQL Server 2008 Server Project in Visual Studio to create and deploy the login.</span></span>

<span data-ttu-id="43c73-202">SQL Server 登录名是一个服务器级对象，而不只是数据库级别对象，因此不依赖于你想要部署的数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-202">A SQL Server login is a server-level object, rather than a database-level object, so it's not dependent on the database you want to deploy.</span></span> <span data-ttu-id="43c73-203">在这种情况下，你可以在任何时刻，创建登录名和最简单的方法通常是登录名之前手动创建数据库服务器上开始部署数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-203">As such, you can create the login at any point, and the easiest approach is often to create the login manually on the database server before you start deploying databases.</span></span> <span data-ttu-id="43c73-204">下一步过程可用于在 SQL Server Management Studio 中创建一个登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-204">You can use the next procedure to create a login in SQL Server Management Studio.</span></span>

<span data-ttu-id="43c73-205">**创建 web 服务器计算机帐户的 SQL Server 登录名**</span><span class="sxs-lookup"><span data-stu-id="43c73-205">**To create a SQL Server login for the web server machine account**</span></span>

1. <span data-ttu-id="43c73-206">在数据库服务器上，在**启动**菜单上，指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，然后单击**SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="43c73-206">On the database server, on the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="43c73-207">在**连接到服务器**对话框中，在**服务器名称**框中，键入数据库服务器的名称，然后单击**连接**。</span><span class="sxs-lookup"><span data-stu-id="43c73-207">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. <span data-ttu-id="43c73-208">在**对象资源管理器**窗格中，右键单击**安全**，指向**新建**，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="43c73-208">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
4. <span data-ttu-id="43c73-209">在**登录名-新建**对话框中，在**登录名**框中，键入你的 web 服务器计算机帐户的名称 (例如， **FABRIKAM\TESTWEB1$**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-209">In the **Login – New** dialog box, in the **Login name** box, type the name of your web server machine account (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. <span data-ttu-id="43c73-210">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="43c73-210">Click **OK**.</span></span>

<span data-ttu-id="43c73-211">此时，你的数据库服务器是可供 Web 部署发布。</span><span class="sxs-lookup"><span data-stu-id="43c73-211">At this point, your database server is ready for Web Deploy publishing.</span></span> <span data-ttu-id="43c73-212">但是，你将部署任何解决方案将不起作用之前机帐户登录名映射到所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-212">However, any solutions you deploy won't work until you map the machine account login to the required database roles.</span></span> <span data-ttu-id="43c73-213">将登录名映射到数据库角色需要大量更认为，作为你不能映射角色直到检查完已部署数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-213">Mapping the login to database roles requires a lot more thought, as you can't map roles until after you've deployed the database.</span></span> <span data-ttu-id="43c73-214">若要将计算机帐户登录名映射到所需的数据库角色中，您可以：</span><span class="sxs-lookup"><span data-stu-id="43c73-214">To map the machine account login to the required database roles, you can either:</span></span>

- <span data-ttu-id="43c73-215">数据库角色为登录名分配手动之后你已将数据库部署第一次。</span><span class="sxs-lookup"><span data-stu-id="43c73-215">Assign the database roles to the login manually, after you've deployed the database for the first time.</span></span>
- <span data-ttu-id="43c73-216">使用后期部署脚本将数据库角色分配给该登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-216">Use a post-deployment script to assign the database roles to the login.</span></span>

<span data-ttu-id="43c73-217">自动创建登录名和数据库角色映射的详细信息，请参阅[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="43c73-217">For more information on automating the creation of logins and database role mappings, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="43c73-218">或者下, 一步过程可用于手动将计算机帐户登录名映射到所需的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-218">Alternatively, you can use the next procedure to map the machine account login to the required database roles manually.</span></span> <span data-ttu-id="43c73-219">请记住，你无法执行此过程之前*后*已部署数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-219">Remember that you can't perform this procedure until *after* you've deployed the database.</span></span>

<span data-ttu-id="43c73-220">**若要将数据库角色映射到 web 服务器计算机帐户登录**</span><span class="sxs-lookup"><span data-stu-id="43c73-220">**To map database roles to the web server machine account login**</span></span>

1. <span data-ttu-id="43c73-221">像以前那样打开 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="43c73-221">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="43c73-222">在**对象资源管理器**窗格中，展开**安全**节点，展开**登录名**节点，然后双击机帐户登录名 (例如， **FABRIKAM\TESTWEB1$**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-222">In the **Object Explorer** pane, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. <span data-ttu-id="43c73-223">在**登录属性**对话框中，单击**用户映射**。</span><span class="sxs-lookup"><span data-stu-id="43c73-223">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="43c73-224">在**映射到此登录名的用户**表中，选择你的数据库的名称 (例如， **ContactManager**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-224">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="43c73-225">在**数据库角色成员身份：** *[数据库名称]*列表中，选择所需的权限。</span><span class="sxs-lookup"><span data-stu-id="43c73-225">In the **Database role membership for:** *[database name]* list, select the permissions required.</span></span> <span data-ttu-id="43c73-226">在联系人管理器示例解决方案中，您必须选择**db\_datareader**和**db\_datawriter**角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-226">In the case of the Contact Manager sample solution, you must select the **db\_datareader** and **db\_datawriter** roles.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. <span data-ttu-id="43c73-227">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="43c73-227">Click **OK**.</span></span>

<span data-ttu-id="43c73-228">时手动将数据库角色映射通常绰绰有余测试环境，它是自动进行的或一键式部署到过渡环境或生产环境不需要的。</span><span class="sxs-lookup"><span data-stu-id="43c73-228">While manually mapping database roles is often more than adequate for test environments, it's less desirable for automated or one-click deployments to staging or production environments.</span></span> <span data-ttu-id="43c73-229">你可以找到有关自动执行这种使用中的后期部署脚本的任务的详细信息[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="43c73-229">You can find more information on automating this kind of task using post-deployment scripts in [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43c73-230">服务器项目和数据库项目的详细信息，请参阅[Visual Studio 2010 SQL Server 数据库项目](https://msdn.microsoft.com/library/ff678491.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c73-230">For more information on server projects and database projects, see [Visual Studio 2010 SQL Server Database Projects](https://msdn.microsoft.com/library/ff678491.aspx).</span></span>


## <a name="configure-permissions-for-the-deployment-account"></a><span data-ttu-id="43c73-231">配置部署帐户的权限</span><span class="sxs-lookup"><span data-stu-id="43c73-231">Configure Permissions for the Deployment Account</span></span>

<span data-ttu-id="43c73-232">如果你将用于运行部署的帐户不是 SQL Server 管理员，你将需要创建此帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="43c73-232">If the account that you'll use to run the deployment is not a SQL Server administrator, you'll also need to create a login for this account.</span></span> <span data-ttu-id="43c73-233">若要创建数据库，帐户必须属于**dbcreator**服务器角色或拥有同等权限。</span><span class="sxs-lookup"><span data-stu-id="43c73-233">In order to create the database, the account must be a member of the **dbcreator** server role or have equivalent permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="43c73-234">当你使用 Web 部署或 VSDBCMD 将数据库部署时，你可以使用 Windows 凭据或 SQL Server 凭据，（如果您的 SQL Server 实例配置为支持混合的模式身份验证）。</span><span class="sxs-lookup"><span data-stu-id="43c73-234">When you use Web Deploy or VSDBCMD to deploy a database, you can use Windows credentials or SQL Server credentials (if your SQL Server instance is configured to support mixed mode authentication).</span></span> <span data-ttu-id="43c73-235">下一步过程假设你想要使用 Windows 凭据，但无需进行任何停止你从在你配置的部署时连接字符串中指定的 SQL Server 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="43c73-235">The next procedure assumes that you want to use Windows credentials, but there's nothing stopping you from specifying a SQL Server user name and password in your connection string when you configure the deployment.</span></span>


<span data-ttu-id="43c73-236">**若要设置的部署帐户的访问权限**</span><span class="sxs-lookup"><span data-stu-id="43c73-236">**To set up permissions for the deployment account**</span></span>

1. <span data-ttu-id="43c73-237">像以前那样打开 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="43c73-237">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="43c73-238">在**对象资源管理器**窗格中，右键单击**安全**，指向**新建**，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="43c73-238">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
3. <span data-ttu-id="43c73-239">在**登录名-新建**对话框中，在**登录名**框中，键入你部署的帐户的名称 (例如， **FABRIKAM\matt**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-239">In the **Login – New** dialog box, in the **Login name** box, type the name of your deployment account (for example, **FABRIKAM\matt**).</span></span>
4. <span data-ttu-id="43c73-240">在**选择页**窗格中，单击**服务器角色**。</span><span class="sxs-lookup"><span data-stu-id="43c73-240">In the **Select a page** pane, click **Server Roles**.</span></span>
5. <span data-ttu-id="43c73-241">选择**dbcreator**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="43c73-241">Select **dbcreator**, and then click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

<span data-ttu-id="43c73-242">若要支持后续的部署，你将还需要部署将帐户添加到**db\_所有者**上首次部署后的数据库角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-242">To support subsequent deployments, you'll also need to add the deploying account to the **db\_owner** role on the database after the first deployment.</span></span> <span data-ttu-id="43c73-243">这是因为在后续部署上您要修改现有数据库架构，而不是创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-243">This is because on subsequent deployments you're modifying the schema of an existing database, rather than creating a new database.</span></span> <span data-ttu-id="43c73-244">如前一部分中所述，无法将用户添加到数据库角色，直到你已创建数据库，原因很明显。</span><span class="sxs-lookup"><span data-stu-id="43c73-244">As described in the previous section, you can't add a user to a database role until you've created the database, for obvious reasons.</span></span>

<span data-ttu-id="43c73-245">**若要部署的帐户登录名映射到的数据库\_所有者数据库角色**</span><span class="sxs-lookup"><span data-stu-id="43c73-245">**To map the deployment account login to the db\_owner database role**</span></span>

1. <span data-ttu-id="43c73-246">像以前那样打开 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="43c73-246">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="43c73-247">在**对象资源管理器**窗口中，展开**安全**节点，展开**登录名**节点，然后双击机帐户登录名 (例如， **FABRIKAM\matt**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-247">In the **Object Explorer** window, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\matt**).</span></span>
3. <span data-ttu-id="43c73-248">在**登录属性**对话框中，单击**用户映射**。</span><span class="sxs-lookup"><span data-stu-id="43c73-248">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="43c73-249">在**映射到此登录名的用户**表中，选择你的数据库的名称 (例如， **ContactManager**)。</span><span class="sxs-lookup"><span data-stu-id="43c73-249">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="43c73-250">在**数据库角色成员身份：** *[数据库名称]*列表中，选择**db\_所有者**角色。</span><span class="sxs-lookup"><span data-stu-id="43c73-250">In the **Database role membership for:** *[database name]* list, select the **db\_owner** role.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. <span data-ttu-id="43c73-251">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="43c73-251">Click **OK**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="43c73-252">结束语</span><span class="sxs-lookup"><span data-stu-id="43c73-252">Conclusion</span></span>

<span data-ttu-id="43c73-253">现在，你的数据库服务器应准备就绪可以接受远程数据库部署，以允许远程 IIS web 服务器以访问您的数据库。</span><span class="sxs-lookup"><span data-stu-id="43c73-253">Your database server should now be ready to accept remote database deployments and to allow remote IIS web servers to access your databases.</span></span> <span data-ttu-id="43c73-254">在尝试部署和使用数据库之前，你可能想要检查这些要点：</span><span class="sxs-lookup"><span data-stu-id="43c73-254">Before you attempt to deploy and use databases, you may want to check these key points:</span></span>

- <span data-ttu-id="43c73-255">已配置为接受远程 TCP/IP 连接的 SQL Server 吗？</span><span class="sxs-lookup"><span data-stu-id="43c73-255">Have you configured SQL Server to accept remote TCP/IP connections?</span></span>
- <span data-ttu-id="43c73-256">已配置任何防火墙以允许 SQL Server 流量吗？</span><span class="sxs-lookup"><span data-stu-id="43c73-256">Have you configured any firewalls to permit SQL Server traffic?</span></span>
- <span data-ttu-id="43c73-257">你是否已创建将访问 SQL Server 的每个 web 服务器计算机帐户登录？</span><span class="sxs-lookup"><span data-stu-id="43c73-257">Have you created a machine account login for every web server that will access SQL Server?</span></span>
- <span data-ttu-id="43c73-258">您的数据库部署是否包括一个脚本以创建用户角色映射，或你是否需要在首次部署数据库后手动创建这些？</span><span class="sxs-lookup"><span data-stu-id="43c73-258">Does your database deployment include a script to create user role mappings, or do you need to create these manually after you deploy the database for the first time?</span></span>
- <span data-ttu-id="43c73-259">你已创建部署帐户的登录名并添加到**dbcreator**服务器角色？</span><span class="sxs-lookup"><span data-stu-id="43c73-259">Have you created a login for the deployment account and added it to the **dbcreator** server role?</span></span>

## <a name="further-reading"></a><span data-ttu-id="43c73-260">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="43c73-260">Further Reading</span></span>

<span data-ttu-id="43c73-261">有关部署数据库项目的指南，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="43c73-261">For guidance on deploying database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="43c73-262">通过运行后期部署脚本创建数据库角色成员身份的指南，请参阅[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="43c73-262">For guidance on creating database role memberships by running a post-deployment script, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="43c73-263">有关如何迎接唯一的部署带来成员资格数据库会带来的挑战的指南，请参阅[将成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="43c73-263">For guidance on how to meet the unique deployment challenges that membership databases pose, see [Deploying Membership Databases to Enterprise Environments](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="43c73-264">[上一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [下一页](creating-a-server-farm-with-the-web-farm-framework.md)</span><span class="sxs-lookup"><span data-stu-id="43c73-264">[Previous](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
[Next](creating-a-server-farm-with-the-web-farm-framework.md)</span></span>
