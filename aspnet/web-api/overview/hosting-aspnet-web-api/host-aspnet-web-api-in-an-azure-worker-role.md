---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: "承载 ASP.NET Web API 2 中的 Azure 辅助角色 |Microsoft 文档"
author: MikeWasson
description: "本教程演示如何承载 ASP.NET Web API 在 Azure 辅助角色中，使用 OWIN 自承载 Web API 框架。 打开 Web 接口的.NET (OWIN) de..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/02/2014
ms.topic: article
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 9a7f8242bf482e81513accfe05e10a64ae0ca0b2
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="47dd3-104">承载 ASP.NET Web API 2 中的 Azure 辅助角色</span><span class="sxs-lookup"><span data-stu-id="47dd3-104">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>
====================
<span data-ttu-id="47dd3-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="47dd3-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="47dd3-106">本教程演示如何承载 ASP.NET Web API 在 Azure 辅助角色中，使用 OWIN 自承载 Web API 框架。</span><span class="sxs-lookup"><span data-stu-id="47dd3-106">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
> 
> <span data-ttu-id="47dd3-107">[打开针对.NET 的 Web 界面](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="47dd3-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="47dd3-108">OWIN 将脱耦在服务器上，这使 OWIN 适合于你自己的过程，在 IIS 外部的 web 应用程序的自承载的 web 应用程序 – 例如，在 Azure 辅助角色。</span><span class="sxs-lookup"><span data-stu-id="47dd3-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
> 
> <span data-ttu-id="47dd3-109">在本教程中，你将使用 Microsoft.Owin.Host.HttpListener 包，其中提供的 HTTP 服务器，它用于自承载 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="47dd3-109">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="47dd3-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="47dd3-110">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="47dd3-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="47dd3-111">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="47dd3-112">Web API 2</span><span class="sxs-lookup"><span data-stu-id="47dd3-112">Web API 2</span></span>
> - [<span data-ttu-id="47dd3-113">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="47dd3-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="47dd3-114">创建 Microsoft Azure 项目</span><span class="sxs-lookup"><span data-stu-id="47dd3-114">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="47dd3-115">使用管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="47dd3-115">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="47dd3-116">要调试应用程序中本地，使用 Azure 计算仿真程序，需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="47dd3-116">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="47dd3-117">上**文件**菜单上，单击**新建**，然后单击**项目**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-117">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="47dd3-118">从**已安装的模板**，在 Visual C# 中，单击**云**，然后单击**Windows Azure 云服务**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-118">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="47dd3-119">将"AzureApp"的项目，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-119">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="47dd3-120">在**新建 Windows Azure 云服务**对话框中，双击**辅助角色**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-120">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="47dd3-121">保留默认名称 ("WorkerRole1")。</span><span class="sxs-lookup"><span data-stu-id="47dd3-121">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="47dd3-122">此步骤将辅助角色添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="47dd3-122">This step adds a worker role to the solution.</span></span> <span data-ttu-id="47dd3-123">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-123">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="47dd3-124">创建 Visual Studio 解决方案包含两个项目：</span><span class="sxs-lookup"><span data-stu-id="47dd3-124">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="47dd3-125">&quot;AzureApp&quot;定义的角色和 Azure 应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="47dd3-125">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="47dd3-126">&quot;WorkerRole1&quot;包含辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="47dd3-126">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="47dd3-127">一般情况下，Azure 应用程序可以包含多个角色，虽然本教程使用单个角色。</span><span class="sxs-lookup"><span data-stu-id="47dd3-127">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="47dd3-128">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="47dd3-128">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="47dd3-129">从**工具**菜单上，单击**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-129">From the **Tools** menu, click **Library Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="47dd3-130">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="47dd3-130">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="47dd3-131">添加一个 HTTP 终结点</span><span class="sxs-lookup"><span data-stu-id="47dd3-131">Add an HTTP Endpoint</span></span>

<span data-ttu-id="47dd3-132">在解决方案资源管理器，展开 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="47dd3-132">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="47dd3-133">展开角色节点，右键单击 WorkerRole1，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-133">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="47dd3-134">单击**终结点**，然后单击**添加终结点**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-134">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="47dd3-135">在**协议**下拉列表中，选择"http"。</span><span class="sxs-lookup"><span data-stu-id="47dd3-135">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="47dd3-136">在**公用端口**和**专用端口**，键入 80。</span><span class="sxs-lookup"><span data-stu-id="47dd3-136">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="47dd3-137">这些端口号可以不同。</span><span class="sxs-lookup"><span data-stu-id="47dd3-137">These port numbers can be different.</span></span> <span data-ttu-id="47dd3-138">公用端口是客户端使用时它们将请求发送到的角色。</span><span class="sxs-lookup"><span data-stu-id="47dd3-138">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="47dd3-139">配置 Web API 的自承载</span><span class="sxs-lookup"><span data-stu-id="47dd3-139">Configure Web API for Self-Host</span></span>

<span data-ttu-id="47dd3-140">在解决方案资源管理器，右键单击 WorkerRole1 项目并选择**添加** / **类**添加新类。</span><span class="sxs-lookup"><span data-stu-id="47dd3-140">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="47dd3-141">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="47dd3-141">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="47dd3-142">将所有此文件中的样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="47dd3-142">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="47dd3-143">添加一个 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="47dd3-143">Add a Web API Controller</span></span>

<span data-ttu-id="47dd3-144">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="47dd3-144">Next, add a Web API controller class.</span></span> <span data-ttu-id="47dd3-145">右键单击 WorkerRole1 项目并选择**添加** / **类**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-145">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="47dd3-146">将类 TestController。</span><span class="sxs-lookup"><span data-stu-id="47dd3-146">Name the class TestController.</span></span> <span data-ttu-id="47dd3-147">将所有此文件中的样板文件代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="47dd3-147">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="47dd3-148">为简单起见，此控制器只需定义返回纯文本的两个 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="47dd3-148">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="47dd3-149">启动 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="47dd3-149">Start the OWIN Host</span></span>

<span data-ttu-id="47dd3-150">打开 WorkerRole.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="47dd3-150">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="47dd3-151">此类定义运行时启动和停止辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="47dd3-151">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="47dd3-152">添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="47dd3-152">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="47dd3-153">添加**IDisposable**成员`WorkerRole`类：</span><span class="sxs-lookup"><span data-stu-id="47dd3-153">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="47dd3-154">在`OnStart`方法，添加以下代码以启动主机：</span><span class="sxs-lookup"><span data-stu-id="47dd3-154">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="47dd3-155">**WebApp.Start**方法会启动 OWIN 主机。</span><span class="sxs-lookup"><span data-stu-id="47dd3-155">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="47dd3-156">名称`Startup`类是方法的类型参数。</span><span class="sxs-lookup"><span data-stu-id="47dd3-156">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="47dd3-157">按照约定，主机将调用`Configure`此类的方法。</span><span class="sxs-lookup"><span data-stu-id="47dd3-157">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="47dd3-158">重写`OnStop`若要释放*\_应用*实例：</span><span class="sxs-lookup"><span data-stu-id="47dd3-158">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="47dd3-159">下面是 WorkerRole.cs 的完整代码：</span><span class="sxs-lookup"><span data-stu-id="47dd3-159">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="47dd3-160">生成解决方案，然后按 F5 以在 Azure 计算模拟器中本地运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="47dd3-160">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="47dd3-161">具体取决于你的防火墙设置，你可能需要允许通过你的防火墙的仿真程序。</span><span class="sxs-lookup"><span data-stu-id="47dd3-161">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="47dd3-162">如果你收到如下所示异常，请参阅[这篇博客文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)要解决此问题。</span><span class="sxs-lookup"><span data-stu-id="47dd3-162">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="47dd3-163">"无法加载文件或程序集 Microsoft.Owin，Version = 2.0.2.0，区域性 = neutral，PublicKeyToken = 31bf3856ad364e35 或其依赖项之一。</span><span class="sxs-lookup"><span data-stu-id="47dd3-163">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="47dd3-164">找到的程序集清单定义与程序集引用不匹配。</span><span class="sxs-lookup"><span data-stu-id="47dd3-164">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="47dd3-165">(异常来自 HRESULT: 0x80131040)"</span><span class="sxs-lookup"><span data-stu-id="47dd3-165">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="47dd3-166">计算仿真程序将本地 IP 地址分配到终结点。</span><span class="sxs-lookup"><span data-stu-id="47dd3-166">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="47dd3-167">可以通过查看计算模拟器 UI 中找到的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="47dd3-167">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="47dd3-168">右键单击任务栏通知区域中的模拟器图标并选择**显示计算模拟器 UI**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-168">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="47dd3-169">找到在服务部署，部署 [id] 服务详细信息的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="47dd3-169">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="47dd3-170">打开 web 浏览器并导航到 http://*地址*/测试/1，其中*地址*是通过计算模拟器中; 分配的 IP 地址等`http://127.0.0.1:80/test/1`。</span><span class="sxs-lookup"><span data-stu-id="47dd3-170">Open a web browser and navigate to http://*address*/test/1, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="47dd3-171">你应看到来自 Web API 控制器的响应：</span><span class="sxs-lookup"><span data-stu-id="47dd3-171">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="47dd3-172">将部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="47dd3-172">Deploy to Azure</span></span>

<span data-ttu-id="47dd3-173">对于此步骤，你必须具有 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="47dd3-173">For this step, you must have an Azure account.</span></span> <span data-ttu-id="47dd3-174">如果你还没有一个，可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="47dd3-174">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="47dd3-175">有关详细信息，请参阅[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="47dd3-175">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="47dd3-176">在解决方案资源管理器，右键单击 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="47dd3-176">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="47dd3-177">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="47dd3-177">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="47dd3-178">如果您未登录到你的 Azure 帐户，请单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-178">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="47dd3-179">你在登录后，选择订阅，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-179">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="47dd3-180">输入云服务的名称，然后选择一个区域。</span><span class="sxs-lookup"><span data-stu-id="47dd3-180">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="47dd3-181">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="47dd3-181">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="47dd3-182">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="47dd3-182">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="47dd3-183">Azure 活动日志窗口显示部署的进度。</span><span class="sxs-lookup"><span data-stu-id="47dd3-183">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="47dd3-184">部署应用程序时，浏览到 http://appname.cloudapp.net/test/1。</span><span class="sxs-lookup"><span data-stu-id="47dd3-184">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="47dd3-185">其他资源</span><span class="sxs-lookup"><span data-stu-id="47dd3-185">Additional Resources</span></span>

- [<span data-ttu-id="47dd3-186">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="47dd3-186">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="47dd3-187">在 GitHub 上的 Katana 项目</span><span class="sxs-lookup"><span data-stu-id="47dd3-187">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
