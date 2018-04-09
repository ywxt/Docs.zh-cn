---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: 托管的 Azure 辅助角色的 OWIN |Microsoft 文档
author: MikeWasson
description: 本教程演示如何自承载在 Microsoft Azure 辅助角色中的 OWIN。 打开 Web 接口的.NET (OWIN) 定义.NET web 服务器之间的抽象...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/11/2014
ms.topic: article
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 13bccc4b2d6f1b22c94446deaf6795dab766275b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="bb5d1-104">在 Azure 辅助角色的 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="bb5d1-104">Host OWIN in an Azure Worker Role</span></span>
====================
<span data-ttu-id="bb5d1-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bb5d1-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="bb5d1-106">本教程演示如何自承载在 Microsoft Azure 辅助角色中的 OWIN。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
> 
> <span data-ttu-id="bb5d1-107">[打开针对.NET 的 Web 界面](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="bb5d1-108">OWIN 将脱耦在服务器上，这使 OWIN 适合于你自己的过程，在 IIS 外部的 web 应用程序的自承载的 web 应用程序 – 例如，在 Azure 辅助角色。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
> 
> <span data-ttu-id="bb5d1-109">在本教程中，你将学习如何自承载的 OWIN 应用程序在 Microsoft Azure 辅助角色。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="bb5d1-110">若要了解有关辅助角色的详细信息，请参阅[Azure 执行模型](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bb5d1-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="bb5d1-111">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="bb5d1-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bb5d1-112">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="bb5d1-113">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="bb5d1-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="bb5d1-114">Microsoft.Owin.Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="bb5d1-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="bb5d1-115">创建 Microsoft Azure 项目</span><span class="sxs-lookup"><span data-stu-id="bb5d1-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="bb5d1-116">使用管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="bb5d1-117">要调试应用程序中本地，使用 Azure 计算仿真程序，需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="bb5d1-118">上**文件**菜单上，单击**新建**，然后单击**项目**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="bb5d1-119">从**已安装的模板**，在 Visual C# 中，单击**云**，然后单击**Windows Azure 云服务**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="bb5d1-120">将"AzureApp"的项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="bb5d1-121">在**新建 Windows Azure 云服务**对话框中，双击**辅助角色**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="bb5d1-122">保留默认名称 ("WorkerRole1")。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="bb5d1-123">此步骤将辅助角色添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="bb5d1-124">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="bb5d1-125">创建 Visual Studio 解决方案包含两个项目：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="bb5d1-126">&quot;AzureApp&quot;定义的角色和 Azure 应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="bb5d1-127">&quot;WorkerRole1&quot;包含辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="bb5d1-128">一般情况下，Azure 应用程序可以包含多个角色，虽然本教程使用单个角色。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="bb5d1-129">将 OWIN 自承载的包添加</span><span class="sxs-lookup"><span data-stu-id="bb5d1-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="bb5d1-130">从**工具**菜单上，单击**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-130">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="bb5d1-131">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="bb5d1-132">添加一个 HTTP 终结点</span><span class="sxs-lookup"><span data-stu-id="bb5d1-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="bb5d1-133">在解决方案资源管理器，展开 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="bb5d1-134">展开角色节点，右键单击 WorkerRole1，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="bb5d1-135">单击**终结点**，然后单击**添加终结点**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="bb5d1-136">在**协议**下拉列表中，选择"http"。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="bb5d1-137">在**公用端口**和**专用端口**，键入 80。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="bb5d1-138">这些端口号可以不同。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-138">These port numbers can be different.</span></span> <span data-ttu-id="bb5d1-139">公用端口是客户端使用时它们将请求发送到的角色。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="bb5d1-140">创建 OWIN Startup 类</span><span class="sxs-lookup"><span data-stu-id="bb5d1-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="bb5d1-141">在解决方案资源管理器，右键单击 WorkerRole1 项目并选择**添加** / **类**添加新类。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="bb5d1-142">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-142">Name the class `Startup`.</span></span>

<span data-ttu-id="bb5d1-143">将所有样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="bb5d1-144">`UseWelcomePage`扩展方法将一个简单的 HTML 页面添加到应用程序，以验证站点是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="bb5d1-145">启动 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="bb5d1-145">Start the OWIN Host</span></span>

<span data-ttu-id="bb5d1-146">打开 WorkerRole.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="bb5d1-147">此类定义运行时启动和停止辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="bb5d1-148">添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="bb5d1-149">添加**IDisposable**成员`WorkerRole`类：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="bb5d1-150">在`OnStart`方法，添加以下代码以启动主机：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="bb5d1-151">**WebApp.Start**方法会启动 OWIN 主机。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="bb5d1-152">名称`Startup`类是方法的类型参数。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="bb5d1-153">按照约定，主机将调用`Configure`此类的方法。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="bb5d1-154">重写`OnStop`若要释放*\_应用*实例：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="bb5d1-155">下面是 WorkerRole.cs 的完整代码：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="bb5d1-156">生成解决方案，然后按 F5 以在 Azure 计算模拟器中本地运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="bb5d1-157">具体取决于你的防火墙设置，你可能需要允许通过你的防火墙的仿真程序。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="bb5d1-158">计算仿真程序将本地 IP 地址分配到终结点。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="bb5d1-159">可以通过查看计算模拟器 UI 中找到的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="bb5d1-160">右键单击任务栏通知区域中的模拟器图标并选择**显示计算模拟器 UI**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="bb5d1-161">找到在服务部署，部署 [id] 服务详细信息的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="bb5d1-162">打开 web 浏览器并导航到 http://<em>地址</em>，其中<em>地址</em>是通过计算模拟器中; 分配的 IP 地址等`http://127.0.0.1:80`。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-162">Open a web browser and navigate to http://<em>address</em>, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="bb5d1-163">你应看到 OWIN 欢迎页：</span><span class="sxs-lookup"><span data-stu-id="bb5d1-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="bb5d1-164">将部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bb5d1-164">Deploy to Azure</span></span>

<span data-ttu-id="bb5d1-165">对于此步骤，你必须具有 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="bb5d1-166">如果你还没有一个，可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bb5d1-167">有关详细信息，请参阅[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="bb5d1-168">在解决方案资源管理器，右键单击 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="bb5d1-169">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="bb5d1-170">如果您未登录到你的 Azure 帐户，请单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="bb5d1-171">你在登录后，选择订阅，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="bb5d1-172">输入云服务的名称，然后选择一个区域。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="bb5d1-173">单击“创建” 。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="bb5d1-174">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="bb5d1-175">Azure 活动日志窗口显示部署的进度。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="bb5d1-176">部署应用程序时，浏览到`http://appname.cloudapp.net/`，其中*appname*是你的云服务的名称。</span><span class="sxs-lookup"><span data-stu-id="bb5d1-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb5d1-177">其他资源</span><span class="sxs-lookup"><span data-stu-id="bb5d1-177">Additional Resources</span></span>

- [<span data-ttu-id="bb5d1-178">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="bb5d1-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="bb5d1-179">在 GitHub 上的 Katana 项目</span><span class="sxs-lookup"><span data-stu-id="bb5d1-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
