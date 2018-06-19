---
uid: signalr/overview/performance/scaleout-with-sql-server
title: 与 SQL Server 的 SignalR 扩展 |Microsoft 文档
author: MikeWasson
description: Visual Studio 2013.NET 4.5 SignalR 本主题中使用软件版本的早期版本的信息的本主题的版本 2 早期版本...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: b3189c36fc076333c0c6007bd039b12e03d63bc8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874364"
---
<a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="6c668-103">与 SQL Server 的 SignalR 扩展</span><span class="sxs-lookup"><span data-stu-id="6c668-103">SignalR Scaleout with SQL Server</span></span>
====================
<span data-ttu-id="6c668-104">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="6c668-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="6c668-105">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6c668-105">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="6c668-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6c668-106">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="6c668-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6c668-107">.NET 4.5</span></span>
> - <span data-ttu-id="6c668-108">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="6c668-108">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="6c668-109">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="6c668-109">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="6c668-110">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6c668-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="6c668-111">问题和意见</span><span class="sxs-lookup"><span data-stu-id="6c668-111">Questions and comments</span></span>
> 
> <span data-ttu-id="6c668-112">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="6c668-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6c668-113">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="6c668-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="6c668-114">在本教程中，你将使用 SQL Server 以将消息分布到的 SignalR 应用程序部署在两个单独的 IIS 实例。</span><span class="sxs-lookup"><span data-stu-id="6c668-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="6c668-115">此外可以在单个测试计算机上，运行本教程，但若要获取完整的效果，你需要 SignalR 将应用部署到两个或多个服务器。</span><span class="sxs-lookup"><span data-stu-id="6c668-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="6c668-116">在一台服务器，或单独的专用服务器上，还必须安装 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="6c668-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="6c668-117">另一种方法是运行在 Azure 上使用虚拟机的教程。</span><span class="sxs-lookup"><span data-stu-id="6c668-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="6c668-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="6c668-118">Prerequisites</span></span>

<span data-ttu-id="6c668-119">Microsoft SQL Server 2005 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6c668-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="6c668-120">底板支持桌面和服务器版本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="6c668-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="6c668-121">它不支持 SQL Server Compact Edition 或 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="6c668-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="6c668-122">（如果你的应用程序托管在 Azure 上，请考虑服务总线底板相反。）</span><span class="sxs-lookup"><span data-stu-id="6c668-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="6c668-123">概述</span><span class="sxs-lookup"><span data-stu-id="6c668-123">Overview</span></span>

<span data-ttu-id="6c668-124">我们获取详细的教程之前，以下是将要执行的操作的快速概览。</span><span class="sxs-lookup"><span data-stu-id="6c668-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="6c668-125">创建一个新的空数据库。</span><span class="sxs-lookup"><span data-stu-id="6c668-125">Create a new empty database.</span></span> <span data-ttu-id="6c668-126">底板将此数据库中创建必要的表。</span><span class="sxs-lookup"><span data-stu-id="6c668-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="6c668-127">将这些 NuGet 包添加到你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="6c668-127">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="6c668-128">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="6c668-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="6c668-129">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="6c668-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="6c668-130">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6c668-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="6c668-131">将以下代码添加到 Startup.cs 配置底板：</span><span class="sxs-lookup"><span data-stu-id="6c668-131">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="6c668-132">此代码使用的默认值配置底板[TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6c668-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="6c668-133">有关更改这些值的信息，请参阅[SignalR 性能： 向外缩放度量值](signalr-performance.md#scaleout_metrics)。</span><span class="sxs-lookup"><span data-stu-id="6c668-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span> 

## <a name="configure-the-database"></a><span data-ttu-id="6c668-134">配置数据库</span><span class="sxs-lookup"><span data-stu-id="6c668-134">Configure the Database</span></span>

<span data-ttu-id="6c668-135">确定应用程序是否将使用 Windows 身份验证或 SQL Server 身份验证来访问数据库。</span><span class="sxs-lookup"><span data-stu-id="6c668-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="6c668-136">无论如何，请确保数据库用户有权登录、 创建架构，并创建表。</span><span class="sxs-lookup"><span data-stu-id="6c668-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="6c668-137">创建用于底板以使用新的数据库。</span><span class="sxs-lookup"><span data-stu-id="6c668-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="6c668-138">你可以为数据库指定任何名称。</span><span class="sxs-lookup"><span data-stu-id="6c668-138">You can give the database any name.</span></span> <span data-ttu-id="6c668-139">不需要在数据库中; 中创建的任何表底板将创建必要的表。</span><span class="sxs-lookup"><span data-stu-id="6c668-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="6c668-140">启用 Service Broker</span><span class="sxs-lookup"><span data-stu-id="6c668-140">Enable Service Broker</span></span>

<span data-ttu-id="6c668-141">建议为底板数据库启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="6c668-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="6c668-142">Service Broker 提供的消息和队列在 SQL Server，这样就更有效地接收更新底板中的本机支持。</span><span class="sxs-lookup"><span data-stu-id="6c668-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="6c668-143">（但是，底板还未工作 Service Broker。）</span><span class="sxs-lookup"><span data-stu-id="6c668-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="6c668-144">若要检查是否启用 Service Broker，请查询**是\_broker\_启用**中的列**sys.databases**目录视图。</span><span class="sxs-lookup"><span data-stu-id="6c668-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="6c668-145">若要启用 Service Broker，请使用以下 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="6c668-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="6c668-146">如果此查询出现死锁，请确保没有连接到的数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="6c668-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>


<span data-ttu-id="6c668-147">如果已启用跟踪，则跟踪还将显示是否已启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="6c668-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="6c668-148">创建 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="6c668-148">Create a SignalR Application</span></span>

<span data-ttu-id="6c668-149">按照这些教程任一创建 SignalR 应用程序：</span><span class="sxs-lookup"><span data-stu-id="6c668-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="6c668-150">开始使用 SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="6c668-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="6c668-151">SignalR 2.0 和 MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="6c668-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="6c668-152">接下来，我们将修改的聊天应用程序，以支持与 SQL Server 的向外缩放。</span><span class="sxs-lookup"><span data-stu-id="6c668-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="6c668-153">首先，将 SignalR.SqlServer NuGet 包添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="6c668-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="6c668-154">在 Visual Studio 中，从**工具**菜单上，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="6c668-154">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="6c668-155">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="6c668-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="6c668-156">接下来，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="6c668-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="6c668-157">以下代码添加到**配置**方法：</span><span class="sxs-lookup"><span data-stu-id="6c668-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="6c668-158">部署并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="6c668-158">Deploy and Run the Application</span></span>

<span data-ttu-id="6c668-159">准备您的 Windows 服务器实例部署 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6c668-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="6c668-160">添加 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="6c668-160">Add the IIS role.</span></span> <span data-ttu-id="6c668-161">包括"应用程序开发"功能，包括 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="6c668-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="6c668-162">此外包括管理服务 （列于"管理工具"下）。</span><span class="sxs-lookup"><span data-stu-id="6c668-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="6c668-163">**安装 Web 部署 3.0。**</span><span class="sxs-lookup"><span data-stu-id="6c668-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="6c668-164">当你运行 IIS 管理器，它将提示你安装 Microsoft Web 平台，或者可以[下载 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="6c668-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="6c668-165">在平台安装程序中，搜索 Web 部署并安装 Web 部署 3.0</span><span class="sxs-lookup"><span data-stu-id="6c668-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="6c668-166">检查 Web 管理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="6c668-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="6c668-167">如果没有，请启动服务。</span><span class="sxs-lookup"><span data-stu-id="6c668-167">If not, start the service.</span></span> <span data-ttu-id="6c668-168">（如果你看不到 Web 管理服务中的 Windows 服务的列表，请确保你添加的 IIS 角色时安装管理服务。）</span><span class="sxs-lookup"><span data-stu-id="6c668-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="6c668-169">最后，打开 TCP 端口 8172。</span><span class="sxs-lookup"><span data-stu-id="6c668-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="6c668-170">这是 Web 部署工具使用的端口。</span><span class="sxs-lookup"><span data-stu-id="6c668-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="6c668-171">现在你已准备好部署到服务器从你的开发计算机的 Visual Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="6c668-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="6c668-172">在解决方案资源管理器，右键单击解决方案，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="6c668-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="6c668-173">有关更多详细有关 web 部署的文档，请参阅[for Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="6c668-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="6c668-174">如果你部署到两个服务器应用程序，可以在一个单独的浏览器窗口中打开每个实例，并查看每个接收来自其他 SignalR 消息。</span><span class="sxs-lookup"><span data-stu-id="6c668-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="6c668-175">（当然，在生产环境中，两台服务器将位于以下位置负载平衡器之后。）</span><span class="sxs-lookup"><span data-stu-id="6c668-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="6c668-176">运行应用程序后，你可以看到 SignalR 自动具有在数据库中创建表：</span><span class="sxs-lookup"><span data-stu-id="6c668-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="6c668-177">SignalR 管理表。</span><span class="sxs-lookup"><span data-stu-id="6c668-177">SignalR manages the tables.</span></span> <span data-ttu-id="6c668-178">只要应用程序部署，不删除行、 修改表中，和等等。</span><span class="sxs-lookup"><span data-stu-id="6c668-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
