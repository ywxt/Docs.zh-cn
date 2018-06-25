---
title: Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考
author: guardrex
description: 了解在 Azure 应用服务和 IIS 上托管 ASP.NET Core 应用的常见错误。
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 30b7f1d8e1cfdfd3d1db865ff428eb2094a84d32
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277314"
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a>Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考

作者：[Luke Latham](https://github.com/guardrex)

以下不是错误的完整列表。 如果遇到此处未列出的错误，请[打开一个新问题](https://github.com/aspnet/Docs/issues/new)，并随附详细说明以重现错误。

收集以下信息：

* 浏览器行为
* 应用程序事件日志条目
* ASP.NET Core 模块 stdout 日志条目

将该信息与以下常见错误进行比较。 如果找到匹配项，请按照故障排除建议进行操作。

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

## <a name="installer-unable-to-obtain-vc-redistributable"></a>安装程序无法获取 VC++ Redistributable

* **安装程序异常：** 0x80072efd 或 0x80072f76 - 未指定的错误

* **安装程序日志异常&#8224;：** 0x80072efd 或 0x80072f76 错误：未能执行 EXE 包

  &#8224;此日志位于 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log。

疑难解答：

* 如果在安装托管捆绑包时系统无法访问 Internet，则在系统阻止安装程序获取 Microsoft Visual C++ 2015 Redistributable 时会出现此异常。 可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53840)获取安装程序。 如果安装程序失败，服务器可能不会收到托管依赖框架的部署 (FDD) 所需的 .NET Core 运行时。 如果托管 FDD，请在“程序和功能”中确认安装了运行时。 如有必要，可从 [.NET All 下载](https://www.microsoft.com/net/download/all)获取运行时安装程序。 安装运行时后，重启系统，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS。

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a>OS 升级删除了 32 位 ASP.NET Core 模块

* **应用程序日志：** 未能加载模块 DLL C:\WINDOWS\system32\inetsrv\aspnetcore.dll。 该数据是个错误。

疑难解答：

* OS 升级期间不会保留 C:\Windows\SysWOW64\inetsrv 目录中的非 OS 文件。 如果在 OS 升级前已安装 ASP.NET Core 模块，且随后在 OS 升级后在 32 位模式下运行任何应用池，则会遇到此问题。 在 OS 升级后修复 ASP.NET Core 模块。 请参阅[安装 .NET Core 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)。 运行安装程序时，选择“修复”。

## <a name="platform-conflicts-with-rid"></a>平台与 RID 冲突

* **浏览器：** HTTP 错误 502.5 - 进程失败

* 应用程序日志：物理根路径为 'C:\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 未能通过 '"C:\\{PATH}{assembly}.{exe|dll}" ' 命令行启动进程，ErrorCode = '0x80004005 : ff。

* ASP.NET Core 模块日志：未经处理的异常: System.BadImageFormatException: 无法加载文件或程序集 '{assembly}.dll'。 试图加载的程序的格式不正确。

疑难解答：

* 确认应用在 Kestrel 上本地运行。 进程失败可能是由应用的内部问题导致的。 有关详细信息，请参阅[疑难解答](xref:host-and-deploy/iis/troubleshoot)。

* 确认 .csproj 中的 `<PlatformTarget>` 不与 RID 冲突。 例如，请勿通过使用 dotnet publish -c Release -r win10-x64 或通过在 .csproj 中将 `<RuntimeIdentifiers>` 设置为 `win10-x64` 来指定 `x86` 的 `<PlatformTarget>` 和以 `win10-x64` 的 RID 进行发布。 项目在不显示任何警告或错误的情况下发布，但会失败，且系统上出现上述记录的异常。

* 如果在升级应用和部署更新的程序集时，Azure 应用部署出现此异常，请从先前的部署中手动删除所有文件。 部署升级的应用时，延迟的不兼容程序集可能造成 `System.BadImageFormatException` 异常。

## <a name="uri-endpoint-wrong-or-stopped-website"></a>URI 终结点错误或网站已停止

* **浏览器：** ERR_CONNECTION_REFUSED

* **应用程序日志：** 没有任何条目

* **ASP.NET Core 模块日志：** 未创建日志文件

疑难解答：

* 确认正在使用的应用的 URI 端点是否正确。 检查绑定。

* 确认 IIS 网站未处于“已停止”状态。

## <a name="corewebengine-or-w3svc-server-features-disabled"></a>已禁用 CoreWebEngine 或 W3SVC 服务器功能

* **OS 异常：** 必须安装 IIS 7.0 CoreWebEngine 和 W3SVC 功能，以便使用 ASP.NET Core 模块。

疑难解答：

* 确认启用了适当的角色和功能。 请参阅 [IIS 配置](xref:host-and-deploy/iis/index#iis-configuration)。

## <a name="incorrect-website-physical-path-or-app-missing"></a>网站物理路径不正确或缺少应用

* **浏览器：** 403 禁止访问 - 访问被拒绝 --或者-- 403.14 禁止访问 - Web 服务器被配置为不列出此目录的内容。

* **应用程序日志：** 没有任何条目

* **ASP.NET Core 模块日志：** 未创建日志文件

疑难解答：

* 检查 IIS 网站的“基本设置”和物理应用文件夹。 确认应用所在的文件夹位于 IIS 网站的物理路径中。

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a>角色不正确、未安装模块或权限不正确

* **浏览器：** 500.19 内部服务器错误 - 无法访问请求的页面，因为该页面的相关配置数据无效。

* **应用程序日志：** 没有任何条目

* **ASP.NET Core 模块日志：** 未创建日志文件

疑难解答：

* 确认启用了适当的角色。 请参阅 [IIS 配置](xref:host-and-deploy/iis/index#iis-configuration)。

* 检查“程序和功能”，确认已安装Microsoft ASP.NET Core 模块。 如果已安装程序列表中没有 Microsoft ASP.NET Core 模块，请安装该模块。 请参阅[安装 .NET Core 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)。

* 请确保将“应用程序池” > “进程模型” > “标识”设置为 ApplicationPoolIdentity，或确保自定义标识具有访问应用部署文件夹的相应权限。

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a>processPath 不正确、缺少 PATH 变量、未安装托管捆绑包、未重启系统/IIS、未安装 VC++ Redistributable 或 dotnet.exe 访问冲突

* **浏览器：** HTTP 错误 502.5 - 进程失败

* 应用程序日志：物理根路径为 'C:\\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 未能通过 '".\{assembly}.exe" ' 命令行启动进程，ErrorCode = '0x80070002 : 0。

* **ASP.NET Core 模块日志：** 已创建日志文件，但该日志文件为空

疑难解答：

* 确认应用在 Kestrel 上本地运行。 进程失败可能是由应用的内部问题导致的。 有关详细信息，请参阅[疑难解答](xref:host-and-deploy/iis/troubleshoot)。

* 检查 web.config 中 `<aspNetCore>` 元素的 processPath 属性，对于依赖框架的部署 (FDD)，确保它为 dotnet，对于独立部署 (SCD)，确保它为 \{assembly}.exe。

* 对于 FDD，可能无法通过路径设置访问 dotnet.exe。 确认系统路径设置中存在 *C:\Program Files\dotnet\*。

* 对于 FDD，应用程序池的用户标识可能无法访问 dotnet.exe。 确认应用程序池用户标识具有访问 C:\Program Files\dotnet 目录的权限。 确认没有为应用池用户标识配置针对 C:\Program Files\dotnet 和应用目录的拒绝规则。

* 可能已部署 FDD 并安装了 .NET Core，但未重启 IIS。 重启服务器，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS。

* 可能已部署 FDD，但未在托管系统上安装 .NET Core 运行时。 如果尚未安装 .NET Core 运行时，则运行系统上的 **.NET Core 托管捆绑包安装程序**。 请参阅[安装 .NET Core 托管捆绑包](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)。 如果在没有 Internet 连接的情况下尝试在系统上安装 .NET Core 运行时，请从 [.NET All 下载](https://www.microsoft.com/net/download/all)获取运行时并运行托管捆绑包安装程序，以安装 ASP.NET Core 模块。 重启系统，或通过从命令提示符依次执行 net stop was /y 和 net start w3svc 来重启 IIS，完成安装。

* 可能已部署 FDD，但系统上未安装 Microsoft Visual C++ 2015 Redistributable (x64)。 可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53840)获取安装程序。

## <a name="incorrect-arguments-of-aspnetcore-element"></a>\<aspNetCore\> 元素的参数不正确

* **浏览器：** HTTP 错误 502.5 - 进程失败

* 应用程序日志：物理根路径为 'C:\\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 未能通过 '"dotnet" .\{assembly}.dll' 命令行启动进程，ErrorCode = '0x80004005 : 80008081。

* ASP.NET Core 模块日志：要执行的应用程序不存在: 'PATH\{assembly}.dll'

疑难解答：

* 确认应用在 Kestrel 上本地运行。 进程失败可能是由应用的内部问题导致的。 有关详细信息，请参阅[疑难解答](xref:host-and-deploy/iis/troubleshoot)。

* 检查 web.config 中 `<aspNetCore>` 元素的 arguments 属性，确认该属性：(a) 对于依赖框架的部署 (FDD) 为 \{assembly}.dll；或 (b) 对于独立部署 (SCD)，则为不存在、为空字符串 (arguments="")，或为应用参数列表 (arguments="arg1, arg2, ...")。

## <a name="missing-net-framework-version"></a>缺少 .NET Framework 版本

* **浏览器：** 502.3 错误网关 - 尝试路由请求时出现连接错误。

* 应用程序日志：ErrorCode = 其物理根路径为 'C:\\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 未能通过 '"dotnet" .\{assembly}.dll' 命令行启动进程，ErrorCode = '0x80004005 : 80008081。

* **ASP.NET Core 模块日志：** 缺少方法、文件或程序集异常。 在异常中指定的方法、文件或程序集是 .NET Framework 方法、文件或程序集。

疑难解答：

* 安装系统缺少的 .NET Framework 版本。

* 对于依赖框架的部署 (FDD)，确认已在系统上安装正确的运行时。 如果项目从 1.1 升级到 2.0、部署到托管系统，并且导致此异常，请确保 2.0 框架位于托管系统上。

## <a name="stopped-application-pool"></a>应用程序池已停止

* **浏览器：** 503 服务不可用

* **应用程序日志：** 没有任何条目

* **ASP.NET Core 模块日志：** 未创建日志文件

疑难解答

* 确认应用程序池未处于“已停止”状态。

## <a name="iis-integration-middleware-not-implemented"></a>未实现 IIS 集成中间件

* **浏览器：** HTTP 错误 502.5 - 进程失败

* 应用程序日志：物理根路径为 'C:\\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 通过 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 命令行创建了进程，但该进程出现故障、未响应或未在给定的端口 '{PORT}' 上侦听，ErrorCode = '0x800705b4'

* **ASP.NET Core 模块日志：** 已创建日志文件，且该日志文件显示正常操作。

疑难解答

* 确认应用在 Kestrel 上本地运行。 进程失败可能是由应用的内部问题导致的。 有关详细信息，请参阅[疑难解答](xref:host-and-deploy/iis/troubleshoot)。

* 确认以下项之一：
  * 通过调用应用的 `WebHostBuilder` 上的 `UseIISIntegration` 方法来引用 IIS 集成中间件 (ASP.NET Core 1.x)
  * 应用使用 `CreateDefaultBuilder` 方法 (ASP.NET Core 2.x)。
  
  有关详细信息，请参阅[在 ASP.NET Core 中托管](xref:fundamentals/host/index)。

## <a name="sub-application-includes-a-handlers-section"></a>子应用程序包括 \<handlers\> 部分

* **浏览器：** HTTP 错误 500.19 - 内部服务器错误

* **应用程序日志：** 没有任何条目

* **ASP.NET Core 模块日志：** 已创建日志文件，且该日志文件显示根应用程序的正常操作。 没有为子应用程序创建日志文件。

疑难解答

* 确认子应用的 web.config 文件不包括 `<handlers>` 部分。

## <a name="stdout-log-path-incorrect"></a>stdout 日志路径不正确

* 浏览器：应用程序正常响应。

* 应用程序日志：警告: 无法创建 stdoutLogFile \\?\C:\_apps\app_folder\bin\Release\netcoreapp2.0\win10-x64\publish\logs\path_doesnt_exist\stdout_8748_201831835937.log, ErrorCode = -2147024893。

* **ASP.NET Core 模块日志：** 未创建日志文件

疑难解答

* web.config 的 `<aspNetCore>` 元素中指定的 `stdoutLogFile` 路径不存在。 有关详细信息，请参阅 ASP.NET Core 模块配置参考主题的[日志创建和重定向](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)部分。

## <a name="application-configuration-general-issue"></a>应用程序配置常见问题

* **浏览器：** HTTP 错误 502.5 - 进程失败

* 应用程序日志：物理根路径为 'C:\\{PATH}\' 的应用程序 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' 通过 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 命令行创建了进程，但该进程出现故障、未响应或未在给定的端口 '{PORT}' 上侦听，ErrorCode = '0x800705b4'

* **ASP.NET Core 模块日志：** 已创建日志文件，但该日志文件为空

疑难解答

* 此一般异常表明进程未能启动，这很可能是由应用配置问题引起的。 请参阅[目录结构](xref:host-and-deploy/directory-structure)，确认应用的已部署文件和文件夹适当，应用的配置文件存在且包含适用于应用和环境的正确设置。 有关详细信息，请参阅[疑难解答](xref:host-and-deploy/iis/troubleshoot)。
