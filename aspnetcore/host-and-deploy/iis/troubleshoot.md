---
title: "解决在 IIS 上的 ASP.NET 核心"
author: guardrex
description: "了解如何使用 IIS 的 ASP.NET Core 应用的部署诊断问题。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: c68070a9cba5667504d1ad4927b02b73f83e6573
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>解决在 IIS 上的 ASP.NET 核心

作者：[Luke Latham](https://github.com/guardrex)

诊断问题 IIS 部署：

* 查看浏览器输出。
* 通过“事件查看器”检查系统的“应用程序”日志。
* 启用 `stdout` 日志记录 ASP.NET Core 模块日志位于 web.config 中 `<aspNetCore>` 元素的 stdoutLogFile 属性提供的路径上。属性值中提供的路径上的任何文件夹都必须存在于部署中。 设置*stdoutLogEnabled*到`true`。 应用程序使用`Microsoft.NET.Sdk.Web`SDK 创建*web.config*文件默认*stdoutLogEnabled*将设置为`false`，请手动提供*web.config*文件或修改文件，以便启用`stdout`日志记录。

使用来自与这些三个源信息[常见错误引用主题](xref:host-and-deploy/azure-iis-errors-reference)以确定问题。 请按照用于解决此问题的故障排除建议。

多种常见错误只有在经过模块的 startupTimeLimit（默认值：120 秒）和 startupRetryCount（默认值：2 次）后，才会在浏览器、应用程序日志和 ASP.NET Core 模块日志中显示。 因此，请先等足六分钟，然后再推断出模块无法为应用启动进程。

一种快速确定应用是否正常工作的方法是直接在 Kestrel 上运行应用。 如果应用程序作为发布[framework 相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，执行`dotnet <assembly_name>.dll`在部署文件夹中，这是 IIS 到应用的物理路径。 如果应用程序作为发布[独立的部署](/dotnet/core/deploying/#self-contained-deployments-scd)中运行应用程序的可执行文件直接从命令提示符处， `<assembly_name>.exe`，部署文件夹中。 如果 Kestrel 正在侦听默认端口 5000，应用程序应该可以在获得`http://localhost:5000/`。 如果应用程序通常响应 Kestrel 终结点地址，该问题更可能是相关的反向代理配置和不太可能在应用内。

若要确定反向代理是否正常工作的一种方法是针对样式表、 脚本或从应用程序的静态文件中的映像执行简单的静态文件请求*wwwroot*使用[静态文件中间件](xref:fundamentals/static-files). 如果应用程序可以为静态文件提供服务，但失败 MVC 视图和其他终结点，该问题是不太可能相关的反向代理配置，并且更可能在应用程序 （如 MVC 路由或 500 内部服务器错误）。

环境变量时 Kestrel 后面 IIS 正常启动，但应用程序不会在系统上运行本地成功运行后，可以临时添加到*web.config*设置`ASPNETCORE_ENVIRONMENT`到`Development`。 只要环境不重写应用程序启动时，设置环境变量允许[开发人员异常页](xref:fundamentals/error-handling)显示应用程序运行时。 设置环境变量中的`ASPNETCORE_ENVIRONMENT`以这种方式仅建议在测试过渡/服务器不公开到 Internet。 请务必删除从该环境变量*web.config*文件完成。 有关如何设置环境变量通过*web.config*，请参阅[environmentVariables 子元素的 aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)。

在大多数情况下，启用应用程序日志记录有助于排查应用问题或反向代理问题。 有关详细信息，请参阅[日志记录](xref:fundamentals/logging/index)。

最后一项故障排除提示将在应用内的开发计算机或包版本上的.NET 核心 SDK 与无法升级或者后运行的应用。 在某些情况下，不同的包可能在执行主要升级时中断应用。 可通过解决这些问题的大多数：

* 删除`bin`和`obj`的项目文件夹。
* 清除包缓存在`%UserProfile%\.nuget\packages\`和`%LocalAppData%\Nuget\v3-cache`。
* 还原和重新生成项目。
* 确认已完全重新部署应用程序之前删除以前部署到服务器上。

> [!TIP]
> 清除包缓存的简便方法是执行`dotnet nuget locals all --clear`从命令提示符。
> 
> 清除包缓存还可通过使用[nuget.exe](https://www.nuget.org/downloads)工具并执行命令`nuget locals all -clear`。 *nuget.exe*不与 Windows 10 的捆绑的安装，并且必须单独获取从 NuGet 网站。
<!--
> [!TIP]
> A convenient way to clear package caches is to:
>
> * Obtain the *NuGet.exe* tool from [NuGet.org](https://www.nuget.org/).
> * Add the path to *NuGet.exe* to the system PATH.
> * Execute `nuget locals all -clear` from a command prompt.
>
> Alternatively, execute `dotnet nuget locals all --clear` from a command prompt without obtaining *NuGet.exe*. -->

## <a name="additional-resources"></a>其他资源

* [Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)
