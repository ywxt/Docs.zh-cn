---
title: 对 Azure 应用服务上的 ASP.NET Core 进行故障排除
author: guardrex
description: 了解如何诊断 ASP.NET Core Azure 应用服务部署问题。
ms.author: riande
ms.custom: mvc
ms.date: 01/31/2018
uid: host-and-deploy/azure-apps/troubleshoot
ms.openlocfilehash: f9918e9162329f4c5dbd1ff18e30fce0db24e651
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272719"
---
# <a name="troubleshoot-aspnet-core-on-azure-app-service"></a><span data-ttu-id="8b2fa-103">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="8b2fa-103">Troubleshoot ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="8b2fa-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8b2fa-104">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

<span data-ttu-id="8b2fa-105">本文说明了如何使用 Azure 应用服务的诊断工具诊断 ASP.NET Core 应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue using Azure App Service's diagnostic tools.</span></span> <span data-ttu-id="8b2fa-106">有关其他故障排除建议，请参阅 Azure 文档中的 [Azure 应用服务诊断概述](/azure/app-service/app-service-diagnostics)和[如何：在 Azure 应用服务中监视应用](/azure/app-service/web-sites-monitor)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-106">For additional troubleshooting advice, see [Azure App Service diagnostics overview](/azure/app-service/app-service-diagnostics) and [How to: Monitor Apps in Azure App Service](/azure/app-service/web-sites-monitor) in the Azure documentation.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="8b2fa-107">应用启动错误</span><span class="sxs-lookup"><span data-stu-id="8b2fa-107">App startup errors</span></span>

<span data-ttu-id="8b2fa-108">**502.5 进程故障**</span><span class="sxs-lookup"><span data-stu-id="8b2fa-108">**502.5 Process Failure**</span></span>  
<span data-ttu-id="8b2fa-109">工作进程失败。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-109">The worker process fails.</span></span> <span data-ttu-id="8b2fa-110">应用不启动。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-110">The app doesn't start.</span></span>

<span data-ttu-id="8b2fa-111">[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)尝试启动工作进程，但启动失败。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-111">The [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="8b2fa-112">检查应用程序事件日志通常可帮助解决此类型的问题。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-112">Examining the Application Event Log often helps troubleshoot this type of problem.</span></span> <span data-ttu-id="8b2fa-113">[应用程序事件日志](#application-event-log)部分中介绍了访问日志。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-113">Accessing the log is explained in the [Application Event Log](#application-event-log) section.</span></span>

<span data-ttu-id="8b2fa-114">配置错误的应用导致工作进程失败时，将返回“502.5 进程故障”错误页面：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-114">The *502.5 Process Failure* error page is returned when a misconfigured app causes the worker process to fail:</span></span>

![显示“502.5 进程故障”页面的浏览器窗口](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="8b2fa-116">**500 内部服务器错误**</span><span class="sxs-lookup"><span data-stu-id="8b2fa-116">**500 Internal Server Error**</span></span>  
<span data-ttu-id="8b2fa-117">应用启动，但某个错误阻止了服务器完成请求。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-117">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="8b2fa-118">在启动期间或在创建响应时，应用的代码内出现此错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-118">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="8b2fa-119">响应可能不包含任何内容，或响应可能会在浏览器中显示为“500 内部服务器错误”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-119">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="8b2fa-120">应用程序事件日志通常表明应用正常启动。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-120">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="8b2fa-121">从服务器的角度来看，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-121">From the server's perspective, that's correct.</span></span> <span data-ttu-id="8b2fa-122">应用已启动，但无法生成有效的响应。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-122">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="8b2fa-123">[在 Kudu 控制台中运行应用](#run-the-app-in-the-kudu-console)或[启用 ASP.NET Core 模块 stdout 日志](#aspnet-core-module-stdout-log)以解决该问题。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-123">[Run the app in the Kudu console](#run-the-app-in-the-kudu-console) or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

<span data-ttu-id="8b2fa-124">**连接重置**</span><span class="sxs-lookup"><span data-stu-id="8b2fa-124">**Connection reset**</span></span>

<span data-ttu-id="8b2fa-125">如果在发送标头后出现错误，则服务器在出现错误时发送“500 内部服务器错误”已经太晚了。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-125">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="8b2fa-126">通常在序列化响应的复杂对象期间出现错误时发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-126">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="8b2fa-127">此类型的错误在客户端上显示为“连接重置”错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-127">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="8b2fa-128">[应用程序日志记录](xref:fundamentals/logging/index)可以帮助解决这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-128">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="8b2fa-129">默认启动限制</span><span class="sxs-lookup"><span data-stu-id="8b2fa-129">Default startup limits</span></span>

<span data-ttu-id="8b2fa-130">ASP.NET Core 模块的默认“startupTimeLimit”配置为 120 秒。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-130">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="8b2fa-131">保留默认值时，在模块记录进程故障之前，可能最多需要两分钟来启动应用。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-131">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="8b2fa-132">有关配置模块的信息，请参阅 [aspNetCore 元素的属性](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-132">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="8b2fa-133">解决应用启动错误</span><span class="sxs-lookup"><span data-stu-id="8b2fa-133">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="8b2fa-134">应用程序事件日志</span><span class="sxs-lookup"><span data-stu-id="8b2fa-134">Application Event Log</span></span>

<span data-ttu-id="8b2fa-135">若要访问应用程序事件日志，请在 Azure 门户中使用“诊断并解决问题”边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-135">To access the Application Event Log, use the **Diagnose and solve problems** blade in the Azure portal :</span></span>

1. <span data-ttu-id="8b2fa-136">在 Azure 门户中，打开“应用服务”边栏选项卡中的应用边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-136">In the Azure portal, open the app's blade in the **App Services** blade.</span></span>
1. <span data-ttu-id="8b2fa-137">选择“诊断并解决问题”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-137">Select the **Diagnose and solve problems** blade.</span></span>
1. <span data-ttu-id="8b2fa-138">在“选择问题类别”下，选择“Web 应用关闭”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-138">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="8b2fa-139">在“建议的解决方案”下，打开“打开应用程序事件日志”对应的窗格。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-139">Under **Suggested Solutions**, open the pane for **Open Application Event Logs**.</span></span> <span data-ttu-id="8b2fa-140">选择“打开应用程序事件日志”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-140">Select the **Open Application Event Logs** button.</span></span>
1. <span data-ttu-id="8b2fa-141">检查“源”列中由 IIS AspNetCoreModule 提供的最新错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-141">Examine the latest error provided by the *IIS AspNetCoreModule* in the **Source** column.</span></span>

<span data-ttu-id="8b2fa-142">使用“诊断并解决问题”边栏选项卡的替代方法是直接使用 [Kudu](https://github.com/projectkudu/kudu/wiki) 检查应用程序事件日志文件：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-142">An alternative to using the **Diagnose and solve problems** blade is to examine the Application Event Log file directly using [Kudu](https://github.com/projectkudu/kudu/wiki):</span></span>

1. <span data-ttu-id="8b2fa-143">选择“开发工具”区域中的“高级工具”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-143">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8b2fa-144">选择“转到&rarr;”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-144">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8b2fa-145">此时将在新的浏览器选项卡或窗口中打开 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-145">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8b2fa-146">使用页面顶部的导航栏，打开“调试控制台”并选择“CMD”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-146">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8b2fa-147">打开 LogFiles 文件夹。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-147">Open the **LogFiles** folder.</span></span>
1. <span data-ttu-id="8b2fa-148">选择 eventlog.xml 文件旁边的铅笔图标。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-148">Select the pencil icon next to the *eventlog.xml* file.</span></span>
1. <span data-ttu-id="8b2fa-149">检查日志。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-149">Examine the log.</span></span> <span data-ttu-id="8b2fa-150">滚动到日志底部以查看最新事件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-150">Scroll to the bottom of the log to see the most recent events.</span></span>

### <a name="run-the-app-in-the-kudu-console"></a><span data-ttu-id="8b2fa-151">在 Kudu 控制台中运行应用</span><span class="sxs-lookup"><span data-stu-id="8b2fa-151">Run the app in the Kudu console</span></span>

<span data-ttu-id="8b2fa-152">许多启动错误未在应用程序事件日志中生成有用信息。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-152">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="8b2fa-153">可以在 [Kudu](https://github.com/projectkudu/kudu/wiki) 远程执行控制台中运行应用以发现错误：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-153">You can run the app in the [Kudu](https://github.com/projectkudu/kudu/wiki) Remote Execution Console to discover the error:</span></span>

1. <span data-ttu-id="8b2fa-154">选择“开发工具”区域中的“高级工具”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-154">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8b2fa-155">选择“转到&rarr;”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-155">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8b2fa-156">此时将在新的浏览器选项卡或窗口中打开 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-156">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8b2fa-157">使用页面顶部的导航栏，打开“调试控制台”并选择“CMD”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-157">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8b2fa-158">打开路径“site > wwwroot”下的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-158">Open the folders to the path **site** > **wwwroot**.</span></span>
1. <span data-ttu-id="8b2fa-159">在控制台中，通过执行应用的程序集来运行该应用。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-159">In the console, run the app by executing the app's assembly.</span></span>
   * <span data-ttu-id="8b2fa-160">如果应用是[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，则使用 dotnet.exe 运行应用的程序集。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-160">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd), run the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="8b2fa-161">在以下命令中，替换 `<assembly_name>` 的应用程序集的名称：`dotnet .\<assembly_name>.dll`</span><span class="sxs-lookup"><span data-stu-id="8b2fa-161">In the following command, substitute the name of the app's assembly for `<assembly_name>`: `dotnet .\<assembly_name>.dll`</span></span>
   * <span data-ttu-id="8b2fa-162">如果应用是[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)，则运行应用的可执行文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-162">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd), run the app's executable.</span></span> <span data-ttu-id="8b2fa-163">在以下命令中，替换 `<assembly_name>` 的应用程序集的名称：`<assembly_name>.exe`</span><span class="sxs-lookup"><span data-stu-id="8b2fa-163">In the following command, substitute the name of the app's assembly for `<assembly_name>`: `<assembly_name>.exe`</span></span>
1. <span data-ttu-id="8b2fa-164">来自应用且显示任何错误的控制台输出将传送到 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-164">The console output from the app, showing any errors, is piped to the Kudu console.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="8b2fa-165">ASP.NET Core 模块 stdout 日志</span><span class="sxs-lookup"><span data-stu-id="8b2fa-165">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="8b2fa-166">ASP.NET Core 模块 stdout 日志通常记录应用程序事件日志中找不到的有用错误消息。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-166">The ASP.NET Core Module stdout log often records useful error messages not found in the Application Event Log.</span></span> <span data-ttu-id="8b2fa-167">若要启用和查看 stdout 日志，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-167">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="8b2fa-168">在 Azure 门户中导航到“诊断并解决问题”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-168">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="8b2fa-169">在“选择问题类别”下，选择“Web 应用关闭”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-169">Under **SELECT PROBLEM CATEGORY**, select the **Web App Down** button.</span></span>
1. <span data-ttu-id="8b2fa-170">在“建议的解决方案” > “启用 Stdout 日志重定向”下，选择“打开 Kudu 控制台以编辑 Web.Config”对应的按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-170">Under **Suggested Solutions** > **Enable Stdout Log Redirection**, select the button to **Open Kudu Console to edit Web.Config**.</span></span>
1. <span data-ttu-id="8b2fa-171">在 Kudu 诊断控制台中，打开路径“站点 > wwwroot”下的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-171">In the Kudu **Diagnostic Console**, open the folders to the path **site** > **wwwroot**.</span></span> <span data-ttu-id="8b2fa-172">向下滚动以在列表底部显示“web.config”文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-172">Scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="8b2fa-173">单击“web.config”文件旁边的铅笔图标。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-173">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="8b2fa-174">将“stdoutLogEnabled”设置为 `true`，并将“stdoutLogFile”路径更改为 `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-174">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="8b2fa-175">选择“保存”以保存已更新的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-175">Select **Save** to save the updated *web.config* file.</span></span>
1. <span data-ttu-id="8b2fa-176">向应用发出请求。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-176">Make a request to the app.</span></span>
1. <span data-ttu-id="8b2fa-177">返回到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-177">Return to the Azure portal.</span></span> <span data-ttu-id="8b2fa-178">选择“开发工具”区域中的“高级工具”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-178">Select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8b2fa-179">选择“转到&rarr;”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-179">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8b2fa-180">此时将在新的浏览器选项卡或窗口中打开 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-180">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8b2fa-181">使用页面顶部的导航栏，打开“调试控制台”并选择“CMD”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-181">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8b2fa-182">选择“LogFiles”文件夹。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-182">Select the **LogFiles** folder.</span></span>
1. <span data-ttu-id="8b2fa-183">检查“已修改”列并选择铅笔图标以编辑具有最新修改日期的 stdout 日志。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-183">Inspect the **Modified** column and select the pencil icon to edit the stdout log with the latest modification date.</span></span>
1. <span data-ttu-id="8b2fa-184">打开日志文件后，将显示错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-184">When the log file opens, the error is displayed.</span></span>

<span data-ttu-id="8b2fa-185">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="8b2fa-185">**Important!**</span></span> <span data-ttu-id="8b2fa-186">故障排除完成后，禁用 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-186">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="8b2fa-187">在 Kudu 诊断控制台中，返回到路径“site > wwwroot”以显示 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-187">In the Kudu **Diagnostic Console**, return to the path **site** > **wwwroot** to reveal the *web.config* file.</span></span> <span data-ttu-id="8b2fa-188">通过选择铅笔图标再次打开 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-188">Open the **web.config** file again by selecting the pencil icon.</span></span>
1. <span data-ttu-id="8b2fa-189">将“stdoutLogEnabled”设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-189">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="8b2fa-190">选择“保存”以保存文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-190">Select **Save** to save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="8b2fa-191">无法禁用 stdout 日志可能会导致应用或服务器出现故障。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-191">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="8b2fa-192">日志文件大小或创建的日志文件数没有限制。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-192">There's no limit on log file size or the number of log files created.</span></span> <span data-ttu-id="8b2fa-193">仅使用 stdout 日志记录来解决应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-193">Only use stdout logging to troubleshoot app startup problems.</span></span>
>
> <span data-ttu-id="8b2fa-194">对于在 ASP.NET Core 应用启动后生成的常规日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-194">For general logging in an ASP.NET Core app after startup, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="8b2fa-195">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-195">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="8b2fa-196">常见启动错误</span><span class="sxs-lookup"><span data-stu-id="8b2fa-196">Common startup errors</span></span> 

<span data-ttu-id="8b2fa-197">请参阅 [ASP.NET Core 常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-197">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="8b2fa-198">参考主题介绍了阻止应用启动的大部分常见问题。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-198">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="8b2fa-199">应用缓慢或挂起</span><span class="sxs-lookup"><span data-stu-id="8b2fa-199">Slow or hanging app</span></span>

<span data-ttu-id="8b2fa-200">当应用响应缓慢或挂起请求时，请参阅[解决 Azure 应用服务中 Web 应用性能缓慢的问题](/azure/app-service/app-service-web-troubleshoot-performance-degradation)以获取调试指导。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-200">When an app responds slowly or hangs on a request, see [Troubleshoot slow web app performance issues in Azure App Service](/azure/app-service/app-service-web-troubleshoot-performance-degradation) for debugging guidance.</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="8b2fa-201">远程调试</span><span class="sxs-lookup"><span data-stu-id="8b2fa-201">Remote debugging</span></span>

<span data-ttu-id="8b2fa-202">请参见下面的主题：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-202">See the following topics:</span></span>

* <span data-ttu-id="8b2fa-203">[使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除的远程调试 Web 应用部分](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug)（Azure 文档）</span><span class="sxs-lookup"><span data-stu-id="8b2fa-203">[Remote debugging web apps section of Troubleshoot a web app in Azure App Service using Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug) (Azure documentation)</span></span>
* <span data-ttu-id="8b2fa-204">[在 Visual Studio 2017 的 Azure 中的 IIS 上远程调试 ASP.NET Core](/visualstudio/debugger/remote-debugging-azure)（Visual Studio 文档）</span><span class="sxs-lookup"><span data-stu-id="8b2fa-204">[Remote Debug ASP.NET Core on IIS in Azure in Visual Studio 2017](/visualstudio/debugger/remote-debugging-azure) (Visual Studio documentation)</span></span>

## <a name="application-insights"></a><span data-ttu-id="8b2fa-205">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8b2fa-205">Application Insights</span></span>

<span data-ttu-id="8b2fa-206">[Application Insights](https://azure.microsoft.com/services/application-insights/) 提供来自 Azure 应用服务中托管的应用的遥测，包括错误日志记录和报告功能。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-206">[Application Insights](https://azure.microsoft.com/services/application-insights/) provides telemetry from apps hosted in the Azure App Service, including error logging and reporting features.</span></span> <span data-ttu-id="8b2fa-207">当应用的日志记录功能变得可用时，Application Insights 只能报告应用启动后出现的错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-207">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="8b2fa-208">有关详细信息，请参阅[用于 ASP.NET Core 的 Application Insights](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-208">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="monitoring-blades"></a><span data-ttu-id="8b2fa-209">监视边栏选项卡</span><span class="sxs-lookup"><span data-stu-id="8b2fa-209">Monitoring blades</span></span>

<span data-ttu-id="8b2fa-210">监视边栏选项卡提供了本主题前面所述的方法的替代故障排除体验。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-210">Monitoring blades provide an alternative troubleshooting experience to the methods described earlier in the topic.</span></span> <span data-ttu-id="8b2fa-211">这些边栏选项卡可用于诊断 500 系列错误。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-211">These blades can be used to diagnose 500-series errors.</span></span>

<span data-ttu-id="8b2fa-212">确认是否已安装 ASP.NET Core 扩展。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-212">Confirm that the ASP.NET Core Extensions are installed.</span></span> <span data-ttu-id="8b2fa-213">如果未安装扩展，请手动进行安装：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-213">If the extensions aren't installed, install them manually:</span></span>

1. <span data-ttu-id="8b2fa-214">在“开发工具”边栏选项卡部分中，选择“扩展”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-214">In the **DEVELOPMENT TOOLS** blade section, select the **Extensions** blade.</span></span>
1. <span data-ttu-id="8b2fa-215">“ASP.NET Core 扩展”应显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-215">The **ASP.NET Core Extensions** should appear in the list.</span></span>
1. <span data-ttu-id="8b2fa-216">如果未安装扩展，请选择“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-216">If the extensions aren't installed, select the **Add** button.</span></span>
1. <span data-ttu-id="8b2fa-217">从列表中选择“ASP.NET Core 扩展”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-217">Choose the **ASP.NET Core Extensions** from the list.</span></span>
1. <span data-ttu-id="8b2fa-218">选择“确定”以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-218">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="8b2fa-219">选择“添加扩展”边栏选项卡上的“确定”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-219">Select **OK** on the **Add extension** blade.</span></span>
1. <span data-ttu-id="8b2fa-220">信息性弹出消息指示成功安装扩展的时间。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-220">An informational pop-up message indicates when the extensions are successfully installed.</span></span>

<span data-ttu-id="8b2fa-221">如果未启用 stdout 日志记录，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-221">If stdout logging isn't enabled, follow these steps:</span></span>

1. <span data-ttu-id="8b2fa-222">在 Azure 门户中，选择“开发工具”区域中的“高级工具”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-222">In the Azure portal, select the **Advanced Tools** blade in the **DEVELOPMENT TOOLS** area.</span></span> <span data-ttu-id="8b2fa-223">选择“转到&rarr;”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-223">Select the **Go&rarr;** button.</span></span> <span data-ttu-id="8b2fa-224">此时将在新的浏览器选项卡或窗口中打开 Kudu 控制台。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-224">The Kudu console opens in a new browser tab or window.</span></span>
1. <span data-ttu-id="8b2fa-225">使用页面顶部的导航栏，打开“调试控制台”并选择“CMD”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-225">Using the navigation bar at the top of the page, open **Debug console** and select **CMD**.</span></span>
1. <span data-ttu-id="8b2fa-226">打开路径“site > wwwroot”下的文件夹，然后向下滚动以显示列表底部的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-226">Open the folders to the path **site** > **wwwroot** and scroll down to reveal the *web.config* file at the bottom of the list.</span></span>
1. <span data-ttu-id="8b2fa-227">单击“web.config”文件旁边的铅笔图标。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-227">Click the pencil icon next to the *web.config* file.</span></span>
1. <span data-ttu-id="8b2fa-228">将“stdoutLogEnabled”设置为 `true`，并将“stdoutLogFile”路径更改为 `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-228">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to: `\\?\%home%\LogFiles\stdout`.</span></span>
1. <span data-ttu-id="8b2fa-229">选择“保存”以保存已更新的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-229">Select **Save** to save the updated *web.config* file.</span></span>

<span data-ttu-id="8b2fa-230">继续激活诊断日志记录：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-230">Proceed to activate diagnostic logging:</span></span>

1. <span data-ttu-id="8b2fa-231">在 Azure 门户中，选择“诊断日志”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-231">In the Azure portal, select the **Diagnostics logs** blade.</span></span>
1. <span data-ttu-id="8b2fa-232">选择“应用程序日志记录(文件系统)”和“详细错误消息”的“开”开关。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-232">Select the **On** switch for **Application Logging (Filesystem)** and **Detailed error messages**.</span></span> <span data-ttu-id="8b2fa-233">选择边栏选项卡顶部的“保存”按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-233">Select the **Save** button at the top of the blade.</span></span>
1. <span data-ttu-id="8b2fa-234">若要包含失败请求跟踪（也称为失败请求事件缓冲 (FREB) 日志记录），请选择“失败请求跟踪”的“开”开关。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-234">To include failed request tracing, also known as Failed Request Event Buffering (FREB) logging, select the **On** switch for **Failed request tracing**.</span></span> 
1. <span data-ttu-id="8b2fa-235">选择“日志流”边栏选项卡，将在门户中的“诊断日志”边栏选项卡下立即列出。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-235">Select the **Log stream** blade, which is listed immediately under the **Diagnostics logs** blade in the portal.</span></span>
1. <span data-ttu-id="8b2fa-236">向应用发出请求。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-236">Make a request to the app.</span></span>
1. <span data-ttu-id="8b2fa-237">在日志流数据中，指示了错误的原因。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-237">Within the log stream data, the cause of the error is indicated.</span></span>

<span data-ttu-id="8b2fa-238">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="8b2fa-238">**Important!**</span></span> <span data-ttu-id="8b2fa-239">故障排除完成后，请务必禁用 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-239">Be sure to disable stdout logging when troubleshooting is complete.</span></span> <span data-ttu-id="8b2fa-240">请参阅 [ASP.NET Core 模块 stdout 日志](#aspnet-core-module-stdout-log)部分中的说明。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-240">See the instructions in the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) section.</span></span>

<span data-ttu-id="8b2fa-241">若要查看失败请求跟踪日志（FREB 日志），请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="8b2fa-241">To view the failed request tracing logs (FREB logs):</span></span>

1. <span data-ttu-id="8b2fa-242">在 Azure 门户中导航到“诊断并解决问题”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-242">Navigate to the **Diagnose and solve problems** blade in the Azure portal.</span></span>
1. <span data-ttu-id="8b2fa-243">从侧栏的“支持工具”区域中选择“失败请求跟踪日志”。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-243">Select **Failed Request Tracing Logs** from the **SUPPORT TOOLS** area of the sidebar.</span></span>

<span data-ttu-id="8b2fa-244">有关详细信息，请参阅[“在 Azure 应用服务中启用 Web 应用的诊断日志记录”主题的“失败请求跟踪”部分](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces)和 [Azure 中的 Web 应用的应用程序性能常见问题：如何打开失败请求跟踪？](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-244">See [Failed request traces section of the Enable diagnostics logging for web apps in Azure App Service topic](/azure/app-service/web-sites-enable-diagnostic-log#failed-request-traces) and the [Application performance FAQs for Web Apps in Azure: How do I turn on failed request tracing?](/azure/app-service/app-service-web-availability-performance-application-issues-faq#how-do-i-turn-on-failed-request-tracing) for more information.</span></span>

<span data-ttu-id="8b2fa-245">有关详细信息，请参阅[在 Azure 应用服务中启用 Web 应用的诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-245">For more information, see [Enable diagnostics logging for web apps in Azure App Service](/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

> [!WARNING]
> <span data-ttu-id="8b2fa-246">无法禁用 stdout 日志可能会导致应用或服务器出现故障。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-246">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="8b2fa-247">日志文件大小或创建的日志文件数没有限制。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-247">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="8b2fa-248">对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-248">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="8b2fa-249">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="8b2fa-249">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b2fa-250">其他资源</span><span class="sxs-lookup"><span data-stu-id="8b2fa-250">Additional resources</span></span>

* [<span data-ttu-id="8b2fa-251">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="8b2fa-251">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="8b2fa-252">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="8b2fa-252">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="8b2fa-253">使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="8b2fa-253">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)
* [<span data-ttu-id="8b2fa-254">解决 Azure Web 应用中的“502 错误的网关”和“503 服务不可用”HTTP 错误</span><span class="sxs-lookup"><span data-stu-id="8b2fa-254">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>](/app-service/app-service-web-troubleshoot-http-502-http-503)
* [<span data-ttu-id="8b2fa-255">解决 Azure 应用服务中 Web 应用性能缓慢的问题</span><span class="sxs-lookup"><span data-stu-id="8b2fa-255">Troubleshoot slow web app performance issues in Azure App Service</span></span>](/azure/app-service/app-service-web-troubleshoot-performance-degradation)
* [<span data-ttu-id="8b2fa-256">Azure 中的 Web 应用的应用程序性能常见问题</span><span class="sxs-lookup"><span data-stu-id="8b2fa-256">Application performance FAQs for Web Apps in Azure</span></span>](/azure/app-service/app-service-web-availability-performance-application-issues-faq)
* [<span data-ttu-id="8b2fa-257">Azure Web 应用沙盒（应用服务运行时执行限制）</span><span class="sxs-lookup"><span data-stu-id="8b2fa-257">Azure Web App sandbox (App Service runtime execution limitations)</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)
* [<span data-ttu-id="8b2fa-258">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="8b2fa-258">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
