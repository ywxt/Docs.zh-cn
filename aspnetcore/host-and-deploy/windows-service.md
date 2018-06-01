---
title: 在 Windows 服务中托管 ASP.NET Core
author: rick-anderson
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/windows-service
ms.openlocfilehash: 29f83ee585c73aeb57a09f70ea8e28650c05ce69
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
ms.locfileid: "34153524"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="056c1-103">在 Windows 服务中托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="056c1-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="056c1-104">作者：[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="056c1-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="056c1-105">不使用 IIS 在 Windows 上托管 ASP.NET Core 应用的推荐方式是在 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)中运行应用。</span><span class="sxs-lookup"><span data-stu-id="056c1-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="056c1-106">作为 Windows 服务托管时，无需人工干预应用即可在重新启动和崩溃后自动启动。</span><span class="sxs-lookup"><span data-stu-id="056c1-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="056c1-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="056c1-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="056c1-108">有关如何运行示例应用的说明，请参阅示例的 README.md 文件。</span><span class="sxs-lookup"><span data-stu-id="056c1-108">For instructions on how to run the sample app, see the sample's *README.md* file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="056c1-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="056c1-109">Prerequisites</span></span>

* <span data-ttu-id="056c1-110">应用必须在 .NET Framework 运行时运行。</span><span class="sxs-lookup"><span data-stu-id="056c1-110">The app must run on the .NET Framework runtime.</span></span> <span data-ttu-id="056c1-111">在 .csproj 文件中，指定 [TargetFramework](/nuget/schema/target-frameworks) 和 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog) 的相应值。</span><span class="sxs-lookup"><span data-stu-id="056c1-111">In the *.csproj* file, specify appropriate values for [TargetFramework](/nuget/schema/target-frameworks) and [RuntimeIdentifier](/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="056c1-112">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="056c1-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="056c1-113">在 Visual Studio 中创建项目时，请使用“ASP.NET Core 应用程序(.NET Framework)”模板。</span><span class="sxs-lookup"><span data-stu-id="056c1-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="056c1-114">如果应用接收来自 Internet（而不仅仅来自内部网络）的请求，则必须使用 [HTTP.sys](xref:fundamentals/servers/httpsys) Web 服务器（对于 ASP.NET Core 1.x 应用，以前称为 [WebListener](xref:fundamentals/servers/weblistener)）而不是 [Kestrel](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="056c1-114">If the app receives requests from the Internet (not just from an internal network), it must use the [HTTP.sys](xref:fundamentals/servers/httpsys) web server (formerly known as [WebListener](xref:fundamentals/servers/weblistener) for ASP.NET Core 1.x apps) rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="056c1-115">建议将 IIS 用作反向代理服务器与 Kestrel 进行 Edge 部署。</span><span class="sxs-lookup"><span data-stu-id="056c1-115">IIS is recommended for use as a reverse proxy server with Kestrel for edge deployments.</span></span> <span data-ttu-id="056c1-116">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="056c1-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="get-started"></a><span data-ttu-id="056c1-117">入门</span><span class="sxs-lookup"><span data-stu-id="056c1-117">Get started</span></span>

<span data-ttu-id="056c1-118">本部分介绍了将现有的 ASP.NET Core 项目设置为在服务中运行所需的最小更改。</span><span class="sxs-lookup"><span data-stu-id="056c1-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

1. <span data-ttu-id="056c1-119">安装 NuGet 包 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)。</span><span class="sxs-lookup"><span data-stu-id="056c1-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

2. <span data-ttu-id="056c1-120">在 `Program.Main` 中，进行下列更改：</span><span class="sxs-lookup"><span data-stu-id="056c1-120">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="056c1-121">调用 `host.RunAsService` 而非 `host.Run`。</span><span class="sxs-lookup"><span data-stu-id="056c1-121">Call `host.RunAsService` instead of `host.Run`.</span></span>

   * <span data-ttu-id="056c1-122">如果代码调用 `UseContentRoot`，请使用发布位置的路径，而不是 `Directory.GetCurrentDirectory()`。</span><span class="sxs-lookup"><span data-stu-id="056c1-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`.</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="056c1-123">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="056c1-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="056c1-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="056c1-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   ---

3. <span data-ttu-id="056c1-125">将应用发布到文件夹。</span><span class="sxs-lookup"><span data-stu-id="056c1-125">Publish the app to a folder.</span></span> <span data-ttu-id="056c1-126">使用可发布到文件夹的 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 或 [Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)。</span><span class="sxs-lookup"><span data-stu-id="056c1-126">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

4. <span data-ttu-id="056c1-127">通过创建和启动服务进行测试。</span><span class="sxs-lookup"><span data-stu-id="056c1-127">Test by creating and starting the service.</span></span>

   <span data-ttu-id="056c1-128">使用管理权限打开命令行界面，以便使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具来创建和启动服务。</span><span class="sxs-lookup"><span data-stu-id="056c1-128">Open a command shell with administrative privileges to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span> <span data-ttu-id="056c1-129">如果将该服务命名为 MyService、发布到 `c:\svc`，以及命名为 AspNetCoreService，则相应的命令为：</span><span class="sxs-lookup"><span data-stu-id="056c1-129">If the service is named MyService, published to `c:\svc`, and named AspNetCoreService, the commands are:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   <span data-ttu-id="056c1-130">`binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。</span><span class="sxs-lookup"><span data-stu-id="056c1-130">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span>

   ![控制台窗口创建和启动示例](windows-service/_static/create-start.png)

   <span data-ttu-id="056c1-132">完成这些命令后，浏览到作为控制台应用运行时的同一路径（默认情况下为 `http://localhost:5000`）：</span><span class="sxs-lookup"><span data-stu-id="056c1-132">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`):</span></span>

   ![在服务中运行](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="056c1-134">提供在服务之外运行的方法</span><span class="sxs-lookup"><span data-stu-id="056c1-134">Provide a way to run outside of a service</span></span>

<span data-ttu-id="056c1-135">在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。</span><span class="sxs-lookup"><span data-stu-id="056c1-135">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="056c1-136">例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：</span><span class="sxs-lookup"><span data-stu-id="056c1-136">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="056c1-137">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="056c1-137">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="056c1-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="056c1-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

---

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="056c1-139">处理停止和启动事件</span><span class="sxs-lookup"><span data-stu-id="056c1-139">Handle stopping and starting events</span></span>

<span data-ttu-id="056c1-140">若要处理 `OnStarting`、`OnStarted` 和 `OnStopping` 事件，请进行以下其他更改：</span><span class="sxs-lookup"><span data-stu-id="056c1-140">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

1. <span data-ttu-id="056c1-141">创建一个从 `WebHostService` 派生的类：</span><span class="sxs-lookup"><span data-stu-id="056c1-141">Create a class that derives from `WebHostService`:</span></span>

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="056c1-142">创建可将自定义 `WebHostService` 传递给 `ServiceBase.Run` 的 `IWebHost` 的扩展方法：</span><span class="sxs-lookup"><span data-stu-id="056c1-142">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`:</span></span>

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="056c1-143">在 `Program.Main` 中，调用新的扩展方法 `RunAsCustomService`，而不是 `RunAsService`：</span><span class="sxs-lookup"><span data-stu-id="056c1-143">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of `RunAsService`:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="056c1-144">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="056c1-144">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="056c1-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="056c1-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   ---

<span data-ttu-id="056c1-146">如果自定义 `WebHostService` 代码需要来自依赖关系注入（如记录器）的服务，请从 `IWebHost` 的 `Services` 属性中获取该服务：</span><span class="sxs-lookup"><span data-stu-id="056c1-146">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the `Services` property of `IWebHost`:</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="056c1-147">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="056c1-147">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="056c1-148">与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。</span><span class="sxs-lookup"><span data-stu-id="056c1-148">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="056c1-149">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="056c1-149">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="056c1-150">鸣谢</span><span class="sxs-lookup"><span data-stu-id="056c1-150">Acknowledgments</span></span>

<span data-ttu-id="056c1-151">本文是在以下出版物来源的帮助下编写的：</span><span class="sxs-lookup"><span data-stu-id="056c1-151">This article was written with the help of published sources:</span></span>

* [<span data-ttu-id="056c1-152">作为 Windows 服务托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="056c1-152">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="056c1-153">如何在 Windows 服务中托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="056c1-153">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
