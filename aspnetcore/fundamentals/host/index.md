---
title: 在 ASP.NET Core 中托管
author: guardrex
description: 了解有关 ASP.NET Core Web 主机和 .NET 通用主机的信息，它们负责应用启动和生存期管理。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/index
ms.openlocfilehash: 7f8ccff7e3da93d6e617505ac93fafc3a82ed880
ms.sourcegitcommit: 63fb07fb3f71b32daf2c9466e132f2e7cc617163
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2018
ms.locfileid: "35252004"
---
# <a name="host-in-aspnet-core"></a>在 ASP.NET Core 中托管

.NET 应用配置和启动主机。 主机负责应用程序启动和生存期管理。 两个主机 API 可供使用：

* [Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。
* [通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。 在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。 通用主机最终将取代 Web 主机。

为托管 ASP.NET Core *Web 应用*，开发者应使用基于 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 的 Web 主机。 为托管*非 Web 应用*，开发者应使用基于 [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) 的通用主机。
