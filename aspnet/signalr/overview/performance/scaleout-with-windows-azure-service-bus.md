---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: "使用 Azure 服务总线的 SignalR 扩展 |Microsoft 文档"
author: MikeWasson
description: "在此主题 Visual Studio 2013.NET 4.5 SignalR 版本的软件版本使用，本主题中，此主题的 SignalR 1.x 版本 2 早期版本..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 7cb68d578fee8d6ee036f8fb096ba45e0c8ef3d6
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="1851b-103">使用 Azure 服务总线的 SignalR 扩展</span><span class="sxs-lookup"><span data-stu-id="1851b-103">SignalR Scaleout with Azure Service Bus</span></span>
====================
<span data-ttu-id="1851b-104">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="1851b-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="1851b-105">在本教程中，你将部署到 Windows Azure Web 角色，使用服务总线底板来分配到每个角色实例的消息的 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1851b-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="1851b-106">(你还可以使用与 Service Bus 底板[web 应用在 Azure App Service](https://docs.microsoft.com/azure/app-service-web/)。)</span><span class="sxs-lookup"><span data-stu-id="1851b-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="1851b-107">先决条件：</span><span class="sxs-lookup"><span data-stu-id="1851b-107">Prerequisites:</span></span>

- <span data-ttu-id="1851b-108">一个 Windows Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="1851b-108">A Windows Azure account.</span></span>
- <span data-ttu-id="1851b-109">[Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="1851b-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="1851b-110">Visual Studio 2012 或 2013年。</span><span class="sxs-lookup"><span data-stu-id="1851b-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="1851b-111">服务总线底板也是与兼容[Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)，版本 1.1。</span><span class="sxs-lookup"><span data-stu-id="1851b-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="1851b-112">但是，它不是与 Service Bus for Windows Server 的 1.0 版兼容的。</span><span class="sxs-lookup"><span data-stu-id="1851b-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="1851b-113">定价</span><span class="sxs-lookup"><span data-stu-id="1851b-113">Pricing</span></span>

<span data-ttu-id="1851b-114">服务总线底板使用主题发送消息。</span><span class="sxs-lookup"><span data-stu-id="1851b-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="1851b-115">有关最新定价的信息，请参阅[Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="1851b-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="1851b-116">在撰写本文时，你可以向发送 1,000,000 消息每月小于 1 美元。</span><span class="sxs-lookup"><span data-stu-id="1851b-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="1851b-117">底板发送 SignalR hub 方法每次调用服务总线消息。</span><span class="sxs-lookup"><span data-stu-id="1851b-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="1851b-118">此外，还存在的连接、 断开连接、 联接或保留组等一些控制消息。</span><span class="sxs-lookup"><span data-stu-id="1851b-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="1851b-119">在大多数应用程序，大多数消息流量将中心方法调用。</span><span class="sxs-lookup"><span data-stu-id="1851b-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="1851b-120">概述</span><span class="sxs-lookup"><span data-stu-id="1851b-120">Overview</span></span>

<span data-ttu-id="1851b-121">我们获取详细的教程之前，以下是将要执行的操作的快速概览。</span><span class="sxs-lookup"><span data-stu-id="1851b-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="1851b-122">使用 Windows Azure 门户创建新的 Service Bus 命名空间。</span><span class="sxs-lookup"><span data-stu-id="1851b-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="1851b-123">将这些 NuGet 包添加到你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="1851b-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="1851b-124">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="1851b-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="1851b-125">Microsoft.AspNet.SignalR.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="1851b-125">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="1851b-126">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1851b-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="1851b-127">将以下代码添加到 Startup.cs 配置底板：</span><span class="sxs-lookup"><span data-stu-id="1851b-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="1851b-128">此代码使用的默认值配置底板[TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1851b-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="1851b-129">有关更改这些值的信息，请参阅[SignalR 性能： 向外缩放度量值](signalr-performance.md#scaleout_metrics)。</span><span class="sxs-lookup"><span data-stu-id="1851b-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="1851b-130">对于每个应用程序，为"YourAppName"选取一个不同的值。</span><span class="sxs-lookup"><span data-stu-id="1851b-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="1851b-131">不要跨多个应用程序中使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="1851b-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="1851b-132">创建 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="1851b-132">Create the Azure Services</span></span>

<span data-ttu-id="1851b-133">中所述创建云服务，[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)。</span><span class="sxs-lookup"><span data-stu-id="1851b-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="1851b-134">按照部分中的步骤"如何： 创建云服务使用快速创建"。</span><span class="sxs-lookup"><span data-stu-id="1851b-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="1851b-135">对于本教程中，你不需要上载证书。</span><span class="sxs-lookup"><span data-stu-id="1851b-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="1851b-136">创建新的 Service Bus 命名空间中所述[如何使用 Service Bus 主题/订阅到](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="1851b-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="1851b-137">按照部分"创建服务 Namespace"中的步骤。</span><span class="sxs-lookup"><span data-stu-id="1851b-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="1851b-138">请确保选择的相同区域的云服务以及服务总线命名空间。</span><span class="sxs-lookup"><span data-stu-id="1851b-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="1851b-139">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="1851b-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="1851b-140">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1851b-140">Start Visual Studio.</span></span> <span data-ttu-id="1851b-141">从**文件**菜单上，单击**新项目**。</span><span class="sxs-lookup"><span data-stu-id="1851b-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="1851b-142">在**新项目**对话框框中，展开**Visual C#**。</span><span class="sxs-lookup"><span data-stu-id="1851b-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="1851b-143">下**已安装的模板**，选择**云**，然后选择**Windows Azure 云服务**。</span><span class="sxs-lookup"><span data-stu-id="1851b-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="1851b-144">保留默认.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="1851b-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="1851b-145">将应用程序 ChatService，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="1851b-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="1851b-146">在**新建 Windows Azure 云服务**对话框中，选择 ASP.NET Web 角色。</span><span class="sxs-lookup"><span data-stu-id="1851b-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="1851b-147">单击右箭头按钮 (**&gt;**) 将该角色添加到你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="1851b-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="1851b-148">鼠标悬停在该新角色，因此可见的铅笔图标。</span><span class="sxs-lookup"><span data-stu-id="1851b-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="1851b-149">单击此图标来重命名该角色。</span><span class="sxs-lookup"><span data-stu-id="1851b-149">Click this icon to rename the role.</span></span> <span data-ttu-id="1851b-150">将"SignalRChat"的角色，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="1851b-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="1851b-151">在**新建 ASP.NET 项目**对话框中，选择**MVC**，单击确定。</span><span class="sxs-lookup"><span data-stu-id="1851b-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="1851b-152">项目向导将创建两个项目：</span><span class="sxs-lookup"><span data-stu-id="1851b-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="1851b-153">ChatService： 此项目是 Windows Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1851b-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="1851b-154">它定义 Azure 角色和其他配置选项。</span><span class="sxs-lookup"><span data-stu-id="1851b-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="1851b-155">SignalRChat： 此项目是你的 ASP.NET MVC 5 项目。</span><span class="sxs-lookup"><span data-stu-id="1851b-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="1851b-156">创建 SignalR 聊天应用程序</span><span class="sxs-lookup"><span data-stu-id="1851b-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="1851b-157">若要创建聊天应用程序，按照本教程中的步骤[SignalR 和 MVC 5 入门](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="1851b-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="1851b-158">使用 NuGet 安装所需的库。</span><span class="sxs-lookup"><span data-stu-id="1851b-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="1851b-159">从**工具**菜单上，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="1851b-159">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1851b-160">在**程序包管理器控制台**窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="1851b-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="1851b-161">使用`-ProjectName`选项以将包安装到 ASP.NET MVC 项目中，而不是 Windows Azure 项目。</span><span class="sxs-lookup"><span data-stu-id="1851b-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="1851b-162">配置底板</span><span class="sxs-lookup"><span data-stu-id="1851b-162">Configure the Backplane</span></span>

<span data-ttu-id="1851b-163">在你的应用程序 Startup.cs 文件中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="1851b-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="1851b-164">现在，你需要获取服务总线连接字符串。</span><span class="sxs-lookup"><span data-stu-id="1851b-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="1851b-165">在 Azure 门户中，选择你创建的服务总线命名空间，然后单击访问密钥图标。</span><span class="sxs-lookup"><span data-stu-id="1851b-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="1851b-166">将连接字符串复制到剪贴板，然后将其粘贴到*connectionString*变量。</span><span class="sxs-lookup"><span data-stu-id="1851b-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="1851b-167">将部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="1851b-167">Deploy to Azure</span></span>

<span data-ttu-id="1851b-168">在解决方案资源管理器，展开**角色**ChatService 项目中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1851b-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="1851b-169">右键单击 SignalRChat 角色并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="1851b-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="1851b-170">选择**配置**选项卡。下**实例**选择 2。</span><span class="sxs-lookup"><span data-stu-id="1851b-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="1851b-171">此外可以将 VM 大小设置为**特小**。</span><span class="sxs-lookup"><span data-stu-id="1851b-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="1851b-172">保存更改。</span><span class="sxs-lookup"><span data-stu-id="1851b-172">Save the changes.</span></span>

<span data-ttu-id="1851b-173">在解决方案资源管理器，右键单击 ChatService 项目。</span><span class="sxs-lookup"><span data-stu-id="1851b-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="1851b-174">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="1851b-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="1851b-175">如果这是你第一次发布到 Windows Azure，你必须下载您的凭据。</span><span class="sxs-lookup"><span data-stu-id="1851b-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="1851b-176">在**发布**向导中，单击"登录以下载凭据"。</span><span class="sxs-lookup"><span data-stu-id="1851b-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="1851b-177">这将提示你登录到 Windows Azure 门户并下载发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="1851b-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="1851b-178">单击**导入**和选择你下载的发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="1851b-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="1851b-179">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="1851b-179">Click **Next**.</span></span> <span data-ttu-id="1851b-180">在**发布设置**对话框下**云服务**，选择前面创建的云服务。</span><span class="sxs-lookup"><span data-stu-id="1851b-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="1851b-181">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="1851b-181">Click **Publish**.</span></span> <span data-ttu-id="1851b-182">它可能需要几分钟来部署应用程序和启动 Vm。</span><span class="sxs-lookup"><span data-stu-id="1851b-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="1851b-183">现在运行聊天应用程序时，角色实例将通过 Azure Service Bus，使用服务总线主题通信。</span><span class="sxs-lookup"><span data-stu-id="1851b-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="1851b-184">主题是消息队列，它允许多个订阅服务器。</span><span class="sxs-lookup"><span data-stu-id="1851b-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="1851b-185">底板会自动创建主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="1851b-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="1851b-186">若要查看的订阅和消息活动，打开 Azure 门户，选择 Service Bus 命名空间，然后单击"主题"。</span><span class="sxs-lookup"><span data-stu-id="1851b-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="1851b-187">它可能需要几分钟时间才会显示在仪表板中的消息活动。</span><span class="sxs-lookup"><span data-stu-id="1851b-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="1851b-188">SignalR 管理主题生存期。</span><span class="sxs-lookup"><span data-stu-id="1851b-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="1851b-189">只要应用程序部署，请勿尝试手动删除主题或主题上更改设置。</span><span class="sxs-lookup"><span data-stu-id="1851b-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1851b-190">疑难解答</span><span class="sxs-lookup"><span data-stu-id="1851b-190">Troubleshooting</span></span>

<span data-ttu-id="1851b-191">**System.InvalidOperationException"唯一受支持的隔离级别是 IsolationLevel.Serializable"。**</span><span class="sxs-lookup"><span data-stu-id="1851b-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="1851b-192">如果操作的事务级别设置为可能出现此错误`Serializable`。</span><span class="sxs-lookup"><span data-stu-id="1851b-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="1851b-193">验证与其他事务级别正在执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="1851b-193">Verify that no operations are being performed with other transaction levels.</span></span>
