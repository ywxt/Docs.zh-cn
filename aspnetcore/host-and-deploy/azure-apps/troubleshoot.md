---
title: "解决在 Azure App Service 上的 ASP.NET 核心"
author: guardrex
description: "了解如何诊断 ASP.NET Core Azure 应用服务部署问题。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/31/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/troubleshoot
ms.openlocfilehash: 150603d17f3bed983f9871fe7665748a70177f89
ms.sourcegitcommit: 9f758b1550fcae88ab1eb284798a89e6320548a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="troubleshoot-aspnet-core-on-azure-app-service"></a><span data-ttu-id="ffc06-103">解决在 Azure App Service 上的 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="ffc06-103">Troubleshoot ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="ffc06-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ffc06-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ffc06-105">本文说明了如何诊断 ASP.NET Core 应用使用 Azure App Service 的诊断工具的启动问题。</span><span class="sxs-lookup"><span data-stu-id="ffc06-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue using Azure App Service's diagnostic tools.</span></span> <span data-ttu-id="ffc06-106">有关其他故障排除建议，请参阅[Azure App Service 诊断概述](/azure/app-service/app-service-diagnostics)和[如何： 在 Azure App Service 中监视应用](/azure/app-service/web-sites-monitor)Azure 文档中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-106">For additional troubleshooting advice, see [Azure App Service diagnostics overview](/azure/app-service/app-service-diagnostics) and [How to: Monitor Apps in Azure App Service](/azure/app-service/web-sites-monitor) in the Azure documentation.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="ffc06-107">应用程序启动错误</span><span class="sxs-lookup"><span data-stu-id="ffc06-107">App startup errors</span></span>

<span data-ttu-id="ffc06-108">**502.5 进程故障**</span><span class="sxs-lookup"><span data-stu-id="ffc06-108">**502.5 Process Failure**</span></span>  
<span data-ttu-id="ffc06-109">工作进程将失败。</span><span class="sxs-lookup"><span data-stu-id="ffc06-109">The worker process fails.</span></span> <span data-ttu-id="ffc06-110">不启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffc06-110">The app doesn't start.</span></span>

<span data-ttu-id="ffc06-111">[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)尝试启动工作进程，但它无法启动。</span><span class="sxs-lookup"><span data-stu-id="ffc06-111">The [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="ffc06-112">经常检查应用程序事件日志可帮助解决这种类型的问题。</span><span class="sxs-lookup"><span data-stu-id="ffc06-112">Examining the Application Event Log often helps troubleshoot this type of problem.</span></span> <span data-ttu-id="ffc06-113">访问日志中进行了说明[应用程序事件日志](#application-event-log)部分。</span><span class="sxs-lookup"><span data-stu-id="ffc06-113">Accessing the log is explained in the [Application Event Log](#application-event-log) section.</span></span>

<span data-ttu-id="ffc06-114">*502.5 进程失败*配置错误的应用程序会导致工作进程失败，返回错误页：</span><span class="sxs-lookup"><span data-stu-id="ffc06-114">The *502.5 Process Failure* error page is returned when a misconfigured app causes the worker process to fail:</span></span>

![显示 502.5 进程失败页的浏览器窗口](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="ffc06-116">**500 内部服务器错误**</span><span class="sxs-lookup"><span data-stu-id="ffc06-116">**500 Internal Server Error**</span></span>  
<span data-ttu-id="ffc06-117">启动该应用程序，但某个错误阻止在完成请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="ffc06-117">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="ffc06-118">启动过程中或创建响应时，应用程序的代码中出现此错误。</span><span class="sxs-lookup"><span data-stu-id="ffc06-118">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="ffc06-119">响应可能包含任何内容，或响应可能显示为*500 内部服务器错误*浏览器中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-119">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="ffc06-120">应用程序事件日志通常表明应用程序正常启动。</span><span class="sxs-lookup"><span data-stu-id="ffc06-120">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="ffc06-121">从服务器的角度来看，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="ffc06-121">From the server's perspective, that's correct.</span></span> <span data-ttu-id="ffc06-122">应用程序未启动，但它无法生成有效的响应。</span><span class="sxs-lookup"><span data-stu-id="ffc06-122">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="ffc06-123">[Kudu 控制台中运行此应用](#run-the-app-in-the-kudu-console)或[启用 ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="ffc06-123">[Run the app in the Kudu console](#run-the-app-in-the-kudu-console) or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

<span data-ttu-id="ffc06-124">**连接重置**</span><span class="sxs-lookup"><span data-stu-id="ffc06-124">**Connection reset**</span></span>

<span data-ttu-id="ffc06-125">如果发送标头后，将发生错误，则服务器尝试发送太晚**500 内部服务器错误**发生错误时。</span><span class="sxs-lookup"><span data-stu-id="ffc06-125">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="ffc06-126">响应的复杂对象的序列化期间发生错误时经常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="ffc06-126">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="ffc06-127">此类型的错误显示为*连接重置*客户端上的错误。</span><span class="sxs-lookup"><span data-stu-id="ffc06-127">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="ffc06-128">[应用程序日志记录](xref:fundamentals/logging/index)可以帮助解决这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="ffc06-128">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="ffc06-129">默认启动限制</span><span class="sxs-lookup"><span data-stu-id="ffc06-129">Default startup limits</span></span>

<span data-ttu-id="ffc06-130">ASP.NET 核心模块配置了默认值*startupTimeLimit*的 120 秒。</span><span class="sxs-lookup"><span data-stu-id="ffc06-130">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="ffc06-131">时保留为默认值，应用可能需要最多两分钟，以启动之前模块记录进程失败。</span><span class="sxs-lookup"><span data-stu-id="ffc06-131">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="ffc06-132">有关模块的配置的信息，请参阅[aspNetCore 元素的特性的](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-132">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="ffc06-133">应用程序启动错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="ffc06-133">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="ffc06-134">应用程序事件日志</span><span class="sxs-lookup"><span data-stu-id="ffc06-134">Application Event Log</span></span>

<span data-ttu-id="ffc06-135">若要访问应用程序事件日志，请使用**诊断并解决问题**在 Azure 门户中的边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="ffc06-135">To access the Application Event Log, use the **Diagnose and solve problems** blade in the Azure portal :</span></span>

1. <span data-ttu-id="ffc06-136">在 Azure 门户中，打开应用的边栏选项卡中**应用程序服务**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-136">In the Azure portal, open the app's blade in the **App Services** blade.</span></span>
1. <span data-ttu-id="ffc06-137">选择**诊断并解决问题**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-137">Select the **Diagnose and solve problems** blade.</span></span>
1. <span data-ttu-id="ffc06-138">下**选择问题类别**，选择**Web 应用程序向下**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-138">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="ffc06-139">下**建议解决方案**，打开的窗格**打开应用程序事件日志**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-139">Under **Suggested Solutions**, open the pane for **Open Application Event Logs**.</span></span> <span data-ttu-id="ffc06-140">选择**打开应用程序事件日志**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-140">Select the **Open Application Event Logs** button.</span></span>
1. <span data-ttu-id="ffc06-141">检查提供的最新错误*IIS AspNetCoreModule*中**源**列。</span><span class="sxs-lookup"><span data-stu-id="ffc06-141">Examine the latest error provided by the *IIS AspNetCoreModule* in the **Source** column.</span></span>

<span data-ttu-id="ffc06-142">除了使用**诊断并解决问题**边栏选项卡是检查应用程序事件日志文件直接使用[Kudu](https://github.com/projectkudu/kudu/wiki):</span><span class="sxs-lookup"><span data-stu-id="ffc06-142">An alternative to using the **Diagnose and solve problems** blade is to examine the Application Event Log file directly using [Kudu](https://github.com/projectkudu/kudu/wiki):</span></span>

1. <span data-ttu-id="ffc06-143">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="ffc06-143">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="ffc06-144">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-144">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="ffc06-145">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-145">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="ffc06-146">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-146">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="ffc06-147">打开**LogFiles**文件夹。</span><span class="sxs-lookup"><span data-stu-id="ffc06-147">Open the **LogFiles** folder.</span></span>
1. <span data-ttu-id="ffc06-148">选择铅笔图标旁边*eventlog.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-148">Select the pencil icon next to the *eventlog.xml* file.</span></span>
1. <span data-ttu-id="ffc06-149">检查日志。</span><span class="sxs-lookup"><span data-stu-id="ffc06-149">Examine the log.</span></span> <span data-ttu-id="ffc06-150">滚动到底部的日志，以查看最新的事件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-150">Scroll to the bottom of the log to see the most recent events.</span></span>

### <a name="run-the-app-in-the-kudu-console"></a><span data-ttu-id="ffc06-151">Kudu 控制台中运行此应用</span><span class="sxs-lookup"><span data-stu-id="ffc06-151">Run the app in the Kudu console</span></span>

<span data-ttu-id="ffc06-152">许多启动错误未生成应用程序事件日志中的有用信息。</span><span class="sxs-lookup"><span data-stu-id="ffc06-152">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="ffc06-153">你可以在运行应用程序[Kudu](https://github.com/projectkudu/kudu/wiki)远程执行控制台，以发现错误：</span><span class="sxs-lookup"><span data-stu-id="ffc06-153">You can run the app in the [Kudu](https://github.com/projectkudu/kudu/wiki) Remote Execution Console to discover the error:</span></span>

1. <span data-ttu-id="ffc06-154">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="ffc06-154">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="ffc06-155">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-155">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="ffc06-156">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-156">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="ffc06-157">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-157">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="ffc06-158">打开的文件夹的路径**站点** > **wwwroot**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-158">Open the folders to the path **site** > **wwwroot**.</span></span>
1. <span data-ttu-id="ffc06-159">在控制台中，通过执行应用程序的程序集运行该应用。</span><span class="sxs-lookup"><span data-stu-id="ffc06-159">In the console, run the app by executing the app's assembly.</span></span>
   * <span data-ttu-id="ffc06-160">如果在应用程序处于[framework 相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，运行具有的应用程序的程序集*dotnet.exe*。</span><span class="sxs-lookup"><span data-stu-id="ffc06-160">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd), run the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="ffc06-161">在下面的命令中，应用程序的程序集的名称替换`<assembly_name>`: `dotnet .\<assembly_name>.dll`</span><span class="sxs-lookup"><span data-stu-id="ffc06-161">In the following command, substitute the name of the app's assembly for `<assembly_name>`: `dotnet .\<assembly_name>.dll`</span></span>
   * <span data-ttu-id="ffc06-162">如果在应用程序处于[独立的部署](/dotnet/core/deploying/#self-contained-deployments-scd)中运行应用程序的可执行文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-162">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd), run the app's executable.</span></span> <span data-ttu-id="ffc06-163">在下面的命令中，应用程序的程序集的名称替换`<assembly_name>`: `<assembly_name>.exe`</span><span class="sxs-lookup"><span data-stu-id="ffc06-163">In the following command, substitute the name of the app's assembly for `<assembly_name>`: `<assembly_name>.exe`</span></span>
1. <span data-ttu-id="ffc06-164">控制台应用程序中，显示任何错误，从输出传送到 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="ffc06-164">The console output from the app, showing any errors, is piped to the Kudu console.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="ffc06-165">ASP.NET 核心模块 stdout 日志</span><span class="sxs-lookup"><span data-stu-id="ffc06-165">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="ffc06-166">ASP.NET 核心模块 stdout 日志通常记录找不到应用程序事件日志中的有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="ffc06-166">The ASP.NET Core Module stdout log often records useful error messages not found in the Application Event Log.</span></span> <span data-ttu-id="ffc06-167">用于启用和查看 stdout 日志：</span><span class="sxs-lookup"><span data-stu-id="ffc06-167">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="ffc06-168">导航到**诊断并解决问题**在 Azure 门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-168">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="ffc06-169">下**选择问题类别**，选择**Web 应用程序向下**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-169">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="ffc06-170">下**建议解决方案** > **启用 Stdout 日志重定向**，选择该按钮**打开 Kudu 控制台编辑 Web.Config**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-170">Under **Suggested Solutions** > **Enable Stdout Log Redirection**, select the button to **Open Kudu Console to edit Web.Config**.</span></span>
1. <span data-ttu-id="ffc06-171">在 Kudu **Diagnostic 控制台**，打开的文件夹的路径**站点** > **wwwroot**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-171">In the Kudu **Diagnostic Console**, open the folders to the path **site** > **wwwroot**.</span></span> <span data-ttu-id="ffc06-172">向下滚动到显示*web.config*列表底部的文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-172">Scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="ffc06-173">单击铅笔图标旁边*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-173">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="ffc06-174">设置**stdoutLogEnabled**到`true`和更改**stdoutLogFile**路径： `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="ffc06-174">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="ffc06-175">选择**保存**以保存已更新*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-175">Select **Save** to save the updated *web.config* file.</span></span>
1. <span data-ttu-id="ffc06-176">向应用程序发出的请求。</span><span class="sxs-lookup"><span data-stu-id="ffc06-176">Make a request to the app.</span></span>
1. <span data-ttu-id="ffc06-177">返回到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="ffc06-177">Return to the Azure portal.</span></span> <span data-ttu-id="ffc06-178">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="ffc06-178">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="ffc06-179">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-179">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="ffc06-180">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-180">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="ffc06-181">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-181">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="ffc06-182">选择**LogFiles**文件夹。</span><span class="sxs-lookup"><span data-stu-id="ffc06-182">Select the **LogFiles** folder.</span></span>
1. <span data-ttu-id="ffc06-183">检查**已修改**列并选择铅笔图标以编辑 stdout 日志的最新的修改日期。</span><span class="sxs-lookup"><span data-stu-id="ffc06-183">Inspect the **Modified** column and select the pencil icon to edit the stdout log with the latest modification date.</span></span>
1. <span data-ttu-id="ffc06-184">在打开日志文件后，将显示错误。</span><span class="sxs-lookup"><span data-stu-id="ffc06-184">When the log file opens, the error is displayed.</span></span>

<span data-ttu-id="ffc06-185">**重要 ！**</span><span class="sxs-lookup"><span data-stu-id="ffc06-185">**Important!**</span></span> <span data-ttu-id="ffc06-186">禁用完成故障排除时，日志记录 stdout。</span><span class="sxs-lookup"><span data-stu-id="ffc06-186">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="ffc06-187">在 Kudu **Diagnostic 控制台**，则返回到路径**站点** > **wwwroot**以显示*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-187">In the Kudu **Diagnostic Console**, return to the path **site** > **wwwroot** to reveal the *web.config* file.</span></span> <span data-ttu-id="ffc06-188">打开**web.config**再次通过选择铅笔图标的文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-188">Open the **web.config** file again by selecting the pencil icon.</span></span>
1. <span data-ttu-id="ffc06-189">设置**stdoutLogEnabled**到`false`。</span><span class="sxs-lookup"><span data-stu-id="ffc06-189">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="ffc06-190">选择**保存**保存文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-190">Select **Save** to save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="ffc06-191">若要禁用 stdout 日志可能会导致应用程序或服务器失败。</span><span class="sxs-lookup"><span data-stu-id="ffc06-191">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="ffc06-192">没有对日志文件大小没有限制或创建的日志文件数。</span><span class="sxs-lookup"><span data-stu-id="ffc06-192">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="ffc06-193">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="ffc06-193">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="ffc06-194">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-194">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="ffc06-195">常见的启动错误</span><span class="sxs-lookup"><span data-stu-id="ffc06-195">Common startup errors</span></span> 

<span data-ttu-id="ffc06-196">请参阅[ASP.NET 核心常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-196">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="ffc06-197">中的参考主题介绍了大部分常见防止应用程序启动的问题。</span><span class="sxs-lookup"><span data-stu-id="ffc06-197">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="ffc06-198">慢速或悬挂应用程序</span><span class="sxs-lookup"><span data-stu-id="ffc06-198">Slow or hanging app</span></span>

<span data-ttu-id="ffc06-199">当应用程序响应速度很慢或挂起的请求时，请参阅[在 Azure App Service 中进行故障排除慢速的 web 应用程序性能问题](/azure/app-service/app-service-web-troubleshoot-performance-degradation)用于调试的指导。</span><span class="sxs-lookup"><span data-stu-id="ffc06-199">When an app responds slowly or hangs on a request, see [Troubleshoot slow web app performance issues in Azure App Service](/azure/app-service/app-service-web-troubleshoot-performance-degradation) for debugging guidance.</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ffc06-200">远程调试</span><span class="sxs-lookup"><span data-stu-id="ffc06-200">Remote debugging</span></span>

<span data-ttu-id="ffc06-201">请参见下面的主题：</span><span class="sxs-lookup"><span data-stu-id="ffc06-201">See the following topics:</span></span>

* <span data-ttu-id="ffc06-202">[远程调试的故障排除 Azure App Service 中使用 Visual Studio 中的 web 应用的 web 应用部分](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug)（Azure 文档）</span><span class="sxs-lookup"><span data-stu-id="ffc06-202">[Remote debugging web apps section of Troubleshoot a web app in Azure App Service using Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) (Azure documentation)</span></span>
* <span data-ttu-id="ffc06-203">[在 Visual Studio 2017 在 Azure 中的 IIS 上的远程调试 ASP.NET Core](/visualstudio/debugger/remote-debugging-azure) （Visual Studio 文档）</span><span class="sxs-lookup"><span data-stu-id="ffc06-203">[Remote Debug ASP.NET Core on IIS in Azure in Visual Studio 2017](/visualstudio/debugger/remote-debugging-azure) (Visual Studio documentation)</span></span>

## <a name="application-insights"></a><span data-ttu-id="ffc06-204">Application Insights</span><span class="sxs-lookup"><span data-stu-id="ffc06-204">Application Insights</span></span>

<span data-ttu-id="ffc06-205">[Application Insights](https://azure.microsoft.com/services/application-insights/)提供从托管在 Azure App Service，包括错误日志记录和报告功能的应用程序的遥测。</span><span class="sxs-lookup"><span data-stu-id="ffc06-205">[Application Insights](https://azure.microsoft.com/services/application-insights/) provides telemetry from apps hosted in the Azure App Service, including error logging and reporting features.</span></span> <span data-ttu-id="ffc06-206">Application Insights 只能针对在应用程序启动时应用的日志记录功能变得可用之后发生的错误报告。</span><span class="sxs-lookup"><span data-stu-id="ffc06-206">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="ffc06-207">有关详细信息，请参阅[Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-207">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="monitoring-blades"></a><span data-ttu-id="ffc06-208">监视边栏选项卡</span><span class="sxs-lookup"><span data-stu-id="ffc06-208">Monitoring blades</span></span>

<span data-ttu-id="ffc06-209">监视边栏选项卡提供疑难解答的体验到本主题前面所述的方法的替代方法。</span><span class="sxs-lookup"><span data-stu-id="ffc06-209">Monitoring blades provide an alternative troubleshooting experience to the methods described earlier in the topic.</span></span> <span data-ttu-id="ffc06-210">这些边栏选项卡可以用于诊断 500 系列错误。</span><span class="sxs-lookup"><span data-stu-id="ffc06-210">These blades can be used to diagnose 500-series errors.</span></span>

<span data-ttu-id="ffc06-211">确认安装了 ASP.NET 核心扩展。</span><span class="sxs-lookup"><span data-stu-id="ffc06-211">Confirm that the ASP.NET Core Extensions are installed.</span></span> <span data-ttu-id="ffc06-212">如果未安装的扩展，请手动安装它们：</span><span class="sxs-lookup"><span data-stu-id="ffc06-212">If the extensions aren't installed, install them manually:</span></span>

1. <span data-ttu-id="ffc06-213">在**开发工具**边栏选项卡部分中，选择**扩展**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-213">In the **DEVELOPMENT TOOLS** blade section, select the **Extensions** blade.</span></span>
1. <span data-ttu-id="ffc06-214">**ASP.NET 核心扩展**应出现在列表中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-214">The **ASP.NET Core Extensions** should appear in the list.</span></span>
1. <span data-ttu-id="ffc06-215">如果未安装的扩展，选择**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-215">If the extensions aren't installed, select the **Add** button.</span></span>
1. <span data-ttu-id="ffc06-216">选择**ASP.NET 核心扩展**从列表中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-216">Choose the **ASP.NET Core Extensions** from the list.</span></span>
1. <span data-ttu-id="ffc06-217">选择**确定**以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="ffc06-217">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="ffc06-218">选择**确定**上**将扩展添加**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-218">Select **OK** on the **Add extension** blade.</span></span>
1. <span data-ttu-id="ffc06-219">弹出一条信息性消息表示成功安装的扩展。</span><span class="sxs-lookup"><span data-stu-id="ffc06-219">An informational pop-up message indicates when the extensions are successfully installed.</span></span>

<span data-ttu-id="ffc06-220">如果未启用 stdout 日志记录，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="ffc06-220">If stdout logging isn't enabled, follow these steps:</span></span>

1. <span data-ttu-id="ffc06-221">在 Azure 门户中，选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="ffc06-221">In the Azure portal, select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="ffc06-222">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-222">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="ffc06-223">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="ffc06-223">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="ffc06-224">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-224">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="ffc06-225">打开的文件夹的路径**站点** > **wwwroot**向下滚至揭示*web.config*列表底部的文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-225">Open the folders to the path **site** > **wwwroot** and scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="ffc06-226">单击铅笔图标旁边*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-226">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="ffc06-227">设置**stdoutLogEnabled**到`true`和更改**stdoutLogFile**路径： `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="ffc06-227">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="ffc06-228">选择**保存**以保存已更新*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ffc06-228">Select **Save** to save the updated *web.config* file.</span></span>

<span data-ttu-id="ffc06-229">继续激活诊断日志记录：</span><span class="sxs-lookup"><span data-stu-id="ffc06-229">Proceed to activate diagnostic logging:</span></span>

1. <span data-ttu-id="ffc06-230">在 Azure 门户中，选择**诊断日志**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-230">In the Azure portal, select the **Diagnostics logs** blade.</span></span>
1. <span data-ttu-id="ffc06-231">选择**上**切换**应用程序日志记录 （文件系统）**和**详细错误消息**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-231">Select the **On** switch for **Application Logging (Filesystem)** and **Detailed error messages**.</span></span> <span data-ttu-id="ffc06-232">选择**保存**边栏选项卡顶部的按钮。</span><span class="sxs-lookup"><span data-stu-id="ffc06-232">Select the **Save** button at the top of the blade.</span></span>
1. <span data-ttu-id="ffc06-233">若要包含失败的请求跟踪，也称为失败请求事件缓冲 (FREB) 日志记录，选择**上**切换**失败请求跟踪**。</span><span class="sxs-lookup"><span data-stu-id="ffc06-233">To include failed request tracing, also known as Failed Request Event Buffering (FREB) logging, select the **On** switch for **Failed request tracing**.</span></span> 
1. <span data-ttu-id="ffc06-234">选择**日志流**边栏选项卡，其中立即下列出**诊断日志**在门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-234">Select the **Log stream** blade, which is listed immediately under the **Diagnostics logs** blade in the portal.</span></span>
1. <span data-ttu-id="ffc06-235">向应用程序发出的请求。</span><span class="sxs-lookup"><span data-stu-id="ffc06-235">Make a request to the app.</span></span>
1. <span data-ttu-id="ffc06-236">在日志的流数据，指示错误的原因。</span><span class="sxs-lookup"><span data-stu-id="ffc06-236">Within the log stream data, the cause of the error is indicated.</span></span>

<span data-ttu-id="ffc06-237">**重要 ！**</span><span class="sxs-lookup"><span data-stu-id="ffc06-237">**Important!**</span></span> <span data-ttu-id="ffc06-238">请务必禁用完成故障排除时，日志记录 stdout。</span><span class="sxs-lookup"><span data-stu-id="ffc06-238">Be sure to disable stdout logging when troubleshooting is complete.</span></span> <span data-ttu-id="ffc06-239">请参阅中的说明[ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)部分。</span><span class="sxs-lookup"><span data-stu-id="ffc06-239">See the instructions in the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) section.</span></span>

<span data-ttu-id="ffc06-240">若要查看失败的请求跟踪日志 （FREB 日志）：</span><span class="sxs-lookup"><span data-stu-id="ffc06-240">To view the failed request tracing logs (FREB logs):</span></span>

1. <span data-ttu-id="ffc06-241">导航到**诊断并解决问题**在 Azure 门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="ffc06-241">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="ffc06-242">选择**失败请求跟踪日志**从**支持工具**侧栏区域。</span><span class="sxs-lookup"><span data-stu-id="ffc06-242">Select **Failed Request Tracing Logs** from the **SUPPORT TOOLS** area of the sidebar.</span></span>

<span data-ttu-id="ffc06-243">请参阅[失败请求跟踪部分中的 Azure App Service 主题中的 web 应用启用诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces)和[Azure 中的 Web 应用的应用程序性能常见问题： 如何打开失败的请求跟踪？](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="ffc06-243">See [Failed request traces section of the Enable diagnostics logging for web apps in Azure App Service topic](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces) and the [Application performance FAQs for Web Apps in Azure: How do I turn on failed request tracing?](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing) for more information.</span></span>

<span data-ttu-id="ffc06-244">有关详细信息，请参阅[启用 Azure App Service 中的 web 应用的诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-244">For more information, see [Enable diagnostics logging for web apps in Azure App Service](/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

> [!WARNING]
> <span data-ttu-id="ffc06-245">若要禁用 stdout 日志可能会导致应用程序或服务器失败。</span><span class="sxs-lookup"><span data-stu-id="ffc06-245">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="ffc06-246">没有对日志文件大小没有限制或创建的日志文件数。</span><span class="sxs-lookup"><span data-stu-id="ffc06-246">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="ffc06-247">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="ffc06-247">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="ffc06-248">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="ffc06-248">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ffc06-249">其他资源</span><span class="sxs-lookup"><span data-stu-id="ffc06-249">Additional resources</span></span>

* [<span data-ttu-id="ffc06-250">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="ffc06-250">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="ffc06-251">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="ffc06-251">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="ffc06-252">对 Azure App Service 中使用 Visual Studio 中的 web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="ffc06-252">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)
* [<span data-ttu-id="ffc06-253">排除"502 错误网关"和"503 服务不可用"Azure web 应用中的 HTTP 的错误</span><span class="sxs-lookup"><span data-stu-id="ffc06-253">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>](/app-service/app-service-web-troubleshoot-http-502-http-503)
* [<span data-ttu-id="ffc06-254">解决在 Azure App Service 的慢速 web 应用程序性能问题</span><span class="sxs-lookup"><span data-stu-id="ffc06-254">Troubleshoot slow web app performance issues in Azure App Service</span></span>](/azure/app-service/app-service-web-troubleshoot-performance-degradation)
* [<span data-ttu-id="ffc06-255">在 Azure 中的 Web 应用的应用程序性能常见问题</span><span class="sxs-lookup"><span data-stu-id="ffc06-255">Application performance FAQs for Web Apps in Azure</span></span>](/azure/app-service/app-service-web-availability-performance-application-issues-faq)
* [<span data-ttu-id="ffc06-256">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="ffc06-256">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
