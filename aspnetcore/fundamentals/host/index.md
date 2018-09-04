---
title: 在 ASP.NET Core 中托管
author: guardrex
description: 了解有关 ASP.NET Core Web 主机和 .NET 通用主机的信息，它们负责应用启动和生存期管理。
ms.author: riande
ms.custom: mvc
ms.date: 08/28/2018
uid: fundamentals/host/index
ms.openlocfilehash: 9927722b5080beb94e5628d9e7b54e6d50a5bff8
ms.sourcegitcommit: a669c4e3f42e387e214a354ac4143555602e6f66
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43336045"
---
# <a name="host-in-aspnet-core"></a>在 ASP.NET Core 中托管

.NET 应用配置和启动主机。 主机负责应用程序启动和生存期管理。 两个主机 API 可供使用：

* [Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。
* [通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。 在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。 通用主机最终将取代 Web 主机。

为托管 ASP.NET Core Web 应用，开发人员应使用基于 <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder> 的 Web 主机。 为托管非 Web 应用，开发人员应使用基于 <xref:Microsoft.Extensions.Hosting.HostBuilder> 的通用主机。

<xref:fundamentals/host/hosted-services>  
了解如何在 ASP.NET Core 中使用托管服务实现后台任务。

<xref:fundamentals/configuration/platform-specific-configuration>  
了解如何使用 <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> 实现从引用或未引用程序集增强 ASP.NET Core 应用。
