---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
title: ASP.NET 承载选项 (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET web 应用程序通常设计、 创建，并在本地开发环境中测试和部署到生产环境 o...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 89a1d2bc-fdfd-4c5c-a3b0-49a08baaf63a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
msc.type: authoredcontent
ms.openlocfilehash: 3adad579c5893fb4f40e7043b9ece78740080f65
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833262"
---
<a name="aspnet-hosting-options-c"></a>ASP.NET 承载选项 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_cs.pdf)

> ASP.NET web 应用程序通常是设计、 创建，并在本地开发环境和需求后已准备好发布部署到生产环境中测试。 本教程提供部署过程的高级概述，并作为本系列教程简介。


## <a name="introduction"></a>介绍

Web 应用程序通常设计、 创建，并且仅在站点上工作的程序员可以访问的开发环境中进行测试。 准备好发布应用程序后，它被移动到生产环境中然后可以在 Internet 上的任何人访问站点。 此部署过程引入了一系列挑战：

- 生产环境中必须存在且必须进行恰当安装，才能部署 ASP.NET 应用程序;此外，在生产环境必须保持最新的最新安全修补程序。
- 正确的标记文件、 代码文件和支持文件集必须在开发环境中复制到生产环境。 对于数据驱动的应用程序，这可能需要复制的数据库架构和/或数据，以及。
- 可能有两种环境之间的配置差异。 在开发环境中使用的数据库连接字符串或电子邮件服务器将可能不同于生产环境。 更重要的是，应用程序的行为可能取决于环境。 例如，在开发过程中发生错误时可以在屏幕上，显示错误的详细信息，但在生产环境中出现错误时，应改为，显示用户友好的错误页和错误详细信息通过电子邮件发送给开发人员。

若要向用户第一次质询-设置和维护生产环境中的很多个人和企业外包到他们的生产环境*的 web 宿主提供程序*。 Web 宿主提供程序是一家公司管理你的名义在生产环境。 有无数的 web 宿主提供程序，每个都有不同的价格和服务级别;请参阅"查找 Web 主机 Provider"节中有关查找此类服务提供程序的提示。

这是一系列的教程，看看部署到生产环境中由 web 主机提供商托管的 ASP.NET web 应用程序时所涉及的步骤中的第一个。 在过去的这些教程将探讨如何使用：

- 需要什么文件部署到 web 宿主提供程序。
- 用于简化部署过程的工具。
- 如何将数据库部署。
- 部署使用的数据库的提示[基于 SQL 的成员身份和角色提供程序](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)，以及如何模拟生产环境中的网站管理工具。
- 顺利地更新在生产环境中的数据库，并且在开发过程中所做的更改的策略。
- 在生产环境，以及发生错误时通知开发人员的方法发生的日志记录错误的方法。

这些教程方便是简洁并提供引导你完成该过程以可视方式很大的屏幕截图的分步说明。 此开篇教程概述了查找 web 宿主提供程序的 ASP.NET 部署过程和建议。 让我们进入正题！

## <a name="an-overview-of-the-aspnet-deployment-process"></a>ASP.NET 部署过程的概述

简单地说，部署 ASP.NET 应用程序涉及以下三个步骤：

1. 在生产环境中配置 web 应用程序、 web 服务器和数据库。
2. 同步 ASP.NET 页面、 代码文件中中的程序集`Bin`文件夹，然后与 HTML 相关的支持文件，如 CSS 和 JavaScript 文件。
3. 同步数据库架构和/或数据。

Web 应用程序的配置信息通常位于`Web.config`文件，并包括 URL 重写规则和电子邮件服务器信息的数据库的连接字符串，错误处理条件。 通常，此信息是不同的开发与生产环境中相同的应用程序中的应用程序。 例如，开发应用程序时最好使用一个开发数据库，以便用户不在测试对生产数据库。 因此，数据库连接字符串通常开发和生产应用程序之间有所不同。 由于这些差异，部署的一部分涉及到对 web 应用程序的配置信息进行更改。

除了 web 应用程序的配置更改，第 1 步还可能需要配置 web 服务器和数据库。 例如，如果 ASP.NET 页创建或从 web 服务器上的目录中删除文件然后需要为 web 服务器将配置为允许这些文件系统修改。 同样，可能需要对数据库进行的权限或身份验证设置。


步骤 2 需要同步组基本的 ASP.NET 页面和开发和生产环境之间的支持文件。 这组特定的 ASP。NET 相关的文件，需要两个环境之间同步取决于项目在 Visual Studio 中，创建并在下一步的教程中，讨论的类型[*确定哪些文件需要部署*](determining-what-files-need-to-be-deployed-cs.md). 第三个和第四个教程- [*部署您的站点使用 FTP* ](deploying-your-site-using-an-ftp-client-cs.md)并[*部署您站点使用的 Visual Studio* ](deploying-your-site-using-visual-studio-cs.md) -检查不同的工具和技术用于同步这些文件。

构建数据驱动的应用程序有要使用的通常为两个数据库时： 一个用于开发，一个在生产环境。 在开发期间，开发数据库的架构可能会修改，以包含新表、 列、 存储的过程和触发器，或可能修改以删除或重命名现有数据库对象。 进行这些更改的时间，该应用程序部署到生产环境的时间，开发和生产数据库不同步。此异步功能需要在部署过程中解决。 在将来的教程中，将检查这些挑战。

## <a name="finding-a-web-host-provider"></a>查找 Web 主机提供商

ASP.NET 应用程序可以部署到了.NET Framework 和 Internet 信息服务 (IIS) 安装任何 web 服务器。 可以从您的个人计算机，托管站点，假设您有宽带连接到 Internet 并了解如何配置路由器，以允许传入 web 请求。 许多公司一样，也可以托管站点从企业内部网中的计算机。 但是，这些教程的重点托管你的网站与 web 宿主提供程序。

> [!NOTE]
> [IIS](https://www.iis.net/)是 Microsoft 的企业级 web 服务器。 它附带的 Windows，如 Windows Server 2008 和某些版本的 Windows Vista 非家用版本。 不需要安装 IIS 以在开发环境中，支持 ASP.NET 应用程序，如 Visual Studio 提供了 ASP.NET 开发 Web 服务器。 但是，ASP.NET 开发 Web 服务器仅接受本地连接，并因此不能在生产环境中使用。


可以将您的网站部署到 web 宿主提供程序之前必须先确定哪家公司有业务往来。 有无数的 web 托管公司在市场上;"web 托管公司"的搜索返回五个 100 万个结果。 如何查找一个最适合你？ 您最喜欢的搜索引擎是很好的起点，网站等一样[TopHosts](http://www.tophosts.com/)和[HostCritique](http://www.hostcritique.net/)，这比较和对比各种托管服务。 我还建议你的同事和同事寻求; 的任何建议建议在提出[承载 Open Forum](https://forums.asp.net/158.aspx)在[ASP.NET 论坛](https://forums.asp.net/)。

Web 托管公司通常提供共享的托管计划和专用托管计划。 与共享承载单个 web 服务器主机数十个，如果不是数百个不同的网站。 与专用托管你租约来自公司提供你的站点和站点单独的计算机。 共享的托管计划可能包括 ASP.NET 页中，使用 Microsoft Access 数据库，5 GB 的磁盘空间和 100 GB 每月的带宽流量的适用于每月 9.95 美元的功能的支持。 另一个共享的托管计划可能包括 ASP.NET 页中，19.95 美元每月的 Microsoft SQL Server 2008 数据库服务器、 10 GB 的磁盘空间和 250 GB 的带宽每月流量的访问的支持。 专用托管计划通常昂贵得多，成本计算数百美元每月，但产品/服务更好的性能和更多共享的控制权承载选项。 你选择哪些计划取决于你的预算、 多少流量收到你的网站，并希望在您的功能需要。

选择 web 宿主提供程序时的两个重要注意事项是客户服务和服务质量。 如果您有问题或配置问题，它需要多长从提交到 web 主机的技术支持问题，直到获得响应？ 公司的服务是如何可靠？ 他们经常有数据库停机吗？ 何种频率 does 则其电子邮件服务器处于脱机状态？ 始终可以让一家公司可以提供有关其正常运行时间的详细信息和查询其客户服务策略，但更有效的办法是要求当前和过去的客户，可以通过在线论坛、 新闻组和电子邮件列表服务执行此操作的反馈.

> [!NOTE]
> 一些 web 托管公司将其业务关注特定的技术堆栈，如.NET 或[LAMP](http://en.wikipedia.org/wiki/LAMP_stack) (**L** inux，**一个**pache， **M**ySQL，并**P** HP)，因此请确保您选择的公司托管的 ASP.NET 应用程序。 此外检查以确保它们支持的 ASP.NET 用来生成应用程序的版本。 如果您正在构建数据驱动的应用程序，请确保 web 主机提供相同的数据库服务器和正在使用的版本。


## <a name="summary"></a>总结

ASP.NET web 应用程序通常是设计、 创建，并在本地开发环境中测试。 准备好发布一个版本后，则将它移到生产环境。 虽然可以在个人计算机上或在公司内部的服务器上托管 ASP.NET 网站，许多企业和个人选择将外包其托管到 web 宿主提供程序。

本教程系列将检查用于部署 ASP.NET 应用程序到 web 主机提供商，了解常见的难题的步骤。 本教程提供 ASP.NET 部署过程的高级概述，并为提示提供了用于查找合适的 web 宿主提供程序。 下一步的教程讨论与 ASP.NET 相关的文件需要部署你的网站时将复制到生产环境。

快乐编程 ！

### <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [下一篇](determining-what-files-need-to-be-deployed-cs.md)
