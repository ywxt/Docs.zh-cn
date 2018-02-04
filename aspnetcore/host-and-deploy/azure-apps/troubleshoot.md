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
ms.openlocfilehash: 144af8e93bb935d07fd064d5f45b40faea4a2664
ms.sourcegitcommit: 7a87d66cf1d01febe6635c7306f2f679434901d1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="troubleshoot-aspnet-core-on-azure-app-service"></a><span data-ttu-id="8c852-103">解决在 Azure App Service 上的 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="8c852-103">Troubleshoot ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="8c852-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8c852-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8c852-105">本文说明了如何诊断 ASP.NET Core 应用使用 Azure App Service 的诊断工具的启动问题。</span><span class="sxs-lookup"><span data-stu-id="8c852-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue using Azure App Service's diagnostic tools.</span></span> <span data-ttu-id="8c852-106">有关其他故障排除建议，请参阅[Azure App Service 诊断概述](/azure/app-service/app-service-diagnostics)和[如何： 在 Azure App Service 中监视应用](/azure/app-service/web-sites-monitor)Azure 文档中。</span><span class="sxs-lookup"><span data-stu-id="8c852-106">For additional troubleshooting advice, see [Azure App Service diagnostics overview](/azure/app-service/app-service-diagnostics) and [How to: Monitor Apps in Azure App Service](/azure/app-service/web-sites-monitor) in the Azure documentation.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="8c852-107">应用程序启动错误</span><span class="sxs-lookup"><span data-stu-id="8c852-107">App startup errors</span></span>

<span data-ttu-id="8c852-108">**502.5 进程故障**</span><span class="sxs-lookup"><span data-stu-id="8c852-108">**502.5 Process Failure**</span></span>  
<span data-ttu-id="8c852-109">工作进程将失败。</span><span class="sxs-lookup"><span data-stu-id="8c852-109">The worker process fails.</span></span> <span data-ttu-id="8c852-110">不启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="8c852-110">The app doesn't start.</span></span>

<span data-ttu-id="8c852-111">[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)尝试启动工作进程，但它无法启动。</span><span class="sxs-lookup"><span data-stu-id="8c852-111">The [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="8c852-112">经常检查应用程序事件日志可帮助解决这种类型的问题。</span><span class="sxs-lookup"><span data-stu-id="8c852-112">Examining the Application Event Log often helps troubleshoot this type of problem.</span></span> <span data-ttu-id="8c852-113">访问日志中进行了说明[应用程序事件日志](#application-event-log)部分。</span><span class="sxs-lookup"><span data-stu-id="8c852-113">Accessing the log is explained in the [Application Event Log](#application-event-log) section.</span></span>

<span data-ttu-id="8c852-114">*502.5 进程失败*配置错误的应用程序会导致工作进程失败，返回错误页：</span><span class="sxs-lookup"><span data-stu-id="8c852-114">The *502.5 Process Failure* error page is returned when a misconfigured app causes the worker process to fail:</span></span>

![显示 502.5 进程失败页的浏览器窗口](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="8c852-116">**500 内部服务器错误**</span><span class="sxs-lookup"><span data-stu-id="8c852-116">**500 Internal Server Error**</span></span>  
<span data-ttu-id="8c852-117">启动该应用程序，但某个错误阻止在完成请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="8c852-117">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="8c852-118">启动过程中或创建响应时，应用程序的代码中出现此错误。</span><span class="sxs-lookup"><span data-stu-id="8c852-118">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="8c852-119">响应可能包含任何内容，或响应可能显示为*500 内部服务器错误*浏览器中。</span><span class="sxs-lookup"><span data-stu-id="8c852-119">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="8c852-120">应用程序事件日志通常表明应用程序正常启动。</span><span class="sxs-lookup"><span data-stu-id="8c852-120">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="8c852-121">从服务器的角度来看，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="8c852-121">From the server's perspective, that's correct.</span></span> <span data-ttu-id="8c852-122">应用程序未启动，但它无法生成有效的响应。</span><span class="sxs-lookup"><span data-stu-id="8c852-122">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="8c852-123">[Kudu 控制台中运行此应用](#run-the-app-in-the-kudu-console)或[启用 ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="8c852-123">[Run the app in the Kudu console](#run-the-app-in-the-kudu-console) or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="8c852-124">应用程序启动错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="8c852-124">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="8c852-125">应用程序事件日志</span><span class="sxs-lookup"><span data-stu-id="8c852-125">Application Event Log</span></span>

<span data-ttu-id="8c852-126">若要访问应用程序事件日志，请使用**诊断并解决问题**在 Azure 门户中的边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="8c852-126">To access the Application Event Log, use the **Diagnose and solve problems** blade in the Azure portal :</span></span>

1. <span data-ttu-id="8c852-127">在 Azure 门户中，打开应用的边栏选项卡中**应用程序服务**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-127">In the Azure portal, open the app's blade in the **App Services** blade.</span></span>
1. <span data-ttu-id="8c852-128">选择**诊断并解决问题**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-128">Select the **Diagnose and solve problems** blade.</span></span>
1. <span data-ttu-id="8c852-129">下**选择问题类别**，选择**Web 应用程序向下**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-129">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="8c852-130">下**建议解决方案**，打开的窗格**打开应用程序事件日志**。</span><span class="sxs-lookup"><span data-stu-id="8c852-130">Under **Suggested Solutions**, open the pane for **Open Application Event Logs**.</span></span> <span data-ttu-id="8c852-131">选择**打开应用程序事件日志**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-131">Select the **Open Application Event Logs** button.</span></span>
1. <span data-ttu-id="8c852-132">检查提供的最新错误*IIS AspNetCoreModule*中**源**列。</span><span class="sxs-lookup"><span data-stu-id="8c852-132">Examine the latest error provided by the *IIS AspNetCoreModule* in the **Source** column.</span></span>

<span data-ttu-id="8c852-133">除了使用**诊断并解决问题**边栏选项卡是检查应用程序事件日志文件直接使用[Kudu](https://github.com/projectkudu/kudu/wiki):</span><span class="sxs-lookup"><span data-stu-id="8c852-133">An alternative to using the **Diagnose and solve problems** blade is to examine the Application Event Log file directly using [Kudu](https://github.com/projectkudu/kudu/wiki):</span></span>

1. <span data-ttu-id="8c852-134">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="8c852-134">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8c852-135">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-135">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8c852-136">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="8c852-136">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8c852-137">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="8c852-137">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8c852-138">打开**LogFiles**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c852-138">Open the **LogFiles** folder.</span></span>
1. <span data-ttu-id="8c852-139">选择铅笔图标旁边*eventlog.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-139">Select the pencil icon next to the *eventlog.xml* file.</span></span>
1. <span data-ttu-id="8c852-140">检查日志。</span><span class="sxs-lookup"><span data-stu-id="8c852-140">Examine the log.</span></span> <span data-ttu-id="8c852-141">滚动到底部的日志，以查看最新的事件。</span><span class="sxs-lookup"><span data-stu-id="8c852-141">Scroll to the bottom of the log to see the most recent events.</span></span>

### <a name="run-the-app-in-the-kudu-console"></a><span data-ttu-id="8c852-142">Kudu 控制台中运行此应用</span><span class="sxs-lookup"><span data-stu-id="8c852-142">Run the app in the Kudu console</span></span>

<span data-ttu-id="8c852-143">许多启动错误未生成应用程序事件日志中的有用信息。</span><span class="sxs-lookup"><span data-stu-id="8c852-143">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="8c852-144">你可以在运行应用程序[Kudu](https://github.com/projectkudu/kudu/wiki)远程执行控制台，以发现错误：</span><span class="sxs-lookup"><span data-stu-id="8c852-144">You can run the app in the [Kudu](https://github.com/projectkudu/kudu/wiki) Remote Execution Console to discover the error:</span></span>

1. <span data-ttu-id="8c852-145">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="8c852-145">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8c852-146">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-146">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8c852-147">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="8c852-147">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8c852-148">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="8c852-148">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8c852-149">打开的文件夹的路径**站点** > **wwwroot**。</span><span class="sxs-lookup"><span data-stu-id="8c852-149">Open the folders to the path **site** > **wwwroot**.</span></span>
1. <span data-ttu-id="8c852-150">在控制台中，通过执行应用程序的程序集与运行应用*dotnet.exe*。</span><span class="sxs-lookup"><span data-stu-id="8c852-150">In the console, run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="8c852-151">在下面的命令中，应用程序的程序集的名称替换`<assembly_name>`:</span><span class="sxs-lookup"><span data-stu-id="8c852-151">In the following command, substitute the name of the app's assembly for `<assembly_name>`:</span></span>
   ```console
   dotnet .\<assembly_name>.dll
   ```
1. <span data-ttu-id="8c852-152">控制台应用程序中，显示任何错误，从输出传送到 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8c852-152">The console output from the app, showing any errors, is piped to the Kudu console.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="8c852-153">ASP.NET 核心模块 stdout 日志</span><span class="sxs-lookup"><span data-stu-id="8c852-153">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="8c852-154">ASP.NET 核心模块 stdout 日志通常记录找不到应用程序事件日志中的有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="8c852-154">The ASP.NET Core Module stdout log often records useful error messages not found in the Application Event Log.</span></span> <span data-ttu-id="8c852-155">用于启用和查看 stdout 日志：</span><span class="sxs-lookup"><span data-stu-id="8c852-155">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="8c852-156">导航到**诊断并解决问题**在 Azure 门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-156">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="8c852-157">下**选择问题类别**，选择**Web 应用程序向下**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-157">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="8c852-158">下**建议解决方案** > **启用 Stdout 日志重定向**，选择该按钮**打开 Kudu 控制台编辑 Web.Config**。</span><span class="sxs-lookup"><span data-stu-id="8c852-158">Under **Suggested Solutions** > **Enable Stdout Log Redirection**, select the button to **Open Kudu Console to edit Web.Config**.</span></span>
1. <span data-ttu-id="8c852-159">在 Kudu **Diagnostic 控制台**，打开的文件夹的路径**站点** > **wwwroot**。</span><span class="sxs-lookup"><span data-stu-id="8c852-159">In the Kudu **Diagnostic Console**, open the folders to the path **site** > **wwwroot**.</span></span> <span data-ttu-id="8c852-160">向下滚动到显示*web.config*列表底部的文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-160">Scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="8c852-161">单击铅笔图标旁边*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-161">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="8c852-162">设置**stdoutLogEnabled**到`true`和更改**stdoutLogFile**路径： `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="8c852-162">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="8c852-163">选择**保存**以保存已更新*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-163">Select **Save** to save the updated *web.config* file.</span></span>
1. <span data-ttu-id="8c852-164">向应用程序发出的请求。</span><span class="sxs-lookup"><span data-stu-id="8c852-164">Make a request to the app.</span></span>
1. <span data-ttu-id="8c852-165">返回到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="8c852-165">Return to the Azure portal.</span></span> <span data-ttu-id="8c852-166">选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="8c852-166">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8c852-167">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-167">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8c852-168">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="8c852-168">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8c852-169">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="8c852-169">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8c852-170">选择**LogFiles**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8c852-170">Select the **LogFiles** folder.</span></span>
1. <span data-ttu-id="8c852-171">检查**已修改**列并选择铅笔图标以编辑 stdout 日志的最新的修改日期。</span><span class="sxs-lookup"><span data-stu-id="8c852-171">Inspect the **Modified** column and select the pencil icon to edit the stdout log with the latest modification date.</span></span>
1. <span data-ttu-id="8c852-172">在打开日志文件后，将显示错误。</span><span class="sxs-lookup"><span data-stu-id="8c852-172">When the log file opens, the error is displayed.</span></span>

<span data-ttu-id="8c852-173">**重要 ！**</span><span class="sxs-lookup"><span data-stu-id="8c852-173">**Important!**</span></span> <span data-ttu-id="8c852-174">禁用完成故障排除时，日志记录 stdout。</span><span class="sxs-lookup"><span data-stu-id="8c852-174">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="8c852-175">在 Kudu **Diagnostic 控制台**，则返回到路径**站点** > **wwwroot**以显示*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-175">In the Kudu **Diagnostic Console**, return to the path **site** > **wwwroot** to reveal the *web.config* file.</span></span> <span data-ttu-id="8c852-176">打开**web.config**再次通过选择铅笔图标的文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-176">Open the **web.config** file again by selecting the pencil icon.</span></span>
1. <span data-ttu-id="8c852-177">设置**stdoutLogEnabled**到`false`。</span><span class="sxs-lookup"><span data-stu-id="8c852-177">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="8c852-178">选择**保存**保存文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-178">Select **Save** to save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="8c852-179">若要禁用 stdout 日志可能会导致应用程序或服务器失败。</span><span class="sxs-lookup"><span data-stu-id="8c852-179">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="8c852-180">没有对日志文件大小没有限制或创建的日志文件数。</span><span class="sxs-lookup"><span data-stu-id="8c852-180">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="8c852-181">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="8c852-181">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="8c852-182">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="8c852-182">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="8c852-183">常见的启动错误</span><span class="sxs-lookup"><span data-stu-id="8c852-183">Common startup errors</span></span> 

<span data-ttu-id="8c852-184">请参阅[ASP.NET 核心常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)。</span><span class="sxs-lookup"><span data-stu-id="8c852-184">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="8c852-185">中的参考主题介绍了大部分常见防止应用程序启动的问题。</span><span class="sxs-lookup"><span data-stu-id="8c852-185">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="process-dump-for-a-slow-or-hanging-app"></a><span data-ttu-id="8c852-186">慢速或悬挂应用程序的进程转储</span><span class="sxs-lookup"><span data-stu-id="8c852-186">Process dump for a slow or hanging app</span></span>

<span data-ttu-id="8c852-187">当应用程序响应速度很慢或挂起的请求时，请参阅[在 Azure App Service 中进行故障排除慢速的 web 应用程序性能问题](/azure/app-service/app-service-web-troubleshoot-performance-degradation)用于调试的指导。</span><span class="sxs-lookup"><span data-stu-id="8c852-187">When an app responds slowly or hangs on a request, see [Troubleshoot slow web app performance issues in Azure App Service](/azure/app-service/app-service-web-troubleshoot-performance-degradation) for debugging guidance.</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="8c852-188">远程调试</span><span class="sxs-lookup"><span data-stu-id="8c852-188">Remote debugging</span></span>

<span data-ttu-id="8c852-189">请参阅[远程调试的故障排除 Azure App Service 中使用 Visual Studio 中的 web 应用的 web 应用部分](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug)Azure 文档中。</span><span class="sxs-lookup"><span data-stu-id="8c852-189">See [Remote debugging web apps section of Troubleshoot a web app in Azure App Service using Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) in the Azure documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="8c852-190">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c852-190">Application Insights</span></span>

<span data-ttu-id="8c852-191">[Application Insights](https://azure.microsoft.com/services/application-insights/)提供从托管在 Azure App Service，包括错误日志记录和报告功能的应用程序的遥测。</span><span class="sxs-lookup"><span data-stu-id="8c852-191">[Application Insights](https://azure.microsoft.com/services/application-insights/) provides telemetry from apps hosted in the Azure App Service, including error logging and reporting features.</span></span> <span data-ttu-id="8c852-192">Application Insights 只能针对在应用程序启动时应用的日志记录功能变得可用之后发生的错误报告。</span><span class="sxs-lookup"><span data-stu-id="8c852-192">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="8c852-193">有关详细信息，请参阅[Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="8c852-193">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="monitoring-blades"></a><span data-ttu-id="8c852-194">监视边栏选项卡</span><span class="sxs-lookup"><span data-stu-id="8c852-194">Monitoring blades</span></span>

<span data-ttu-id="8c852-195">监视边栏选项卡提供疑难解答的体验到本主题前面所述的方法的替代方法。</span><span class="sxs-lookup"><span data-stu-id="8c852-195">Monitoring blades provide an alternative troubleshooting experience to the methods described earlier in the topic.</span></span> <span data-ttu-id="8c852-196">这些边栏选项卡可以用于诊断 500 系列错误。</span><span class="sxs-lookup"><span data-stu-id="8c852-196">These blades can be used to diagnose 500-series errors.</span></span>

<span data-ttu-id="8c852-197">确认安装了 ASP.NET 核心扩展。</span><span class="sxs-lookup"><span data-stu-id="8c852-197">Confirm that the ASP.NET Core Extensions are installed.</span></span> <span data-ttu-id="8c852-198">如果未安装的扩展，请手动安装它们：</span><span class="sxs-lookup"><span data-stu-id="8c852-198">If the extensions aren't installed, install them manually:</span></span>

1. <span data-ttu-id="8c852-199">在**开发工具**边栏选项卡部分中，选择**扩展**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-199">In the **DEVELOPMENT TOOLS** blade section, select the **Extensions** blade.</span></span>
1. <span data-ttu-id="8c852-200">**ASP.NET 核心扩展**应出现在列表中。</span><span class="sxs-lookup"><span data-stu-id="8c852-200">The **ASP.NET Core Extensions** should appear in the list.</span></span>
1. <span data-ttu-id="8c852-201">如果未安装的扩展，选择**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-201">If the extensions aren't installed, select the **Add** button.</span></span>
1. <span data-ttu-id="8c852-202">选择**ASP.NET 核心扩展**从列表中。</span><span class="sxs-lookup"><span data-stu-id="8c852-202">Choose the **ASP.NET Core Extensions** from the list.</span></span>
1. <span data-ttu-id="8c852-203">选择**确定**以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="8c852-203">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="8c852-204">选择**确定**上**将扩展添加**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-204">Select **OK** on the **Add extension** blade.</span></span>
1. <span data-ttu-id="8c852-205">弹出一条信息性消息表示成功安装的扩展。</span><span class="sxs-lookup"><span data-stu-id="8c852-205">An informational pop-up message indicates when the extensions are successfully installed.</span></span>

<span data-ttu-id="8c852-206">如果未启用 stdout 日志记录，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="8c852-206">If stdout logging isn't enabled, follow these steps:</span></span>

1. <span data-ttu-id="8c852-207">在 Azure 门户中，选择**高级工具**中的边栏选项卡**开发工具**区域。</span><span class="sxs-lookup"><span data-stu-id="8c852-207">In the Azure portal, select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8c852-208">选择**转&rarr;**按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-208">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8c852-209">Kudu 控制台打开新浏览器选项卡或窗口中。</span><span class="sxs-lookup"><span data-stu-id="8c852-209">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8c852-210">使用的页上，顶部导航栏打开**调试控制台**和选择**CMD**。</span><span class="sxs-lookup"><span data-stu-id="8c852-210">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8c852-211">打开的文件夹的路径**站点** > **wwwroot**向下滚至揭示*web.config*列表底部的文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-211">Open the folders to the path **site** > **wwwroot** and scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="8c852-212">单击铅笔图标旁边*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-212">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="8c852-213">设置**stdoutLogEnabled**到`true`和更改**stdoutLogFile**路径： `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="8c852-213">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="8c852-214">选择**保存**以保存已更新*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="8c852-214">Select **Save** to save the updated *web.config* file.</span></span>

<span data-ttu-id="8c852-215">继续激活诊断日志记录：</span><span class="sxs-lookup"><span data-stu-id="8c852-215">Proceed to activate diagnostic logging:</span></span>

1. <span data-ttu-id="8c852-216">在 Azure 门户中，选择**诊断日志**边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-216">In the Azure portal, select the **Diagnostics logs** blade.</span></span>
1. <span data-ttu-id="8c852-217">选择**上**切换**应用程序日志记录 （文件系统）**和**详细错误消息**。</span><span class="sxs-lookup"><span data-stu-id="8c852-217">Select the **On** switch for **Application Logging (Filesystem)** and **Detailed error messages**.</span></span> <span data-ttu-id="8c852-218">选择**保存**边栏选项卡顶部的按钮。</span><span class="sxs-lookup"><span data-stu-id="8c852-218">Select the **Save** button at the top of the blade.</span></span>
1. <span data-ttu-id="8c852-219">若要包含失败的请求跟踪，也称为失败请求事件缓冲 (FREB) 日志记录，选择**上**切换**失败请求跟踪**。</span><span class="sxs-lookup"><span data-stu-id="8c852-219">To include failed request tracing, also known as Failed Request Event Buffering (FREB) logging, select the **On** switch for **Failed request tracing**.</span></span> 
1. <span data-ttu-id="8c852-220">选择**日志流**边栏选项卡，其中立即下列出**诊断日志**在门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-220">Select the **Log stream** blade, which is listed immediately under the **Diagnostics logs** blade in the portal.</span></span>
1. <span data-ttu-id="8c852-221">向应用程序发出的请求。</span><span class="sxs-lookup"><span data-stu-id="8c852-221">Make a request to the app.</span></span>
1. <span data-ttu-id="8c852-222">在日志的流数据，指示错误的原因。</span><span class="sxs-lookup"><span data-stu-id="8c852-222">Within the log stream data, the cause of the error is indicated.</span></span>

<span data-ttu-id="8c852-223">**重要 ！**</span><span class="sxs-lookup"><span data-stu-id="8c852-223">**Important!**</span></span> <span data-ttu-id="8c852-224">请务必禁用完成故障排除时，日志记录 stdout。</span><span class="sxs-lookup"><span data-stu-id="8c852-224">Be sure to disable stdout logging when troubleshooting is complete.</span></span> <span data-ttu-id="8c852-225">请参阅中的说明[ASP.NET 核心模块 stdout 日志](#aspnet-core-module-stdout-log)部分。</span><span class="sxs-lookup"><span data-stu-id="8c852-225">See the instructions in the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) section.</span></span>

<span data-ttu-id="8c852-226">若要查看失败的请求跟踪日志 （FREB 日志）：</span><span class="sxs-lookup"><span data-stu-id="8c852-226">To view the failed request tracing logs (FREB logs):</span></span>

1. <span data-ttu-id="8c852-227">导航到**诊断并解决问题**在 Azure 门户中的边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8c852-227">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="8c852-228">选择**失败请求跟踪日志**从**支持工具**侧栏区域。</span><span class="sxs-lookup"><span data-stu-id="8c852-228">Select **Failed Request Tracing Logs** from the **SUPPORT TOOLS** area of the sidebar.</span></span>

<span data-ttu-id="8c852-229">请参阅[失败请求跟踪部分中的 Azure App Service 主题中的 web 应用启用诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces)和[Azure 中的 Web 应用的应用程序性能常见问题： 如何打开失败的请求跟踪？](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="8c852-229">See [Failed request traces section of the Enable diagnostics logging for web apps in Azure App Service topic](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces) and the [Application performance FAQs for Web Apps in Azure: How do I turn on failed request tracing?](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing) for more information.</span></span>

<span data-ttu-id="8c852-230">有关详细信息，请参阅[启用 Azure App Service 中的 web 应用的诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="8c852-230">For more information, see [Enable diagnostics logging for web apps in Azure App Service](/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

> [!WARNING]
> <span data-ttu-id="8c852-231">若要禁用 stdout 日志可能会导致应用程序或服务器失败。</span><span class="sxs-lookup"><span data-stu-id="8c852-231">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="8c852-232">没有对日志文件大小没有限制或创建的日志文件数。</span><span class="sxs-lookup"><span data-stu-id="8c852-232">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="8c852-233">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="8c852-233">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="8c852-234">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="8c852-234">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c852-235">其他资源</span><span class="sxs-lookup"><span data-stu-id="8c852-235">Additional resources</span></span>

* [<span data-ttu-id="8c852-236">ASP.NET 核心中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="8c852-236">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="8c852-237">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="8c852-237">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="8c852-238">对 Azure App Service 中使用 Visual Studio 中的 web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="8c852-238">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)
* [<span data-ttu-id="8c852-239">排除"502 错误网关"和"503 服务不可用"Azure web 应用中的 HTTP 的错误</span><span class="sxs-lookup"><span data-stu-id="8c852-239">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>](/app-service/app-service-web-troubleshoot-http-502-http-503)
* [<span data-ttu-id="8c852-240">解决在 Azure App Service 的慢速 web 应用程序性能问题</span><span class="sxs-lookup"><span data-stu-id="8c852-240">Troubleshoot slow web app performance issues in Azure App Service</span></span>](/azure/app-service/app-service-web-troubleshoot-performance-degradation)
* [<span data-ttu-id="8c852-241">在 Azure 中的 Web 应用的应用程序性能常见问题</span><span class="sxs-lookup"><span data-stu-id="8c852-241">Application performance FAQs for Web Apps in Azure</span></span>](/azure/app-service/app-service-web-availability-performance-application-issues-faq)
* [<span data-ttu-id="8c852-242">Azure Friday: Azure 应用程序服务诊断和故障排除体验 （12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="8c852-242">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
