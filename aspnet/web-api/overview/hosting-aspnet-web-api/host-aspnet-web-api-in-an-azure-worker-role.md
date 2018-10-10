---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: 承载 ASP.NET Web API 2 中的 Azure 辅助角色 |Microsoft Docs
author: MikeWasson
description: 本教程演示如何在托管在 Azure 辅助角色中，ASP.NET Web API 使用 OWIN 自托管 Web API 框架。 开放 Web 接口的.NET (OWIN) de...
ms.author: riande
ms.date: 04/02/2014
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 40cb1a4514beaf81e7ed75bbd3e478f2ba146fe5
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910741"
---
<a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="3cb0c-104">承载 ASP.NET Web API 2 中的 Azure 辅助角色</span><span class="sxs-lookup"><span data-stu-id="3cb0c-104">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>
====================
<span data-ttu-id="3cb0c-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3cb0c-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="3cb0c-106">本教程演示如何在托管在 Azure 辅助角色中，ASP.NET Web API 使用 OWIN 自托管 Web API 框架。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-106">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="3cb0c-107">[用于.NET 开放 Web 接口](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="3cb0c-108">OWIN 将分离 web 应用程序从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序 – 例如，在 Azure 辅助角色。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="3cb0c-109">在本教程中，您将使用 Microsoft.Owin.Host.HttpListener 包，其中提供的 HTTP 服务器，用于自托管 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-109">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3cb0c-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3cb0c-110">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="3cb0c-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3cb0c-111">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3cb0c-112">Web API 2</span><span class="sxs-lookup"><span data-stu-id="3cb0c-112">Web API 2</span></span>
> - [<span data-ttu-id="3cb0c-113">Azure SDK for.NET 2.3</span><span class="sxs-lookup"><span data-stu-id="3cb0c-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="3cb0c-114">创建 Microsoft Azure 项目</span><span class="sxs-lookup"><span data-stu-id="3cb0c-114">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="3cb0c-115">使用管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-115">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="3cb0c-116">本地调试应用程序，使用 Azure 计算仿真程序时需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-116">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="3cb0c-117">上**文件**菜单上，单击**新建**，然后单击**项目**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-117">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="3cb0c-118">从**已安装的模板**，在 Visual C# 中，单击**云**，然后单击**Windows Azure 云服务**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-118">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="3cb0c-119">命名项目"AzureApp"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-119">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="3cb0c-120">在中**新的 Windows Azure 云服务**对话框中，双击**辅助角色**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-120">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="3cb0c-121">保留默认名称 ("WorkerRole1")。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-121">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="3cb0c-122">此步骤将辅助角色添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-122">This step adds a worker role to the solution.</span></span> <span data-ttu-id="3cb0c-123">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-123">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="3cb0c-124">创建 Visual Studio 解决方案包含两个项目：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-124">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="3cb0c-125">&quot;AzureApp&quot;定义的角色和配置 Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-125">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="3cb0c-126">&quot;WorkerRole1&quot;包含辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-126">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="3cb0c-127">一般情况下，Azure 应用程序可以包含多个角色，但本教程使用单个角色。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-127">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="3cb0c-128">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="3cb0c-128">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="3cb0c-129">从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-129">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="3cb0c-130">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-130">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="3cb0c-131">添加 HTTP 终结点</span><span class="sxs-lookup"><span data-stu-id="3cb0c-131">Add an HTTP Endpoint</span></span>

<span data-ttu-id="3cb0c-132">在解决方案资源管理器，展开 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-132">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="3cb0c-133">展开角色节点，右键单击 WorkerRole1，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-133">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="3cb0c-134">单击**终结点**，然后单击**添加终结点**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-134">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="3cb0c-135">在中**协议**下拉列表中，选择"http"。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-135">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="3cb0c-136">在中**公用端口**并**专用端口**，键入 80。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-136">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="3cb0c-137">这些端口编号可以不同。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-137">These port numbers can be different.</span></span> <span data-ttu-id="3cb0c-138">公用端口是客户端使用时将请求发送到的角色。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-138">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="3cb0c-139">配置 Web API 的自托管</span><span class="sxs-lookup"><span data-stu-id="3cb0c-139">Configure Web API for Self-Host</span></span>

<span data-ttu-id="3cb0c-140">在解决方案资源管理器，右键单击 WorkerRole1 项目并选择**外** / **类**以添加一个新类。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-140">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="3cb0c-141">将此类命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-141">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="3cb0c-142">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-142">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="3cb0c-143">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="3cb0c-143">Add a Web API Controller</span></span>

<span data-ttu-id="3cb0c-144">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-144">Next, add a Web API controller class.</span></span> <span data-ttu-id="3cb0c-145">右键单击 WorkerRole1 项目并选择**外** / **类**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-145">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="3cb0c-146">类 TestController 命名。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-146">Name the class TestController.</span></span> <span data-ttu-id="3cb0c-147">使用以下内容替换所有样板代码，此文件中：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-147">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="3cb0c-148">为简单起见，此控制器只是定义返回纯文本的两个 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-148">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="3cb0c-149">启动 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="3cb0c-149">Start the OWIN Host</span></span>

<span data-ttu-id="3cb0c-150">打开 WorkerRole.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-150">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="3cb0c-151">此类定义运行时辅助角色启动和停止的代码。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-151">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="3cb0c-152">添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-152">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="3cb0c-153">添加**IDisposable**成员添加到`WorkerRole`类：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-153">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="3cb0c-154">在`OnStart`方法中，添加以下代码以启动主机：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-154">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="3cb0c-155">**WebApp.Start**方法启动的 OWIN 主机。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-155">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="3cb0c-156">名称`Startup`类是方法的类型参数。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-156">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="3cb0c-157">按照约定，宿主将调用`Configure`此类的方法。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-157">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="3cb0c-158">重写`OnStop`释放*\_应用*实例：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-158">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="3cb0c-159">下面是 WorkerRole.cs 的完整代码：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-159">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="3cb0c-160">生成解决方案，然后按 F5 以在 Azure 计算模拟器中本地运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-160">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="3cb0c-161">根据防火墙设置，可能需要允许通过防火墙的仿真程序。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-161">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb0c-162">如果您收到类似于以下异常，请参阅[这篇博客文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)的一种解决方法。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-162">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="3cb0c-163">"无法加载文件或程序集 Microsoft.Owin，版本 = 2.0.2.0，区域性 = 中性，PublicKeyToken = 31bf3856ad364e35 或其某个依赖项。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-163">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="3cb0c-164">找到的程序集清单定义与程序集引用不匹配。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-164">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="3cb0c-165">(异常来自 HRESULT: 0x80131040)"</span><span class="sxs-lookup"><span data-stu-id="3cb0c-165">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="3cb0c-166">在计算仿真程序将本地 IP 地址分配到的终结点。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-166">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="3cb0c-167">可以通过查看计算仿真程序用户界面中找到的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-167">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="3cb0c-168">右键单击任务栏通知区域中的模拟器图标并选择**显示计算模拟器 UI**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-168">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="3cb0c-169">找到服务部署，部署 [id] 服务详细信息下的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-169">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="3cb0c-170">打开 web 浏览器并浏览至 http://<em>地址</em>/测试/1，其中<em>地址</em>是由计算模拟器; 分配的 IP 地址，如 `http://127.0.0.1:80/test/1` 。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-170">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="3cb0c-171">应会看到来自 Web API 控制器的响应：</span><span class="sxs-lookup"><span data-stu-id="3cb0c-171">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="3cb0c-172">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="3cb0c-172">Deploy to Azure</span></span>

<span data-ttu-id="3cb0c-173">对于此步骤，必须具有 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-173">For this step, you must have an Azure account.</span></span> <span data-ttu-id="3cb0c-174">如果你还没有一个，可以在几分钟即可完成创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-174">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3cb0c-175">有关详细信息，请参阅[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-175">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="3cb0c-176">在解决方案资源管理器，右键单击 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-176">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="3cb0c-177">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-177">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="3cb0c-178">如果您未登录到你的 Azure 帐户，请单击**Sign In**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-178">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="3cb0c-179">登录后，选择订阅，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-179">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="3cb0c-180">输入云服务的名称并选择区域。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-180">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="3cb0c-181">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-181">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="3cb0c-182">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-182">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="3cb0c-183">Azure 活动日志窗口显示部署进度。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-183">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="3cb0c-184">部署应用程序时，浏览到 http://appname.cloudapp.net/test/1 。</span><span class="sxs-lookup"><span data-stu-id="3cb0c-184">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="3cb0c-185">其他资源</span><span class="sxs-lookup"><span data-stu-id="3cb0c-185">Additional Resources</span></span>

- [<span data-ttu-id="3cb0c-186">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="3cb0c-186">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="3cb0c-187">GitHub 上的 Katana 项目</span><span class="sxs-lookup"><span data-stu-id="3cb0c-187">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
