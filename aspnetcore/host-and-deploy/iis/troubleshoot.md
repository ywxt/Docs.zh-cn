---
title: 解决在 IIS 上的 ASP.NET 核心
author: guardrex
description: 了解如何诊断问题的 ASP.NET Core 应用的 Internet 信息服务 (IIS) 部署。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/07/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: e44892d2022ca1a176cee9d027e220e196c6572d
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="d0fe4-103">解决在 IIS 上的 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="d0fe4-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="d0fe4-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="d0fe4-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d0fe4-105">本文说明了如何诊断 ASP.NET Core 应用启动问题使用承载时[Internet 信息服务 (IIS)](/iis)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue when hosting with [Internet Information Services (IIS)](/iis).</span></span> <span data-ttu-id="d0fe4-106">这篇文章中的信息适用于在 Windows Server 和 Windows 桌面上的 IIS 中承载。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-106">The information in this article applies to hosting in IIS on Windows Server and Windows Desktop.</span></span>

<span data-ttu-id="d0fe4-107">在 Visual Studio 中，ASP.NET Core 项目默认为[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)承载在调试过程。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-107">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="d0fe4-108">A *502.5 进程失败*本地调试可能会使用本主题中的建议的 troubleshooted 时发生。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-108">A *502.5 Process Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

<span data-ttu-id="d0fe4-109">其他故障排除主题：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-109">Additional troubleshooting topics:</span></span>

[<span data-ttu-id="d0fe4-110">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="d0fe4-110">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="d0fe4-111">尽管应用程序服务使用[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)和 IIS 承载应用程序，请参阅说明特定于应用程序服务的专用的主题。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-111">Although App Service uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and IIS to host apps, see the dedicated topic for instructions specific to App Service.</span></span>

[<span data-ttu-id="d0fe4-112">处理错误</span><span class="sxs-lookup"><span data-stu-id="d0fe4-112">Handle errors</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="d0fe4-113">了解如何在本地系统上的开发过程中处理 ASP.NET Core 应用中的错误。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-113">Discover how to handle errors in ASP.NET Core apps during development on a local system.</span></span>

[<span data-ttu-id="d0fe4-114">了解如何使用 Visual Studio 进行调试</span><span class="sxs-lookup"><span data-stu-id="d0fe4-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="d0fe4-115">本主题介绍 Visual Studio 调试器的功能。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-115">This topic introduces the features of the Visual Studio debugger.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="d0fe4-116">应用程序启动错误</span><span class="sxs-lookup"><span data-stu-id="d0fe4-116">App startup errors</span></span>

<span data-ttu-id="d0fe4-117">**502.5 进程故障**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-117">**502.5 Process Failure**</span></span>  
<span data-ttu-id="d0fe4-118">工作进程将失败。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-118">The worker process fails.</span></span> <span data-ttu-id="d0fe4-119">不启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-119">The app doesn't start.</span></span>

<span data-ttu-id="d0fe4-120">ASP.NET 核心模块尝试启动工作进程，但它无法启动。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-120">The ASP.NET Core Module attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="d0fe4-121">进程启动失败的原因通常根据中的条目[应用程序事件日志](#application-event-log)和[ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-121">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span>

<span data-ttu-id="d0fe4-122">*502.5 进程失败*当承载或应用程序配置错误导致工作进程失败时返回错误页：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-122">The *502.5 Process Failure* error page is returned when a hosting or app misconfiguration causes the worker process to fail:</span></span>

![显示 502.5 进程失败页的浏览器窗口](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="d0fe4-124">**500 内部服务器错误**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-124">**500 Internal Server Error**</span></span>  
<span data-ttu-id="d0fe4-125">启动该应用程序，但某个错误阻止在完成请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-125">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="d0fe4-126">启动过程中或创建响应时，应用程序的代码中出现此错误。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-126">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="d0fe4-127">响应可能包含任何内容，或响应可能显示为*500 内部服务器错误*浏览器中。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-127">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="d0fe4-128">应用程序事件日志通常表明应用程序正常启动。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-128">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="d0fe4-129">从服务器的角度来看，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-129">From the server's perspective, that's correct.</span></span> <span data-ttu-id="d0fe4-130">应用程序未启动，但它无法生成有效的响应。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-130">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="d0fe4-131">[在命令提示符下运行应用程序](#run-the-app-at-a-command-prompt)服务器上或[启用 ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-131">[Run the app at a command prompt](#run-the-app-at-a-command-prompt) on the server or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

<span data-ttu-id="d0fe4-132">**连接重置**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-132">**Connection reset**</span></span>

<span data-ttu-id="d0fe4-133">如果发送标头后，将发生错误，则服务器尝试发送太晚**500 内部服务器错误**发生错误时。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-133">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="d0fe4-134">响应的复杂对象的序列化期间发生错误时经常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-134">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="d0fe4-135">此类型的错误显示为*连接重置*客户端上的错误。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-135">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="d0fe4-136">[应用程序日志记录](xref:fundamentals/logging/index)可以帮助解决这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-136">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="d0fe4-137">默认启动限制</span><span class="sxs-lookup"><span data-stu-id="d0fe4-137">Default startup limits</span></span>

<span data-ttu-id="d0fe4-138">ASP.NET 核心模块配置了默认值*startupTimeLimit*的 120 秒。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-138">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="d0fe4-139">时保留为默认值，应用可能需要最多两分钟，以启动之前模块记录进程失败。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-139">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="d0fe4-140">有关模块的配置的信息，请参阅[aspNetCore 元素的特性的](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-140">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="d0fe4-141">应用程序启动错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="d0fe4-141">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="d0fe4-142">应用程序事件日志</span><span class="sxs-lookup"><span data-stu-id="d0fe4-142">Application Event Log</span></span>

<span data-ttu-id="d0fe4-143">访问应用程序事件日志：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-143">Access the Application Event Log:</span></span>

1. <span data-ttu-id="d0fe4-144">打开开始菜单，搜索**事件查看器**，然后选择**事件查看器**应用。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-144">Open the Start menu, search for **Event Viewer**, and then select the **Event Viewer** app.</span></span>
1. <span data-ttu-id="d0fe4-145">在**事件查看器**，打开**Windows 日志**节点。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-145">In **Event Viewer**, open the **Windows Logs** node.</span></span>
1. <span data-ttu-id="d0fe4-146">选择**应用程序**以打开应用程序事件日志。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-146">Select **Application** to open the Application Event Log.</span></span>
1. <span data-ttu-id="d0fe4-147">搜索与失败应用相关联的错误。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-147">Search for errors associated with the failing app.</span></span> <span data-ttu-id="d0fe4-148">错误都具有值*IIS AspNetCore 模块*或*IIS Express AspNetCore 模块*中*源*列。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-148">Errors have a value of *IIS AspNetCore Module* or *IIS Express AspNetCore Module* in the *Source* column.</span></span>

### <a name="run-the-app-at-a-command-prompt"></a><span data-ttu-id="d0fe4-149">在命令提示符下运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d0fe4-149">Run the app at a command prompt</span></span>

<span data-ttu-id="d0fe4-150">许多启动错误未生成应用程序事件日志中的有用信息。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-150">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="d0fe4-151">你可以通过在命令提示符下运行应用，在主机系统上找到某些错误的原因。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-151">You can find the cause of some errors by running the app at a command prompt on the hosting system.</span></span>

<span data-ttu-id="d0fe4-152">**依赖于框架的部署**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-152">**Framework-dependent deployment**</span></span>

<span data-ttu-id="d0fe4-153">如果在应用程序处于[framework 相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span><span class="sxs-lookup"><span data-stu-id="d0fe4-153">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span></span>

1. <span data-ttu-id="d0fe4-154">在命令提示符处，导航到部署文件夹，并通过执行应用程序的程序集与运行应用*dotnet.exe*。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-154">At a command prompt, navigate to the deployment folder and run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="d0fe4-155">在下面的命令中，应用程序的程序集的名称替换\<程序集 _ 名称 >: `dotnet .\<assembly_name>.dll`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-155">In the following command, substitute the name of the app's assembly for \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span></span>
1. <span data-ttu-id="d0fe4-156">控制台应用程序中，显示任何错误，从输出写入到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-156">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="d0fe4-157">如果向应用程序发出请求时出现错误，请向主机和其中 Kestrel 侦听的端口发出请求。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-157">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="d0fe4-158">使用默认主机和开机自检，请发出请求以`http://localhost:5000/`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-158">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="d0fe4-159">如果应用程序通常响应 Kestrel 终结点地址，该问题更可能是相关的反向代理配置和不太可能在应用内。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-159">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

<span data-ttu-id="d0fe4-160">**自包含的部署**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-160">**Self-contained deployment**</span></span>

<span data-ttu-id="d0fe4-161">如果在应用程序处于[独立的部署](/dotnet/core/deploying/#self-contained-deployments-scd):</span><span class="sxs-lookup"><span data-stu-id="d0fe4-161">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd):</span></span>

1. <span data-ttu-id="d0fe4-162">在命令提示符处，导航到部署文件夹并运行应用程序的可执行文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-162">At a command prompt, navigate to the deployment folder and run the app's executable.</span></span> <span data-ttu-id="d0fe4-163">在下面的命令中，应用程序的程序集的名称替换\<程序集 _ 名称 >: `<assembly_name>.exe`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-163">In the following command, substitute the name of the app's assembly for \<assembly_name>: `<assembly_name>.exe`.</span></span>
1. <span data-ttu-id="d0fe4-164">控制台应用程序中，显示任何错误，从输出写入到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-164">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="d0fe4-165">如果向应用程序发出请求时出现错误，请向主机和其中 Kestrel 侦听的端口发出请求。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-165">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="d0fe4-166">使用默认主机和开机自检，请发出请求以`http://localhost:5000/`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-166">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="d0fe4-167">如果应用程序通常响应 Kestrel 终结点地址，该问题更可能是相关的反向代理配置和不太可能在应用内。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-167">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="d0fe4-168">ASP.NET 核心模块 stdout 日志</span><span class="sxs-lookup"><span data-stu-id="d0fe4-168">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="d0fe4-169">用于启用和查看 stdout 日志：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-169">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="d0fe4-170">导航到主机系统上的站点的部署文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-170">Navigate to the site's deployment folder on the hosting system.</span></span>
1. <span data-ttu-id="d0fe4-171">如果*日志*文件夹不存在、 创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-171">If the *logs* folder isn't present, create the folder.</span></span> <span data-ttu-id="d0fe4-172">有关如何启用 MSBuild 的说明创建*日志*部署中的文件夹自动，请参阅[目录结构](xref:host-and-deploy/directory-structure)主题。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-172">For instructions on how to enable MSBuild to create the *logs* folder in the deployment automatically, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>
1. <span data-ttu-id="d0fe4-173">编辑*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-173">Edit the *web.config* file.</span></span> <span data-ttu-id="d0fe4-174">设置**stdoutLogEnabled**到`true`和更改**stdoutLogFile**路径以指向*日志*文件夹 (例如， `.\logs\stdout`)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-174">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to point to the *logs* folder (for example, `.\logs\stdout`).</span></span> <span data-ttu-id="d0fe4-175">`stdout` 在路径中是日志文件名称前缀。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-175">`stdout` in the path is the log file name prefix.</span></span> <span data-ttu-id="d0fe4-176">时间戳、 进程 id 和文件扩展名自动添加了时创建日志。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-176">A timestamp, process id, and file extension are added automatically when the log is created.</span></span> <span data-ttu-id="d0fe4-177">使用`stdout`作为文件名称前缀，典型的日志文件名为*stdout_20180205184032_5412.log*。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-177">Using `stdout` as the file name prefix, a typical log file is named *stdout_20180205184032_5412.log*.</span></span> 
1. <span data-ttu-id="d0fe4-178">保存已更新*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-178">Save the updated *web.config* file.</span></span>
1. <span data-ttu-id="d0fe4-179">向应用程序发出的请求。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-179">Make a request to the app.</span></span>
1. <span data-ttu-id="d0fe4-180">导航到*日志*文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-180">Navigate to the *logs* folder.</span></span> <span data-ttu-id="d0fe4-181">查找并打开最新的标准输出日志。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-181">Find and open the most recent stdout log.</span></span>
1. <span data-ttu-id="d0fe4-182">研究错误的日志。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-182">Study the log for errors.</span></span>

<span data-ttu-id="d0fe4-183">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="d0fe4-183">**Important!**</span></span> <span data-ttu-id="d0fe4-184">禁用完成故障排除时，日志记录 stdout。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-184">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="d0fe4-185">编辑*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-185">Edit the *web.config* file.</span></span>
1. <span data-ttu-id="d0fe4-186">设置**stdoutLogEnabled**到`false`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-186">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="d0fe4-187">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-187">Save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="d0fe4-188">若要禁用 stdout 日志可能会导致应用程序或服务器失败。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-188">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="d0fe4-189">日志文件大小或创建的日志文件数没有限制。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-189">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="d0fe4-190">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-190">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="d0fe4-191">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-191">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="enabling-the-developer-exception-page"></a><span data-ttu-id="d0fe4-192">启用开发人员异常页</span><span class="sxs-lookup"><span data-stu-id="d0fe4-192">Enabling the Developer Exception Page</span></span>

<span data-ttu-id="d0fe4-193">`ASPNETCORE_ENVIRONMENT` [环境变量可以添加到 web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)在开发环境中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-193">The `ASPNETCORE_ENVIRONMENT` [environment variable can be added to web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) to run the app in the Development environment.</span></span> <span data-ttu-id="d0fe4-194">只要环境不重写中的应用程序启动`UseEnvironment`主机生成器中，在设置环境变量允许[开发人员异常页](xref:fundamentals/error-handling)显示应用程序运行时。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-194">As long as the environment isn't overridden in app startup by `UseEnvironment` on the host builder, setting the environment variable allows the [Developer Exception Page](xref:fundamentals/error-handling) to appear when the app is run.</span></span>

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

<span data-ttu-id="d0fe4-195">设置环境变量中的`ASPNETCORE_ENVIRONMENT`建议只在过渡和测试不公开到 Internet 的服务器上使用。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-195">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` is only recommended for use on staging and testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="d0fe4-196">删除从该环境变量*web.config*诊断后的文件。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-196">Remove the environment variable from the *web.config* file after troubleshooting.</span></span> <span data-ttu-id="d0fe4-197">有关设置环境变量的信息*web.config*，请参阅[environmentVariables 子元素的 aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-197">For information on setting environment variables in *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="d0fe4-198">常见的启动错误</span><span class="sxs-lookup"><span data-stu-id="d0fe4-198">Common startup errors</span></span> 

<span data-ttu-id="d0fe4-199">请参阅[ASP.NET 核心常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-199">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="d0fe4-200">中的参考主题介绍了大部分常见防止应用程序启动的问题。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-200">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="d0fe4-201">慢速或悬挂应用程序</span><span class="sxs-lookup"><span data-stu-id="d0fe4-201">Slow or hanging app</span></span>

<span data-ttu-id="d0fe4-202">当应用程序响应速度很慢或挂起的请求时，获取并分析[转储文件](/visualstudio/debugger/using-dump-files)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-202">When an app responds slowly or hangs on a request, obtain and analyze a [dump file](/visualstudio/debugger/using-dump-files).</span></span> <span data-ttu-id="d0fe4-203">可以使用任何以下工具获取转储文件：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-203">Dump files can be obtained using any of the following tools:</span></span>

* [<span data-ttu-id="d0fe4-204">ProcDump</span><span class="sxs-lookup"><span data-stu-id="d0fe4-204">ProcDump</span></span>](/sysinternals/downloads/procdump)
* [<span data-ttu-id="d0fe4-205">DebugDiag</span><span class="sxs-lookup"><span data-stu-id="d0fe4-205">DebugDiag</span></span>](https://www.microsoft.com/download/details.aspx?id=49924)
* <span data-ttu-id="d0fe4-206">WinDbg:[下载适用于 Windows 调试工具](https://developer.microsoft.com/windows/hardware/download-windbg)，[调试使用 WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span><span class="sxs-lookup"><span data-stu-id="d0fe4-206">WinDbg: [Download Debugging tools for Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debugging Using WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="d0fe4-207">远程调试</span><span class="sxs-lookup"><span data-stu-id="d0fe4-207">Remote debugging</span></span>

<span data-ttu-id="d0fe4-208">请参阅[在 Visual Studio 2017 远程 IIS 计算机上的远程调试 ASP.NET Core](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) Visual Studio 文档中。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-208">See [Remote Debug ASP.NET Core on a Remote IIS Computer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in the Visual Studio documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="d0fe4-209">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d0fe4-209">Application Insights</span></span>

<span data-ttu-id="d0fe4-210">[Application Insights](/azure/application-insights/)提供从托管的 IIS，包括错误日志记录和报告功能的应用程序的遥测。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-210">[Application Insights](/azure/application-insights/) provides telemetry from apps hosted by IIS, including error logging and reporting features.</span></span> <span data-ttu-id="d0fe4-211">Application Insights 只能针对在应用程序启动时应用的日志记录功能变得可用之后发生的错误报告。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-211">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="d0fe4-212">有关详细信息，请参阅[Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-212">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="additional-troubleshooting-advice"></a><span data-ttu-id="d0fe4-213">其他故障排除建议</span><span class="sxs-lookup"><span data-stu-id="d0fe4-213">Additional troubleshooting advice</span></span>

<span data-ttu-id="d0fe4-214">有时会正常运行的应用程序升级任一.NET 核心 SDK 在应用内的开发计算机或包版本之后立即失败。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-214">Sometimes a functioning app fails immediately after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="d0fe4-215">在某些情况下，不同的包可能在执行主要升级时中断应用。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-215">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="d0fe4-216">可以按以下说明来修复大部分这些问题：</span><span class="sxs-lookup"><span data-stu-id="d0fe4-216">Most of these issues can be fixed by following these instructions:</span></span>

1. <span data-ttu-id="d0fe4-217">删除*bin*和*obj*文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-217">Delete the *bin* and *obj* folders.</span></span>
1. <span data-ttu-id="d0fe4-218">在包的缓存清除*%userprofile%\\.nuget\\包*和*%localappdata%\\Nuget\\v3 缓存*。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-218">Clear the package caches at *%UserProfile%\\.nuget\\packages* and *%LocalAppData%\\Nuget\\v3-cache*.</span></span>
1. <span data-ttu-id="d0fe4-219">还原和重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-219">Restore and rebuild the project.</span></span>
1. <span data-ttu-id="d0fe4-220">确认已完全重新部署应用程序之前删除以前部署到服务器上。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-220">Confirm that the prior deployment on the server has been completely deleted prior to redeploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="d0fe4-221">清除包缓存的简便方法是执行`dotnet nuget locals all --clear`从命令提示符。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-221">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
> 
> <span data-ttu-id="d0fe4-222">清除包缓存还可通过使用[nuget.exe](https://www.nuget.org/downloads)工具并执行命令`nuget locals all -clear`。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-222">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="d0fe4-223">*nuget.exe*必须从单独获取和不与 Windows 桌面操作系统的捆绑的安装[NuGet 网站](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="d0fe4-223">*nuget.exe* isn't a bundled install with the Windows desktop operating system and must be obtained separately from the [NuGet website](https://www.nuget.org/downloads).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0fe4-224">其他资源</span><span class="sxs-lookup"><span data-stu-id="d0fe4-224">Additional resources</span></span>

* [<span data-ttu-id="d0fe4-225">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="d0fe4-225">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="d0fe4-226">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="d0fe4-226">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="d0fe4-227">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="d0fe4-227">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="d0fe4-228">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="d0fe4-228">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
