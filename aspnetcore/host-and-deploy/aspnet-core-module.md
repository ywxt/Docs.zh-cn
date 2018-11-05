---
title: ASP.NET Core 模块配置参考
author: guardrex
description: 了解如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 09/21/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 0d167f779f9dcae6b0d946dce5e341793daf43bf
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50091010"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="baa15-103">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="baa15-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="baa15-104">作者：[Luke Latham](https://github.com/guardrex)、[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="baa15-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="baa15-105">本文档说明了如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="baa15-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="baa15-106">有关 ASP.NET Core 模块简介和安装说明，请参阅 [ASP.NET Core 模块概述](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="baa15-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a><span data-ttu-id="baa15-107">托管模型</span><span class="sxs-lookup"><span data-stu-id="baa15-107">Hosting model</span></span>

<span data-ttu-id="baa15-108">对于在 .NET Core 2.2 或更高版本上运行的应用，该模块支持进程内托管模型以便提高性能（与反向代理(进程外)托管相比）。</span><span class="sxs-lookup"><span data-stu-id="baa15-108">For apps running on .NET Core 2.2 or later, the module supports an in-process hosting model for improved performance compared to reverse-proxy (out-of-process) hosting.</span></span> <span data-ttu-id="baa15-109">有关更多信息，请参见<xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>。</span><span class="sxs-lookup"><span data-stu-id="baa15-109">For more information, see <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>.</span></span>

<span data-ttu-id="baa15-110">进程内托管选择使用现有应用，但 [dotnet new](/dotnet/core/tools/dotnet-new) 模板默认使用所有 IIS 和 IIS Express 方案的进程内托管模型。</span><span class="sxs-lookup"><span data-stu-id="baa15-110">In-procsess hosting is opt-in for existing apps, but [dotnet new](/dotnet/core/tools/dotnet-new) templates default to the in-process hosting model for all IIS and IIS Express scenarios.</span></span>

<span data-ttu-id="baa15-111">若要配置用于进程内托管的应用，请将 `<AspNetCoreModuleHostingModel>` 属性添加到值为 `inprocess`（进程外托管使用 `outofprocess` 进行设置）的应用项目文件：</span><span class="sxs-lookup"><span data-stu-id="baa15-111">To configure an app for in-process hosting, add the `<AspNetCoreModuleHostingModel>` property to the app's project file with a value of `inprocess` (out-of-process hosting is set with `outofprocess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreModuleHostingModel>inprocess</AspNetCoreModuleHostingModel>
</PropertyGroup>
```

<span data-ttu-id="baa15-112">在进程内托管时，将应用以下特征：</span><span class="sxs-lookup"><span data-stu-id="baa15-112">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="baa15-113">不会使用 [Kestrel 服务器](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="baa15-113">The [Kestrel server](xref:fundamentals/servers/kestrel) isn't used.</span></span> <span data-ttu-id="baa15-114">自定义 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 实现 `IISHttpServer` 充当应用的服务器。</span><span class="sxs-lookup"><span data-stu-id="baa15-114">A custom <xref:Microsoft.AspNetCore.Hosting.Server.IServer> implementation, `IISHttpServer` acts as the app's server.</span></span>

* <span data-ttu-id="baa15-115">[requestTimeout 属性](#attributes-of-the-aspnetcore-element)不适用于进程内托管。</span><span class="sxs-lookup"><span data-stu-id="baa15-115">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="baa15-116">不支持在应用之间共享应用池。</span><span class="sxs-lookup"><span data-stu-id="baa15-116">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="baa15-117">每个应用使用一个应用池。</span><span class="sxs-lookup"><span data-stu-id="baa15-117">Use one app pool per app.</span></span>

* <span data-ttu-id="baa15-118">使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)或手动将 [app_offline.htm 文件置于部署中](xref:host-and-deploy/iis/index#locked-deployment-files)时，如果有已打开的连接，则应用可能不会立即关闭。</span><span class="sxs-lookup"><span data-stu-id="baa15-118">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="baa15-119">例如，WebSocket 连接可能会延迟应用关闭。</span><span class="sxs-lookup"><span data-stu-id="baa15-119">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="baa15-120">应用和已安装的运行时（x64 或 x86）的体系结构（位数）必须与应用池的体系结构匹配。</span><span class="sxs-lookup"><span data-stu-id="baa15-120">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="baa15-121">如果使用 `WebHostBuilder`（而不是使用 [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)）手动设置应用的主机，并且应用曾经直接在 Kestrel 服务器上运行（自托管），则先调用 `UseKestrel`，再调用 `UseIISIntegration`。</span><span class="sxs-lookup"><span data-stu-id="baa15-121">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="baa15-122">如果顺序颠倒，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="baa15-122">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="baa15-123">检测到客户端连接断开。</span><span class="sxs-lookup"><span data-stu-id="baa15-123">Client disconnects are detected.</span></span> <span data-ttu-id="baa15-124">客户端连接断开时，[HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 取消标记将会取消。</span><span class="sxs-lookup"><span data-stu-id="baa15-124">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="baa15-125">托管模型更改</span><span class="sxs-lookup"><span data-stu-id="baa15-125">Hosting model changes</span></span>

<span data-ttu-id="baa15-126">如果 `hostingModel` 设置在 web.config 文件中被更改（如 [web.config 的配置](#configuration-with-webconfig)部分中所述），则该模块会再循环 IIS 工作进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-126">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="baa15-127">对于 IIS Express，该模块不会再循环工作进程，但改为触发当前 IIS Express 进程的正常关闭。</span><span class="sxs-lookup"><span data-stu-id="baa15-127">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="baa15-128">应用的下一个请求会生成新的 IIS Express 进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-128">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="baa15-129">进程名</span><span class="sxs-lookup"><span data-stu-id="baa15-129">Process name</span></span>

<span data-ttu-id="baa15-130">`Process.GetCurrentProcess().ProcessName` 报告 `w3wp`（进程内）或 `dotnet`（进程外）。</span><span class="sxs-lookup"><span data-stu-id="baa15-130">`Process.GetCurrentProcess().ProcessName` reports either `w3wp` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

## <a name="configuration-with-webconfig"></a><span data-ttu-id="baa15-131">web.config 的配置</span><span class="sxs-lookup"><span data-stu-id="baa15-131">Configuration with web.config</span></span>

<span data-ttu-id="baa15-132">在站点的 *web.config* 文件中使用 `system.webServer` 节点的 `aspNetCore` 部分配置 ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="baa15-132">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="baa15-133">以下 *web.config* 文件发布用于[依赖框架的部署](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)，并配置 ASP.NET Core 模块以处理站点请求：</span><span class="sxs-lookup"><span data-stu-id="baa15-133">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" 
                arguments=".\MyApp.dll" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" 
                hostingModel="inprocess" />
  </system.webServer>
</configuration>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

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

::: moniker-end

<span data-ttu-id="baa15-134">以下 web.config 发布用于[独立部署](/dotnet/articles/core/deploying/#self-contained-deployments-scd)：</span><span class="sxs-lookup"><span data-stu-id="baa15-134">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" 
                hostingModel="inprocess" />
  </system.webServer>
</configuration>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

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

::: moniker-end

<span data-ttu-id="baa15-135">将应用部署为 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)时，`stdoutLogFile` 路径将设置为 `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="baa15-135">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="baa15-136">该路径会将 stdout 日志保存到 *LogFiles* 文件夹，该文件夹是由服务自动创建的位置。</span><span class="sxs-lookup"><span data-stu-id="baa15-136">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="baa15-137">有关在子应用中配置 *web.config* 文件的重要说明，请参阅[子应用程序配置](xref:host-and-deploy/iis/index#sub-application-configuration)。</span><span class="sxs-lookup"><span data-stu-id="baa15-137">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="baa15-138">aspNetCore 元素的属性</span><span class="sxs-lookup"><span data-stu-id="baa15-138">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="baa15-139">特性</span><span class="sxs-lookup"><span data-stu-id="baa15-139">Attribute</span></span> | <span data-ttu-id="baa15-140">描述</span><span class="sxs-lookup"><span data-stu-id="baa15-140">Description</span></span> | <span data-ttu-id="baa15-141">默认</span><span class="sxs-lookup"><span data-stu-id="baa15-141">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="baa15-142">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-142">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-143">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="baa15-143">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="baa15-144">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-144">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-145">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="baa15-145">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="baa15-146">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-146">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-147">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-147">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="baa15-148">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="baa15-148">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="baa15-149">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-149">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-150">将托管模型指定为进程内 (`inprocess`) 或进程外 (`outofprocess`)。</span><span class="sxs-lookup"><span data-stu-id="baa15-150">Specifies the hosting model as in-process (`inprocess`) or out-of-process (`outofprocess`).</span></span></p> | `outofprocess` |
| `processesPerApplication` | <p><span data-ttu-id="baa15-151">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-151">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-152">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="baa15-152">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="baa15-153">&dagger;对于进程内托管，值限制为 `1`。</span><span class="sxs-lookup"><span data-stu-id="baa15-153">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="baa15-154">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-154">Default: `1`</span></span><br><span data-ttu-id="baa15-155">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-155">Min: `1`</span></span><br><span data-ttu-id="baa15-156">最大值：`100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="baa15-156">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="baa15-157">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-157">Required string attribute.</span></span></p><p><span data-ttu-id="baa15-158">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-158">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="baa15-159">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-159">Relative paths are supported.</span></span> <span data-ttu-id="baa15-160">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-160">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="baa15-161">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-161">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-162">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="baa15-162">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="baa15-163">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-163">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="baa15-164">不支持进程内托管。</span><span class="sxs-lookup"><span data-stu-id="baa15-164">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="baa15-165">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-165">Default: `10`</span></span><br><span data-ttu-id="baa15-166">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-166">Min: `0`</span></span><br><span data-ttu-id="baa15-167">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="baa15-167">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="baa15-168">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-168">Optional timespan attribute.</span></span></p><p><span data-ttu-id="baa15-169">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="baa15-169">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="baa15-170">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</span><span class="sxs-lookup"><span data-stu-id="baa15-170">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="baa15-171">不适用于进程内托管。</span><span class="sxs-lookup"><span data-stu-id="baa15-171">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="baa15-172">对于进程内托管，该模块等待应用处理该请求。</span><span class="sxs-lookup"><span data-stu-id="baa15-172">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="baa15-173">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-173">Default: `00:02:00`</span></span><br><span data-ttu-id="baa15-174">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-174">Min: `00:00:00`</span></span><br><span data-ttu-id="baa15-175">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-175">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="baa15-176">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-176">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-177">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-177">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="baa15-178">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-178">Default: `10`</span></span><br><span data-ttu-id="baa15-179">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-179">Min: `0`</span></span><br><span data-ttu-id="baa15-180">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="baa15-180">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="baa15-181">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-181">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-182">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-182">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="baa15-183">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-183">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="baa15-184">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="baa15-184">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="baa15-185">值 0（零）不被视为无限超时。</span><span class="sxs-lookup"><span data-stu-id="baa15-185">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="baa15-186">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="baa15-186">Default: `120`</span></span><br><span data-ttu-id="baa15-187">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-187">Min: `0`</span></span><br><span data-ttu-id="baa15-188">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="baa15-188">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="baa15-189">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-189">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-190">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-190">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="baa15-191">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-191">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-192">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-192">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="baa15-193">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-193">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="baa15-194">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-194">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="baa15-195">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-195">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="baa15-196">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="baa15-196">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="baa15-197">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="baa15-197">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="baa15-198">特性</span><span class="sxs-lookup"><span data-stu-id="baa15-198">Attribute</span></span> | <span data-ttu-id="baa15-199">描述</span><span class="sxs-lookup"><span data-stu-id="baa15-199">Description</span></span> | <span data-ttu-id="baa15-200">默认</span><span class="sxs-lookup"><span data-stu-id="baa15-200">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="baa15-201">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-201">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-202">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="baa15-202">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="baa15-203">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-203">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-204">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="baa15-204">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="baa15-205">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-205">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-206">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-206">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="baa15-207">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="baa15-207">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="baa15-208">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-208">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-209">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="baa15-209">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="baa15-210">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-210">Default: `1`</span></span><br><span data-ttu-id="baa15-211">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-211">Min: `1`</span></span><br><span data-ttu-id="baa15-212">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="baa15-212">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="baa15-213">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-213">Required string attribute.</span></span></p><p><span data-ttu-id="baa15-214">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-214">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="baa15-215">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-215">Relative paths are supported.</span></span> <span data-ttu-id="baa15-216">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-216">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="baa15-217">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-217">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-218">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="baa15-218">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="baa15-219">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-219">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="baa15-220">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-220">Default: `10`</span></span><br><span data-ttu-id="baa15-221">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-221">Min: `0`</span></span><br><span data-ttu-id="baa15-222">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="baa15-222">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="baa15-223">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-223">Optional timespan attribute.</span></span></p><p><span data-ttu-id="baa15-224">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="baa15-224">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="baa15-225">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</span><span class="sxs-lookup"><span data-stu-id="baa15-225">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="baa15-226">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-226">Default: `00:02:00`</span></span><br><span data-ttu-id="baa15-227">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-227">Min: `00:00:00`</span></span><br><span data-ttu-id="baa15-228">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-228">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="baa15-229">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-229">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-230">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-230">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="baa15-231">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-231">Default: `10`</span></span><br><span data-ttu-id="baa15-232">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-232">Min: `0`</span></span><br><span data-ttu-id="baa15-233">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="baa15-233">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="baa15-234">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-234">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-235">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-235">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="baa15-236">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-236">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="baa15-237">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="baa15-237">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="baa15-238">值 0（零）不被视为无限超时。</span><span class="sxs-lookup"><span data-stu-id="baa15-238">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="baa15-239">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="baa15-239">Default: `120`</span></span><br><span data-ttu-id="baa15-240">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-240">Min: `0`</span></span><br><span data-ttu-id="baa15-241">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="baa15-241">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="baa15-242">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-242">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-243">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-243">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="baa15-244">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-244">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-245">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-245">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="baa15-246">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-246">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="baa15-247">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-247">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="baa15-248">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-248">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="baa15-249">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="baa15-249">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="baa15-250">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="baa15-250">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="baa15-251">特性</span><span class="sxs-lookup"><span data-stu-id="baa15-251">Attribute</span></span> | <span data-ttu-id="baa15-252">描述</span><span class="sxs-lookup"><span data-stu-id="baa15-252">Description</span></span> | <span data-ttu-id="baa15-253">默认</span><span class="sxs-lookup"><span data-stu-id="baa15-253">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="baa15-254">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-254">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-255">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="baa15-255">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="baa15-256">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-256">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-257">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="baa15-257">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="baa15-258">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-258">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-259">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-259">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="baa15-260">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="baa15-260">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="baa15-261">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-261">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-262">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="baa15-262">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="baa15-263">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-263">Default: `1`</span></span><br><span data-ttu-id="baa15-264">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="baa15-264">Min: `1`</span></span><br><span data-ttu-id="baa15-265">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="baa15-265">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="baa15-266">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-266">Required string attribute.</span></span></p><p><span data-ttu-id="baa15-267">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-267">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="baa15-268">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-268">Relative paths are supported.</span></span> <span data-ttu-id="baa15-269">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-269">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="baa15-270">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-270">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-271">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="baa15-271">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="baa15-272">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-272">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="baa15-273">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-273">Default: `10`</span></span><br><span data-ttu-id="baa15-274">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-274">Min: `0`</span></span><br><span data-ttu-id="baa15-275">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="baa15-275">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="baa15-276">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-276">Optional timespan attribute.</span></span></p><p><span data-ttu-id="baa15-277">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="baa15-277">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="baa15-278">在 ASP.NET Core 2.0 或更早版本附带的 ASP.NET Core 模块版本中，必须仅使用整分钟数指定 `requestTimeout`，否则默认为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="baa15-278">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="baa15-279">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-279">Default: `00:02:00`</span></span><br><span data-ttu-id="baa15-280">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-280">Min: `00:00:00`</span></span><br><span data-ttu-id="baa15-281">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="baa15-281">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="baa15-282">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-282">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-283">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-283">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="baa15-284">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="baa15-284">Default: `10`</span></span><br><span data-ttu-id="baa15-285">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-285">Min: `0`</span></span><br><span data-ttu-id="baa15-286">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="baa15-286">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="baa15-287">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-287">Optional integer attribute.</span></span></p><p><span data-ttu-id="baa15-288">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="baa15-288">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="baa15-289">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-289">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="baa15-290">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="baa15-290">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="baa15-291">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="baa15-291">Default: `120`</span></span><br><span data-ttu-id="baa15-292">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="baa15-292">Min: `0`</span></span><br><span data-ttu-id="baa15-293">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="baa15-293">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="baa15-294">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-294">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="baa15-295">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-295">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="baa15-296">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-296">Optional string attribute.</span></span></p><p><span data-ttu-id="baa15-297">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-297">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="baa15-298">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="baa15-298">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="baa15-299">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-299">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="baa15-300">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-300">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="baa15-301">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="baa15-301">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="baa15-302">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="baa15-302">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="baa15-303">设置环境变量</span><span class="sxs-lookup"><span data-stu-id="baa15-303">Setting environment variables</span></span>

<span data-ttu-id="baa15-304">可以为 `processPath` 属性中的进程指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="baa15-304">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="baa15-305">使用 `environmentVariables` 集合元素的 `environmentVariable` 子元素指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="baa15-305">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="baa15-306">本部分中设置的环境变量优先于系统环境变量。</span><span class="sxs-lookup"><span data-stu-id="baa15-306">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="baa15-307">以下示例设置了两个环境变量。</span><span class="sxs-lookup"><span data-stu-id="baa15-307">The following example sets two environment variables.</span></span> <span data-ttu-id="baa15-308">`ASPNETCORE_ENVIRONMENT` 将应用的环境配置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="baa15-308">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="baa15-309">开发人员可能会暂时在 web.config 文件中设置此值，以便在调试应用异常时强制加载[开发人员异常页面](xref:fundamentals/error-handling)。</span><span class="sxs-lookup"><span data-stu-id="baa15-309">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="baa15-310">`CONFIG_DIR` 是用户定义的环境变量的一个示例，其中开发人员已写入可在启动时读取值的代码以便形成用于加载应用配置文件的路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-310">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="inprocess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

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

::: moniker-end

> [!WARNING]
> <span data-ttu-id="baa15-311">在不可访问不受信任的网络（如 Internet）的暂存服务器和测试服务器上，仅将 `ASPNETCORE_ENVIRONMENT` 环境变量设置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="baa15-311">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="baa15-312">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="baa15-312">app_offline.htm</span></span>

<span data-ttu-id="baa15-313">如果在应用的根目录中检测到名为 “app_offline.htm”的文件，ASP.NET Core 模块将尝试正常关闭应用并停止处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="baa15-313">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="baa15-314">如果应用在 `shutdownTimeLimit` 中定义的秒数之后仍在运行，ASP.NET Core 模块将终止正在运行的进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-314">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="baa15-315">存在 app_offline.htm 文件时，ASP.NET Core 模块会通过发送回 app_offline.htm 文件的内容来响应请求。</span><span class="sxs-lookup"><span data-stu-id="baa15-315">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="baa15-316">删除 app_offline.htm 文件后，下一个请求将启动应用。</span><span class="sxs-lookup"><span data-stu-id="baa15-316">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="baa15-317">使用进程外托管模型时，如果有已打开的连接，则应用可能不会立即关闭。</span><span class="sxs-lookup"><span data-stu-id="baa15-317">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="baa15-318">例如，WebSocket 连接可能会延迟应用关闭。</span><span class="sxs-lookup"><span data-stu-id="baa15-318">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="baa15-319">启动错误页面</span><span class="sxs-lookup"><span data-stu-id="baa15-319">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="baa15-320">*仅适用于进程外托管。*</span><span class="sxs-lookup"><span data-stu-id="baa15-320">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="baa15-321">如果 ASP.NET Core 模块无法启动后端进程或后端进程启动但无法在配置的端口上侦听，则将显示“502.5 进程失败”状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="baa15-321">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 Process Failure* status code page appears.</span></span> <span data-ttu-id="baa15-322">若要禁止显示此页面并还原为默认 IIS 502 状态代码页面，请使用 `disableStartUpErrorPage` 属性。</span><span class="sxs-lookup"><span data-stu-id="baa15-322">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="baa15-323">有关配置自定义错误消息的详细信息，请参阅 [HTTP 错误 `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="baa15-323">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/).</span></span>

![“502.5 进程失败”状态代码页面](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="baa15-325">日志创建和重定向</span><span class="sxs-lookup"><span data-stu-id="baa15-325">Log creation and redirection</span></span>

<span data-ttu-id="baa15-326">如果已设置 `aspNetCore` 元素的 `stdoutLogEnabled` 和 `stdoutLogFile` 属性，ASP.NET Core 模块会将 stdout 和 stderr 控制台输出重定向到磁盘。</span><span class="sxs-lookup"><span data-stu-id="baa15-326">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="baa15-327">`stdoutLogFile` 路径中的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-327">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="baa15-328">应用池必须对写入日志的位置具有写入权限（使用 `IIS AppPool\<app_pool_name>` 提供写入权限）。</span><span class="sxs-lookup"><span data-stu-id="baa15-328">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="baa15-329">日志不会旋转，除非回收/重新启动进程。</span><span class="sxs-lookup"><span data-stu-id="baa15-329">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="baa15-330">宿主负责限制日志占用的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="baa15-330">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="baa15-331">仅建议使用 stdout 日志来解决应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="baa15-331">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="baa15-332">不要将 stdout 日志用于常规应用日志记录。</span><span class="sxs-lookup"><span data-stu-id="baa15-332">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="baa15-333">对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="baa15-333">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="baa15-334">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="baa15-334">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="baa15-335">创建日志文件时，将自动添加时间戳和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="baa15-335">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="baa15-336">日志文件名是通过将时间戳、进程 ID 和文件扩展名 (.log) 附加到由下划线分隔的 `stdoutLogFile` 路径的最后一段（通常为 stdout）组合而成的。</span><span class="sxs-lookup"><span data-stu-id="baa15-336">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="baa15-337">如果 `stdoutLogFile` 路径以 stdout 结尾，则 PID 为 1934 且于 2018 年 2 月 5 日 19:42:32 创建的应用的日志的文件名为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="baa15-337">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

<span data-ttu-id="baa15-338">以下示例 `aspNetCore` 元素为 Azure 应用服务中托管的应用配置 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="baa15-338">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="baa15-339">本地日志记录可以接受本地路径或网络共享路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-339">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="baa15-340">确认应用池用户标识是否已提供写入路径的权限。</span><span class="sxs-lookup"><span data-stu-id="baa15-340">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="inprocess">
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="baa15-341">增强的诊断日志</span><span class="sxs-lookup"><span data-stu-id="baa15-341">Enhanced diagnostic logs</span></span>

<span data-ttu-id="baa15-342">可以配置 ASP.NET Core 模块提供内容以提供增强的诊断日志。</span><span class="sxs-lookup"><span data-stu-id="baa15-342">The ASP.NET Core Module provides is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="baa15-343">向 web.config 中的 `<aspNetCore>` 元素添加 `<handlerSettings>` 元素。将 `debugLevel` 设置为 `TRACE` 将提供更准确的诊断信息：</span><span class="sxs-lookup"><span data-stu-id="baa15-343">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="inprocess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="baa15-344">调试级别 (`debugLevel`) 值可以同时包含级别和位置。</span><span class="sxs-lookup"><span data-stu-id="baa15-344">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="baa15-345">级别（详细程度由低到高）：</span><span class="sxs-lookup"><span data-stu-id="baa15-345">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="baa15-346">错误</span><span class="sxs-lookup"><span data-stu-id="baa15-346">ERROR</span></span>
* <span data-ttu-id="baa15-347">警告</span><span class="sxs-lookup"><span data-stu-id="baa15-347">WARNING</span></span>
* <span data-ttu-id="baa15-348">信息</span><span class="sxs-lookup"><span data-stu-id="baa15-348">INFO</span></span>
* <span data-ttu-id="baa15-349">TRACE</span><span class="sxs-lookup"><span data-stu-id="baa15-349">TRACE</span></span>

<span data-ttu-id="baa15-350">位置（允许多个位置）：</span><span class="sxs-lookup"><span data-stu-id="baa15-350">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="baa15-351">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="baa15-351">CONSOLE</span></span>
* <span data-ttu-id="baa15-352">事件日志</span><span class="sxs-lookup"><span data-stu-id="baa15-352">EVENTLOG</span></span>
* <span data-ttu-id="baa15-353">文件</span><span class="sxs-lookup"><span data-stu-id="baa15-353">FILE</span></span>

<span data-ttu-id="baa15-354">还可以通过环境变量提供处理程序设置：</span><span class="sxs-lookup"><span data-stu-id="baa15-354">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="baa15-355">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 调试日志文件的路径。</span><span class="sxs-lookup"><span data-stu-id="baa15-355">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="baa15-356">（默认值：aspnetcore debug.log）</span><span class="sxs-lookup"><span data-stu-id="baa15-356">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="baa15-357">`ASPNETCORE_MODULE_DEBUG` &ndash; 调试级别设置。</span><span class="sxs-lookup"><span data-stu-id="baa15-357">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="baa15-358">部署中启用的调试日志记录的时间不要超出排除故障所需的时间。</span><span class="sxs-lookup"><span data-stu-id="baa15-358">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="baa15-359">日志大小不限。</span><span class="sxs-lookup"><span data-stu-id="baa15-359">The size of the log isn't limited.</span></span> <span data-ttu-id="baa15-360">持续启用调试日志可能耗尽可用磁盘空间并导致服务器或应用服务崩溃。</span><span class="sxs-lookup"><span data-stu-id="baa15-360">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="baa15-361">有关 web.config 文件中的 `aspNetCore` 元素的示例，请参阅 [web.config 的配置](#configuration-with-webconfig)。</span><span class="sxs-lookup"><span data-stu-id="baa15-361">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="baa15-362">代理配置使用 HTTP 协议和配对令牌</span><span class="sxs-lookup"><span data-stu-id="baa15-362">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="baa15-363">*仅适用于进程外托管。*</span><span class="sxs-lookup"><span data-stu-id="baa15-363">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="baa15-364">在 ASP.NET Core 模块和 Kestrel 之间创建的代理使用 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="baa15-364">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="baa15-365">使用 HTTP 是一种性能优化，其中模块和 Kestrel 之间的流量发生于脱离网络接口的环回地址。</span><span class="sxs-lookup"><span data-stu-id="baa15-365">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="baa15-366">因此，不存在从脱离服务器的位置窃取模块和 Kestrel 之间的流量的风险。</span><span class="sxs-lookup"><span data-stu-id="baa15-366">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="baa15-367">配对令牌用于保证 Kestrel 收到的请求已由 IIS 代理且不来自某些其他源。</span><span class="sxs-lookup"><span data-stu-id="baa15-367">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="baa15-368">模块已创建配对令牌并将其设置到环境变量 (`ASPNETCORE_TOKEN`)。</span><span class="sxs-lookup"><span data-stu-id="baa15-368">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="baa15-369">此外，配对令牌还设置到每个代理请求的标头 (`MSAspNetCoreToken`)。</span><span class="sxs-lookup"><span data-stu-id="baa15-369">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="baa15-370">IIS 中间件检查它所接收的每个请求，以确认配对令牌标头值与环境变量值相匹配。</span><span class="sxs-lookup"><span data-stu-id="baa15-370">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="baa15-371">如果令牌值不匹配，则将记录请求并拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="baa15-371">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="baa15-372">无法从脱离服务器的位置访问配对令牌环境变量及模块和 Kestrel 之间的流量。</span><span class="sxs-lookup"><span data-stu-id="baa15-372">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="baa15-373">如果不知道配对令牌值，攻击者就无法提交绕过 IIS 中间件中的检查的请求。</span><span class="sxs-lookup"><span data-stu-id="baa15-373">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="baa15-374">具有 IIS 共享配置的 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="baa15-374">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="baa15-375">ASP.NET Core 模块安装程序使用系统帐户的权限运行。</span><span class="sxs-lookup"><span data-stu-id="baa15-375">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="baa15-376">由于本地系统帐户没有对 IIS 共享配置所用的共享路径的修改权限，因此在尝试配置共享上的 applicationHost.config 中的模块设置时，安装程序将遇到拒绝访问错误。</span><span class="sxs-lookup"><span data-stu-id="baa15-376">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="baa15-377">使用 IIS 共享配置时，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="baa15-377">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="baa15-378">禁用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="baa15-378">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="baa15-379">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="baa15-379">Run the installer.</span></span>
1. <span data-ttu-id="baa15-380">将已更新的 applicationHost.config 文件导出到共享。</span><span class="sxs-lookup"><span data-stu-id="baa15-380">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="baa15-381">重新启用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="baa15-381">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="baa15-382">模块版本和托管捆绑安装程序日志</span><span class="sxs-lookup"><span data-stu-id="baa15-382">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="baa15-383">若要确定已安装 ASP.NET Core 模块的版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="baa15-383">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="baa15-384">在托管系统上，导航到 %windir%\System32\inetsrv。</span><span class="sxs-lookup"><span data-stu-id="baa15-384">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="baa15-385">找到 aspnetcore.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-385">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="baa15-386">右键单击该文件，然后从上下文菜单中选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="baa15-386">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="baa15-387">选择“详细信息”选项卡。“文件版本”和“产品版本”表示模块的已安装版本。</span><span class="sxs-lookup"><span data-stu-id="baa15-387">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="baa15-388">在 C:\\Users\\%UserName%\\AppData\\Local\\Temp 中找到了模块的托管捆绑安装程序日志。该文件名为 dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log。</span><span class="sxs-lookup"><span data-stu-id="baa15-388">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="baa15-389">模块、架构和配置文件位置</span><span class="sxs-lookup"><span data-stu-id="baa15-389">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="baa15-390">模块</span><span class="sxs-lookup"><span data-stu-id="baa15-390">Module</span></span>

<span data-ttu-id="baa15-391">**IIS (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="baa15-391">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="baa15-392">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="baa15-392">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="baa15-393">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="baa15-393">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="baa15-394">**IIS Express (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="baa15-394">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="baa15-395">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="baa15-395">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="baa15-396">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="baa15-396">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="baa15-397">架构</span><span class="sxs-lookup"><span data-stu-id="baa15-397">Schema</span></span>

<span data-ttu-id="baa15-398">**IIS**</span><span class="sxs-lookup"><span data-stu-id="baa15-398">**IIS**</span></span>

   * <span data-ttu-id="baa15-399">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="baa15-399">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="baa15-400">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="baa15-400">**IIS Express**</span></span>

   * <span data-ttu-id="baa15-401">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="baa15-401">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="baa15-402">配置</span><span class="sxs-lookup"><span data-stu-id="baa15-402">Configuration</span></span>

<span data-ttu-id="baa15-403">**IIS**</span><span class="sxs-lookup"><span data-stu-id="baa15-403">**IIS**</span></span>

   * <span data-ttu-id="baa15-404">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="baa15-404">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="baa15-405">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="baa15-405">**IIS Express**</span></span>

   * <span data-ttu-id="baa15-406">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="baa15-406">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="baa15-407">可以通过在 applicationHost.config 文件中搜索 aspnetcore.dll 找到这些文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-407">The files can be found by searching for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="baa15-408">对于 IIS Express，默认情况下不会存在 applicationHost.config 文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-408">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="baa15-409">在 Visual Studio 解决方案中启动任何 Web 应用项目时，将在 \<application_root>\\.vs\\config 中创建该文件。</span><span class="sxs-lookup"><span data-stu-id="baa15-409">The file is created at *\<application_root>\\.vs\\config* when starting any web app project in the Visual Studio solution.</span></span>
