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
ms.openlocfilehash: 7ad059e39866f59040c12b7ac15e9fa3405a9aad
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="host-in-aspnet-core"></a>在 ASP.NET Core 中托管

.NET 应用配置和启动主机。 主机负责应用程序启动和生存期管理。 两个主机 API 可供使用：

* [Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。
* [通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。 在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。 通用主机最终将取代 Web 主机。

目前，开发人员应基于 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 使用 [Web 主机](xref:fundamentals/host/web-host)，来托管 ASP.NET Core 应用。
