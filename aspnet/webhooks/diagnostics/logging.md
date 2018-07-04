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
# <a name="aspnet-webhooks-logging"></a>ASP.NET Webhook 日志记录

Microsoft ASP.NET Webhook 作为报告出现的问题的一种方法需要使用日志记录。 默认情况下使用写入日志[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)它们可以托管使用[跟踪侦听器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日志流。

在部署 Web 应用程序作为 Azure Web 应用，自动选取的日志，并可以与任何其他托管[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)日志记录。 有关详细信息，请参阅[启用 Azure 应用服务中的 web 应用的诊断日志记录](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

此外，日志可以获取直接来自在 Visual Studio 中所述[使用 Visual Studio 的 Azure 应用服务中 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="redirecting-logs"></a>将日志重定向

而不是写入到日志[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)，则可以提供一种备用日志记录实现，如记录到日志管理器直接[Log4Net](http://logging.apache.org/log4net/)和[NLog](http://nlog-project.org/). 只需提供的实现[ILogger](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)并将其注册到所选的依赖项注入引擎并将获取 Microsoft ASP.NET Webhook 选取。 请参阅[ASP.NET Web API 2 中的依赖关系注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)有关详细信息。
