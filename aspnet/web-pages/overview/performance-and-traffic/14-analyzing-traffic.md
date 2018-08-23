---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 跟踪 ASP.NET Web Pages (Razor) 站点访问者信息 （分析） |Microsoft Docs
author: tfitzmac
description: 您已经看到了将你的网站后，你可能想要分析网站流量。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: aabe3177ba9479bfafafe81e1ea99a58f29d5271
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833139"
---
<a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>跟踪 ASP.NET Web Pages (Razor) 站点的访问者信息 （分析）
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用一个帮助程序将网站分析添加到 ASP.NET Web Pages (Razor) 网站中的页面。
> 
> 你将学习：
> 
> - 如何将有关你的网站流量的信息发送到的分析提供程序。
> 
> 这些是 ASP.NET 编程一文中引入的功能：
> 
> - `Analytics`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - ASP.NET Web Helpers Library （NuGet 包）


Analytics 是技术，用于测量你的网站上的流量，以便您可以了解人们如何使用该站点的常规术语。 许多分析服务都可用，包括 Google、 Yahoo、 StatCounter，及其他公司的服务。

方法分析的工作原理是，您注册的帐户分析提供程序，其中注册该站点，您想要跟踪。提供程序向你发送包含 ID 或跟踪你的帐户的代码的 JavaScript 代码片段。 您想要跟踪的站点上的 web 页面添加 JavaScript 代码片段。（通常添加分析代码段的页脚或布局页面或其他站点中的每一页显示的 HTML 标记。）当用户请求的页面，包含这些 JavaScript 代码段之一时，该代码片段将有关当前页的信息发送到分析提供程序，用户记录页有关的各种详细信息。

当你想要我们来看一下您站点的统计信息时，您登录到分析提供程序的网站。 然后，您可以像有关你的网站，查看各种类型的报表：

- 单个页面的页面视图数。 这将告知您 （大致） 有多少人正在访问站点，并且你的站点上的页都是最受欢迎。
- 人员花费的时间在特定页面上。 这可以告诉您是否让您的主页上保持人们的兴趣等。
- 常见的站点已在之前他们访问您的站点。 这有助于你了解你的流量来自链接，从搜索中，依次类推。
- 当用户访问你的网站，它们保持多长时间。
- 您的访问者是从哪些国家/地区。
- 哪些浏览器和操作系统使用您的访问者。

    ![Ch14traffic 1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>使用一个帮助程序将分析添加到页面

ASP.NET 网页包括多个分析帮助程序 (`Analytics.GetGoogleHtml`， `Analytics.GetYahooHtml`，和`Analytics.GetStatCounterHtml`)，使其更容易地管理用于分析的 JavaScript 代码段。 而不是找出如何以及在何处放置的 JavaScript 代码，只需是向页面添加帮助器。 你需要提供的唯一信息是帐户名称、 ID 或跟踪代码。 （有关 StatCounter，还必须提供了几个其他值。）

在此过程中，你将创建一个使用的布局页`GetGoogleHtml`帮助器。 如果您已具有包含其他分析提供程序之一的帐户，可以改为使用该帐户，并根据需要进行细微调整。

> [!NOTE]
> 创建 analytics 帐户时，你将注册你想要跟踪的站点的 URL。 如果您要测试的所有内容在本地计算机上，不会跟踪实际流量 （流量只能是您），因此你无法再记录和查看站点统计信息。 但此过程演示如何将分析帮助程序添加到一个页面。 在发布你的站点时，实时站点会将信息发送到分析提供程序。


1. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。
2. 使用 Google Analytics 中创建帐户并记录帐户名称。
3. 创建一个名为的布局页*Analytics.cshtml*并添加以下标记：

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > 必须将放置在调用`Analytics`web 页的正文中的帮助程序 (之前`</body>`标记)。 否则，在浏览器将不运行该脚本。

    如果使用的不同的分析提供程序，请改为使用以下帮助器之一：

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. 替换为`myaccount`帐户、 ID 或在步骤 1 中创建的跟踪代码的名称。
5. 在浏览器中运行页。 (请确保的页中选择**文件**工作区之前运行它。)
6. 在浏览器中查看页面源文件。 你将能够看到呈现的分析代码：

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. 登录到 Google Analytics 站点并检查你的站点的统计信息。 如果您在实时站点上运行页上，您将看到记录访问页面的条目。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [Google Analytics 站点](https://www.google.com/analytics/)
- [Yahoo ！Web Analytics 站点](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 站点](http://statcounter.com/)
