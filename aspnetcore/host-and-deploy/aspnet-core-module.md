---
title: ASP.NET Core 模块配置参考
author: guardrex
description: 了解如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 954841a1b1465c80e60d5745ad9e22294a88fdf4
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
ms.locfileid: "31483742"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="863f8-103">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="863f8-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="863f8-104">作者：[Luke Latham](https://github.com/guardrex)、[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="863f8-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="863f8-105">本文档说明了如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="863f8-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="863f8-106">有关 ASP.NET Core 模块简介和安装说明，请参阅 [ASP.NET Core 模块概述](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="863f8-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="863f8-107">web.config 的配置</span><span class="sxs-lookup"><span data-stu-id="863f8-107">Configuration with web.config</span></span>

<span data-ttu-id="863f8-108">在站点的 *web.config* 文件中使用 `system.webServer` 节点的 `aspNetCore` 部分配置 ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="863f8-108">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="863f8-109">以下 *web.config* 文件发布用于[依赖框架的部署](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)，并配置 ASP.NET Core 模块以处理站点请求：</span><span class="sxs-lookup"><span data-stu-id="863f8-109">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" 
                arguments=".\MyApp.dll" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="863f8-110">以下 web.config 发布用于[独立部署](/dotnet/articles/core/deploying/#self-contained-deployments-scd)：</span><span class="sxs-lookup"><span data-stu-id="863f8-110">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="863f8-111">将应用部署为 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)时，`stdoutLogFile` 路径将设置为 `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="863f8-111">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="863f8-112">该路径会将 stdout 日志保存到 *LogFiles* 文件夹，该文件夹是由服务自动创建的位置。</span><span class="sxs-lookup"><span data-stu-id="863f8-112">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="863f8-113">有关在子应用中配置 *web.config* 文件的重要说明，请参阅[子应用程序配置](xref:host-and-deploy/iis/index#sub-application-configuration)。</span><span class="sxs-lookup"><span data-stu-id="863f8-113">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="863f8-114">aspNetCore 元素的属性</span><span class="sxs-lookup"><span data-stu-id="863f8-114">Attributes of the aspNetCore element</span></span>

::: moniker range="<= aspnetcore-2.0"
| <span data-ttu-id="863f8-115">特性</span><span class="sxs-lookup"><span data-stu-id="863f8-115">Attribute</span></span> | <span data-ttu-id="863f8-116">描述</span><span class="sxs-lookup"><span data-stu-id="863f8-116">Description</span></span> | <span data-ttu-id="863f8-117">默认</span><span class="sxs-lookup"><span data-stu-id="863f8-117">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="863f8-118">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-118">Optional string attribute.</span></span></p><p><span data-ttu-id="863f8-119">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="863f8-119">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <span data-ttu-id="863f8-120">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="863f8-120">true or false.</span></span></p><p><span data-ttu-id="863f8-121">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="863f8-121">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <span data-ttu-id="863f8-122">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="863f8-122">true or false.</span></span></p><p><span data-ttu-id="863f8-123">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-123">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="863f8-124">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="863f8-124">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processPath` | <p><span data-ttu-id="863f8-125">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-125">Required string attribute.</span></span></p><p><span data-ttu-id="863f8-126">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-126">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="863f8-127">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-127">Relative paths are supported.</span></span> <span data-ttu-id="863f8-128">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="863f8-128">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="863f8-129">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-129">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-130">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="863f8-130">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="863f8-131">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-131">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | `10` |
| `requestTimeout` | <p><span data-ttu-id="863f8-132">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-132">Optional timespan attribute.</span></span></p><p><span data-ttu-id="863f8-133">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="863f8-133">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="863f8-134">在 ASP.NET Core 2.0 或更早版本附带的 ASP.NET Core 模块版本中，必须仅使用整分钟数指定 `requestTimeout`，否则默认为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="863f8-134">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | `00:02:00` |
| `shutdownTimeLimit` | <p><span data-ttu-id="863f8-135">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-135">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-136">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="863f8-136">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | `10` |
| `startupTimeLimit` | <p><span data-ttu-id="863f8-137">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-137">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-138">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="863f8-138">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="863f8-139">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-139">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="863f8-140">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="863f8-140">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | `120` |
| `stdoutLogEnabled` | <p><span data-ttu-id="863f8-141">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-141">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="863f8-142">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-142">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="863f8-143">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-143">Optional string attribute.</span></span></p><p><span data-ttu-id="863f8-144">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-144">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="863f8-145">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="863f8-145">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="863f8-146">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-146">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="863f8-147">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-147">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="863f8-148">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="863f8-148">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="863f8-149">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="863f8-149">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| <span data-ttu-id="863f8-150">特性</span><span class="sxs-lookup"><span data-stu-id="863f8-150">Attribute</span></span> | <span data-ttu-id="863f8-151">描述</span><span class="sxs-lookup"><span data-stu-id="863f8-151">Description</span></span> | <span data-ttu-id="863f8-152">默认</span><span class="sxs-lookup"><span data-stu-id="863f8-152">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="863f8-153">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-153">Optional string attribute.</span></span></p><p><span data-ttu-id="863f8-154">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="863f8-154">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <span data-ttu-id="863f8-155">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="863f8-155">true or false.</span></span></p><p><span data-ttu-id="863f8-156">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="863f8-156">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <span data-ttu-id="863f8-157">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="863f8-157">true or false.</span></span></p><p><span data-ttu-id="863f8-158">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-158">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="863f8-159">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="863f8-159">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processPath` | <p><span data-ttu-id="863f8-160">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-160">Required string attribute.</span></span></p><p><span data-ttu-id="863f8-161">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-161">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="863f8-162">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-162">Relative paths are supported.</span></span> <span data-ttu-id="863f8-163">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="863f8-163">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="863f8-164">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-164">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-165">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="863f8-165">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="863f8-166">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-166">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | `10` |
| `requestTimeout` | <p><span data-ttu-id="863f8-167">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-167">Optional timespan attribute.</span></span></p><p><span data-ttu-id="863f8-168">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="863f8-168">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="863f8-169">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</span><span class="sxs-lookup"><span data-stu-id="863f8-169">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | `00:02:00` |
| `shutdownTimeLimit` | <p><span data-ttu-id="863f8-170">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-170">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-171">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="863f8-171">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | `10` |
| `startupTimeLimit` | <p><span data-ttu-id="863f8-172">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-172">Optional integer attribute.</span></span></p><p><span data-ttu-id="863f8-173">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="863f8-173">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="863f8-174">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-174">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="863f8-175">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="863f8-175">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | `120` |
| `stdoutLogEnabled` | <p><span data-ttu-id="863f8-176">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-176">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="863f8-177">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-177">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="863f8-178">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-178">Optional string attribute.</span></span></p><p><span data-ttu-id="863f8-179">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-179">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="863f8-180">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="863f8-180">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="863f8-181">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-181">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="863f8-182">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-182">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="863f8-183">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="863f8-183">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="863f8-184">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="863f8-184">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |
::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="863f8-185">设置环境变量</span><span class="sxs-lookup"><span data-stu-id="863f8-185">Setting environment variables</span></span>

<span data-ttu-id="863f8-186">可以为 `processPath` 属性中的进程指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="863f8-186">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="863f8-187">使用 `environmentVariables` 集合元素的 `environmentVariable` 子元素指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="863f8-187">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="863f8-188">本部分中设置的环境变量优先于系统环境变量。</span><span class="sxs-lookup"><span data-stu-id="863f8-188">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="863f8-189">以下示例设置了两个环境变量。</span><span class="sxs-lookup"><span data-stu-id="863f8-189">The following example sets two environment variables.</span></span> <span data-ttu-id="863f8-190">`ASPNETCORE_ENVIRONMENT` 将应用的环境配置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="863f8-190">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="863f8-191">开发人员可能会暂时在 web.config 文件中设置此值，以便在调试应用异常时强制加载[开发人员异常页面](xref:fundamentals/error-handling)。</span><span class="sxs-lookup"><span data-stu-id="863f8-191">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="863f8-192">`CONFIG_DIR` 是用户定义的环境变量的一个示例，其中开发人员已写入可在启动时读取值的代码以便形成用于加载应用配置文件的路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-192">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

> [!WARNING]
> <span data-ttu-id="863f8-193">在不可访问不受信任的网络（如 Internet）的暂存服务器和测试服务器上，仅将 `ASPNETCORE_ENVIRONMENT` 环境变量设置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="863f8-193">Only set the `ASPNETCORE_ENVIRONMENT` envirnonment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="863f8-194">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="863f8-194">app_offline.htm</span></span>

<span data-ttu-id="863f8-195">如果在应用的根目录中检测到名为 “app_offline.htm”的文件，ASP.NET Core 模块将尝试正常关闭应用并停止处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="863f8-195">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="863f8-196">如果应用在 `shutdownTimeLimit` 中定义的秒数之后仍在运行，ASP.NET Core 模块将终止正在运行的进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-196">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="863f8-197">存在 app_offline.htm 文件时，ASP.NET Core 模块会通过发送回 app_offline.htm 文件的内容来响应请求。</span><span class="sxs-lookup"><span data-stu-id="863f8-197">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="863f8-198">删除 app_offline.htm 文件后，下一个请求将启动应用。</span><span class="sxs-lookup"><span data-stu-id="863f8-198">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

## <a name="start-up-error-page"></a><span data-ttu-id="863f8-199">启动错误页面</span><span class="sxs-lookup"><span data-stu-id="863f8-199">Start-up error page</span></span>

<span data-ttu-id="863f8-200">如果 ASP.NET Core 模块无法启动后端进程或后端进程启动但无法在配置的端口上侦听，则将显示“502.5 进程失败”状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="863f8-200">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 Process Failure* status code page appears.</span></span> <span data-ttu-id="863f8-201">若要禁止显示此页面并还原为默认 IIS 502 状态代码页面，请使用 `disableStartUpErrorPage` 属性。</span><span class="sxs-lookup"><span data-stu-id="863f8-201">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="863f8-202">有关配置自定义错误消息的详细信息，请参阅 [HTTP 错误 `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="863f8-202">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/).</span></span>

![“502.5 进程失败”状态代码页面](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="863f8-204">日志创建和重定向</span><span class="sxs-lookup"><span data-stu-id="863f8-204">Log creation and redirection</span></span>

<span data-ttu-id="863f8-205">如果已设置 `aspNetCore` 元素的 `stdoutLogEnabled` 和 `stdoutLogFile` 属性，ASP.NET Core 模块会将 stdout 和 stderr 日志重定向到磁盘。</span><span class="sxs-lookup"><span data-stu-id="863f8-205">The ASP.NET Core Module redirects stdout and stderr logs to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="863f8-206">`stdoutLogFile` 路径中的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-206">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="863f8-207">应用池必须对写入日志的位置具有写入权限（使用 `IIS AppPool\<app_pool_name>` 提供写入权限）。</span><span class="sxs-lookup"><span data-stu-id="863f8-207">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="863f8-208">日志不会旋转，除非回收/重新启动进程。</span><span class="sxs-lookup"><span data-stu-id="863f8-208">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="863f8-209">宿主负责限制日志占用的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="863f8-209">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="863f8-210">仅建议使用 stdout 日志来解决应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="863f8-210">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="863f8-211">不要将 stdout 日志用于常规应用日志记录。</span><span class="sxs-lookup"><span data-stu-id="863f8-211">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="863f8-212">对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="863f8-212">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="863f8-213">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="863f8-213">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="863f8-214">创建日志文件时，将自动添加时间戳和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="863f8-214">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="863f8-215">日志文件名是通过将时间戳、进程 ID 和文件扩展名 (.log) 附加到由下划线分隔的 `stdoutLogFile` 路径的最后一段（通常为 stdout）组合而成的。</span><span class="sxs-lookup"><span data-stu-id="863f8-215">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="863f8-216">如果 `stdoutLogFile` 路径以 stdout 结尾，则 PID 为 1934 且于 2018 年 2 月 5 日 19:42:32 创建的应用的日志的文件名为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="863f8-216">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

<span data-ttu-id="863f8-217">以下示例 `aspNetCore` 元素为 Azure 应用服务中托管的应用配置 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="863f8-217">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="863f8-218">本地日志记录可以接受本地路径或网络共享路径。</span><span class="sxs-lookup"><span data-stu-id="863f8-218">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="863f8-219">确认应用池用户标识是否已提供写入路径的权限。</span><span class="sxs-lookup"><span data-stu-id="863f8-219">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

<span data-ttu-id="863f8-220">有关 web.config 文件中的 `aspNetCore` 元素的示例，请参阅 [web.config 的配置](#configuration-with-webconfig)。</span><span class="sxs-lookup"><span data-stu-id="863f8-220">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="863f8-221">代理配置使用 HTTP 协议和配对令牌</span><span class="sxs-lookup"><span data-stu-id="863f8-221">Proxy configuration uses HTTP protocol and a pairing token</span></span>

<span data-ttu-id="863f8-222">在 ASP.NET Core 模块和 Kestrel 之间创建的代理使用 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="863f8-222">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="863f8-223">使用 HTTP 是一种性能优化，其中模块和 Kestrel 之间的流量发生于脱离网络接口的环回地址。</span><span class="sxs-lookup"><span data-stu-id="863f8-223">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="863f8-224">因此，不存在从脱离服务器的位置窃取模块和 Kestrel 之间的流量的风险。</span><span class="sxs-lookup"><span data-stu-id="863f8-224">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="863f8-225">配对令牌用于保证 Kestrel 收到的请求已由 IIS 代理且不来自某些其他源。</span><span class="sxs-lookup"><span data-stu-id="863f8-225">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="863f8-226">模块已创建配对令牌并将其设置到环境变量 (`ASPNETCORE_TOKEN`)。</span><span class="sxs-lookup"><span data-stu-id="863f8-226">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="863f8-227">此外，配对令牌还设置到每个代理请求的标头 (`MSAspNetCoreToken`)。</span><span class="sxs-lookup"><span data-stu-id="863f8-227">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="863f8-228">IIS 中间件检查它所接收的每个请求，以确认配对令牌标头值与环境变量值相匹配。</span><span class="sxs-lookup"><span data-stu-id="863f8-228">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="863f8-229">如果令牌值不匹配，则将记录请求并拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="863f8-229">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="863f8-230">无法从脱离服务器的位置访问配对令牌环境变量及模块和 Kestrel 之间的流量。</span><span class="sxs-lookup"><span data-stu-id="863f8-230">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="863f8-231">如果不知道配对令牌值，攻击者就无法提交绕过 IIS 中间件中的检查的请求。</span><span class="sxs-lookup"><span data-stu-id="863f8-231">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="863f8-232">具有 IIS 共享配置的 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="863f8-232">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="863f8-233">ASP.NET Core 模块安装程序使用系统帐户的权限运行。</span><span class="sxs-lookup"><span data-stu-id="863f8-233">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="863f8-234">由于本地系统帐户没有对 IIS 共享配置所用的共享路径的修改权限，因此在尝试配置共享上的 applicationHost.config 中的模块设置时，安装程序将遇到拒绝访问错误。</span><span class="sxs-lookup"><span data-stu-id="863f8-234">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="863f8-235">使用 IIS 共享配置时，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="863f8-235">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="863f8-236">禁用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="863f8-236">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="863f8-237">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="863f8-237">Run the installer.</span></span>
1. <span data-ttu-id="863f8-238">将已更新的 applicationHost.config 文件导出到共享。</span><span class="sxs-lookup"><span data-stu-id="863f8-238">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="863f8-239">重新启用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="863f8-239">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="863f8-240">模块版本和托管捆绑安装程序日志</span><span class="sxs-lookup"><span data-stu-id="863f8-240">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="863f8-241">若要确定已安装 ASP.NET Core 模块的版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="863f8-241">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="863f8-242">在托管系统上，导航到 %windir%\System32\inetsrv。</span><span class="sxs-lookup"><span data-stu-id="863f8-242">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="863f8-243">找到 aspnetcore.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-243">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="863f8-244">右键单击该文件，然后从上下文菜单中选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="863f8-244">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="863f8-245">选择“详细信息”选项卡。“文件版本”和“产品版本”表示模块的已安装版本。</span><span class="sxs-lookup"><span data-stu-id="863f8-245">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="863f8-246">在 C:\\Users\\%UserName%\\AppData\\Local\\Temp 中找到了模块的托管捆绑安装程序日志。该文件名为 dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log。</span><span class="sxs-lookup"><span data-stu-id="863f8-246">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="863f8-247">模块、架构和配置文件位置</span><span class="sxs-lookup"><span data-stu-id="863f8-247">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="863f8-248">模块</span><span class="sxs-lookup"><span data-stu-id="863f8-248">Module</span></span>

<span data-ttu-id="863f8-249">**IIS (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="863f8-249">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="863f8-250">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="863f8-250">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="863f8-251">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="863f8-251">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="863f8-252">**IIS Express (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="863f8-252">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="863f8-253">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="863f8-253">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="863f8-254">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="863f8-254">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="863f8-255">架构</span><span class="sxs-lookup"><span data-stu-id="863f8-255">Schema</span></span>

<span data-ttu-id="863f8-256">**IIS**</span><span class="sxs-lookup"><span data-stu-id="863f8-256">**IIS**</span></span>

   * <span data-ttu-id="863f8-257">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="863f8-257">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="863f8-258">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="863f8-258">**IIS Express**</span></span>

   * <span data-ttu-id="863f8-259">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="863f8-259">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="863f8-260">配置</span><span class="sxs-lookup"><span data-stu-id="863f8-260">Configuration</span></span>

<span data-ttu-id="863f8-261">**IIS**</span><span class="sxs-lookup"><span data-stu-id="863f8-261">**IIS**</span></span>

   * <span data-ttu-id="863f8-262">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="863f8-262">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="863f8-263">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="863f8-263">**IIS Express**</span></span>

   * <span data-ttu-id="863f8-264">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="863f8-264">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="863f8-265">可以通过在 applicationHost.config 文件中搜索 aspnetcore.dll 找到这些文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-265">The files can be found by searching for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="863f8-266">对于 IIS Express，默认情况下不会存在 applicationHost.config 文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-266">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="863f8-267">在 Visual Studio 解决方案中启动任何 Web 应用项目时，将在 \<application_root>\\.vs\\config 中创建该文件。</span><span class="sxs-lookup"><span data-stu-id="863f8-267">The file is created at *\<application_root>\\.vs\\config* when starting any web app project in the Visual Studio solution.</span></span>
