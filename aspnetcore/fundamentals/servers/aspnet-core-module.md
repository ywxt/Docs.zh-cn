---
title: ASP.NET Core 模块
author: guardrex
description: 了解 ASP.NET Core 模块如何使 Kestrel Web 服务器可以使用 IIS 或 IIS Express。
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/30/2018
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: d3f3a42dd7aebc425905b865376a584bcf0e5153
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861454"
---
# <a name="aspnet-core-module"></a>ASP.NET Core 模块

作者：[Tom Dykstra](https://github.com/tdykstra)、[Rick Strahl](https://github.com/RickStrahl) 和 [Chris Ross](https://github.com/Tratcher)

::: moniker range=">= aspnetcore-2.2"

ASP.NET Core 模块允许 ASP.NET Core 应用在 IIS 工作进程中运行（进程内）或在采用反向代理配置的 IIS 后运行（进程外）。 IIS 具有高级 Web 应用安全性和易管理性。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

ASP.NET Core 模块允许 ASP.NET Core 应用在采用反向代理配置的 IIS 后运行。 IIS 具有高级 Web 应用安全性和易管理性。

::: moniker-end

受支持的 Windows 版本：

* Windows 7 或更高版本
* Windows Server 2008 R2 或更高版本

::: moniker range=">= aspnetcore-2.2"

正在进行托管时，该模块会使用 IIS 进程内服务器实现，即 IIS HTTP 服务器 (`IISHttpServer`)。

在进程外托管时，该模块仅适用于 Kestrel。 该模块与 [HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）不兼容。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

该模块仅适用于 Kestrel。 该模块与 [HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）不兼容。

::: moniker-end

## <a name="aspnet-core-module-description"></a>ASP.NET Core 模块说明

::: moniker range=">= aspnetcore-2.2"

ASP.NET Core 模块是插入 IIS 管道的本机 IIS 模块，用于：

* 在 IIS 工作进程 (`w3wp.exe`) 内托管 ASP.NET Core 应用，称为[进程内托管模型](#in-process-hosting-model)。

* 将 Web 请求转发到运行 [Kestrel 服务器](xref:fundamentals/servers/kestrel)的后端 ASP.NET Core 应用，称为[进程外托管模型](#out-of-process-hosting-model)。

### <a name="in-process-hosting-model"></a>进程内托管模型

使用进程内托管，ASP.NET Core 在与其 IIS 工作进程相同的进程中运行。 这样可以避免在使用进程外托管模型时通过环回适配器代理请求的性能损失。 IIS 使用 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 处理进程管理。

ASP.NET Core 模块：

* 执行应用初始化。
  * 加载 [CoreCLR](/dotnet/standard/glossary#coreclr)。
  * 调用 `Program.Main`。
* 处理 IIS 本机请求的生存期。

下图说明了 IIS、ASP.NET Core 模块和进程内托管的应用之间的关系：

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-inprocess.png)

请求从 Web 到达内核模式 HTTP.sys 驱动程序。 驱动程序将本机请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。 该模块接收本机请求，并将它传递给 IIS HTTP 服务器 (`IISHttpServer`)。 IIS HTTP 服务器是将请求从本机转换为托管的 IIS 进程内服务器实现。

IIS HTTP 服务器处理请求之后，请求会被推送到 ASP.NET Core 中间件管道中。 中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。 应用的响应传递回 IIS，IIS 将响应推送回发起请求的客户端。

### <a name="out-of-process-hosting-model"></a>进程外托管模型

由于 ASP.NET Core 应用在独立于 IIS 工作进程的进程中运行，因此该模块会处理进程管理。 该模块在第一个请求到达时启动 ASP.NET Core 应用的进程，并在应用关闭或崩溃时重新启动该应用。 这基本上与在 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 托管的进程内运行的应用中出现的行为相同。

下图说明了 IIS、ASP.NET Core 模块和进程外托管的应用之间的关系：

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-outofprocess.png)

请求从 Web 到达内核模式 HTTP.sys 驱动程序。 驱动程序将请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。 该模块将该请求转发到应用的随机端口（非端口 80/443）上的 Kestrel。

该模块在启动时通过环境变量指定端口，IIS 集成中间件将服务器配置为侦听 `http://localhost:{port}`。 执行其他检查，拒绝不是来自该模块的请求。 该模块不支持 HTTPS 转发，因此即使请求由 IIS 通过 HTTPS 接收，它们还是通过 HTTP 转发。

Kestrel 从模块获取请求后，请求会被推送到 ASP.NET Core 中间件管道中。 中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。 IIS 集成添加的中间件会将方案、远程 IP 和 pathbase 更新到帐户以将请求转发到 Kestrel。 应用的响应传递回 IIS，IIS 将响应推送回发起请求的 HTTP 客户端。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

ASP.NET Core 模块是插入 IIS 管道的本机 IIS 模块，用于将 Web 请求转发到后端 ASP.NET Core 应用。

由于 ASP.NET Core 应用在独立于 IIS 辅助进程的进程中运行，因此该模块还处理进程管理。 该模块在第一个请求到达时启动 ASP.NET Core 应用的进程，并在应用崩溃时重新启动该应用。 这基本上与在 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 托管的 IIS 中在进程内运行的 ASP.NET 4.x 应用中出现的行为相同。

下图说明了 IIS、ASP.NET Core 模块和应用之间的关系：

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-outofprocess.png)

请求从 Web 到达内核模式 HTTP.sys 驱动程序。 驱动程序将请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。 该模块将该请求转发到应用的随机端口（非端口 80/443）上的 Kestrel。

该模块在启动时通过环境变量指定端口，IIS 集成中间件将服务器配置为侦听 `http://localhost:{port}`。 执行其他检查，拒绝不是来自该模块的请求。 该模块不支持 HTTPS 转发，因此即使请求由 IIS 通过 HTTPS 接收，它们还是通过 HTTP 转发。

Kestrel 从模块获取请求后，请求会被推送到 ASP.NET Core 中间件管道中。 中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。 IIS 集成添加的中间件会将方案、远程 IP 和 pathbase 更新到帐户以将请求转发到 Kestrel。 应用的响应传递回 IIS，IIS 将响应推送回发起请求的 HTTP 客户端。

::: moniker-end

许多本机模块（如 Windows 身份验证）仍处于活动状态。 要详细了解随该模块活动的 IIS 模块，请参阅 <xref:host-and-deploy/iis/modules>。

ASP.NET Core 模块具有一些其他功能。 该模块可以：

* 为工作进程设置环境变量。
* 将 stdout 输出记录到文件存储器，以解决启动问题。
* 转发 Windows 身份验证令牌。

## <a name="how-to-install-and-use-the-aspnet-core-module"></a>如何安装和使用 ASP.NET Core 模块

有关如何安装和使用 ASP.NET Core 模块的详细说明，请参阅 <xref:host-and-deploy/iis/index>。 有关配置模块的信息，请参阅 <xref:host-and-deploy/aspnet-core-module>。

## <a name="additional-resources"></a>其他资源

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* [ASP.NET Core 模块 GitHub 存储库（源代码）](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
