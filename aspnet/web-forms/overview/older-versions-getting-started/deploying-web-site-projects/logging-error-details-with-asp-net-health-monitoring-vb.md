---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
title: ASP.NET 运行状况监视 (VB) 的日志记录错误详细信息 |Microsoft Docs
author: rick-anderson
description: Microsoft 的运行状况监控系统提供了简单且可自定义的方式记录各种 web 事件，包括未经处理的异常。 本教程介绍如何对...
ms.author: aspnetcontent
ms.date: 06/09/2009
ms.assetid: 09a6c74e-936a-4c04-8547-5bb313a4e4a3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
msc.type: authoredcontent
ms.openlocfilehash: a19c1dc6ad5b3b45501befded4d8f14f7549b019
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809918"
---
<a name="logging-error-details-with-aspnet-health-monitoring-vb"></a>ASP.NET 运行状况监视 (VB) 的日志记录错误详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_VB.zip)或[下载 PDF](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_vb.pdf)

> Microsoft 的运行状况监控系统提供了简单且可自定义的方式记录各种 web 事件，包括未经处理的异常。 本教程将指导完成未经处理的异常记录到数据库并通知通过电子邮件的开发人员设置运行状况监控系统。


## <a name="introduction"></a>介绍

日志记录是一个有用的工具用于监视部署的应用程序的运行状况和诊断可能会出现任何问题。 特别是，务必记录发生在已部署的应用程序中，以便它们可以纠正的错误。 `Error` ASP.NET 应用程序; 中出现未处理的异常时将引发事件[前面的教程](processing-unhandled-exceptions-vb.md)介绍了如何通知错误的开发人员并通过创建的事件处理程序记录其详细信息`Error`事件。 但是，创建`Error`事件处理程序来记录错误的详细信息并通知开发人员是不必要的因为可以由 ASP 执行此任务。NET 的*运行状况监控系统*。

运行状况监控系统在 ASP.NET 2.0 中引入，它旨在监视已部署的 ASP.NET 应用程序的运行状况，通过在应用程序或请求的生存期期间发生的日志记录事件。 记录运行状况监控系统的事件嘿 *运行状况监视事件*或*Web 事件*，并且包括：

- 应用程序生存期事件，例如当应用程序启动或停止
- 安全事件，其中包括登录尝试失败和失败的 URL 授权请求
- 应用程序错误，包括未经处理的异常，异常、 请求验证异常和其他类型的错误中的编译错误，分析的视图状态。

当运行状况监视事件引发时它可以记录到任意数量的指定*日志源*。 运行状况监控系统附带 Web 事件记录到 Windows 事件日志中，或通过电子邮件，其他项中的 Microsoft SQL Server 数据库的日志源。 此外可以创建自己的日志源。

中定义的事件日志的运行状况监控系统，以及使用，日志源`Web.config`。 借助几行配置标记可以使用运行状况监视所有未经处理的异常记录到数据库并通知你通过电子邮件的异常。

## <a name="exploring-the-health-monitoring-systems-configuration"></a>探索的运行状况监视系统的配置

运行状况监视系统的行为由其配置信息，它位于[`<healthMonitoring>`元素](https://msdn.microsoft.com/library/2fwh2ss9.aspx)中`Web.config`。 此外，此配置节定义信息的以下 3 个重要部分：

1. 运行状况监视事件，当引发时，应记录
2. 日志源和
3. 如何将每个运行状况监视事件 (1) 中定义映射到的日志源中 (2) 定义。

通过三个子配置元素指定此信息： [ `<eventMappings>` ](https://msdn.microsoft.com/library/yc5yk01w.aspx)， [ `<providers>` ](https://msdn.microsoft.com/library/zaa41kz1.aspx)，以及[ `<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)分别。

默认运行状况监控系统配置信息可在`Web.config`文件中`%WINDIR%\Microsoft.NET\Framework\version\CONFIG`文件夹。 此默认的配置信息，为简便起见，删除一些标记如下所示：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample1.xml)]

监视感兴趣的事件定义中的运行状况`<eventMappings>`元素，从而使运行状况监视事件的类用户友好名称。 在上面，标记`<eventMappings>`元素指定的用户友好名称"的所有错误"的运行状况监视事件的类型`WebBaseErrorEvent`和名称"失败审核"运行状况监视事件的类型为`WebFailureAuditEvent`。

`<providers>`元素定义为他们提供用户友好名称和指定的任何日志特定于源的配置信息的日志源。 第一个`<add>`元素定义记录指定的运行状况监视事件使用的"EventLogProvider"提供程序`EventLogWebEventProvider`类。 `EventLogWebEventProvider`类将事件记录到 Windows 事件日志。 第二个`<add>`元素定义事件记录到通过在 Microsoft SQL Server 数据库的"SqlWebEventProvider"提供程序`SqlWebEventProvider`类。 "SqlWebEventProvider"配置指定数据库的连接字符串 (`connectionStringName`) 以及其他配置选项。

`<rules>`元素将映射中指定的事件`<eventMappings>`元素中的日志源`<providers>`元素。 默认情况下，ASP.NET web 应用程序记录所有未处理的异常和审核故障到 Windows 事件日志中。

## <a name="logging-events-to-a-database"></a>到数据库的日志记录事件

运行状况监视系统的默认配置可以自定义基于 web 的应用程序的 web 应用程序通过添加`<healthMonitoring>`应用程序的部分`Web.config`文件。 可以包含其他元素中的`<eventMappings>`， `<providers>`，并`<rules>`部分中的，通过使用`<add>`元素。 若要删除设置默认配置，请使用从`<remove>`元素或使用`<clear />`从上述部分之一删除所有默认值。 让我们书评 web 应用程序配置为记录所有未经处理的异常到 Microsoft SQL Server 数据库使用`SqlWebEventProvider`类。

`SqlWebEventProvider`类是运行状况监控系统的一部分，并记录运行状况监视事件到指定的 SQL Server 数据库。 `SqlWebEventProvider`类期望指定的数据库包括一个名为的存储的过程`aspnet_WebEvent_LogEvent`。 此存储的过程传递事件的详细信息，肩负存储事件的详细信息。 好消息是您不需要创建此存储过程，也不存储事件的详细信息的表。 可以将这些对象添加到你的数据库使用`aspnet_regsql.exe`工具。

> [!NOTE]
> `aspnet_regsql.exe`工具已返回中所述[*配置网站，使用应用程序服务*教程](configuring-a-website-that-uses-application-services-vb.md)时，我们添加了对 ASP 支持。NET 的应用程序服务。 因此，书评网站的数据库已包含`aspnet_WebEvent_LogEvent`存储过程，将存储到名为的表的事件信息`aspnet_WebEvent_Events`。


必需执行的存储的过程和表添加到你的数据库后，所有的就是以指示运行状况监视到数据库中记录所有未经处理的异常。 完成此操作通过将以下标记添加到你的网站`Web.config`文件：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample2.xml)]

运行状况监视上面使用的配置标记`<clear />`擦除预定义的运行状况监视中的配置信息的元素`<eventMappings>`， `<providers>`，和`<rules>`部分。 然后，它将单个条目添加到以下各节。

- `<eventMappings>`元素定义单一的运行状况监视感兴趣的名为"所有"的错误时出现未处理的异常，将引发的事件。
- `<providers>`元素定义一个名为"SqlWebEventProvider"使用的单个日志源`SqlWebEventProvider`类。 `connectionStringName`属性已设置为"ReviewsConnectionString"，是我们连接的名称中定义的字符串`<connectionStrings>`部分。
- 最后，&lt;规则&gt;元素指示的"所有错误"事件怎样时它应记录的使用"SqlWebEventProvider"提供程序。

此配置信息指示运行状况监视系统到书评数据库记录所有未经处理的异常。

> [!NOTE]
> `WebBaseErrorEvent`服务器错误只引发事件; 它不会引发 HTTP 错误，例如找不到的 ASP.NET 资源的请求。 这不同于的行为`HttpApplication`类的`Error`事件，该服务器和 HTTP 错误引发事件。


若要查看运行状况监视系统中操作，请访问网站和生成运行时错误，请访问`Genre.aspx?ID=foo`。 您会看到相应的错误页的异常详细信息黄色屏幕死机 （当访问本地） 或自定义错误页上 （当访问在生产环境中的站点）。 在后台运行状况监控系统记录到数据库中的错误信息。 应在一条记录`aspnet_WebEvent_Events`表 (请参阅**图 1**); 此记录包含有关刚刚发生运行时错误的信息。

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image1.png)

**图 1**： 错误详细信息记录到`aspnet_WebEvent_Events`表  
([单击此项可查看原尺寸图像](logging-error-details-with-asp-net-health-monitoring-vb/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>在网页中显示错误日志

使用网站的当前配置运行状况监控系统数据库中记录所有未经处理的异常。 但是，运行状况监视不提供任何机制来查看通过网页错误日志。 但是，您可以构建 ASP.NET 页显示来自数据库的此信息。 （我们将看到暂时不可用，您可以选择将发送给你的电子邮件中的错误详细信息。）

如果创建此类页时，请确保您采取措施来仅允许授权的用户以查看错误详细信息。 如果您的网站已部署了用户帐户，则可以使用 URL 授权规则来限制对页向特定用户或角色的访问。 有关如何授予或限制对网页根据登录用户的访问的详细信息，请参阅我[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

> [!NOTE]
> 后续教程探讨了名为 ELMAH 备用错误日志记录和通知系统。 Elmah 却包含内置的机制来查看错误日志从这两个网页和 RSS 源的形式。


## <a name="logging-events-to-email"></a>日志事件记录到电子邮件

运行状况监控系统包括到电子邮件"日志"事件日志源提供程序。 日志源包含相同的信息记录到电子邮件正文中的数据库。 此日志源可用于在某个运行状况监视事件发生时通知开发人员。

让我们更新网站的配置，以便我们收到的电子邮件，无论异常何时发生书评。 若要实现此目的，我们需要执行三个任务：

1. 配置 ASP.NET web 应用程序发送电子邮件。 这通过指定如何通过发送电子邮件实现`<system.net>`配置元素。 有关详细信息发送电子邮件中的 ASP.NET 应用程序的消息指[在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)和[System.Net.Mail 常见问题解答](http://systemnetmail.com/)。
2. 注册电子邮件日志源提供程序中的`<providers>`元素，并
3. 将条目添加到`<rules>`映射到在步骤 (2) 中添加的日志源提供程序的"所有错误"事件的元素。

运行状况监控系统包括两个电子邮件日志源提供程序类：`SimpleMailWebEventProvider`和`TemplatedMailWebEventProvider`。 [ `SimpleMailWebEventProvider`类](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx)发送纯文本电子邮件消息，其中包含事件详细信息和提供的电子邮件正文的小自定义。 与[`TemplatedMailWebEventProvider`类](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)指定 ASP.NET 页面的呈现的标记用作电子邮件正文。 [ `TemplatedMailWebEventProvider`类](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)可提供很好地控制更高版本的内容和格式的电子邮件，但需要更多前期工作，因为您必须创建生成电子邮件消息的正文的 ASP.NET 页。 本教程重点介绍使用`SimpleMailWebEventProvider`类。

更新监视系统的运行状况`<providers>`中的元素`Web.config`文件以包含的日志源`SimpleMailWebEventProvider`类：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample3.xml)]

上面的标记使用`SimpleMailWebEventProvider`类作为日志源提供程序，并将其分配的友好名称"EmailWebEventProvider"。 此外，`<add>`属性包含其他配置选项，例如收件人和从电子邮件地址。

与电子邮件日志源定义，剩下的就是以指示运行状况监视系统使用此源用于"记录"未经处理的异常。 这通过添加新的规则中实现`<rules>`部分：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample4.xml)]

`<rules>`部分现在包括两个规则。 第一个名为"所有错误到电子邮件"，将所有未经处理的异常发送到"EmailWebEventProvider"日志源。 此规则的效果在网站上的错误的详细信息发送到指定的地址。 "到数据库的所有错误"规则的站点数据库中记录错误详细信息。 因此，每当未处理的异常发生时在站点上其详细信息都记录到数据库并且发送到指定的电子邮件地址。

**图 2**显示了生成的电子邮件`SimpleMailWebEventProvider`类访问时`Genre.aspx?ID=foo`。

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image4.png)

**图 2**: 电子邮件消息中发送错误详细信息  
([单击此项可查看原尺寸图像](logging-error-details-with-asp-net-health-monitoring-vb/_static/image6.png))

## <a name="summary"></a>总结

ASP.NET 运行状况监视系统，旨在允许管理员监视已部署的 web 应用程序的运行状况。 当特定的操作，将展开，例如当应用程序停止时，当用户成功登录到站点，或发生未经处理的异常，则会引发运行状况监视事件。 这些事件可以记录到任意数量的日志源。 本教程介绍了如何记录未处理异常的详细信息，到数据库并通过电子邮件。

本教程侧重于使用运行状况监视记录未处理的异常，但请记住，运行状况监视用于度量已部署的 ASP.NET 应用程序的总体运行状况和包括丰富的运行状况监视事件和不日志源此处介绍了。 更多的是什么，您可以创建自己的运行状况监视事件和日志源需要出现。 如果您有兴趣学习有关运行状况监视的详细信息，很好的第一步是读取[Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)的[运行状况监视常见问题](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)。 接下来，请查阅[如何： 使用运行状况监视功能在 ASP.NET 2.0](https://msdn.microsoft.com/library/ms998306.aspx)。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 运行状况监视概述](https://msdn.microsoft.com/library/bb398933.aspx)
- [配置和自定义运行状况监视系统的 ASP.NET](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [常见问题-ASP.NET 2.0 中监视的运行状况](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [如何： 发送电子邮件运行状况监视通知](https://msdn.microsoft.com/library/ms227553.aspx)
- [如何： 使用 ASP.NET 中的运行状况监视](https://msdn.microsoft.com/library/ms998306.aspx)
- [在 ASP.NET 中监视的运行状况](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [上一页](processing-unhandled-exceptions-vb.md)
> [下一页](logging-error-details-with-elmah-vb.md)
