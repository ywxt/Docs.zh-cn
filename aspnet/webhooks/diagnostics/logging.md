---
uid: webhooks/diagnostics/logging
title: ASP.NET Webhook 日志记录 |Microsoft Docs
author: rick-anderson
description: 如何执行 ASP.NET Webhook 中的日志记录。
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.technology: ''
ms.openlocfilehash: 5501d250ea6dd86c0cfddec8d9941ec16b4f57ba
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364101"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="7fb6f-103">ASP.NET Webhook 日志记录</span><span class="sxs-lookup"><span data-stu-id="7fb6f-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="7fb6f-104">Microsoft ASP.NET Webhook 作为报告出现的问题的一种方法需要使用日志记录。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="7fb6f-105">默认情况下使用写入日志[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)它们可以托管使用[跟踪侦听器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日志流。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="7fb6f-106">在部署 Web 应用程序作为 Azure Web 应用，自动选取的日志，并可以与任何其他托管[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)日志记录。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="7fb6f-107">有关详细信息，请参阅[启用 Azure 应用服务中的 web 应用的诊断日志记录](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="7fb6f-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="7fb6f-108">此外，日志可以获取直接来自在 Visual Studio 中所述[使用 Visual Studio 的 Azure 应用服务中 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="7fb6f-109">将日志重定向</span><span class="sxs-lookup"><span data-stu-id="7fb6f-109">Redirecting Logs</span></span>

<span data-ttu-id="7fb6f-110">而不是写入到日志[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)，则可以提供一种备用日志记录实现，如记录到日志管理器直接[Log4Net](http://logging.apache.org/log4net/)和[NLog](http://nlog-project.org/).</span><span class="sxs-lookup"><span data-stu-id="7fb6f-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="7fb6f-111">只需提供的实现[ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)并将其注册到所选的依赖项注入引擎并将获取 Microsoft ASP.NET Webhook 选取。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="7fb6f-112">请参阅[ASP.NET Web API 2 中的依赖关系注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="7fb6f-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
