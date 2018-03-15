---
title: "在 Windows 服务中的主机 ASP.NET 核心"
author: tdykstra
description: "了解如何托管的 ASP.NET Core 应用 Windows 服务中。"
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/windows-service
ms.openlocfilehash: f3455e47cfc06a4492dc4e34871b348184c6ecfb
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="8de3a-103">在 Windows 服务中的主机 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="8de3a-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="8de3a-104">作者：[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8de3a-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="8de3a-105">没有使用 IIS 是在运行承载 ASP.NET Core 应用在 Windows 上的推荐的方式[Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)。</span><span class="sxs-lookup"><span data-stu-id="8de3a-105">The recommended way to host an ASP.NET Core app on Windows without using IIS is to run it in a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="8de3a-106">当托管为 Windows 服务，应用程序可以自动启动之后启动重新启动和崩溃而无需人工干预。</span><span class="sxs-lookup"><span data-stu-id="8de3a-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="8de3a-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="8de3a-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="8de3a-108">有关说明如何运行示例应用程序，请参阅示例的*README.md*文件。</span><span class="sxs-lookup"><span data-stu-id="8de3a-108">For instructions on how to run the sample app, see the sample's *README.md* file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8de3a-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="8de3a-109">Prerequisites</span></span>

* <span data-ttu-id="8de3a-110">应用程序必须在.NET Framework 运行时上运行。</span><span class="sxs-lookup"><span data-stu-id="8de3a-110">The app must run on the .NET Framework runtime.</span></span> <span data-ttu-id="8de3a-111">在*.csproj*文件中，指定为相应值[TargetFramework](/nuget/schema/target-frameworks)和[RuntimeIdentifier](/dotnet/articles/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="8de3a-111">In the *.csproj* file, specify appropriate values for [TargetFramework](/nuget/schema/target-frameworks) and [RuntimeIdentifier](/dotnet/articles/core/rid-catalog).</span></span> <span data-ttu-id="8de3a-112">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="8de3a-112">Here's an example:</span></span>

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  <span data-ttu-id="8de3a-113">当在 Visual Studio 中创建项目，请使用**ASP.NET 核心应用程序 (.NET Framework)**模板。</span><span class="sxs-lookup"><span data-stu-id="8de3a-113">When creating a project in Visual Studio, use the **ASP.NET Core Application (.NET Framework)** template.</span></span>

* <span data-ttu-id="8de3a-114">如果应用程序接收来自 Internet （而不仅仅是从内部网络） 的请求，它必须使用[HTTP.sys](xref:fundamentals/servers/httpsys) web 服务器 (以前称为[WebListener](xref:fundamentals/servers/weblistener)对于 ASP.NET Core 1.x 应用程序) 而不是[Kestrel](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="8de3a-114">If the app receives requests from the Internet (not just from an internal network), it must use the [HTTP.sys](xref:fundamentals/servers/httpsys) web server (formerly known as [WebListener](xref:fundamentals/servers/weblistener) for ASP.NET Core 1.x apps) rather than [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="8de3a-115">IIS 被建议用于为反向代理服务器的 Kestrel 边缘部署。</span><span class="sxs-lookup"><span data-stu-id="8de3a-115">IIS is recommended for use as a reverse proxy server with Kestrel for edge deployments.</span></span> <span data-ttu-id="8de3a-116">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="8de3a-116">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

## <a name="get-started"></a><span data-ttu-id="8de3a-117">入门</span><span class="sxs-lookup"><span data-stu-id="8de3a-117">Get started</span></span>

<span data-ttu-id="8de3a-118">本部分介绍将现有的 ASP.NET Core 项目设置为在服务中运行所需的最小更改。</span><span class="sxs-lookup"><span data-stu-id="8de3a-118">This section explains the minimum changes required to set up an existing ASP.NET Core project to run in a service.</span></span>

1. <span data-ttu-id="8de3a-119">安装 NuGet 程序包[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)。</span><span class="sxs-lookup"><span data-stu-id="8de3a-119">Install the NuGet package [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

1. <span data-ttu-id="8de3a-120">进行中的以下更改`Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="8de3a-120">Make the following changes in `Program.Main`:</span></span>
  
   * <span data-ttu-id="8de3a-121">调用`host.RunAsService`而不是`host.Run`。</span><span class="sxs-lookup"><span data-stu-id="8de3a-121">Call `host.RunAsService` instead of `host.Run`.</span></span>
  
   * <span data-ttu-id="8de3a-122">如果代码调用`UseContentRoot`，到发布位置而不是使用路径`Directory.GetCurrentDirectory()`。</span><span class="sxs-lookup"><span data-stu-id="8de3a-122">If the code calls `UseContentRoot`, use a path to the publish location instead of `Directory.GetCurrentDirectory()`.</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8de3a-123">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8de3a-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   ---

1. <span data-ttu-id="8de3a-125">将应用发布到的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8de3a-125">Publish the app to a folder.</span></span> <span data-ttu-id="8de3a-126">使用[dotnet 发布](/dotnet/articles/core/tools/dotnet-publish)或[Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)，它发布到的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8de3a-126">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles) that publishes to a folder.</span></span>

1. <span data-ttu-id="8de3a-127">通过创建和启动服务测试。</span><span class="sxs-lookup"><span data-stu-id="8de3a-127">Test by creating and starting the service.</span></span>

   <span data-ttu-id="8de3a-128">使用管理特权才能使用打开命令行界面[sc.exe](https://technet.microsoft.com/library/bb490995)命令行工具来创建和启动服务。</span><span class="sxs-lookup"><span data-stu-id="8de3a-128">Open a command shell with administrative privileges to use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create and start a service.</span></span> <span data-ttu-id="8de3a-129">如果该服务名为 MyService，发布到`c:\svc`，以及名为 AspNetCoreService，命令：</span><span class="sxs-lookup"><span data-stu-id="8de3a-129">If the service is named MyService, published to `c:\svc`, and named AspNetCoreService, the commands are:</span></span>

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   <span data-ttu-id="8de3a-130">`binPath`值是应用程序的可执行文件，其中包括可执行文件名称的路径。</span><span class="sxs-lookup"><span data-stu-id="8de3a-130">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span>

   ![控制台窗口创建并启动示例](windows-service/_static/create-start.png)

   <span data-ttu-id="8de3a-132">在这些命令完成后，浏览到相同的路径作为控制台应用程序运行时 (默认情况下， `http://localhost:5000`):</span><span class="sxs-lookup"><span data-stu-id="8de3a-132">When these commands finish, browse to the same path as when running as a console app (by default, `http://localhost:5000`):</span></span>

   ![服务中运行](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="8de3a-134">提供服务的外部运行的方法</span><span class="sxs-lookup"><span data-stu-id="8de3a-134">Provide a way to run outside of a service</span></span>

<span data-ttu-id="8de3a-135">很容易地测试和调试时运行外部服务，因此通常将调用的代码添加`RunAsService`仅在某些情况下。</span><span class="sxs-lookup"><span data-stu-id="8de3a-135">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="8de3a-136">例如，应用程序可以作为包含的控制台应用程序运行`--console`命令行自变量，或如果附加调试器：</span><span class="sxs-lookup"><span data-stu-id="8de3a-136">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8de3a-137">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-137">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8de3a-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

---

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="8de3a-139">处理停止和启动事件</span><span class="sxs-lookup"><span data-stu-id="8de3a-139">Handle stopping and starting events</span></span>

<span data-ttu-id="8de3a-140">若要处理`OnStarting`， `OnStarted`，和`OnStopping`事件，进行以下其他更改：</span><span class="sxs-lookup"><span data-stu-id="8de3a-140">To handle `OnStarting`, `OnStarted`, and `OnStopping` events, make the following additional changes:</span></span>

1. <span data-ttu-id="8de3a-141">创建一个类，派生自`WebHostService`:</span><span class="sxs-lookup"><span data-stu-id="8de3a-141">Create a class that derives from `WebHostService`:</span></span>

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

1. <span data-ttu-id="8de3a-142">创建扩展方法`IWebHost`，通过自定义`WebHostService`到`ServiceBase.Run`:</span><span class="sxs-lookup"><span data-stu-id="8de3a-142">Create an extension method for `IWebHost` that passes the custom `WebHostService` to `ServiceBase.Run`:</span></span>

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

1. <span data-ttu-id="8de3a-143">在`Program.Main`，调用新的扩展方法， `RunAsCustomService`，而不是`RunAsService`:</span><span class="sxs-lookup"><span data-stu-id="8de3a-143">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of `RunAsService`:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8de3a-144">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-144">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8de3a-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8de3a-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   ---

<span data-ttu-id="8de3a-146">如果自定义`WebHostService`代码需要从依赖关系注入 （如记录器） 服务，以获取从`Services`属性`IWebHost`:</span><span class="sxs-lookup"><span data-stu-id="8de3a-146">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the `Services` property of `IWebHost`:</span></span>

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="acknowledgments"></a><span data-ttu-id="8de3a-147">致谢</span><span class="sxs-lookup"><span data-stu-id="8de3a-147">Acknowledgments</span></span>

<span data-ttu-id="8de3a-148">本文是已发布的源的帮助下编写的：</span><span class="sxs-lookup"><span data-stu-id="8de3a-148">This article was written with the help of published sources:</span></span>

* [<span data-ttu-id="8de3a-149">作为 Windows 服务承载 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="8de3a-149">Hosting ASP.NET Core as Windows service</span></span>](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [<span data-ttu-id="8de3a-150">如何托管 Windows 服务中将 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="8de3a-150">How to host your ASP.NET Core in a Windows Service</span></span>](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
