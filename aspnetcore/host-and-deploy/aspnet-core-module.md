---
title: "ASP.NET 核心模块配置参考"
author: guardrex
description: "了解如何配置 ASP.NET 核心模块用于承载 ASP.NET Core 应用。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 5aac5cf2b8fd4bc53ba7201645b9bb02a5d1ecae
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="c6438-103">ASP.NET 核心模块配置参考</span><span class="sxs-lookup"><span data-stu-id="c6438-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="c6438-104">通过[Luke Latham](https://github.com/guardrex)， [Rick Anderson](https://twitter.com/RickAndMSFT)，和[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="c6438-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="c6438-105">本文档将说明了如何配置 ASP.NET 核心模块用于承载 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c6438-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="c6438-106">有关 ASP.NET 核心模块和安装说明简介，请参阅[ASP.NET 核心模块概述](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="c6438-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="c6438-107">Web.config 配置</span><span class="sxs-lookup"><span data-stu-id="c6438-107">Configuration with web.config</span></span>

<span data-ttu-id="c6438-108">使用配置 ASP.NET 核心模块`aspNetCore`部分`system.webServer`在站点的节点*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-108">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="c6438-109">以下*web.config*发布文件以便进行[framework 相关部署](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)和配置 ASP.NET 核心模块，以处理站点请求：</span><span class="sxs-lookup"><span data-stu-id="c6438-109">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

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

<span data-ttu-id="c6438-110">以下*web.config*为发布[独立的部署](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span><span class="sxs-lookup"><span data-stu-id="c6438-110">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

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

<span data-ttu-id="c6438-111">当应用程序部署到[Azure App Service](https://azure.microsoft.com/services/app-service/)、`stdoutLogFile`路径设置为`\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="c6438-111">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="c6438-112">路径将保存到 stdout 日志*LogFiles*文件夹，它是一个位置自动创建的服务。</span><span class="sxs-lookup"><span data-stu-id="c6438-112">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="c6438-113">请参阅[子应用程序配置](xref:host-and-deploy/iis/index#sub-application-configuration)的与配置相关的重要说明*web.config*子应用程序中的文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-113">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="c6438-114">AspNetCore 元素的特性</span><span class="sxs-lookup"><span data-stu-id="c6438-114">Attributes of the aspNetCore element</span></span>

| <span data-ttu-id="c6438-115">特性</span><span class="sxs-lookup"><span data-stu-id="c6438-115">Attribute</span></span> | <span data-ttu-id="c6438-116">描述</span><span class="sxs-lookup"><span data-stu-id="c6438-116">Description</span></span> | <span data-ttu-id="c6438-117">默认</span><span class="sxs-lookup"><span data-stu-id="c6438-117">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="c6438-118">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-118">Optional string attribute.</span></span></p><p><span data-ttu-id="c6438-119">可执行文件中指定的自变量**processPath**。</span><span class="sxs-lookup"><span data-stu-id="c6438-119">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <span data-ttu-id="c6438-120">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="c6438-120">true or false.</span></span></p><p><span data-ttu-id="c6438-121">如果为 true， **502.5-进程失败**页被禁止显示，并且 502 状态代码页中配置*web.config*优先。</span><span class="sxs-lookup"><span data-stu-id="c6438-121">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <span data-ttu-id="c6438-122">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="c6438-122">true or false.</span></span></p><p><span data-ttu-id="c6438-123">如果为 true，该令牌将转发到侦听作为每个请求的标头 MS ASPNETCORE WINAUTHTOKEN 的 %aspnetcore_port%的子进程。</span><span class="sxs-lookup"><span data-stu-id="c6438-123">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="c6438-124">它是该进程可以在每个请求此令牌上调用 CloseHandle 责任。</span><span class="sxs-lookup"><span data-stu-id="c6438-124">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processPath` | <p><span data-ttu-id="c6438-125">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-125">Required string attribute.</span></span></p><p><span data-ttu-id="c6438-126">将启动侦听 HTTP 请求的进程的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="c6438-126">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="c6438-127">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="c6438-127">Relative paths are supported.</span></span> <span data-ttu-id="c6438-128">如果路径以开始`.`，考虑使用该路径是相对站点根。</span><span class="sxs-lookup"><span data-stu-id="c6438-128">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="c6438-129">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-129">Optional integer attribute.</span></span></p><p><span data-ttu-id="c6438-130">指定在指定的进程的次数**processPath**允许每分钟崩溃。</span><span class="sxs-lookup"><span data-stu-id="c6438-130">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="c6438-131">如果超出此限制，该模块将停止启动剩余秒数的进程。</span><span class="sxs-lookup"><span data-stu-id="c6438-131">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | `10` |
| `requestTimeout` | <p><span data-ttu-id="c6438-132">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-132">Optional timespan attribute.</span></span></p><p><span data-ttu-id="c6438-133">指定为其 ASP.NET 核心模块等待侦听 %aspnetcore_port%的进程响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="c6438-133">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="c6438-134">`requestTimeout`必须指定整分钟数，否则它将默认为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="c6438-134">The `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | `00:02:00` |
| `shutdownTimeLimit` | <p><span data-ttu-id="c6438-135">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-135">Optional integer attribute.</span></span></p><p><span data-ttu-id="c6438-136">正常关闭的可执行文件的模块等待的秒数的持续时间时*app_offline.htm*检测到文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-136">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | `10` |
| `startupTimeLimit` | <p><span data-ttu-id="c6438-137">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-137">Optional integer attribute.</span></span></p><p><span data-ttu-id="c6438-138">持续时间以启动侦听端口的进程的可执行文件的模块等待的秒数。</span><span class="sxs-lookup"><span data-stu-id="c6438-138">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="c6438-139">如果超过此时间限制，该模块可终止进程。</span><span class="sxs-lookup"><span data-stu-id="c6438-139">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="c6438-140">模块将尝试重新启动该过程，在它接收新请求，并将继续尝试重新启动此过程在后续的传入请求，除非应用程序启动失败时**rapidFailsPerMinute**次数在最后一个滚动分钟。</span><span class="sxs-lookup"><span data-stu-id="c6438-140">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | `120` |
| `stdoutLogEnabled` | <p><span data-ttu-id="c6438-141">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-141">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="c6438-142">如果为 true， **stdout**和**stderr**中指定的进程的**processPath**重定向到中指定的文件**stdoutLogFile**。</span><span class="sxs-lookup"><span data-stu-id="c6438-142">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="c6438-143">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-143">Optional string attribute.</span></span></p><p><span data-ttu-id="c6438-144">为其指定的相对或绝对文件路径**stdout**和**stderr**中指定的进程从**processPath**记录。</span><span class="sxs-lookup"><span data-stu-id="c6438-144">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="c6438-145">相对路径是相对于站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="c6438-145">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="c6438-146">从任何路径`.`是相对于站点根和所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="c6438-146">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="c6438-147">路径中提供的任何文件夹必须存在于要创建的日志文件的模块的顺序。</span><span class="sxs-lookup"><span data-stu-id="c6438-147">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="c6438-148">使用下划线分隔符、 时间戳、 进程 ID 和文件扩展名 (*.log*) 添加到最后一个段**stdoutLogFile**路径。</span><span class="sxs-lookup"><span data-stu-id="c6438-148">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="c6438-149">如果`.\logs\stdout`提供一个值，作为示例 stdout 日志另存为*stdout_20180205194132_1934.log*中*日志*文件夹保存在 19:41:32 并且进程 ID 为 1934年 2/5/2018年。</span><span class="sxs-lookup"><span data-stu-id="c6438-149">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

### <a name="setting-environment-variables"></a><span data-ttu-id="c6438-150">设置环境变量</span><span class="sxs-lookup"><span data-stu-id="c6438-150">Setting environment variables</span></span>

<span data-ttu-id="c6438-151">环境变量可以为中的过程指定`processPath`属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-151">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="c6438-152">指定的环境变量`environmentVariable`的子元素`environmentVariables`集合元素。</span><span class="sxs-lookup"><span data-stu-id="c6438-152">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="c6438-153">在本部分中设置的环境变量优先于系统环境变量。</span><span class="sxs-lookup"><span data-stu-id="c6438-153">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="c6438-154">下面的示例设置两个环境变量。</span><span class="sxs-lookup"><span data-stu-id="c6438-154">The following example sets two environment variables.</span></span> <span data-ttu-id="c6438-155">`ASPNETCORE_ENVIRONMENT` 配置应用程序的环境以`Development`。</span><span class="sxs-lookup"><span data-stu-id="c6438-155">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="c6438-156">开发人员可能将此值暂时设置*web.config*文件以便强制[开发人员异常页](xref:fundamentals/error-handling)以便在调试应用程序异常时加载。</span><span class="sxs-lookup"><span data-stu-id="c6438-156">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="c6438-157">`CONFIG_DIR` 是一种用户定义的环境变量中，开发人员曾读取启动窗体中用于加载应用程序的配置文件的路径上的值的代码。</span><span class="sxs-lookup"><span data-stu-id="c6438-157">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

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
> <span data-ttu-id="c6438-158">只能设置`ASPNETCORE_ENVIRONMENT`envirnonment 变量`Development`过渡和测试不到不受信任的网络，例如 Internet 可访问的服务器上。</span><span class="sxs-lookup"><span data-stu-id="c6438-158">Only set the `ASPNETCORE_ENVIRONMENT` envirnonment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="c6438-159">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="c6438-159">app_offline.htm</span></span>

<span data-ttu-id="c6438-160">如果具有名称的文件*app_offline.htm*中检测到一个应用程序的根目录下 ASP.NET 核心模块尝试正常关闭应用程序，并停止处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="c6438-160">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="c6438-161">如果应用程序中定义的秒数后仍在运行`shutdownTimeLimit`，ASP.NET 核心模块将终止正在运行的进程。</span><span class="sxs-lookup"><span data-stu-id="c6438-161">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="c6438-162">虽然*app_offline.htm*存在文件，则 ASP.NET 核心模块响应请求通过发回的内容*app_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-162">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="c6438-163">当*app_offline.htm*删除文件，则下一个请求启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="c6438-163">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

## <a name="start-up-error-page"></a><span data-ttu-id="c6438-164">启动错误页</span><span class="sxs-lookup"><span data-stu-id="c6438-164">Start-up error page</span></span>

<span data-ttu-id="c6438-165">如果 ASP.NET 核心模块无法启动后端进程或后端进程启动但不能在配置的端口上侦听*502.5 进程失败*状态代码页将出现。</span><span class="sxs-lookup"><span data-stu-id="c6438-165">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 Process Failure* status code page appears.</span></span> <span data-ttu-id="c6438-166">若要禁止显示此页并还原为默认 IIS 502 状态代码页，请使用`disableStartUpErrorPage`属性。</span><span class="sxs-lookup"><span data-stu-id="c6438-166">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="c6438-167">有关配置自定义错误消息的详细信息，请参阅[HTTP 错误`<httpErrors>` ](/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="c6438-167">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 进程失败状态代码页](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="c6438-169">日志创建和重定向</span><span class="sxs-lookup"><span data-stu-id="c6438-169">Log creation and redirection</span></span>

<span data-ttu-id="c6438-170">ASP.NET 核心模块将重定向`stdout`和`stderr`日志磁盘如果`stdoutLogEnabled`和`stdoutLogFile`属性`aspNetCore`元素设置。</span><span class="sxs-lookup"><span data-stu-id="c6438-170">The ASP.NET Core Module redirects `stdout` and `stderr` logs to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="c6438-171">中的任何文件夹`stdoutLogFile`路径必须存在于要创建的日志文件的模块的顺序。</span><span class="sxs-lookup"><span data-stu-id="c6438-171">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="c6438-172">创建日志文件时，将自动添加时间戳和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="c6438-172">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="c6438-173">日志不轮换，除非进程回收/重新启动时发生。</span><span class="sxs-lookup"><span data-stu-id="c6438-173">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="c6438-174">它负责的托管商来限制日志使用的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="c6438-174">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span> <span data-ttu-id="c6438-175">使用`stdout`日志仅建议进行故障诊断应用程序启动问题。</span><span class="sxs-lookup"><span data-stu-id="c6438-175">Using the `stdout` log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="c6438-176">不要使用用于常规应用程序日志记录的 stdout 日志。</span><span class="sxs-lookup"><span data-stu-id="c6438-176">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="c6438-177">对于例程日志记录在 ASP.NET Core 应用程序，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="c6438-177">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="c6438-178">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="c6438-178">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="c6438-179">日志文件名称由后面追加时间戳、 进程 ID 和文件扩展名 (*.log*) 到的最后一段`stdoutLogFile`路径 (通常*stdout*) 由下划线分隔。</span><span class="sxs-lookup"><span data-stu-id="c6438-179">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="c6438-180">如果`stdoutLogFile`路径以结束*stdout*，pid 为 1934 在 19:42:32 2/5/2018年上创建的应用程序日志中的文件名称*stdout_20180205194132_1934.log*。</span><span class="sxs-lookup"><span data-stu-id="c6438-180">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

<span data-ttu-id="c6438-181">下面的示例`aspNetCore`元素会配置`stdout`已在 Azure App Service 中托管的应用程序的日志记录。</span><span class="sxs-lookup"><span data-stu-id="c6438-181">The following sample `aspNetCore` element configures `stdout` logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="c6438-182">本地路径或网络共享路径是可接受的本地日志记录。</span><span class="sxs-lookup"><span data-stu-id="c6438-182">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="c6438-183">确认应用程序池用户标识有权写入提供的路径。</span><span class="sxs-lookup"><span data-stu-id="c6438-183">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

<span data-ttu-id="c6438-184">请参阅[web.config 配置](#configuration-with-webconfig)有关的示例`aspNetCore`中的元素*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-184">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="c6438-185">代理配置使用 HTTP 协议和配对令牌</span><span class="sxs-lookup"><span data-stu-id="c6438-185">Proxy configuration uses HTTP protocol and a pairing token</span></span>

<span data-ttu-id="c6438-186">在 ASP.NET 核心模块和 Kestrel 之间创建的代理服务器使用 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="c6438-186">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="c6438-187">使用 HTTP 是一种性能优化，其中模块和 Kestrel 之间的通信发生在上环回地址从网络接口中移出。</span><span class="sxs-lookup"><span data-stu-id="c6438-187">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="c6438-188">没有任何风险的窃听模块和 Kestrel 从服务器中移出的位置之间的通信。</span><span class="sxs-lookup"><span data-stu-id="c6438-188">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="c6438-189">配对令牌用于保证 Kestrel 收到的请求已由 IIS 代理且不来自某些其他源。</span><span class="sxs-lookup"><span data-stu-id="c6438-189">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="c6438-190">创建并设置环境变量到配对的令牌 (`ASPNETCORE_TOKEN`) 由模块。</span><span class="sxs-lookup"><span data-stu-id="c6438-190">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="c6438-191">此外，配对令牌还设置到每个代理请求的标头 (`MSAspNetCoreToken`)。</span><span class="sxs-lookup"><span data-stu-id="c6438-191">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="c6438-192">IIS 中间件检查它所接收的每个请求，以确认配对令牌标头值与环境变量值相匹配。</span><span class="sxs-lookup"><span data-stu-id="c6438-192">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="c6438-193">如果令牌值不匹配，则将记录请求并拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="c6438-193">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="c6438-194">配对的令牌的环境变量和模块和 Kestrel 之间的通信无法访问从服务器中移出的位置。</span><span class="sxs-lookup"><span data-stu-id="c6438-194">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="c6438-195">如果不知道配对令牌值，攻击者就无法提交绕过 IIS 中间件中的检查的请求。</span><span class="sxs-lookup"><span data-stu-id="c6438-195">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="c6438-196">ASP.NET 核心模块与 IIS 共享配置</span><span class="sxs-lookup"><span data-stu-id="c6438-196">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="c6438-197">ASP.NET 核心模块安装程序使用的特权运行**系统**帐户。</span><span class="sxs-lookup"><span data-stu-id="c6438-197">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="c6438-198">安装程序的本地系统帐户不具有修改权限使用 IIS 共享配置的共享路径，因为达到拒绝访问错误时尝试进行配置中的模块设置*applicationHost.config*共享上。</span><span class="sxs-lookup"><span data-stu-id="c6438-198">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="c6438-199">在将非 IIS 共享配置，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="c6438-199">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="c6438-200">禁用 IIS 共享的配置。</span><span class="sxs-lookup"><span data-stu-id="c6438-200">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="c6438-201">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="c6438-201">Run the installer.</span></span>
1. <span data-ttu-id="c6438-202">导出已更新*applicationHost.config*到共享的文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-202">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="c6438-203">重新启用 IIS 共享的配置。</span><span class="sxs-lookup"><span data-stu-id="c6438-203">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="c6438-204">模块版本和托管捆绑安装程序日志</span><span class="sxs-lookup"><span data-stu-id="c6438-204">Module version and hosting bundle installer logs</span></span>

<span data-ttu-id="c6438-205">若要确定已安装 ASP.NET 核心模块的版本：</span><span class="sxs-lookup"><span data-stu-id="c6438-205">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="c6438-206">在托管系统上，导航到*%windir%\System32\inetsrv*。</span><span class="sxs-lookup"><span data-stu-id="c6438-206">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="c6438-207">找到*aspnetcore.dll*文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-207">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="c6438-208">右键单击该文件并选择**属性**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="c6438-208">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="c6438-209">选择**详细信息**选项卡。**文件版本**和**产品版本**表示已安装的模块版本。</span><span class="sxs-lookup"><span data-stu-id="c6438-209">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="c6438-210">Windows 服务器承载捆绑安装程序日志模块位于*c:\\用户\\%username%\\AppData\\本地\\Temp*。将文件命名为*dd_DotNetCoreWinSvrHosting__\<时间戳 > _000_AspNetCoreModule_x64.log*。</span><span class="sxs-lookup"><span data-stu-id="c6438-210">The Windows Server Hosting bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="c6438-211">模块、 架构和配置文件位置</span><span class="sxs-lookup"><span data-stu-id="c6438-211">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="c6438-212">模块</span><span class="sxs-lookup"><span data-stu-id="c6438-212">Module</span></span>

<span data-ttu-id="c6438-213">**IIS (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="c6438-213">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="c6438-214">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="c6438-214">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="c6438-215">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="c6438-215">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="c6438-216">**IIS Express (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="c6438-216">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="c6438-217">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="c6438-217">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="c6438-218">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="c6438-218">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="c6438-219">架构</span><span class="sxs-lookup"><span data-stu-id="c6438-219">Schema</span></span>

<span data-ttu-id="c6438-220">**IIS**</span><span class="sxs-lookup"><span data-stu-id="c6438-220">**IIS**</span></span>

   * <span data-ttu-id="c6438-221">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="c6438-221">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="c6438-222">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="c6438-222">**IIS Express**</span></span>

   * <span data-ttu-id="c6438-223">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="c6438-223">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="c6438-224">配置</span><span class="sxs-lookup"><span data-stu-id="c6438-224">Configuration</span></span>

<span data-ttu-id="c6438-225">**IIS**</span><span class="sxs-lookup"><span data-stu-id="c6438-225">**IIS**</span></span>

   * <span data-ttu-id="c6438-226">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="c6438-226">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="c6438-227">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="c6438-227">**IIS Express**</span></span>

   * <span data-ttu-id="c6438-228">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="c6438-228">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="c6438-229">可以通过搜索找到文件*aspnetcore.dll*中*applicationHost.config*文件。</span><span class="sxs-lookup"><span data-stu-id="c6438-229">The files can be found by searching for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="c6438-230">IIS express， *applicationHost.config*文件不存在默认情况下。</span><span class="sxs-lookup"><span data-stu-id="c6438-230">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="c6438-231">在创建文件 *\<application_root >\\.vs\\配置*时从任何 web 应用程序项目开始在 Visual Studio 解决方案。</span><span class="sxs-lookup"><span data-stu-id="c6438-231">The file is created at *\<application_root>\\.vs\\config* when starting any web app project in the Visual Studio solution.</span></span>
