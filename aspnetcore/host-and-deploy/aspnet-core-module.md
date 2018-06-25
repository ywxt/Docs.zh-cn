---
title: ASP.NET Core 模块配置参考
author: guardrex
description: 了解如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 8d4283c61163a586557135fddfb85440251aaf29
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275614"
---
# <a name="aspnet-core-module-configuration-reference"></a>ASP.NET Core 模块配置参考

作者：[Luke Latham](https://github.com/guardrex)、[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Sourabh Shirhatti](https://twitter.com/sshirhatti)

本文档说明了如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。 有关 ASP.NET Core 模块简介和安装说明，请参阅 [ASP.NET Core 模块概述](xref:fundamentals/servers/aspnet-core-module)。

## <a name="configuration-with-webconfig"></a>web.config 的配置

在站点的 *web.config* 文件中使用 `system.webServer` 节点的 `aspNetCore` 部分配置 ASP.NET Core 模块。

以下 *web.config* 文件发布用于[依赖框架的部署](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)，并配置 ASP.NET Core 模块以处理站点请求：

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

以下 web.config 发布用于[独立部署](/dotnet/articles/core/deploying/#self-contained-deployments-scd)：

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

将应用部署为 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)时，`stdoutLogFile` 路径将设置为 `\\?\%home%\LogFiles\stdout`。 该路径会将 stdout 日志保存到 *LogFiles* 文件夹，该文件夹是由服务自动创建的位置。

有关在子应用中配置 *web.config* 文件的重要说明，请参阅[子应用程序配置](xref:host-and-deploy/iis/index#sub-application-configuration)。

### <a name="attributes-of-the-aspnetcore-element"></a>aspNetCore 元素的属性

::: moniker range="<= aspnetcore-2.0"
| 特性 | 描述 | 默认 |
| --------- | ----------- | :-----: |
| `arguments` | <p>可选的字符串属性。</p><p>processPath 中指定的可执行文件的参数。</p>| |
| `disableStartUpErrorPage` | “真”或“假”。</p><p>如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</p> | `false` |
| `forwardWindowsAuthToken` | “真”或“假”。</p><p>如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。 该进程负责在每个请求的此令牌上调用 CloseHandle。</p> | `true` |
| `processPath` | <p>必需的字符串属性。</p><p>为 HTTP 请求启动进程侦听的可执行文件的路径。 支持相对路径。 如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</p> | |
| `rapidFailsPerMinute` | <p>可选的整数属性。</p><p>指定允许 processPath 中指定的进程每分钟崩溃的次数。 如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</p> | `10` |
| `requestTimeout` | <p>可选的 timespan 属性。</p><p>指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</p><p>在 ASP.NET Core 2.0 或更早版本附带的 ASP.NET Core 模块版本中，必须仅使用整分钟数指定 `requestTimeout`，否则默认为 2 分钟。</p> | `00:02:00` |
| `shutdownTimeLimit` | <p>可选的整数属性。</p><p>检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</p> | `10` |
| `startupTimeLimit` | <p>可选的整数属性。</p><p>模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。 如果超出了此时间限制，模块将终止该进程。 模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</p> | `120` |
| `stdoutLogEnabled` | <p>可选布尔属性。</p><p>如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</p> | `false` |
| `stdoutLogFile` | <p>可选的字符串属性。</p><p>指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。 相对路径与站点根目录相对。 以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。 路径中提供的任何文件夹都必须存在，以便模块创建日志文件。 使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。 如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</p> | `aspnetcore-stdout` |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| 特性 | 描述 | 默认 |
| --------- | ----------- | :-----: |
| `arguments` | <p>可选的字符串属性。</p><p>processPath 中指定的可执行文件的参数。</p>| |
| `disableStartUpErrorPage` | “真”或“假”。</p><p>如果为 true，将禁止显示“502.5 - 进程失败”页面，而会优先显示 web.config 中配置的 502 状态代码页面。</p> | `false` |
| `forwardWindowsAuthToken` | “真”或“假”。</p><p>如果为 true，会将令牌作为每个请求的标头“MS-ASPNETCORE-WINAUTHTOKEN”，转发到在 %ASPNETCORE_PORT% 上侦听的子进程。 该进程负责在每个请求的此令牌上调用 CloseHandle。</p> | `true` |
| `processPath` | <p>必需的字符串属性。</p><p>为 HTTP 请求启动进程侦听的可执行文件的路径。 支持相对路径。 如果路径以 `.` 开头，则该路径被视为与站点根目录相对。</p> | |
| `rapidFailsPerMinute` | <p>可选的整数属性。</p><p>指定允许 processPath 中指定的进程每分钟崩溃的次数。 如果超出了此限制，模块将在剩余分钟数内停止启动该进程。</p> | `10` |
| `requestTimeout` | <p>可选的 timespan 属性。</p><p>指定 ASP.NET Core 模块等待来自 %ASPNETCORE_PORT% 上侦听的进程的响应的持续时间。</p><p>在 ASP.NET Core 2.1 或更高版本附带的 ASP.NET Core 模块版本中，使用小时数、分钟数和秒数指定 `requestTimeout`。</p> | `00:02:00` |
| `shutdownTimeLimit` | <p>可选的整数属性。</p><p>检测到 app_offline.htm 文件时，模块等待可执行文件正常关闭的持续时间（以秒为单位）。</p> | `10` |
| `startupTimeLimit` | <p>可选的整数属性。</p><p>模块等待可执行文件启动端口上侦听的进程的持续时间（以秒为单位）。 如果超出了此时间限制，模块将终止该进程。 模块在收到新请求时尝试重新启动该进程，并在收到后续传入请求时继续尝试重新启动该进程，除非应用在上一回滚分钟内无法启动 rapidFailsPerMinute 次。</p> | `120` |
| `stdoutLogEnabled` | <p>可选布尔属性。</p><p>如果为 true，processPath 中指定的 进程的 stdout 和 stderr 将重定向到 stdoutLogFile 中指定的文件。</p> | `false` |
| `stdoutLogFile` | <p>可选的字符串属性。</p><p>指定在其中记录 processPath 中指定进程的 stdout 和 stderr 的相对路径或绝对路径。 相对路径与站点根目录相对。 以 `.` 开头的任何路径均与站点根目录相对，所有其他路径被视为绝对路径。 路径中提供的任何文件夹都必须存在，以便模块创建日志文件。 使用下划线分隔符，将时间戳、进程 ID 和文件扩展名 (.log) 添加到 stdoutLogFile 路径的最后一段。 如果 `.\logs\stdout` 作为值提供，则在示例 stdout 日志使用进程 ID 1934 于 2018 年 2 月 5 日 19:41:32 保存时，将在 logs 文件夹中保存为 stdout_20180205194132_1934.log。</p> | `aspnetcore-stdout` |
::: moniker-end

### <a name="setting-environment-variables"></a>设置环境变量

可以为 `processPath` 属性中的进程指定环境变量。 使用 `environmentVariables` 集合元素的 `environmentVariable` 子元素指定环境变量。 本部分中设置的环境变量优先于系统环境变量。

以下示例设置了两个环境变量。 `ASPNETCORE_ENVIRONMENT` 将应用的环境配置为 `Development`。 开发人员可能会暂时在 web.config 文件中设置此值，以便在调试应用异常时强制加载[开发人员异常页面](xref:fundamentals/error-handling)。 `CONFIG_DIR` 是用户定义的环境变量的一个示例，其中开发人员已写入可在启动时读取值的代码以便形成用于加载应用配置文件的路径。

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
> 在不可访问不受信任的网络（如 Internet）的暂存服务器和测试服务器上，仅将 `ASPNETCORE_ENVIRONMENT` 环境变量设置为 `Development`。

## <a name="appofflinehtm"></a>app_offline.htm

如果在应用的根目录中检测到名为 “app_offline.htm”的文件，ASP.NET Core 模块将尝试正常关闭应用并停止处理传入请求。 如果应用在 `shutdownTimeLimit` 中定义的秒数之后仍在运行，ASP.NET Core 模块将终止正在运行的进程。

存在 app_offline.htm 文件时，ASP.NET Core 模块会通过发送回 app_offline.htm 文件的内容来响应请求。 删除 app_offline.htm 文件后，下一个请求将启动应用。

## <a name="start-up-error-page"></a>启动错误页面

如果 ASP.NET Core 模块无法启动后端进程或后端进程启动但无法在配置的端口上侦听，则将显示“502.5 进程失败”状态代码页面。 若要禁止显示此页面并还原为默认 IIS 502 状态代码页面，请使用 `disableStartUpErrorPage` 属性。 有关配置自定义错误消息的详细信息，请参阅 [HTTP 错误 `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/)。

![“502.5 进程失败”状态代码页面](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a>日志创建和重定向

如果已设置 `aspNetCore` 元素的 `stdoutLogEnabled` 和 `stdoutLogFile` 属性，ASP.NET Core 模块会将 stdout 和 stderr 日志重定向到磁盘。 `stdoutLogFile` 路径中的任何文件夹都必须存在，以便模块创建日志文件。 应用池必须对写入日志的位置具有写入权限（使用 `IIS AppPool\<app_pool_name>` 提供写入权限）。

日志不会旋转，除非回收/重新启动进程。 宿主负责限制日志占用的磁盘空间。

仅建议使用 stdout 日志来解决应用启动问题。 不要将 stdout 日志用于常规应用日志记录。 对于 ASP.NET Core 应用中的例程日志记录，使用限制日志文件大小和旋转日志的日志记录库。 有关详细信息，请参阅[第三方日志记录提供程序](xref:fundamentals/logging/index#third-party-logging-providers)。

创建日志文件时，将自动添加时间戳和文件扩展名。 日志文件名是通过将时间戳、进程 ID 和文件扩展名 (.log) 附加到由下划线分隔的 `stdoutLogFile` 路径的最后一段（通常为 stdout）组合而成的。 如果 `stdoutLogFile` 路径以 stdout 结尾，则 PID 为 1934 且于 2018 年 2 月 5 日 19:42:32 创建的应用的日志的文件名为 stdout_20180205194132_1934.log。

以下示例 `aspNetCore` 元素为 Azure 应用服务中托管的应用配置 stdout 日志记录。 本地日志记录可以接受本地路径或网络共享路径。 确认应用池用户标识是否已提供写入路径的权限。

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

有关 web.config 文件中的 `aspNetCore` 元素的示例，请参阅 [web.config 的配置](#configuration-with-webconfig)。

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a>代理配置使用 HTTP 协议和配对令牌

在 ASP.NET Core 模块和 Kestrel 之间创建的代理使用 HTTP 协议。 使用 HTTP 是一种性能优化，其中模块和 Kestrel 之间的流量发生于脱离网络接口的环回地址。 因此，不存在从脱离服务器的位置窃取模块和 Kestrel 之间的流量的风险。

配对令牌用于保证 Kestrel 收到的请求已由 IIS 代理且不来自某些其他源。 模块已创建配对令牌并将其设置到环境变量 (`ASPNETCORE_TOKEN`)。 此外，配对令牌还设置到每个代理请求的标头 (`MSAspNetCoreToken`)。 IIS 中间件检查它所接收的每个请求，以确认配对令牌标头值与环境变量值相匹配。 如果令牌值不匹配，则将记录请求并拒绝该请求。 无法从脱离服务器的位置访问配对令牌环境变量及模块和 Kestrel 之间的流量。 如果不知道配对令牌值，攻击者就无法提交绕过 IIS 中间件中的检查的请求。

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a>具有 IIS 共享配置的 ASP.NET Core 模块

ASP.NET Core 模块安装程序使用系统帐户的权限运行。 由于本地系统帐户没有对 IIS 共享配置所用的共享路径的修改权限，因此在尝试配置共享上的 applicationHost.config 中的模块设置时，安装程序将遇到拒绝访问错误。 使用 IIS 共享配置时，请执行以下步骤：

1. 禁用 IIS 共享配置。
1. 运行安装程序。
1. 将已更新的 applicationHost.config 文件导出到共享。
1. 重新启用 IIS 共享配置。

## <a name="module-version-and-hosting-bundle-installer-logs"></a>模块版本和托管捆绑安装程序日志

若要确定已安装 ASP.NET Core 模块的版本，请执行以下操作：

1. 在托管系统上，导航到 %windir%\System32\inetsrv。
1. 找到 aspnetcore.dll 文件。
1. 右键单击该文件，然后从上下文菜单中选择“属性”。
1. 选择“详细信息”选项卡。“文件版本”和“产品版本”表示模块的已安装版本。

在 C:\\Users\\%UserName%\\AppData\\Local\\Temp 中找到了模块的托管捆绑安装程序日志。该文件名为 dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log。

## <a name="module-schema-and-configuration-file-locations"></a>模块、架构和配置文件位置

### <a name="module"></a>模块

**IIS (x86/amd64)**：

   * %windir%\System32\inetsrv\aspnetcore.dll

   * %windir%\SysWOW64\inetsrv\aspnetcore.dll

**IIS Express (x86/amd64)**：

   * %ProgramFiles%\IIS Express\aspnetcore.dll

   * %ProgramFiles(x86)%\IIS Express\aspnetcore.dll

### <a name="schema"></a>架构

**IIS**

   * %windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml

**IIS Express**

   * %ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml

### <a name="configuration"></a>配置

**IIS**

   * %windir%\System32\inetsrv\config\applicationHost.config

**IIS Express**

   * .vs\config\applicationHost.config

可以通过在 applicationHost.config 文件中搜索 aspnetcore.dll 找到这些文件。 对于 IIS Express，默认情况下不会存在 applicationHost.config 文件。 在 Visual Studio 解决方案中启动任何 Web 应用项目时，将在 \<application_root>\\.vs\\config 中创建该文件。
