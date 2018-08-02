---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 4fd0cc881eff3b1bbdfdf51e223d0fd42051c31d
ms.sourcegitcommit: 516d0645c35ea784a3ae807be087ae70446a46ee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39320734"
---
# <a name="host-aspnet-core-in-a-windows-service"></a><span data-ttu-id="12171-103">在 Windows 服务中托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="12171-103">Host ASP.NET Core in a Windows Service</span></span>

<span data-ttu-id="12171-104">作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="12171-104">By [Luke Latham](https://github.com/guardrex) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="12171-105">不将 IIS 用作 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)时，可在 Windows 上托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="12171-105">An ASP.NET Core app can be hosted on Windows without using IIS as a [Windows Service](/dotnet/framework/windows-services/introduction-to-windows-service-applications).</span></span> <span data-ttu-id="12171-106">作为 Windows 服务托管时，无需人工干预应用即可在重新启动和崩溃后自动启动。</span><span class="sxs-lookup"><span data-stu-id="12171-106">When hosted as a Windows Service, the app can automatically start after reboots and crashes without requiring human intervention.</span></span>

<span data-ttu-id="12171-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="12171-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="get-started"></a><span data-ttu-id="12171-108">入门</span><span class="sxs-lookup"><span data-stu-id="12171-108">Get started</span></span>

<span data-ttu-id="12171-109">要将现有 ASP.NET Core 项目设置为在服务中运行，需要执行以下最小更改：</span><span class="sxs-lookup"><span data-stu-id="12171-109">The following minimum changes are required to set up an existing ASP.NET Core project to run in a service:</span></span>

1. <span data-ttu-id="12171-110">在项目文件中：</span><span class="sxs-lookup"><span data-stu-id="12171-110">In the project file:</span></span>

   1. <span data-ttu-id="12171-111">确认是否存在运行时标识符，或将其添加到包含目标框架的 \<PropertyGroup> 中：</span><span class="sxs-lookup"><span data-stu-id="12171-111">Confirm the presence of the runtime identifier or add it to the **\<PropertyGroup>** that contains the target framework:</span></span>

      ::: moniker range=">= aspnetcore-2.1"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="= aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="< aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

   1. <span data-ttu-id="12171-112">为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/) 添加包引用。</span><span class="sxs-lookup"><span data-stu-id="12171-112">Add a package reference for [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/).</span></span>

1. <span data-ttu-id="12171-113">在 `Program.Main` 中，进行下列更改：</span><span class="sxs-lookup"><span data-stu-id="12171-113">Make the following changes in `Program.Main`:</span></span>

   * <span data-ttu-id="12171-114">调用 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)，而不是 `host.Run`。</span><span class="sxs-lookup"><span data-stu-id="12171-114">Call [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice) instead of `host.Run`.</span></span>

   * <span data-ttu-id="12171-115">调用 [UseContentRoot](xref:fundamentals/host/web-host#content-root) 并使用应用的发布位置路径，而不是 `Directory.GetCurrentDirectory()`。</span><span class="sxs-lookup"><span data-stu-id="12171-115">Call [UseContentRoot](xref:fundamentals/host/web-host#content-root) and use a path to the app's published location instead of `Directory.GetCurrentDirectory()`.</span></span>

     ::: moniker range=">= aspnetcore-2.0"

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,12)]

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]

     ::: moniker-end

1. <span data-ttu-id="12171-116">发布应用。</span><span class="sxs-lookup"><span data-stu-id="12171-116">Publish the app.</span></span> <span data-ttu-id="12171-117">使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 或 [Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)。</span><span class="sxs-lookup"><span data-stu-id="12171-117">Use [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) or a [Visual Studio publish profile](xref:host-and-deploy/visual-studio-publish-profiles).</span></span>

   <span data-ttu-id="12171-118">要从命令行发布示例应用，请从项目文件夹中的控制台窗口中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="12171-118">To publish the sample app from the command line, run the following command in a console window from the project folder:</span></span>

   ```console
   dotnet publish --configuration Release
   ```

1. <span data-ttu-id="12171-119">使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具创建服务。</span><span class="sxs-lookup"><span data-stu-id="12171-119">Use the [sc.exe](https://technet.microsoft.com/library/bb490995) command-line tool to create the service.</span></span> <span data-ttu-id="12171-120">`binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。</span><span class="sxs-lookup"><span data-stu-id="12171-120">The `binPath` value is the path to the app's executable, which includes the executable file name.</span></span> <span data-ttu-id="12171-121">等于号和路径开头的引号字符之间需要添加空格。</span><span class="sxs-lookup"><span data-stu-id="12171-121">**The space between the equal sign and the quote character at the start of the path is required.**</span></span>

   ```console
   sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"
   ```

   <span data-ttu-id="12171-122">对于项目文件夹中发布的服务，请使用 publish 文件夹的路径创建服务。</span><span class="sxs-lookup"><span data-stu-id="12171-122">For a service published in the project folder, use the path to the *publish* folder to create the service.</span></span> <span data-ttu-id="12171-123">下例中的服务已实现以下操作：</span><span class="sxs-lookup"><span data-stu-id="12171-123">In the following example, the service is:</span></span>

   * <span data-ttu-id="12171-124">命名为“MyService”。</span><span class="sxs-lookup"><span data-stu-id="12171-124">Named **MyService**.</span></span>
   * <span data-ttu-id="12171-125">发布到 c:\\my_services\\AspNetCoreService\\bin\\Release\\&lt;TARGET_FRAMEWORK&gt;\\publish 文件夹。</span><span class="sxs-lookup"><span data-stu-id="12171-125">Published to the *c:\\my_services\\AspNetCoreService\\bin\\Release\\&lt;TARGET_FRAMEWORK&gt;\\publish* folder.</span></span>
   * <span data-ttu-id="12171-126">由名为 AspNetCoreService.exe 的应用可执行文件表示。</span><span class="sxs-lookup"><span data-stu-id="12171-126">Represented by an app executable named *AspNetCoreService.exe*.</span></span>

   <span data-ttu-id="12171-127">利用管理员特权打开一个命令行界面，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="12171-127">Open a command shell with administrative privileges and run the following command:</span></span>

   ```console
   sc create MyService binPath= "c:\my_services\AspNetCoreService\bin\Release\<TARGET_FRAMEWORK>\publish\AspNetCoreService.exe"
   ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="12171-128">确保 `binPath=` 参数与其值之间存在空格。</span><span class="sxs-lookup"><span data-stu-id="12171-128">Make sure the space is present between the `binPath=` argument and its value.</span></span>
   
   <span data-ttu-id="12171-129">从其他文件夹发布和启动服务：</span><span class="sxs-lookup"><span data-stu-id="12171-129">To publish and start the service from a different folder:</span></span>
   
   1. <span data-ttu-id="12171-130">使用 `dotnet publish` 命令上的 [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) 选项。</span><span class="sxs-lookup"><span data-stu-id="12171-130">Use the [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) option on the `dotnet publish` command.</span></span>
   1. <span data-ttu-id="12171-131">通过使用输出文件夹路径的 `sc.exe` 命令创建服务。</span><span class="sxs-lookup"><span data-stu-id="12171-131">Create the service with the `sc.exe` command using the output folder path.</span></span> <span data-ttu-id="12171-132">在向 `binPath` 提供的路径中包含服务可执行文件的名称。</span><span class="sxs-lookup"><span data-stu-id="12171-132">Include the name of the service's executable in the path provided to `binPath`.</span></span>

1. <span data-ttu-id="12171-133">使用 `sc start <SERVICE_NAME>` 命令启动服务。</span><span class="sxs-lookup"><span data-stu-id="12171-133">Start the service with the `sc start <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="12171-134">要启动示例应用服务，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="12171-134">To start the sample app service, use the following command:</span></span>

   ```console
   sc start MyService
   ```

   <span data-ttu-id="12171-135">此命令需要几秒钟才能启动服务。</span><span class="sxs-lookup"><span data-stu-id="12171-135">The command takes a few seconds to start the service.</span></span>

1. <span data-ttu-id="12171-136">`sc query <SERVICE_NAME>` 命令可用于检查并确定服务状态：</span><span class="sxs-lookup"><span data-stu-id="12171-136">The `sc query <SERVICE_NAME>` command can be used to check the status of the service to determine its status:</span></span>

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   <span data-ttu-id="12171-137">使用以下命令检查示例应用服务的状态：</span><span class="sxs-lookup"><span data-stu-id="12171-137">Use the following command to check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

1. <span data-ttu-id="12171-138">当服务处于 `RUNNING` 状态并且服务是 Web 应用时，在应用所在路径中浏览应用（默认路径为 `http://localhost:5000`；在使用 [HTTPS 重定向中间件](xref:security/enforcing-ssl)时，它将重定向到 `https://localhost:5001`）。</span><span class="sxs-lookup"><span data-stu-id="12171-138">When the service is in the `RUNNING` state and if the service is a web app, browse the app at its path (by default, `http://localhost:5000`, which redirects to `https://localhost:5001` when using [HTTPS Redirection Middleware](xref:security/enforcing-ssl)).</span></span>

   <span data-ttu-id="12171-139">对于示例应用服务，请在 `http://localhost:5000` 浏览应用。</span><span class="sxs-lookup"><span data-stu-id="12171-139">For the sample app service, browse the app at `http://localhost:5000`.</span></span>

1. <span data-ttu-id="12171-140">使用 `sc stop <SERVICE_NAME>` 命令停止服务。</span><span class="sxs-lookup"><span data-stu-id="12171-140">Stop the service with the `sc stop <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="12171-141">以下命令可停止示例应用服务：</span><span class="sxs-lookup"><span data-stu-id="12171-141">The following command stops the sample app service:</span></span>

   ```console
   sc stop MyService
   ```

1. <span data-ttu-id="12171-142">停止服务并经过短暂延迟后，使用 `sc delete <SERVICE_NAME>` 命令卸载服务。</span><span class="sxs-lookup"><span data-stu-id="12171-142">After a short delay to stop a service, uninstall the service with the `sc delete <SERVICE_NAME>` command.</span></span>

   <span data-ttu-id="12171-143">检查示例应用服务的状态：</span><span class="sxs-lookup"><span data-stu-id="12171-143">Check the status of the sample app service:</span></span>

   ```console
   sc query MyService
   ```

   <span data-ttu-id="12171-144">当示例应用服务处于 `STOPPED` 状态时，使用以下命令卸载示例应用服务：</span><span class="sxs-lookup"><span data-stu-id="12171-144">When the sample app service is in the `STOPPED` state, use the following command to uninstall the sample app service:</span></span>

   ```console
   sc delete MyService
   ```

## <a name="provide-a-way-to-run-outside-of-a-service"></a><span data-ttu-id="12171-145">提供在服务之外运行的方法</span><span class="sxs-lookup"><span data-stu-id="12171-145">Provide a way to run outside of a service</span></span>

<span data-ttu-id="12171-146">在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。</span><span class="sxs-lookup"><span data-stu-id="12171-146">It's easier to test and debug when running outside of a service, so it's customary to add code that calls `RunAsService` only under certain conditions.</span></span> <span data-ttu-id="12171-147">例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：</span><span class="sxs-lookup"><span data-stu-id="12171-147">For example, the app can run as a console app with a `--console` command-line argument or if the debugger is attached:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

<span data-ttu-id="12171-148">由于 ASP.NET Core 配置需要命令行参数的名称/值对，因此将先删除 `--console` 开关，然后再将参数传递到 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)。</span><span class="sxs-lookup"><span data-stu-id="12171-148">Because ASP.NET Core configuration requires name-value pairs for command-line arguments, the `--console` switch is removed before the arguments are passed to [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder).</span></span>

> [!NOTE]
> <span data-ttu-id="12171-149">不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。</span><span class="sxs-lookup"><span data-stu-id="12171-149">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

::: moniker-end

## <a name="handle-stopping-and-starting-events"></a><span data-ttu-id="12171-150">处理停止和启动事件</span><span class="sxs-lookup"><span data-stu-id="12171-150">Handle stopping and starting events</span></span>

<span data-ttu-id="12171-151">要处理 [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting)、[OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 和 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 事件，请执行以下额外更改：</span><span class="sxs-lookup"><span data-stu-id="12171-151">To handle [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting), [OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted), and [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) events, make the following additional changes:</span></span>

1. <span data-ttu-id="12171-152">创建从 [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice) 派生的类：</span><span class="sxs-lookup"><span data-stu-id="12171-152">Create a class that derives from [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. <span data-ttu-id="12171-153">创建可将自定义 `WebHostService` 传递给 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run) 的 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 的扩展方法：</span><span class="sxs-lookup"><span data-stu-id="12171-153">Create an extension method for [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) that passes the custom `WebHostService` to [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run):</span></span>

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. <span data-ttu-id="12171-154">在 `Program.Main` 中，调用新扩展方法 `RunAsCustomService`，而不是 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)：</span><span class="sxs-lookup"><span data-stu-id="12171-154">In `Program.Main`, call the new extension method, `RunAsCustomService`, instead of [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice):</span></span>

   ::: moniker range=">= aspnetcore-2.0"

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=14)]

   > [!NOTE]
   > <span data-ttu-id="12171-155">不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。</span><span class="sxs-lookup"><span data-stu-id="12171-155">`isService` isn't passed from `Main` into `CreateWebHostBuilder` because the signature of `CreateWebHostBuilder` must be `CreateWebHostBuilder(string[])` in order for [integration testing](xref:test/integration-tests) to work properly.</span></span>

   ::: moniker-end

   ::: moniker range="< aspnetcore-2.0"

   [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=27)]

   ::: moniker-end

<span data-ttu-id="12171-156">如果自定义 `WebHostService` 代码需要来自依赖项注入（如记录器）的服务，请从 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 属性中获取：</span><span class="sxs-lookup"><span data-stu-id="12171-156">If the custom `WebHostService` code requires a service from dependency injection (such as a logger), obtain it from the [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) property:</span></span>

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="12171-157">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="12171-157">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="12171-158">与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。</span><span class="sxs-lookup"><span data-stu-id="12171-158">Services that interact with requests from the Internet or a corporate network and are behind a proxy or load balancer might require additional configuration.</span></span> <span data-ttu-id="12171-159">有关更多信息，请参见<xref:host-and-deploy/proxy-load-balancer>。</span><span class="sxs-lookup"><span data-stu-id="12171-159">For more information, see <xref:host-and-deploy/proxy-load-balancer>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12171-160">其他资源</span><span class="sxs-lookup"><span data-stu-id="12171-160">Additional resources</span></span>

* <span data-ttu-id="12171-161">[Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）</span><span class="sxs-lookup"><span data-stu-id="12171-161">[Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) (includes HTTPS configuration and SNI support)</span></span>
* <xref:fundamentals/host/web-host>
