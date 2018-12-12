---
title: 对 IIS 上的 ASP.NET Core 进行故障排除
author: guardrex
description: 了解如何诊断 ASP.NET Core 应用的 Internet Information Services (IIS) 部署的问题。
ms.author: riande
ms.custom: mvc
ms.date: 11/26/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 2ff870623de43676be38c5de8f338a7913e885a8
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450705"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="123d5-103">对 IIS 上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="123d5-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="123d5-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="123d5-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="123d5-105">本文说明了如何在使用 [Internet Information Services (IIS)](/iis) 托管时诊断 ASP.NET Core 应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="123d5-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue when hosting with [Internet Information Services (IIS)](/iis).</span></span> <span data-ttu-id="123d5-106">本文提供的信息适用于在 Windows Server 和 Windows 桌面上的 IIS 中托管。</span><span class="sxs-lookup"><span data-stu-id="123d5-106">The information in this article applies to hosting in IIS on Windows Server and Windows Desktop.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="123d5-107">在 Visual Studio 中，ASP.NET Core 项目默认为在调试期间进行 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 托管。</span><span class="sxs-lookup"><span data-stu-id="123d5-107">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="123d5-108">本地调试时出现的“502.5 - 进程失败”或“500.30 - 启动失败”可以使用本主题中的建议进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="123d5-108">A *502.5 - Process Failure* or a *500.30 - Start Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="123d5-109">在 Visual Studio 中，ASP.NET Core 项目默认为在调试期间进行 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 托管。</span><span class="sxs-lookup"><span data-stu-id="123d5-109">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="123d5-110">可以使用本主题中的建议对本地调试进行故障排除时，出现“502.5 进程失败”。</span><span class="sxs-lookup"><span data-stu-id="123d5-110">A *502.5 Process Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

::: moniker-end

<span data-ttu-id="123d5-111">其他故障排除主题：</span><span class="sxs-lookup"><span data-stu-id="123d5-111">Additional troubleshooting topics:</span></span>

<xref:host-and-deploy/azure-apps/troubleshoot>  
<span data-ttu-id="123d5-112">虽然应用服务使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)和 IIS 托管应用，但若要获取特定于应用服务的说明，请参阅专用主题。</span><span class="sxs-lookup"><span data-stu-id="123d5-112">Although App Service uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and IIS to host apps, see the dedicated topic for instructions specific to App Service.</span></span>

<xref:fundamentals/error-handling>  
<span data-ttu-id="123d5-113">了解如何在本地系统上处理 ASP.NET Core 应用在开发期间的错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-113">Discover how to handle errors in ASP.NET Core apps during development on a local system.</span></span>

[<span data-ttu-id="123d5-114">了解如何使用 Visual Studio 进行调试</span><span class="sxs-lookup"><span data-stu-id="123d5-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="123d5-115">本主题介绍了 Visual Studio 调试器的功能。</span><span class="sxs-lookup"><span data-stu-id="123d5-115">This topic introduces the features of the Visual Studio debugger.</span></span>

[<span data-ttu-id="123d5-116">使用 Visual Studio Code 进行调试</span><span class="sxs-lookup"><span data-stu-id="123d5-116">Debugging with Visual Studio Code</span></span>](https://code.visualstudio.com/docs/editor/debugging)  
<span data-ttu-id="123d5-117">了解 Visual Studio Code 中内置的调试支持。</span><span class="sxs-lookup"><span data-stu-id="123d5-117">Learn about the debugging support built into Visual Studio Code.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="123d5-118">应用启动错误</span><span class="sxs-lookup"><span data-stu-id="123d5-118">App startup errors</span></span>

### <a name="5025-process-failure"></a><span data-ttu-id="123d5-119">502.5 进程失败</span><span class="sxs-lookup"><span data-stu-id="123d5-119">502.5 Process Failure</span></span>

<span data-ttu-id="123d5-120">工作进程失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-120">The worker process fails.</span></span> <span data-ttu-id="123d5-121">应用不启动。</span><span class="sxs-lookup"><span data-stu-id="123d5-121">The app doesn't start.</span></span>

<span data-ttu-id="123d5-122">ASP.NET Core 模块尝试启动后端 dotnet 进程，但启动失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-122">The ASP.NET Core Module attempts to start the backend dotnet process but it fails to start.</span></span> <span data-ttu-id="123d5-123">通常可以从“[应用程序事件日志](#application-event-log)”和“[ASP.NET Core 模块 stdout 日志](#aspnet-core-module-stdout-log)”的条目中确定进程启动失败的原因。</span><span class="sxs-lookup"><span data-stu-id="123d5-123">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span> 

<span data-ttu-id="123d5-124">常见的失败情况是，由于目标 ASP.NET Core 共享框架版本不存在，因此应用配置错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-124">A common failure condition is the app is misconfigured due to targeting a version of the ASP.NET Core shared framework that isn't present.</span></span> <span data-ttu-id="123d5-125">检查目标计算机上安装的 ASP.NET Core 共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="123d5-125">Check which versions of the ASP.NET Core shared framework are installed on the target machine.</span></span>

<span data-ttu-id="123d5-126">托管或应用配置错误导致工作进程失败时，将返回“502.5 进程失败”错误页面：</span><span class="sxs-lookup"><span data-stu-id="123d5-126">The *502.5 Process Failure* error page is returned when a hosting or app misconfiguration causes the worker process to fail:</span></span>

![显示“502.5 进程故障”页面的浏览器窗口](troubleshoot/_static/process-failure-page.png)

::: moniker range=">= aspnetcore-2.2"

### <a name="50030-in-process-startup-failure"></a><span data-ttu-id="123d5-128">500.30 进程内启动失败</span><span class="sxs-lookup"><span data-stu-id="123d5-128">500.30 In-Process Startup Failure</span></span>

<span data-ttu-id="123d5-129">工作进程失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-129">The worker process fails.</span></span> <span data-ttu-id="123d5-130">应用不启动。</span><span class="sxs-lookup"><span data-stu-id="123d5-130">The app doesn't start.</span></span>

<span data-ttu-id="123d5-131">ASP.NET Core 模块尝试进程内启动 .NET Core CLR，但启动失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-131">The ASP.NET Core Module attempts to start the .NET Core CLR in-process, but it fails to start.</span></span> <span data-ttu-id="123d5-132">通常可以从“[应用程序事件日志](#application-event-log)”和“[ASP.NET Core 模块 stdout 日志](#aspnet-core-module-stdout-log)”的条目中确定进程启动失败的原因。</span><span class="sxs-lookup"><span data-stu-id="123d5-132">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span> 

<span data-ttu-id="123d5-133">常见的失败情况是，由于目标 ASP.NET Core 共享框架版本不存在，因此应用配置错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-133">A common failure condition is the app is misconfigured due to targeting a version of the ASP.NET Core shared framework that isn't present.</span></span> <span data-ttu-id="123d5-134">检查目标计算机上安装的 ASP.NET Core 共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="123d5-134">Check which versions of the ASP.NET Core shared framework are installed on the target machine.</span></span>

### <a name="5000-in-process-handler-load-failure"></a><span data-ttu-id="123d5-135">500.0 进程内处理程序加载失败</span><span class="sxs-lookup"><span data-stu-id="123d5-135">500.0 In-Process Handler Load Failure</span></span>

<span data-ttu-id="123d5-136">工作进程失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-136">The worker process fails.</span></span> <span data-ttu-id="123d5-137">应用不启动。</span><span class="sxs-lookup"><span data-stu-id="123d5-137">The app doesn't start.</span></span>

<span data-ttu-id="123d5-138">ASP.NET Core 模块无法找到 .NET Core CLR 和进程内请求处理程序 (aspnetcorev2_inprocess.dll)。</span><span class="sxs-lookup"><span data-stu-id="123d5-138">The ASP.NET Core Module fails to find the .NET Core CLR and find the in-process request handler (*aspnetcorev2_inprocess.dll*).</span></span> <span data-ttu-id="123d5-139">检查：</span><span class="sxs-lookup"><span data-stu-id="123d5-139">Check that:</span></span>

* <span data-ttu-id="123d5-140">该应用针对 [Microsoft.AspNetCore.Server.IIS NuGet](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) 包或 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)。</span><span class="sxs-lookup"><span data-stu-id="123d5-140">The app targets either the [Microsoft.AspNetCore.Server.IIS](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) NuGet package or the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>
* <span data-ttu-id="123d5-141">目标计算机上安装了该应用所针对的 ASP.NET Core 共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="123d5-141">The version of the ASP.NET Core shared framework that the app targets is installed on the target machine.</span></span>

### <a name="5000-out-of-process-handler-load-failure"></a><span data-ttu-id="123d5-142">500.0 进程外处理程序加载失败</span><span class="sxs-lookup"><span data-stu-id="123d5-142">500.0 Out-Of-Process Handler Load Failure</span></span>

<span data-ttu-id="123d5-143">工作进程失败。</span><span class="sxs-lookup"><span data-stu-id="123d5-143">The worker process fails.</span></span> <span data-ttu-id="123d5-144">应用不启动。</span><span class="sxs-lookup"><span data-stu-id="123d5-144">The app doesn't start.</span></span>

<span data-ttu-id="123d5-145">ASP.NET Core 模块无法找到进程外托管请求处理程序。</span><span class="sxs-lookup"><span data-stu-id="123d5-145">The ASP.NET Core Module fails to find the out-of-process hosting request handler.</span></span> <span data-ttu-id="123d5-146">请确保 aspnetcorev2.dll 旁边的子文件夹中存在 aspnetcorev2_outofprocess.dll。</span><span class="sxs-lookup"><span data-stu-id="123d5-146">Make sure the *aspnetcorev2_outofprocess.dll* is present in a subfolder next to *aspnetcorev2.dll*.</span></span> 

::: moniker-end

### <a name="500-internal-server-error"></a><span data-ttu-id="123d5-147">500 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="123d5-147">500 Internal Server Error</span></span>

<span data-ttu-id="123d5-148">应用启动，但某个错误阻止了服务器完成请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-148">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="123d5-149">在启动期间或在创建响应时，应用的代码内出现此错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-149">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="123d5-150">响应可能不包含任何内容，或响应可能会在浏览器中显示为“500 内部服务器错误”。</span><span class="sxs-lookup"><span data-stu-id="123d5-150">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="123d5-151">应用程序事件日志通常表明应用正常启动。</span><span class="sxs-lookup"><span data-stu-id="123d5-151">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="123d5-152">从服务器的角度来看，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="123d5-152">From the server's perspective, that's correct.</span></span> <span data-ttu-id="123d5-153">应用已启动，但无法生成有效的响应。</span><span class="sxs-lookup"><span data-stu-id="123d5-153">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="123d5-154">在服务器上[在命令提示符处运行应用](#run-the-app-at-a-command-prompt)或[启用 ASP.NET Core 模块 stdout 日志](#aspnet-core-module-stdout-log)以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="123d5-154">[Run the app at a command prompt](#run-the-app-at-a-command-prompt) on the server or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

### <a name="connection-reset"></a><span data-ttu-id="123d5-155">连接重置</span><span class="sxs-lookup"><span data-stu-id="123d5-155">Connection reset</span></span>

<span data-ttu-id="123d5-156">如果在发送标头后出现错误，则服务器在出现错误时发送“500 内部服务器错误”已经太晚了。</span><span class="sxs-lookup"><span data-stu-id="123d5-156">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="123d5-157">通常在序列化响应的复杂对象期间出现错误时发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="123d5-157">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="123d5-158">此类型的错误在客户端上显示为“连接重置”错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-158">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="123d5-159">[应用程序日志记录](xref:fundamentals/logging/index)可以帮助解决这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-159">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="123d5-160">默认启动限制</span><span class="sxs-lookup"><span data-stu-id="123d5-160">Default startup limits</span></span>

<span data-ttu-id="123d5-161">ASP.NET Core 模块的默认“startupTimeLimit”配置为 120 秒。</span><span class="sxs-lookup"><span data-stu-id="123d5-161">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="123d5-162">保留默认值时，在模块记录进程故障之前，可能最多需要两分钟来启动应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-162">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="123d5-163">有关配置模块的信息，请参阅 [aspNetCore 元素的属性](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="123d5-163">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="123d5-164">解决应用启动错误</span><span class="sxs-lookup"><span data-stu-id="123d5-164">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="123d5-165">应用程序事件日志</span><span class="sxs-lookup"><span data-stu-id="123d5-165">Application Event Log</span></span>

<span data-ttu-id="123d5-166">访问应用程序事件日志：</span><span class="sxs-lookup"><span data-stu-id="123d5-166">Access the Application Event Log:</span></span>

1. <span data-ttu-id="123d5-167">打开“开始”菜单，搜索“事件查看器”，然后选择“事件查看器”应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-167">Open the Start menu, search for **Event Viewer**, and then select the **Event Viewer** app.</span></span>
1. <span data-ttu-id="123d5-168">在“事件查看器”中，打开“Windows 日志”节点。</span><span class="sxs-lookup"><span data-stu-id="123d5-168">In **Event Viewer**, open the **Windows Logs** node.</span></span>
1. <span data-ttu-id="123d5-169">选择“应用程序”以打开应用程序事件日志。</span><span class="sxs-lookup"><span data-stu-id="123d5-169">Select **Application** to open the Application Event Log.</span></span>
1. <span data-ttu-id="123d5-170">搜索与失败应用相关联的错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-170">Search for errors associated with the failing app.</span></span> <span data-ttu-id="123d5-171">错误具有“源”列中“IIS AspNetCore 模块”或“IIS Express AspNetCore 模块”的值。</span><span class="sxs-lookup"><span data-stu-id="123d5-171">Errors have a value of *IIS AspNetCore Module* or *IIS Express AspNetCore Module* in the *Source* column.</span></span>

### <a name="run-the-app-at-a-command-prompt"></a><span data-ttu-id="123d5-172">在命令提示符处运行应用</span><span class="sxs-lookup"><span data-stu-id="123d5-172">Run the app at a command prompt</span></span>

<span data-ttu-id="123d5-173">许多启动错误未在应用程序事件日志中生成有用信息。</span><span class="sxs-lookup"><span data-stu-id="123d5-173">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="123d5-174">可以通过在托管系统上在命令提示符处运行应用来找到某些错误的原因。</span><span class="sxs-lookup"><span data-stu-id="123d5-174">You can find the cause of some errors by running the app at a command prompt on the hosting system.</span></span>

#### <a name="framework-dependent-deployment"></a><span data-ttu-id="123d5-175">依赖框架的部署</span><span class="sxs-lookup"><span data-stu-id="123d5-175">Framework-dependent deployment</span></span>

<span data-ttu-id="123d5-176">如果应用是[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)：</span><span class="sxs-lookup"><span data-stu-id="123d5-176">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span></span>

1. <span data-ttu-id="123d5-177">在命令提示符处，导航到部署文件夹并通过使用 dotnet.exe 执行应用的程序集来运行应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-177">At a command prompt, navigate to the deployment folder and run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="123d5-178">在以下命令中，替换 \<assembly_name> 的应用程序集的名称：`dotnet .\<assembly_name>.dll`。</span><span class="sxs-lookup"><span data-stu-id="123d5-178">In the following command, substitute the name of the app's assembly for \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span></span>
1. <span data-ttu-id="123d5-179">来自应用且显示任何错误的控制台输出将写入控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="123d5-179">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="123d5-180">如果向应用发出请求时出现错误，请向 Kestrel 侦听所在的主机和端口发出请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-180">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="123d5-181">如果使用默认主机和端口，请向 `http://localhost:5000/` 发出请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-181">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="123d5-182">如果应用在 Kestrel 终结点地址处正常响应，则问题更可能与反向代理配置相关，而不太可能在于应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-182">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

#### <a name="self-contained-deployment"></a><span data-ttu-id="123d5-183">独立部署</span><span class="sxs-lookup"><span data-stu-id="123d5-183">Self-contained deployment</span></span>

<span data-ttu-id="123d5-184">如果应用是[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)：</span><span class="sxs-lookup"><span data-stu-id="123d5-184">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd):</span></span>

1. <span data-ttu-id="123d5-185">在命令提示符处，导航到部署文件夹并运行应用的可执行文件。</span><span class="sxs-lookup"><span data-stu-id="123d5-185">At a command prompt, navigate to the deployment folder and run the app's executable.</span></span> <span data-ttu-id="123d5-186">在以下命令中，替换 \<assembly_name> 的应用程序集的名称：`<assembly_name>.exe`。</span><span class="sxs-lookup"><span data-stu-id="123d5-186">In the following command, substitute the name of the app's assembly for \<assembly_name>: `<assembly_name>.exe`.</span></span>
1. <span data-ttu-id="123d5-187">来自应用且显示任何错误的控制台输出将写入控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="123d5-187">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="123d5-188">如果向应用发出请求时出现错误，请向 Kestrel 侦听所在的主机和端口发出请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-188">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="123d5-189">如果使用默认主机和端口，请向 `http://localhost:5000/` 发出请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-189">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="123d5-190">如果应用在 Kestrel 终结点地址处正常响应，则问题更可能与反向代理配置相关，而不太可能在于应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-190">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="123d5-191">ASP.NET Core 模块 stdout 日志</span><span class="sxs-lookup"><span data-stu-id="123d5-191">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="123d5-192">若要启用和查看 stdout 日志，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="123d5-192">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="123d5-193">在托管系统上导航到站点的部署文件夹。</span><span class="sxs-lookup"><span data-stu-id="123d5-193">Navigate to the site's deployment folder on the hosting system.</span></span>
1. <span data-ttu-id="123d5-194">如果 logs 文件夹不存在，请创建该文件夹。</span><span class="sxs-lookup"><span data-stu-id="123d5-194">If the *logs* folder isn't present, create the folder.</span></span> <span data-ttu-id="123d5-195">有关如何启用 MSBuild 以在部署中自动创建 logs 文件夹的说明，请参阅[目录结构](xref:host-and-deploy/directory-structure)主题。</span><span class="sxs-lookup"><span data-stu-id="123d5-195">For instructions on how to enable MSBuild to create the *logs* folder in the deployment automatically, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>
1. <span data-ttu-id="123d5-196">编辑 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="123d5-196">Edit the *web.config* file.</span></span> <span data-ttu-id="123d5-197">将“stdoutLogEnabled”设置为 `true` 并更改“stdoutLogFile”路径以指向 logs 文件夹（例如，`.\logs\stdout`）。</span><span class="sxs-lookup"><span data-stu-id="123d5-197">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to point to the *logs* folder (for example, `.\logs\stdout`).</span></span> <span data-ttu-id="123d5-198">路径中的 `stdout` 是日志文件名的前缀。</span><span class="sxs-lookup"><span data-stu-id="123d5-198">`stdout` in the path is the log file name prefix.</span></span> <span data-ttu-id="123d5-199">创建日志时，将自动添加时间戳、进程 ID 和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="123d5-199">A timestamp, process id, and file extension are added automatically when the log is created.</span></span> <span data-ttu-id="123d5-200">如果将 `stdout` 用作文件名的前缀，典型的日志文件将命名为“stdout_20180205184032_5412.log”。</span><span class="sxs-lookup"><span data-stu-id="123d5-200">Using `stdout` as the file name prefix, a typical log file is named *stdout_20180205184032_5412.log*.</span></span> 
1. <span data-ttu-id="123d5-201">请确保应用程序池的标识具有对日志文件夹的写入权限。</span><span class="sxs-lookup"><span data-stu-id="123d5-201">Ensure your application pool's identity has write permissions to the *logs* folder.</span></span>
1. <span data-ttu-id="123d5-202">保存已更新的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="123d5-202">Save the updated *web.config* file.</span></span>
1. <span data-ttu-id="123d5-203">向应用发出请求。</span><span class="sxs-lookup"><span data-stu-id="123d5-203">Make a request to the app.</span></span>
1. <span data-ttu-id="123d5-204">导航到 logs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="123d5-204">Navigate to the *logs* folder.</span></span> <span data-ttu-id="123d5-205">查找并打开最新的 stdout 日志。</span><span class="sxs-lookup"><span data-stu-id="123d5-205">Find and open the most recent stdout log.</span></span>
1. <span data-ttu-id="123d5-206">研究日志以查找错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-206">Study the log for errors.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="123d5-207">故障排除完成后，禁用 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="123d5-207">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="123d5-208">编辑 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="123d5-208">Edit the *web.config* file.</span></span>
1. <span data-ttu-id="123d5-209">将“stdoutLogEnabled”设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="123d5-209">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="123d5-210">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="123d5-210">Save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="123d5-211">无法禁用 stdout 日志可能会导致应用或服务器出现故障。</span><span class="sxs-lookup"><span data-stu-id="123d5-211">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="123d5-212">日志文件大小或创建的日志文件数没有限制。</span><span class="sxs-lookup"><span data-stu-id="123d5-212">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="123d5-213">对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="123d5-213">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="123d5-214">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="123d5-214">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="enable-the-developer-exception-page"></a><span data-ttu-id="123d5-215">启用开发人员异常页面</span><span class="sxs-lookup"><span data-stu-id="123d5-215">Enable the Developer Exception Page</span></span>

<span data-ttu-id="123d5-216">`ASPNETCORE_ENVIRONMENT` [环境变量可以添加到 web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 以在开发环境中运行应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-216">The `ASPNETCORE_ENVIRONMENT` [environment variable can be added to web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) to run the app in the Development environment.</span></span> <span data-ttu-id="123d5-217">只要在应用启动时环境不被主机生成器上的 `UseEnvironment` 重写，设置环境变量就会在运行应用时显示“[开发人员异常页面](xref:fundamentals/error-handling)”。</span><span class="sxs-lookup"><span data-stu-id="123d5-217">As long as the environment isn't overridden in app startup by `UseEnvironment` on the host builder, setting the environment variable allows the [Developer Exception Page](xref:fundamentals/error-handling) to appear when the app is run.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout"
      hostingModel="inprocess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

<span data-ttu-id="123d5-218">仅建议在未向 Internet 公开的暂存服务器和测试服务器上设置 `ASPNETCORE_ENVIRONMENT` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="123d5-218">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` is only recommended for use on staging and testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="123d5-219">在故障排除后从 web.config 文件中删除环境变量。</span><span class="sxs-lookup"><span data-stu-id="123d5-219">Remove the environment variable from the *web.config* file after troubleshooting.</span></span> <span data-ttu-id="123d5-220">有关设置 web.config 中的环境变量的信息，请参阅 [aspNetCore 的 environmentVariables 子元素](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="123d5-220">For information on setting environment variables in *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="123d5-221">常见启动错误</span><span class="sxs-lookup"><span data-stu-id="123d5-221">Common startup errors</span></span>

<span data-ttu-id="123d5-222">请参阅 <xref:host-and-deploy/azure-iis-errors-reference>。</span><span class="sxs-lookup"><span data-stu-id="123d5-222">See <xref:host-and-deploy/azure-iis-errors-reference>.</span></span> <span data-ttu-id="123d5-223">参考主题介绍了阻止应用启动的大部分常见问题。</span><span class="sxs-lookup"><span data-stu-id="123d5-223">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="obtain-data-from-an-app"></a><span data-ttu-id="123d5-224">从应用中获取数据</span><span class="sxs-lookup"><span data-stu-id="123d5-224">Obtain data from an app</span></span>

<span data-ttu-id="123d5-225">如果应用能够响应请求，则使用终端内联中间件从应用中获取请求、连接和其他数据。</span><span class="sxs-lookup"><span data-stu-id="123d5-225">If an app is capable of responding to requests, obtain request, connection, and additional data from the app using terminal inline middleware.</span></span> <span data-ttu-id="123d5-226">有关详细信息和示例代码，请参阅<xref:test/troubleshoot#obtain-data-from-an-app>。</span><span class="sxs-lookup"><span data-stu-id="123d5-226">For more information and sample code, see <xref:test/troubleshoot#obtain-data-from-an-app>.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="123d5-227">应用缓慢或挂起</span><span class="sxs-lookup"><span data-stu-id="123d5-227">Slow or hanging app</span></span>

<span data-ttu-id="123d5-228">当应用响应缓慢或挂起请求时，获取并分析[转储文件](/visualstudio/debugger/using-dump-files)。</span><span class="sxs-lookup"><span data-stu-id="123d5-228">When an app responds slowly or hangs on a request, obtain and analyze a [dump file](/visualstudio/debugger/using-dump-files).</span></span> <span data-ttu-id="123d5-229">可以使用以下任何工具获取转储文件：</span><span class="sxs-lookup"><span data-stu-id="123d5-229">Dump files can be obtained using any of the following tools:</span></span>

* [<span data-ttu-id="123d5-230">ProcDump</span><span class="sxs-lookup"><span data-stu-id="123d5-230">ProcDump</span></span>](/sysinternals/downloads/procdump)
* [<span data-ttu-id="123d5-231">DebugDiag</span><span class="sxs-lookup"><span data-stu-id="123d5-231">DebugDiag</span></span>](https://www.microsoft.com/download/details.aspx?id=49924)
* <span data-ttu-id="123d5-232">WinDbg：[下载 Windows 调试工具](https://developer.microsoft.com/windows/hardware/download-windbg)，[使用 WinDbg 进行调试](/windows-hardware/drivers/debugger/debugging-using-windbg)</span><span class="sxs-lookup"><span data-stu-id="123d5-232">WinDbg: [Download Debugging tools for Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debugging Using WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="123d5-233">远程调试</span><span class="sxs-lookup"><span data-stu-id="123d5-233">Remote debugging</span></span>

<span data-ttu-id="123d5-234">请参阅 Visual Studio 文档中的[在 Visual Studio 2017 中远程调试远程 IIS 计算机上的 ASP.NET Core](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer)。</span><span class="sxs-lookup"><span data-stu-id="123d5-234">See [Remote Debug ASP.NET Core on a Remote IIS Computer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in the Visual Studio documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="123d5-235">Application Insights</span><span class="sxs-lookup"><span data-stu-id="123d5-235">Application Insights</span></span>

<span data-ttu-id="123d5-236">[Application Insights](/azure/application-insights/) 提供来自 IIS 托管的应用的遥测，包括错误日志记录和报告功能。</span><span class="sxs-lookup"><span data-stu-id="123d5-236">[Application Insights](/azure/application-insights/) provides telemetry from apps hosted by IIS, including error logging and reporting features.</span></span> <span data-ttu-id="123d5-237">当应用的日志记录功能变得可用时，Application Insights 只能报告应用启动后出现的错误。</span><span class="sxs-lookup"><span data-stu-id="123d5-237">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="123d5-238">有关详细信息，请参阅[用于 ASP.NET Core 的 Application Insights](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="123d5-238">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="additional-advice"></a><span data-ttu-id="123d5-239">其他建议</span><span class="sxs-lookup"><span data-stu-id="123d5-239">Additional advice</span></span>

<span data-ttu-id="123d5-240">有时，正常运行的应用在开发计算机上升级 .NET Core SDK 或在应用内升级包版本后立即出现故障。</span><span class="sxs-lookup"><span data-stu-id="123d5-240">Sometimes a functioning app fails immediately after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="123d5-241">在某些情况下，不同的包可能在执行主要升级时中断应用。</span><span class="sxs-lookup"><span data-stu-id="123d5-241">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="123d5-242">可以按照以下说明来修复其中大部分问题：</span><span class="sxs-lookup"><span data-stu-id="123d5-242">Most of these issues can be fixed by following these instructions:</span></span>

1. <span data-ttu-id="123d5-243">删除 bin 和 obj 文件夹。</span><span class="sxs-lookup"><span data-stu-id="123d5-243">Delete the *bin* and *obj* folders.</span></span>
1. <span data-ttu-id="123d5-244">清除 %UserProfile%\\.nuget\\packages 和 %LocalAppData%\\Nuget\\v3-cache 中的包缓存。</span><span class="sxs-lookup"><span data-stu-id="123d5-244">Clear the package caches at *%UserProfile%\\.nuget\\packages* and *%LocalAppData%\\Nuget\\v3-cache*.</span></span>
1. <span data-ttu-id="123d5-245">还原并重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="123d5-245">Restore and rebuild the project.</span></span>
1. <span data-ttu-id="123d5-246">确认在重新部署应用之前已完全删除服务器上的先前部署。</span><span class="sxs-lookup"><span data-stu-id="123d5-246">Confirm that the prior deployment on the server has been completely deleted prior to redeploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="123d5-247">清除包缓存的简便方法是从命令提示符执行 `dotnet nuget locals all --clear`。</span><span class="sxs-lookup"><span data-stu-id="123d5-247">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
>
> <span data-ttu-id="123d5-248">清除包缓存还可通过使用 [nuget.exe](https://www.nuget.org/downloads) 工具并执行命令 `nuget locals all -clear` 来完成。</span><span class="sxs-lookup"><span data-stu-id="123d5-248">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="123d5-249">*nuget.exe* 不是与 Windows 桌面操作系统的捆绑安装，必须从 [NuGet 网站](https://www.nuget.org/downloads)中单独获取。</span><span class="sxs-lookup"><span data-stu-id="123d5-249">*nuget.exe* isn't a bundled install with the Windows desktop operating system and must be obtained separately from the [NuGet website](https://www.nuget.org/downloads).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="123d5-250">其他资源</span><span class="sxs-lookup"><span data-stu-id="123d5-250">Additional resources</span></span>

* <xref:test/troubleshoot>
* <xref:fundamentals/error-handling>
* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/azure-apps/troubleshoot>
