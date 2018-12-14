---
title: ASP.NET Core 模块配置参考
author: guardrex
description: 了解如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 12/06/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 0ad73d89ffa3a8a3625c6e248efaad821e1b4d0a
ms.sourcegitcommit: 49faca2644590fc081d86db46ea5e29edfc28b7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2018
ms.locfileid: "53121552"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="de40b-103">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="de40b-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="de40b-104">作者：[Luke Latham](https://github.com/guardrex)、[Rick Anderson](https://twitter.com/RickAndMSFT)、[Sourabh Shirhatti](https://twitter.com/sshirhatti) 和 [Justin Kotalik](https://github.com/jkotalik)</span><span class="sxs-lookup"><span data-stu-id="de40b-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), and [Justin Kotalik](https://github.com/jkotalik)</span></span>

<span data-ttu-id="de40b-105">本文档说明了如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="de40b-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="de40b-106">有关 ASP.NET Core 模块简介和安装说明，请参阅 [ASP.NET Core 模块概述](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="de40b-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a><span data-ttu-id="de40b-107">托管模型</span><span class="sxs-lookup"><span data-stu-id="de40b-107">Hosting model</span></span>

<span data-ttu-id="de40b-108">对于在 .NET Core 2.2 或更高版本上运行的应用，该模块支持进程内托管模型以便提高性能（与反向代理(进程外)托管相比）。</span><span class="sxs-lookup"><span data-stu-id="de40b-108">For apps running on .NET Core 2.2 or later, the module supports an in-process hosting model for improved performance compared to reverse-proxy (out-of-process) hosting.</span></span> <span data-ttu-id="de40b-109">有关更多信息，请参见<xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>。</span><span class="sxs-lookup"><span data-stu-id="de40b-109">For more information, see <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>.</span></span>

<span data-ttu-id="de40b-110">进程内托管选择使用现有应用，但 [dotnet new](/dotnet/core/tools/dotnet-new) 模板默认使用所有 IIS 和 IIS Express 方案的进程内托管模型。</span><span class="sxs-lookup"><span data-stu-id="de40b-110">In-procsess hosting is opt-in for existing apps, but [dotnet new](/dotnet/core/tools/dotnet-new) templates default to the in-process hosting model for all IIS and IIS Express scenarios.</span></span>

<span data-ttu-id="de40b-111">若要配置用于进程内托管的应用，请将 `<AspNetCoreHostingModel>` 属性添加到值为 `InProcess`（进程外托管使用 `outofprocess` 进行设置）的应用项目文件（例如，MyApp.csproj）：</span><span class="sxs-lookup"><span data-stu-id="de40b-111">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file (for example, *MyApp.csproj*) with a value of `InProcess` (out-of-process hosting is set with `outofprocess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>InProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="de40b-112">在进程内托管时，将应用以下特征：</span><span class="sxs-lookup"><span data-stu-id="de40b-112">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="de40b-113">使用 IIS HTTP 服务器 (`IISHttpServer`) 而不是 [Kestrel](xref:fundamentals/servers/kestrel) 服务器。</span><span class="sxs-lookup"><span data-stu-id="de40b-113">IIS HTTP Server (`IISHttpServer`) is used instead of the [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span> <span data-ttu-id="de40b-114">IIS HTTP 服务器 (`IISHttpServer`) 是另一种 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 实现，可将 IIS 本机请求转换为 ASP.NET Core 托管请求以便应用进行处理。</span><span class="sxs-lookup"><span data-stu-id="de40b-114">IIS HTTP Server (`IISHttpServer`) is another <xref:Microsoft.AspNetCore.Hosting.Server.IServer> implementation that converts IIS native requests into ASP.NET Core managed requests for processing by the app.</span></span>

* <span data-ttu-id="de40b-115">[requestTimeout 属性](#attributes-of-the-aspnetcore-element)不适用于进程内托管。</span><span class="sxs-lookup"><span data-stu-id="de40b-115">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="de40b-116">不支持在应用之间共享应用池。</span><span class="sxs-lookup"><span data-stu-id="de40b-116">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="de40b-117">每个应用使用一个应用池。</span><span class="sxs-lookup"><span data-stu-id="de40b-117">Use one app pool per app.</span></span>

* <span data-ttu-id="de40b-118">使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)或手动将 [app_offline.htm 文件置于部署中](xref:host-and-deploy/iis/index#locked-deployment-files)时，如果有已打开的连接，则应用可能不会立即关闭。</span><span class="sxs-lookup"><span data-stu-id="de40b-118">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="de40b-119">例如，WebSocket 连接可能会延迟应用关闭。</span><span class="sxs-lookup"><span data-stu-id="de40b-119">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="de40b-120">应用和已安装的运行时（x64 或 x86）的体系结构（位数）必须与应用池的体系结构匹配。</span><span class="sxs-lookup"><span data-stu-id="de40b-120">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="de40b-121">如果使用 `WebHostBuilder`（而不是使用 [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)）手动设置应用的主机，并且应用曾经直接在 Kestrel 服务器上运行（自托管），则先调用 `UseKestrel`，再调用 `UseIISIntegration`。</span><span class="sxs-lookup"><span data-stu-id="de40b-121">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="de40b-122">如果顺序颠倒，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="de40b-122">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="de40b-123">检测到客户端连接断开。</span><span class="sxs-lookup"><span data-stu-id="de40b-123">Client disconnects are detected.</span></span> <span data-ttu-id="de40b-124">客户端连接断开时，[HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 取消标记将会取消。</span><span class="sxs-lookup"><span data-stu-id="de40b-124">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="de40b-125"><xref:System.IO.Directory.GetCurrentDirectory*> 会返回 IIS 启动的进程的工作目录而非应用目录（例如，对于 w3wp.exe，是 C:\Windows\System32\inetsrv）。</span><span class="sxs-lookup"><span data-stu-id="de40b-125"><xref:System.IO.Directory.GetCurrentDirectory*> returns the worker directory of the process started by IIS rather than the app's directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

  <span data-ttu-id="de40b-126">对于设置应用的当前目录的示例代码，请参阅 [CurrentDirectoryHelpers 类](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs)。</span><span class="sxs-lookup"><span data-stu-id="de40b-126">For sample code that sets the app's current directory, see the [CurrentDirectoryHelpers class](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs).</span></span> <span data-ttu-id="de40b-127">调用 `SetCurrentDirectory` 方法。</span><span class="sxs-lookup"><span data-stu-id="de40b-127">Call the `SetCurrentDirectory` method.</span></span> <span data-ttu-id="de40b-128">后续 <xref:System.IO.Directory.GetCurrentDirectory*> 调用提供应用的目录。</span><span class="sxs-lookup"><span data-stu-id="de40b-128">Subsequent calls to <xref:System.IO.Directory.GetCurrentDirectory*> provide the app's directory.</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="de40b-129">托管模型更改</span><span class="sxs-lookup"><span data-stu-id="de40b-129">Hosting model changes</span></span>

<span data-ttu-id="de40b-130">如果 `hostingModel` 设置在 web.config 文件中被更改（如 [web.config 的配置](#configuration-with-webconfig)部分中所述），则该模块会再循环 IIS 工作进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-130">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="de40b-131">对于 IIS Express，该模块不会再循环工作进程，但改为触发当前 IIS Express 进程的正常关闭。</span><span class="sxs-lookup"><span data-stu-id="de40b-131">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="de40b-132">应用的下一个请求会生成新的 IIS Express 进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-132">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="de40b-133">进程名</span><span class="sxs-lookup"><span data-stu-id="de40b-133">Process name</span></span>

<span data-ttu-id="de40b-134">`Process.GetCurrentProcess().ProcessName` 报告 `w3wp`/`iisexpress`（进程内）或 `dotnet`（进程外）。</span><span class="sxs-lookup"><span data-stu-id="de40b-134">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

## <a name="configuration-with-webconfig"></a><span data-ttu-id="de40b-135">web.config 的配置</span><span class="sxs-lookup"><span data-stu-id="de40b-135">Configuration with web.config</span></span>

<span data-ttu-id="de40b-136">在站点的 *web.config* 文件中使用 `system.webServer` 节点的 `aspNetCore` 部分配置 ASP.NET Core 模块。</span><span class="sxs-lookup"><span data-stu-id="de40b-136">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="de40b-137">以下 *web.config* 文件发布用于[依赖框架的部署](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)，并配置 ASP.NET Core 模块以处理站点请求：</span><span class="sxs-lookup"><span data-stu-id="de40b-137">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" 
                  arguments=".\MyApp.dll" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
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

<span data-ttu-id="de40b-138">以下 web.config 发布用于[独立部署](/dotnet/articles/core/deploying/#self-contained-deployments-scd)：</span><span class="sxs-lookup"><span data-stu-id="de40b-138">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

<span data-ttu-id="de40b-139">将 <xref:System.Configuration.SectionInformation.InheritInChildApplications*> 属性设置为 `false`，表示 [\<>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) 元素中指定的设置不会由驻留在应用子目录中的应用继承。</span><span class="sxs-lookup"><span data-stu-id="de40b-139">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the app.</span></span>

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

<span data-ttu-id="de40b-140">将应用部署为 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)时，`stdoutLogFile` 路径将设置为 `\\?\%home%\LogFiles\stdout`。</span><span class="sxs-lookup"><span data-stu-id="de40b-140">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="de40b-141">该路径会将 stdout 日志保存到 *LogFiles* 文件夹，该文件夹是由服务自动创建的位置。</span><span class="sxs-lookup"><span data-stu-id="de40b-141">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="de40b-142">有关 IIS 子应用程序配置的信息，请参阅<xref:host-and-deploy/iis/index#sub-applications>。</span><span class="sxs-lookup"><span data-stu-id="de40b-142">For information on IIS sub-application configuration, see <xref:host-and-deploy/iis/index#sub-applications>.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="de40b-143">aspNetCore 元素的属性</span><span class="sxs-lookup"><span data-stu-id="de40b-143">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="de40b-144">特性</span><span class="sxs-lookup"><span data-stu-id="de40b-144">Attribute</span></span> | <span data-ttu-id="de40b-145">说明</span><span class="sxs-lookup"><span data-stu-id="de40b-145">Description</span></span> | <span data-ttu-id="de40b-146">默认</span><span class="sxs-lookup"><span data-stu-id="de40b-146">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="de40b-147">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-147">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-148">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="de40b-148">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="de40b-149">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-149">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-150">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="de40b-150">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="de40b-151">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-151">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-152">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-152">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="de40b-153">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="de40b-153">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="de40b-154">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-154">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-155">将托管模型指定为进程内 (`InProcess`) 或进程外 (`OutOfProcess`)。</span><span class="sxs-lookup"><span data-stu-id="de40b-155">Specifies the hosting model as in-process (`InProcess`) or out-of-process (`OutOfProcess`).</span></span></p> | `OutOfProcess` |
| `processesPerApplication` | <p><span data-ttu-id="de40b-156">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-156">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-157">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="de40b-157">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="de40b-158">&dagger;对于进程内托管，值限制为 `1`。</span><span class="sxs-lookup"><span data-stu-id="de40b-158">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="de40b-159">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-159">Default: `1`</span></span><br><span data-ttu-id="de40b-160">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-160">Min: `1`</span></span><br><span data-ttu-id="de40b-161">最大值：`100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="de40b-161">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="de40b-162">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-162">Required string attribute.</span></span></p><p><span data-ttu-id="de40b-163">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-163">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="de40b-164">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-164">Relative paths are supported.</span></span> <span data-ttu-id="de40b-165">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-165">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="de40b-166">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-166">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-167">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="de40b-167">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="de40b-168">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-168">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="de40b-169">不支持进程内托管。</span><span class="sxs-lookup"><span data-stu-id="de40b-169">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="de40b-170">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-170">Default: `10`</span></span><br><span data-ttu-id="de40b-171">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-171">Min: `0`</span></span><br><span data-ttu-id="de40b-172">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="de40b-172">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="de40b-173">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-173">Optional timespan attribute.</span></span></p><p><span data-ttu-id="de40b-174">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="de40b-174">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="de40b-175">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</span><span class="sxs-lookup"><span data-stu-id="de40b-175">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="de40b-176">不适用于进程内托管。</span><span class="sxs-lookup"><span data-stu-id="de40b-176">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="de40b-177">对于进程内托管，该模块等待应用处理该请求。</span><span class="sxs-lookup"><span data-stu-id="de40b-177">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="de40b-178">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-178">Default: `00:02:00`</span></span><br><span data-ttu-id="de40b-179">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-179">Min: `00:00:00`</span></span><br><span data-ttu-id="de40b-180">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-180">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="de40b-181">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-181">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-182">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-182">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="de40b-183">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-183">Default: `10`</span></span><br><span data-ttu-id="de40b-184">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-184">Min: `0`</span></span><br><span data-ttu-id="de40b-185">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="de40b-185">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="de40b-186">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-186">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-187">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-187">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="de40b-188">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-188">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="de40b-189">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="de40b-189">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="de40b-190">值 0（零）不被视为无限超时。</span><span class="sxs-lookup"><span data-stu-id="de40b-190">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="de40b-191">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="de40b-191">Default: `120`</span></span><br><span data-ttu-id="de40b-192">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-192">Min: `0`</span></span><br><span data-ttu-id="de40b-193">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="de40b-193">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="de40b-194">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-194">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-195">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-195">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="de40b-196">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-196">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-197">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-197">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="de40b-198">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-198">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="de40b-199">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-199">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="de40b-200">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-200">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="de40b-201">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="de40b-201">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="de40b-202">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="de40b-202">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="de40b-203">特性</span><span class="sxs-lookup"><span data-stu-id="de40b-203">Attribute</span></span> | <span data-ttu-id="de40b-204">说明</span><span class="sxs-lookup"><span data-stu-id="de40b-204">Description</span></span> | <span data-ttu-id="de40b-205">默认</span><span class="sxs-lookup"><span data-stu-id="de40b-205">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="de40b-206">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-206">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-207">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="de40b-207">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="de40b-208">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-208">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-209">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="de40b-209">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="de40b-210">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-210">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-211">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-211">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="de40b-212">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="de40b-212">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="de40b-213">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-213">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-214">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="de40b-214">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="de40b-215">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-215">Default: `1`</span></span><br><span data-ttu-id="de40b-216">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-216">Min: `1`</span></span><br><span data-ttu-id="de40b-217">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="de40b-217">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="de40b-218">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-218">Required string attribute.</span></span></p><p><span data-ttu-id="de40b-219">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-219">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="de40b-220">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-220">Relative paths are supported.</span></span> <span data-ttu-id="de40b-221">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-221">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="de40b-222">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-222">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-223">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="de40b-223">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="de40b-224">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-224">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="de40b-225">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-225">Default: `10`</span></span><br><span data-ttu-id="de40b-226">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-226">Min: `0`</span></span><br><span data-ttu-id="de40b-227">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="de40b-227">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="de40b-228">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-228">Optional timespan attribute.</span></span></p><p><span data-ttu-id="de40b-229">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="de40b-229">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="de40b-230">在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</span><span class="sxs-lookup"><span data-stu-id="de40b-230">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="de40b-231">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-231">Default: `00:02:00`</span></span><br><span data-ttu-id="de40b-232">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-232">Min: `00:00:00`</span></span><br><span data-ttu-id="de40b-233">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-233">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="de40b-234">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-234">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-235">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-235">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="de40b-236">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-236">Default: `10`</span></span><br><span data-ttu-id="de40b-237">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-237">Min: `0`</span></span><br><span data-ttu-id="de40b-238">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="de40b-238">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="de40b-239">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-239">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-240">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-240">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="de40b-241">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-241">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="de40b-242">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="de40b-242">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="de40b-243">值 0（零）不被视为无限超时。</span><span class="sxs-lookup"><span data-stu-id="de40b-243">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="de40b-244">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="de40b-244">Default: `120`</span></span><br><span data-ttu-id="de40b-245">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-245">Min: `0`</span></span><br><span data-ttu-id="de40b-246">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="de40b-246">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="de40b-247">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-247">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-248">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-248">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="de40b-249">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-249">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-250">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-250">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="de40b-251">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-251">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="de40b-252">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-252">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="de40b-253">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-253">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="de40b-254">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="de40b-254">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="de40b-255">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="de40b-255">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="de40b-256">特性</span><span class="sxs-lookup"><span data-stu-id="de40b-256">Attribute</span></span> | <span data-ttu-id="de40b-257">说明</span><span class="sxs-lookup"><span data-stu-id="de40b-257">Description</span></span> | <span data-ttu-id="de40b-258">默认</span><span class="sxs-lookup"><span data-stu-id="de40b-258">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="de40b-259">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-259">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-260">processPath 中指定的可执行文件的参数。</span><span class="sxs-lookup"><span data-stu-id="de40b-260">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="de40b-261">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-261">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-262">如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</span><span class="sxs-lookup"><span data-stu-id="de40b-262">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="de40b-263">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-263">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-264">如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-264">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="de40b-265">该进程负责在每个请求的此令牌上调用 CloseHandle。</span><span class="sxs-lookup"><span data-stu-id="de40b-265">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="de40b-266">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-266">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-267">指定每个应用均可启动的 **processPath** 设置中指定的进程的实例数。</span><span class="sxs-lookup"><span data-stu-id="de40b-267">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="de40b-268">默认值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-268">Default: `1`</span></span><br><span data-ttu-id="de40b-269">最小值：`1`</span><span class="sxs-lookup"><span data-stu-id="de40b-269">Min: `1`</span></span><br><span data-ttu-id="de40b-270">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="de40b-270">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="de40b-271">必需的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-271">Required string attribute.</span></span></p><p><span data-ttu-id="de40b-272">为 HTTP 请求启动进程侦听的可执行文件的路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-272">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="de40b-273">支持相对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-273">Relative paths are supported.</span></span> <span data-ttu-id="de40b-274">如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-274">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="de40b-275">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-275">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-276">指定允许 processPath 中指定的进程每分钟崩溃的次数。</span><span class="sxs-lookup"><span data-stu-id="de40b-276">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="de40b-277">如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-277">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="de40b-278">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-278">Default: `10`</span></span><br><span data-ttu-id="de40b-279">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-279">Min: `0`</span></span><br><span data-ttu-id="de40b-280">最大值：`100`</span><span class="sxs-lookup"><span data-stu-id="de40b-280">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="de40b-281">可选的 timespan 属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-281">Optional timespan attribute.</span></span></p><p><span data-ttu-id="de40b-282">指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</span><span class="sxs-lookup"><span data-stu-id="de40b-282">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="de40b-283">在 ASP.NET Core 2.0 或更早版本附带的 ASP.NET Core 模块版本中，必须仅使用整分钟数指定 `requestTimeout`，否则默认为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="de40b-283">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="de40b-284">默认值：`00:02:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-284">Default: `00:02:00`</span></span><br><span data-ttu-id="de40b-285">最小值：`00:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-285">Min: `00:00:00`</span></span><br><span data-ttu-id="de40b-286">最大值：`360:00:00`</span><span class="sxs-lookup"><span data-stu-id="de40b-286">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="de40b-287">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-287">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-288">检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-288">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="de40b-289">默认值：`10`</span><span class="sxs-lookup"><span data-stu-id="de40b-289">Default: `10`</span></span><br><span data-ttu-id="de40b-290">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-290">Min: `0`</span></span><br><span data-ttu-id="de40b-291">最大值：`600`</span><span class="sxs-lookup"><span data-stu-id="de40b-291">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="de40b-292">可选的整数属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-292">Optional integer attribute.</span></span></p><p><span data-ttu-id="de40b-293">模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。</span><span class="sxs-lookup"><span data-stu-id="de40b-293">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="de40b-294">如果超出了此时间限制，模块将终止该进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-294">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="de40b-295">模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</span><span class="sxs-lookup"><span data-stu-id="de40b-295">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="de40b-296">默认值：`120`</span><span class="sxs-lookup"><span data-stu-id="de40b-296">Default: `120`</span></span><br><span data-ttu-id="de40b-297">最小值：`0`</span><span class="sxs-lookup"><span data-stu-id="de40b-297">Min: `0`</span></span><br><span data-ttu-id="de40b-298">最大值：`3600`</span><span class="sxs-lookup"><span data-stu-id="de40b-298">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="de40b-299">可选布尔属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-299">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="de40b-300">如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-300">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="de40b-301">可选的字符串属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-301">Optional string attribute.</span></span></p><p><span data-ttu-id="de40b-302">指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-302">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="de40b-303">相对路径与站点根目录相对。</span><span class="sxs-lookup"><span data-stu-id="de40b-303">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="de40b-304">以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-304">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="de40b-305">路径中提供的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-305">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="de40b-306">使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。</span><span class="sxs-lookup"><span data-stu-id="de40b-306">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="de40b-307">如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="de40b-307">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="de40b-308">设置环境变量</span><span class="sxs-lookup"><span data-stu-id="de40b-308">Setting environment variables</span></span>

<span data-ttu-id="de40b-309">可以为 `processPath` 属性中的进程指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="de40b-309">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="de40b-310">使用 `environmentVariables` 集合元素的 `environmentVariable` 子元素指定环境变量。</span><span class="sxs-lookup"><span data-stu-id="de40b-310">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="de40b-311">本部分中设置的环境变量优先于系统环境变量。</span><span class="sxs-lookup"><span data-stu-id="de40b-311">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="de40b-312">以下示例设置了两个环境变量。</span><span class="sxs-lookup"><span data-stu-id="de40b-312">The following example sets two environment variables.</span></span> <span data-ttu-id="de40b-313">`ASPNETCORE_ENVIRONMENT` 将应用的环境配置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="de40b-313">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="de40b-314">开发人员可能会暂时在 web.config 文件中设置此值，以便在调试应用异常时强制加载[开发人员异常页面](xref:fundamentals/error-handling)。</span><span class="sxs-lookup"><span data-stu-id="de40b-314">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="de40b-315">`CONFIG_DIR` 是用户定义的环境变量的一个示例，其中开发人员已写入可在启动时读取值的代码以便形成用于加载应用配置文件的路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-315">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="InProcess">
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
> <span data-ttu-id="de40b-316">在不可访问不受信任的网络（如 Internet）的暂存服务器和测试服务器上，仅将 `ASPNETCORE_ENVIRONMENT` 环境变量设置为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="de40b-316">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="de40b-317">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="de40b-317">app_offline.htm</span></span>

<span data-ttu-id="de40b-318">如果在应用的根目录中检测到名为 “app_offline.htm”的文件，ASP.NET Core 模块将尝试正常关闭应用并停止处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="de40b-318">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="de40b-319">如果应用在 `shutdownTimeLimit` 中定义的秒数之后仍在运行，ASP.NET Core 模块将终止正在运行的进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-319">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="de40b-320">存在 app_offline.htm 文件时，ASP.NET Core 模块会通过发送回 app_offline.htm 文件的内容来响应请求。</span><span class="sxs-lookup"><span data-stu-id="de40b-320">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="de40b-321">删除 app_offline.htm 文件后，下一个请求将启动应用。</span><span class="sxs-lookup"><span data-stu-id="de40b-321">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="de40b-322">使用进程外托管模型时，如果有已打开的连接，则应用可能不会立即关闭。</span><span class="sxs-lookup"><span data-stu-id="de40b-322">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="de40b-323">例如，WebSocket 连接可能会延迟应用关闭。</span><span class="sxs-lookup"><span data-stu-id="de40b-323">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="de40b-324">启动错误页面</span><span class="sxs-lookup"><span data-stu-id="de40b-324">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="de40b-325">进程内和进程外托管在无法启动应用时均会生成自定义错误页面。</span><span class="sxs-lookup"><span data-stu-id="de40b-325">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="de40b-326">如果 ASP.NET Core 模块无法找到进程内或进程外请求处理程序，则会显示“500.0 - 进程内/进程外处理程序加载失败”状态代码页。</span><span class="sxs-lookup"><span data-stu-id="de40b-326">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="de40b-327">对于进程内托管，如果 ASP.NET Core 模块无法启动应用，则会显示“500.30 - 启动失败”状态代码页。</span><span class="sxs-lookup"><span data-stu-id="de40b-327">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="de40b-328">对于进程外托管，如果 ASP.NET Core 模块无法启动后端进程或后端进程启动但无法在配置的端口上侦听，则将显示“502.5 - 进程失败”状态代码页。</span><span class="sxs-lookup"><span data-stu-id="de40b-328">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="de40b-329">若要禁止显示此页面并还原为默认 IIS 5xx 状态代码页，请使用 `disableStartUpErrorPage` 属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-329">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="de40b-330">有关配置自定义错误消息的详细信息，请参阅 [HTTP 错误 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="de40b-330">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="de40b-331">如果 ASP.NET Core 模块无法启动后端进程或后端进程启动但无法在配置的端口上侦听，则将显示“502.5 - 进程失败”状态代码页。</span><span class="sxs-lookup"><span data-stu-id="de40b-331">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="de40b-332">若要禁止显示此页面并还原为默认 IIS 502 状态代码页面，请使用 `disableStartUpErrorPage` 属性。</span><span class="sxs-lookup"><span data-stu-id="de40b-332">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="de40b-333">有关配置自定义错误消息的详细信息，请参阅 [HTTP 错误 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)。</span><span class="sxs-lookup"><span data-stu-id="de40b-333">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

![“502.5 进程失败”状态代码页面](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="de40b-335">日志创建和重定向</span><span class="sxs-lookup"><span data-stu-id="de40b-335">Log creation and redirection</span></span>

<span data-ttu-id="de40b-336">如果已设置 `aspNetCore` 元素的 `stdoutLogEnabled` 和 `stdoutLogFile` 属性，ASP.NET Core 模块会将 stdout 和 stderr 控制台输出重定向到磁盘。</span><span class="sxs-lookup"><span data-stu-id="de40b-336">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="de40b-337">`stdoutLogFile` 路径中的任何文件夹都必须存在，以便模块创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-337">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="de40b-338">应用池必须对写入日志的位置具有写入权限（使用 `IIS AppPool\<app_pool_name>` 提供写入权限）。</span><span class="sxs-lookup"><span data-stu-id="de40b-338">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="de40b-339">日志不会旋转，除非回收/重新启动进程。</span><span class="sxs-lookup"><span data-stu-id="de40b-339">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="de40b-340">宿主负责限制日志占用的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="de40b-340">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="de40b-341">仅建议使用 stdout 日志来解决应用启动问题。</span><span class="sxs-lookup"><span data-stu-id="de40b-341">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="de40b-342">不要将 stdout 日志用于常规应用日志记录。</span><span class="sxs-lookup"><span data-stu-id="de40b-342">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="de40b-343">对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。</span><span class="sxs-lookup"><span data-stu-id="de40b-343">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="de40b-344">有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。</span><span class="sxs-lookup"><span data-stu-id="de40b-344">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="de40b-345">创建日志文件时，将自动添加时间戳和文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="de40b-345">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="de40b-346">日志文件名是通过将时间戳、进程 ID 和文件扩展名 (.log) 附加到由下划线分隔的 `stdoutLogFile` 路径的最后一段（通常为 stdout）组合而成的。</span><span class="sxs-lookup"><span data-stu-id="de40b-346">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="de40b-347">如果 `stdoutLogFile` 路径以 stdout 结尾，则 PID 为 1934 且于 2018 年 2 月 5 日 19:42:32 创建的应用的日志的文件名为 stdout_20180205194132_1934.log。</span><span class="sxs-lookup"><span data-stu-id="de40b-347">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="de40b-348">如果 `stdoutLogEnabled` 为 false，则会捕获应用启动时发生的错误，并将其发送到事件日志，最大为 30 KB。</span><span class="sxs-lookup"><span data-stu-id="de40b-348">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="de40b-349">启动后，将丢弃所有其他日志。</span><span class="sxs-lookup"><span data-stu-id="de40b-349">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="de40b-350">以下示例 `aspNetCore` 元素为 Azure 应用服务中托管的应用配置 stdout 日志记录。</span><span class="sxs-lookup"><span data-stu-id="de40b-350">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="de40b-351">本地日志记录可以接受本地路径或网络共享路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-351">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="de40b-352">确认应用池用户标识是否已提供写入路径的权限。</span><span class="sxs-lookup"><span data-stu-id="de40b-352">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
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

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="de40b-353">增强的诊断日志</span><span class="sxs-lookup"><span data-stu-id="de40b-353">Enhanced diagnostic logs</span></span>

<span data-ttu-id="de40b-354">可以配置 ASP.NET Core 模块提供内容以提供增强的诊断日志。</span><span class="sxs-lookup"><span data-stu-id="de40b-354">The ASP.NET Core Module provides is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="de40b-355">向 web.config 中的 `<aspNetCore>` 元素添加 `<handlerSettings>` 元素。将 `debugLevel` 设置为 `TRACE` 将提供更准确的诊断信息：</span><span class="sxs-lookup"><span data-stu-id="de40b-355">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="de40b-356">调试级别 (`debugLevel`) 值可以同时包含级别和位置。</span><span class="sxs-lookup"><span data-stu-id="de40b-356">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="de40b-357">级别（详细程度由低到高）：</span><span class="sxs-lookup"><span data-stu-id="de40b-357">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="de40b-358">错误</span><span class="sxs-lookup"><span data-stu-id="de40b-358">ERROR</span></span>
* <span data-ttu-id="de40b-359">警告</span><span class="sxs-lookup"><span data-stu-id="de40b-359">WARNING</span></span>
* <span data-ttu-id="de40b-360">信息</span><span class="sxs-lookup"><span data-stu-id="de40b-360">INFO</span></span>
* <span data-ttu-id="de40b-361">TRACE</span><span class="sxs-lookup"><span data-stu-id="de40b-361">TRACE</span></span>

<span data-ttu-id="de40b-362">位置（允许多个位置）：</span><span class="sxs-lookup"><span data-stu-id="de40b-362">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="de40b-363">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="de40b-363">CONSOLE</span></span>
* <span data-ttu-id="de40b-364">事件日志</span><span class="sxs-lookup"><span data-stu-id="de40b-364">EVENTLOG</span></span>
* <span data-ttu-id="de40b-365">文件</span><span class="sxs-lookup"><span data-stu-id="de40b-365">FILE</span></span>

<span data-ttu-id="de40b-366">还可以通过环境变量提供处理程序设置：</span><span class="sxs-lookup"><span data-stu-id="de40b-366">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="de40b-367">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 调试日志文件的路径。</span><span class="sxs-lookup"><span data-stu-id="de40b-367">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="de40b-368">（默认值：aspnetcore debug.log）</span><span class="sxs-lookup"><span data-stu-id="de40b-368">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="de40b-369">`ASPNETCORE_MODULE_DEBUG` &ndash; 调试级别设置。</span><span class="sxs-lookup"><span data-stu-id="de40b-369">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="de40b-370">部署中启用的调试日志记录的时间不要超出排除故障所需的时间。</span><span class="sxs-lookup"><span data-stu-id="de40b-370">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="de40b-371">日志大小不限。</span><span class="sxs-lookup"><span data-stu-id="de40b-371">The size of the log isn't limited.</span></span> <span data-ttu-id="de40b-372">持续启用调试日志可能耗尽可用磁盘空间并导致服务器或应用服务崩溃。</span><span class="sxs-lookup"><span data-stu-id="de40b-372">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="de40b-373">有关 web.config 文件中的 `aspNetCore` 元素的示例，请参阅 [web.config 的配置](#configuration-with-webconfig)。</span><span class="sxs-lookup"><span data-stu-id="de40b-373">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="de40b-374">代理配置使用 HTTP 协议和配对令牌</span><span class="sxs-lookup"><span data-stu-id="de40b-374">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="de40b-375">*仅适用于进程外托管。*</span><span class="sxs-lookup"><span data-stu-id="de40b-375">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="de40b-376">在 ASP.NET Core 模块和 Kestrel 之间创建的代理使用 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="de40b-376">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="de40b-377">使用 HTTP 是一种性能优化，其中模块和 Kestrel 之间的流量发生于脱离网络接口的环回地址。</span><span class="sxs-lookup"><span data-stu-id="de40b-377">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="de40b-378">因此，不存在从脱离服务器的位置窃取模块和 Kestrel 之间的流量的风险。</span><span class="sxs-lookup"><span data-stu-id="de40b-378">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="de40b-379">配对令牌用于保证 Kestrel 收到的请求已由 IIS 代理且不来自某些其他源。</span><span class="sxs-lookup"><span data-stu-id="de40b-379">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="de40b-380">模块已创建配对令牌并将其设置到环境变量 (`ASPNETCORE_TOKEN`)。</span><span class="sxs-lookup"><span data-stu-id="de40b-380">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="de40b-381">此外，配对令牌还设置到每个代理请求的标头 (`MSAspNetCoreToken`)。</span><span class="sxs-lookup"><span data-stu-id="de40b-381">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="de40b-382">IIS 中间件检查它所接收的每个请求，以确认配对令牌标头值与环境变量值相匹配。</span><span class="sxs-lookup"><span data-stu-id="de40b-382">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="de40b-383">如果令牌值不匹配，则将记录请求并拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="de40b-383">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="de40b-384">无法从脱离服务器的位置访问配对令牌环境变量及模块和 Kestrel 之间的流量。</span><span class="sxs-lookup"><span data-stu-id="de40b-384">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="de40b-385">如果不知道配对令牌值，攻击者就无法提交绕过 IIS 中间件中的检查的请求。</span><span class="sxs-lookup"><span data-stu-id="de40b-385">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="de40b-386">具有 IIS 共享配置的 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="de40b-386">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="de40b-387">ASP.NET Core 模块安装程序使用系统帐户的权限运行。</span><span class="sxs-lookup"><span data-stu-id="de40b-387">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="de40b-388">由于本地系统帐户没有对 IIS 共享配置所用的共享路径的修改权限，因此在尝试配置共享上的 applicationHost.config 中的模块设置时，安装程序将遇到拒绝访问错误。</span><span class="sxs-lookup"><span data-stu-id="de40b-388">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="de40b-389">使用 IIS 共享配置时，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="de40b-389">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="de40b-390">禁用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="de40b-390">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="de40b-391">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="de40b-391">Run the installer.</span></span>
1. <span data-ttu-id="de40b-392">将已更新的 applicationHost.config 文件导出到共享。</span><span class="sxs-lookup"><span data-stu-id="de40b-392">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="de40b-393">重新启用 IIS 共享配置。</span><span class="sxs-lookup"><span data-stu-id="de40b-393">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="de40b-394">模块版本和托管捆绑安装程序日志</span><span class="sxs-lookup"><span data-stu-id="de40b-394">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="de40b-395">若要确定已安装 ASP.NET Core 模块的版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="de40b-395">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="de40b-396">在托管系统上，导航到 %windir%\System32\inetsrv。</span><span class="sxs-lookup"><span data-stu-id="de40b-396">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="de40b-397">找到 aspnetcore.dll 文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-397">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="de40b-398">右键单击该文件，然后从上下文菜单中选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="de40b-398">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="de40b-399">选择“详细信息”选项卡。“文件版本”和“产品版本”表示模块的已安装版本。</span><span class="sxs-lookup"><span data-stu-id="de40b-399">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="de40b-400">在 C:\\Users\\%UserName%\\AppData\\Local\\Temp 中找到了模块的托管捆绑安装程序日志。该文件名为 dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log。</span><span class="sxs-lookup"><span data-stu-id="de40b-400">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="de40b-401">模块、架构和配置文件位置</span><span class="sxs-lookup"><span data-stu-id="de40b-401">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="de40b-402">模块</span><span class="sxs-lookup"><span data-stu-id="de40b-402">Module</span></span>

<span data-ttu-id="de40b-403">**IIS (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="de40b-403">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="de40b-404">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-404">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="de40b-405">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-405">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="de40b-406">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-406">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="de40b-407">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-407">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="de40b-408">**IIS Express (x86/amd64)**：</span><span class="sxs-lookup"><span data-stu-id="de40b-408">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="de40b-409">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-409">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="de40b-410">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-410">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="de40b-411">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-411">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="de40b-412">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="de40b-412">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="de40b-413">架构</span><span class="sxs-lookup"><span data-stu-id="de40b-413">Schema</span></span>

<span data-ttu-id="de40b-414">**IIS**</span><span class="sxs-lookup"><span data-stu-id="de40b-414">**IIS**</span></span>

   * <span data-ttu-id="de40b-415">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="de40b-415">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="de40b-416">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="de40b-416">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="de40b-417">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="de40b-417">**IIS Express**</span></span>

   * <span data-ttu-id="de40b-418">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="de40b-418">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="de40b-419">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="de40b-419">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="de40b-420">配置</span><span class="sxs-lookup"><span data-stu-id="de40b-420">Configuration</span></span>

<span data-ttu-id="de40b-421">**IIS**</span><span class="sxs-lookup"><span data-stu-id="de40b-421">**IIS**</span></span>

   * <span data-ttu-id="de40b-422">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="de40b-422">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="de40b-423">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="de40b-423">**IIS Express**</span></span>

   * <span data-ttu-id="de40b-424">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="de40b-424">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span></span>

<span data-ttu-id="de40b-425">可以通过在 applicationHost.config 文件中搜索 aspnetcore 找到这些文件。</span><span class="sxs-lookup"><span data-stu-id="de40b-425">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>
