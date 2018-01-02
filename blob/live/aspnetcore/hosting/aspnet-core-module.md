---
title: "ASP.NET 核心模块配置参考"
author: guardrex
description: "如何配置适用于托管 ASP.NET Core 应用程序的 ASP.NET 核心模块。"
keywords: "ASP.NET 核心，ancm、 核心模块、 iis、 stdout 日志记录、 环境变量、 env var、 subapplication、 subapp、 appoffline、 app_offline，502，架构"
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: article
ms.assetid: 5de0c8f7-50ce-4e2c-b3d4-a1bd9fdfcff5
ms.technology: aspnet
ms.prod: asp.net-core
uid: hosting/aspnet-core-module
ms.openlocfilehash: 277e63a5663aca622e8252d6c6be1671e57cbf68
ms.sourcegitcommit: 44a62f59d4db39d685c4487a0345a486be18d7c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="159ad-104">ASP.NET 核心模块配置参考</span><span class="sxs-lookup"><span data-stu-id="159ad-104">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="159ad-105">通过[Luke Latham](https://github.com/guardrex)， [Rick Anderson](https://twitter.com/RickAndMSFT)，和[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="159ad-105">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="159ad-106">本文档提供有关如何配置 ASP.NET 核心模块用于托管 ASP.NET Core 应用程序的详细信息。</span><span class="sxs-lookup"><span data-stu-id="159ad-106">This document provides details on how to configure the ASP.NET Core Module for hosting ASP.NET Core applications.</span></span> <span data-ttu-id="159ad-107">有关 ASP.NET 核心模块和安装说明简介，请参阅[ASP.NET 核心模块概述](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="159ad-107">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

## <a name="configuration-via-webconfig"></a><span data-ttu-id="159ad-108">通过 web.config 配置</span><span class="sxs-lookup"><span data-stu-id="159ad-108">Configuration via web.config</span></span>

<span data-ttu-id="159ad-109">通过站点或应用程序配置 ASP.NET 核心模块*web.config*文件，并都具有其自己`aspNetCore`内的配置部分`system.webServer`。</span><span class="sxs-lookup"><span data-stu-id="159ad-109">The ASP.NET Core Module is configured via a site or application *web.config* file and has its own `aspNetCore` configuration section within `system.webServer`.</span></span> <span data-ttu-id="159ad-110">下面是一个示例*web.config*文件`Microsoft.NET.Sdk.Web`SDK 将提供的发布项目时[framework 相关部署](https://docs.microsoft.com/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)带有占位符`processPath`和`arguments`:</span><span class="sxs-lookup"><span data-stu-id="159ad-110">Here's an example *web.config* file that the `Microsoft.NET.Sdk.Web` SDK will provide when the project is published for a [framework-dependent deployment](https://docs.microsoft.com/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) with placeholders for the `processPath` and `arguments`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="%LAUNCHER_PATH%" 
        arguments="%LAUNCHER_ARGS%" 
        stdoutLogEnabled="false" 
        stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="159ad-111">*Web.config*下面的示例适用于[独立的部署](https://docs.microsoft.com/dotnet/articles/core/deploying/#self-contained-deployments-scd)到[Azure App Service](https://azure.microsoft.com/services/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="159ad-111">The *web.config* example below is for a [self-contained deployment](https://docs.microsoft.com/dotnet/articles/core/deploying/#self-contained-deployments-scd) to the [Azure App Service](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="159ad-112">有关详细信息，请参阅[发布到 IIS](xref:publishing/iis)。</span><span class="sxs-lookup"><span data-stu-id="159ad-112">For more information, see [Publishing to IIS](xref:publishing/iis).</span></span> <span data-ttu-id="159ad-113">请参阅[的子应用程序配置](xref:publishing/iis#configuration-of-sub-applications)的与配置相关的重要说明*web.config*子应用程序中的文件。</span><span class="sxs-lookup"><span data-stu-id="159ad-113">See [Configuration of sub-applications](xref:publishing/iis#configuration-of-sub-applications) for an important note pertaining to the configuration of *web.config* files in sub-applications.</span></span>

```xml
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
        stdoutLogEnabled="false" 
        stdoutLogFile="\\?\%home%\LogFiles\stdout" />
  </system.webServer>
</configuration>
```

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="159ad-114">AspNetCore 元素的特性</span><span class="sxs-lookup"><span data-stu-id="159ad-114">Attributes of the aspNetCore element</span></span>

| <span data-ttu-id="159ad-115">特性</span><span class="sxs-lookup"><span data-stu-id="159ad-115">Attribute</span></span> | <span data-ttu-id="159ad-116">描述</span><span class="sxs-lookup"><span data-stu-id="159ad-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="159ad-117">processPath</span><span class="sxs-lookup"><span data-stu-id="159ad-117">processPath</span></span> | <p><span data-ttu-id="159ad-118">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-118">Required string attribute.</span></span></p><p><span data-ttu-id="159ad-119">将启动侦听 HTTP 请求的进程的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="159ad-119">Path to the executable that will launch a process listening for HTTP requests.</span></span> <span data-ttu-id="159ad-120">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="159ad-120">Relative paths are supported.</span></span> <span data-ttu-id="159ad-121">如果路径以。，考虑使用该路径是相对站点根。</span><span class="sxs-lookup"><span data-stu-id="159ad-121">If the path begins with '.', the path is considered to be relative to the site root.</span></span></p><p><span data-ttu-id="159ad-122">没有默认值。</span><span class="sxs-lookup"><span data-stu-id="159ad-122">There is no default value.</span></span></p> |
| <span data-ttu-id="159ad-123">自变量</span><span class="sxs-lookup"><span data-stu-id="159ad-123">arguments</span></span> | <p><span data-ttu-id="159ad-124">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-124">Optional string attribute.</span></span></p><p><span data-ttu-id="159ad-125">可执行文件中指定的自变量**processPath**。</span><span class="sxs-lookup"><span data-stu-id="159ad-125">Arguments to the executable specified in **processPath**.</span></span></p><p><span data-ttu-id="159ad-126">默认值为一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="159ad-126">The default value is an empty string.</span></span></p> |
| <span data-ttu-id="159ad-127">startupTimeLimit</span><span class="sxs-lookup"><span data-stu-id="159ad-127">startupTimeLimit</span></span> | <p><span data-ttu-id="159ad-128">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-128">Optional integer attribute.</span></span></p><p><span data-ttu-id="159ad-129">以秒为单位，模块将等待启动侦听端口的进程的可执行文件的持续时间。</span><span class="sxs-lookup"><span data-stu-id="159ad-129">Duration in seconds that the module will wait for the executable to start a process listening on the port.</span></span> <span data-ttu-id="159ad-130">如果超过此时间限制，该模块将终止的进程。</span><span class="sxs-lookup"><span data-stu-id="159ad-130">If this time limit is exceeded, the module will kill the process.</span></span> <span data-ttu-id="159ad-131">该模块将尝试重新启动该过程，在它接收新请求，并将继续尝试重新启动在后续的传入请求的过程，除非应用程序启动失败时**rapidFailsPerMinute**数最后一个滚动分钟内的时间。</span><span class="sxs-lookup"><span data-stu-id="159ad-131">The module will attempt to launch the process again when it receives a new request and will continue to attempt to restart the process on subsequent incoming requests unless the application fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="159ad-132">默认值为 120。</span><span class="sxs-lookup"><span data-stu-id="159ad-132">The default value is 120.</span></span></p> |
| <span data-ttu-id="159ad-133">shutdownTimeLimit</span><span class="sxs-lookup"><span data-stu-id="159ad-133">shutdownTimeLimit</span></span> | <p><span data-ttu-id="159ad-134">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-134">Optional integer attribute.</span></span></p><p><span data-ttu-id="159ad-135">以秒为单位为其模块将等待正常关闭的可执行文件的持续时间时*app_offline.htm*检测到文件。</span><span class="sxs-lookup"><span data-stu-id="159ad-135">Duration in seconds for which the module will wait for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p><p><span data-ttu-id="159ad-136">默认值为 10。</span><span class="sxs-lookup"><span data-stu-id="159ad-136">The default value is 10.</span></span></p> |
| <span data-ttu-id="159ad-137">rapidFailsPerMinute</span><span class="sxs-lookup"><span data-stu-id="159ad-137">rapidFailsPerMinute</span></span> | <p><span data-ttu-id="159ad-138">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-138">Optional integer attribute.</span></span></p><p><span data-ttu-id="159ad-139">指定在指定的进程的次数**processPath**允许每分钟崩溃。</span><span class="sxs-lookup"><span data-stu-id="159ad-139">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="159ad-140">如果超出此限制，该模块将停止启动剩余秒数的进程。</span><span class="sxs-lookup"><span data-stu-id="159ad-140">If this limit is exceeded, the module will stop launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="159ad-141">默认值为 10。</span><span class="sxs-lookup"><span data-stu-id="159ad-141">The default value is 10.</span></span></p> |
| <span data-ttu-id="159ad-142">requestTimeout</span><span class="sxs-lookup"><span data-stu-id="159ad-142">requestTimeout</span></span> | <p><span data-ttu-id="159ad-143">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-143">Optional timespan attribute.</span></span></p><p><span data-ttu-id="159ad-144">指定 ASP.NET 核心模块将等待侦听 %aspnetcore_port%的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="159ad-144">Specifies the duration for which the ASP.NET Core Module will wait for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="159ad-145">默认值为“00:02:00”。</span><span class="sxs-lookup"><span data-stu-id="159ad-145">The default value is "00:02:00".</span></span></p><p><span data-ttu-id="159ad-146">`requestTimeout`必须指定整分钟数，否则它将默认为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="159ad-146">The `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> |
| <span data-ttu-id="159ad-147">stdoutLogEnabled</span><span class="sxs-lookup"><span data-stu-id="159ad-147">stdoutLogEnabled</span></span> | <p><span data-ttu-id="159ad-148">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-148">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="159ad-149">如果为 true， **stdout**和**stderr**中指定的进程的**processPath**将重定向到中指定的文件**stdoutLogFile**.</span><span class="sxs-lookup"><span data-stu-id="159ad-149">If true, **stdout** and **stderr** for the process specified in **processPath** will be redirected to the file specified in **stdoutLogFile**.</span></span></p><p><span data-ttu-id="159ad-150">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="159ad-150">The default value is false.</span></span></p> |
| <span data-ttu-id="159ad-151">stdoutLogFile</span><span class="sxs-lookup"><span data-stu-id="159ad-151">stdoutLogFile</span></span> | <p><span data-ttu-id="159ad-152">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-152">Optional string attribute.</span></span></p><p><span data-ttu-id="159ad-153">为其指定的相对或绝对文件路径**stdout**和**stderr**中指定的进程从**processPath**将记录。</span><span class="sxs-lookup"><span data-stu-id="159ad-153">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span> <span data-ttu-id="159ad-154">相对路径是相对于站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="159ad-154">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="159ad-155">从任何路径。 将相对站点根和所有其他路径将被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="159ad-155">Any path starting with '.' will be relative to the site root and all other paths will be treated as absolute paths.</span></span> <span data-ttu-id="159ad-156">路径中提供的任何文件夹必须存在于要创建的日志文件的模块的顺序。</span><span class="sxs-lookup"><span data-stu-id="159ad-156">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="159ad-157">进程 ID，时间戳 (*yyyyMdhms*)，和文件扩展名 (*.log*) 以下划线分隔符将添加到最后一个段**stdoutLogFile**提供。</span><span class="sxs-lookup"><span data-stu-id="159ad-157">The process ID, timestamp (*yyyyMdhms*), and file extension (*.log*) with underscore delimiters are added to the last segment of the **stdoutLogFile** provided.</span></span></p><p><span data-ttu-id="159ad-158">默认值为 `aspnetcore-stdout`。</span><span class="sxs-lookup"><span data-stu-id="159ad-158">The default value is `aspnetcore-stdout`.</span></span></p> |
| <span data-ttu-id="159ad-159">forwardWindowsAuthToken</span><span class="sxs-lookup"><span data-stu-id="159ad-159">forwardWindowsAuthToken</span></span> | <span data-ttu-id="159ad-160">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="159ad-160">true or false.</span></span></p><p><span data-ttu-id="159ad-161">如果为 true，则令牌将转发到侦听作为每个请求的标头 MS ASPNETCORE WINAUTHTOKEN 的 %aspnetcore_port%的子进程。</span><span class="sxs-lookup"><span data-stu-id="159ad-161">If true, the token will be forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="159ad-162">它是该进程可以在每个请求此令牌上调用 CloseHandle 责任。</span><span class="sxs-lookup"><span data-stu-id="159ad-162">It is the responsibility of that process to call CloseHandle on this token per request.</span></span></p><p><span data-ttu-id="159ad-163">默认值为 true。</span><span class="sxs-lookup"><span data-stu-id="159ad-163">The default value is true.</span></span></p> |
| <span data-ttu-id="159ad-164">disableStartUpErrorPage</span><span class="sxs-lookup"><span data-stu-id="159ad-164">disableStartUpErrorPage</span></span> | <span data-ttu-id="159ad-165">“真”或“假”。</span><span class="sxs-lookup"><span data-stu-id="159ad-165">true or false.</span></span></p><p><span data-ttu-id="159ad-166">如果为 true， **502.5-进程失败**页将禁止显示，并且 502 状态代码页中配置你*web.config*将优先。</span><span class="sxs-lookup"><span data-stu-id="159ad-166">If true, the **502.5 - Process Failure** page will be suppressed, and the 502 status code page configured in your *web.config* will take precedence.</span></span></p><p><span data-ttu-id="159ad-167">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="159ad-167">The default value is false.</span></span></p> |

### <a name="setting-environment-variables"></a><span data-ttu-id="159ad-168">设置环境变量</span><span class="sxs-lookup"><span data-stu-id="159ad-168">Setting environment variables</span></span>

<span data-ttu-id="159ad-169">ASP.NET 核心模块允许你指定中指定的进程的环境变量`processPath`通过一个或多中指定它们的属性`environmentVariable`的子元素`environmentVariables`集合元素下的`aspNetCore`元素。</span><span class="sxs-lookup"><span data-stu-id="159ad-169">The ASP.NET Core Module allows you specify environment variables for the process specified in the `processPath` attribute by specifying them in one or more `environmentVariable` child elements of an `environmentVariables` collection element under the `aspNetCore` element.</span></span> <span data-ttu-id="159ad-170">在本部分中设置的环境变量优先于系统进程的环境变量。</span><span class="sxs-lookup"><span data-stu-id="159ad-170">Environment variables set in this section take precedence over system environment variables for the process.</span></span>

<span data-ttu-id="159ad-171">下面的示例设置两个环境变量。</span><span class="sxs-lookup"><span data-stu-id="159ad-171">The example below sets two environment variables.</span></span> <span data-ttu-id="159ad-172">`ASPNETCORE_ENVIRONMENT`将配置应用程序的环境`Development`。</span><span class="sxs-lookup"><span data-stu-id="159ad-172">`ASPNETCORE_ENVIRONMENT` will configure the application's environment to `Development`.</span></span> <span data-ttu-id="159ad-173">开发人员可能将此值暂时设置*web.config*文件以便强制[开发人员异常页](xref:fundamentals/error-handling)以便在调试应用程序异常时加载。</span><span class="sxs-lookup"><span data-stu-id="159ad-173">A developer may temporarily set this value in the *web.config* file in order to force the [developer exception page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="159ad-174">`CONFIG_DIR`是一种用户定义的环境变量中，开发人员曾将读取在启动时，才能加载应用程序的配置文件组合成路径的值的代码。</span><span class="sxs-lookup"><span data-stu-id="159ad-174">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that will read the value on startup to form a path in order to load the app's configuration file.</span></span>

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

## <a name="appofflinehtm"></a><span data-ttu-id="159ad-175">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="159ad-175">app_offline.htm</span></span>

<span data-ttu-id="159ad-176">如果名称的文件放*app_offline.htm* ASP.NET 核心模块将在 web 应用程序目录的根目录，尝试正常关闭应用程序并停止处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="159ad-176">If you place a file with the name *app_offline.htm* at the root of a web application directory, the ASP.NET Core Module will attempt to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="159ad-177">如果应用程序仍在运行`shutdownTimeLimit`数 ASP.NET 核心模块将为秒，终止正在运行的进程。</span><span class="sxs-lookup"><span data-stu-id="159ad-177">If the app is still running after `shutdownTimeLimit` number of seconds, the ASP.NET Core Module will kill the running process.</span></span>

<span data-ttu-id="159ad-178">虽然*app_offline.htm*文件不存在，如果通过发回的内容，ASP.NET 核心模块将将响应的请求*app_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="159ad-178">While the *app_offline.htm* file is present, the ASP.NET Core Module will respond to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="159ad-179">一次*app_offline.htm*删除文件下, 一个请求加载应用程序，然后将响应请求。</span><span class="sxs-lookup"><span data-stu-id="159ad-179">Once the *app_offline.htm* file is removed, the next request loads the application, which then responds to requests.</span></span>

## <a name="start-up-error-page"></a><span data-ttu-id="159ad-180">启动错误页</span><span class="sxs-lookup"><span data-stu-id="159ad-180">Start-up error page</span></span>

<span data-ttu-id="159ad-181">如果 ASP.NET 核心模块无法启动后端进程或后端进程启动但不能在配置的端口上侦听时，你将看到了 HTTP 502.5 状态的代码页。</span><span class="sxs-lookup"><span data-stu-id="159ad-181">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, you will see an HTTP 502.5 status code page.</span></span> <span data-ttu-id="159ad-182">若要禁止显示此页并还原为默认 IIS 502 状态代码页，请使用`disableStartUpErrorPage`属性。</span><span class="sxs-lookup"><span data-stu-id="159ad-182">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="159ad-183">有关配置自定义错误消息的详细信息，请参阅[HTTP 错误`<httpErrors>` ](https://docs.microsoft.com/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="159ad-183">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](https://docs.microsoft.com/iis/configuration/system.webServer/httpErrors/).</span></span>

![502 状态页](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="159ad-185">日志创建和重定向</span><span class="sxs-lookup"><span data-stu-id="159ad-185">Log creation and redirection</span></span>

<span data-ttu-id="159ad-186">ASP.NET 核心模块将重定向`stdout`和`stderr`日志磁盘如果你设置`stdoutLogEnabled`和`stdoutLogFile`属性`aspNetCore`元素。</span><span class="sxs-lookup"><span data-stu-id="159ad-186">The ASP.NET Core Module redirects `stdout` and `stderr` logs to disk if you set the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element.</span></span> <span data-ttu-id="159ad-187">中的任何文件夹`stdoutLogFile`路径必须存在于要创建的日志文件的模块的顺序。</span><span class="sxs-lookup"><span data-stu-id="159ad-187">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="159ad-188">创建日志文件时，将自动添加时间戳和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="159ad-188">A timestamp and file extension will be added automatically when the log file is created.</span></span> <span data-ttu-id="159ad-189">不旋转日志，除非进程回收/重新启动时发生。</span><span class="sxs-lookup"><span data-stu-id="159ad-189">Logs are not rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="159ad-190">它负责的托管商来限制日志使用的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="159ad-190">It is the responsibility of the hoster to limit the disk space the logs consume.</span></span> <span data-ttu-id="159ad-191">使用`stdout`日志仅建议用于故障排除应用程序启动问题并不用于常规应用程序日志记录。</span><span class="sxs-lookup"><span data-stu-id="159ad-191">Using the `stdout` log is only recommended for troubleshooting application startup issues and not for general application logging purposes.</span></span>

<span data-ttu-id="159ad-192">日志文件名称由追加的进程 ID (PID)，时间戳 (*yyyyMdhms*)，和文件扩展名 (*.log*) 到的最后一段`stdoutLogFile`路径 (通常*stdout*) 由下划线分隔。</span><span class="sxs-lookup"><span data-stu-id="159ad-192">The log file name is composed by appending the process ID (PID), timestamp (*yyyyMdhms*), and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="159ad-193">例如如果`stdoutLogFile`路径以结束*stdout*，pid 为 10652 在 12:05:02 8/10/2017年上创建的应用程序日志中的文件名称*stdout_10652_20178101252.log*。</span><span class="sxs-lookup"><span data-stu-id="159ad-193">For example if the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 10652 created on 8/10/2017 at 12:05:02 has the file name *stdout_10652_20178101252.log*.</span></span>

<span data-ttu-id="159ad-194">下面是一个示例`aspNetCore`配置元素`stdout`日志记录。</span><span class="sxs-lookup"><span data-stu-id="159ad-194">Here's a sample `aspNetCore` element that configures `stdout` logging.</span></span> <span data-ttu-id="159ad-195">`stdoutLogFile`示例所示的路径是否适用于 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="159ad-195">The `stdoutLogFile` path shown in the example is appropriate for the Azure App Service.</span></span> <span data-ttu-id="159ad-196">本地路径或网络共享路径是可接受的本地日志记录。</span><span class="sxs-lookup"><span data-stu-id="159ad-196">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="159ad-197">确认应用程序池用户标识有权写入提供的路径。</span><span class="sxs-lookup"><span data-stu-id="159ad-197">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```
<span data-ttu-id="159ad-198">请参阅[通过 web.config 配置](#configuration-via-webconfig)有关的示例`aspNetCore`中的元素*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="159ad-198">See [Configuration via web.config](#configuration-via-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="159ad-199">ASP.NET 核心模块与 IIS 共享配置</span><span class="sxs-lookup"><span data-stu-id="159ad-199">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="159ad-200">ASP.NET 核心模块安装程序使用的特权运行**系统**帐户。</span><span class="sxs-lookup"><span data-stu-id="159ad-200">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="159ad-201">本地系统帐户不具有修改权限由 IIS 共享配置的共享路径，因为安装程序将命中拒绝访问错误时尝试进行配置中的模块设置*applicationHost.config*共享上。</span><span class="sxs-lookup"><span data-stu-id="159ad-201">Because the local system account does not have modify permission for the share path which is used by the IIS Shared Configuration, the installer will hit an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span>

<span data-ttu-id="159ad-202">不受支持的解决方法是禁用 IIS 共享配置、 运行安装程序、 导出更新*applicationHost.config*文件到共享，并重新启用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="159ad-202">The unsupported workaround is to disable the IIS Shared Configuration, run the installer, export the updated *applicationHost.config* file to the share, and re-enable the IIS Shared Configuration.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="159ad-203">模块、 架构和配置文件位置</span><span class="sxs-lookup"><span data-stu-id="159ad-203">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="159ad-204">模块</span><span class="sxs-lookup"><span data-stu-id="159ad-204">Module</span></span>

<span data-ttu-id="159ad-205">**IIS (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="159ad-205">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="159ad-206">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="159ad-206">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="159ad-207">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="159ad-207">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="159ad-208">**IIS Express (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="159ad-208">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="159ad-209">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="159ad-209">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="159ad-210">%Programfiles (x86) %\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="159ad-210">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="159ad-211">架构</span><span class="sxs-lookup"><span data-stu-id="159ad-211">Schema</span></span>

<span data-ttu-id="159ad-212">**IIS**</span><span class="sxs-lookup"><span data-stu-id="159ad-212">**IIS**</span></span>

   * <span data-ttu-id="159ad-213">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="159ad-213">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="159ad-214">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="159ad-214">**IIS Express**</span></span>

   * <span data-ttu-id="159ad-215">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="159ad-215">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="159ad-216">配置</span><span class="sxs-lookup"><span data-stu-id="159ad-216">Configuration</span></span>

<span data-ttu-id="159ad-217">**IIS**</span><span class="sxs-lookup"><span data-stu-id="159ad-217">**IIS**</span></span>

   * <span data-ttu-id="159ad-218">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="159ad-218">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="159ad-219">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="159ad-219">**IIS Express**</span></span>

   * <span data-ttu-id="159ad-220">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="159ad-220">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="159ad-221">你可以搜索*aspnetcore.dll*中*applicationHost.config*文件。</span><span class="sxs-lookup"><span data-stu-id="159ad-221">You can search for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="159ad-222">IIS express， *applicationHost.config*文件不存在默认情况下。</span><span class="sxs-lookup"><span data-stu-id="159ad-222">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="159ad-223">在创建文件*{应用程序根目录}\.vs\config*时启动 Visual Studio 解决方案中的任何 web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="159ad-223">The file is created at *{application root}\.vs\config* when you start any web application project in the Visual Studio solution.</span></span>
