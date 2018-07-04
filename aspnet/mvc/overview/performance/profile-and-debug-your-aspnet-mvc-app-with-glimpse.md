---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 分析和调试使用 Glimpse 对 ASP.NET MVC 应用程序 |Microsoft Docs
author: Rick-Anderson
description: Glimpse 是一个蓬勃发展和不断增加的开源 NuGet 包提供了详细的性能的系列内容，调试和诊断信息的 ASP.NET...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: ef65b512645d3f013ea34d3557da93254425c419
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391065"
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>分析和调试使用 Glimpse 对 ASP.NET MVC 应用程序
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> Glimpse 是一个蓬勃发展和不断增加的开源 NuGet 包提供了详细的性能的系列内容，调试和诊断信息的 ASP.NET 应用程序。 它是容易安装、 轻量、 超快，并在每一页的底部显示关键性能指标。 它允许您向下钻取到你的应用时需要了解在服务器上正在运行的内容。 大致了解提供了我们建议使用整个开发周期，包括 Azure 测试环境很有价值的信息。 虽然[Fiddler](http://www.telerik.com/fiddler)并[F-12 开发工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供客户端视图，大致了解提供从服务器的详细的视图。 本教程将重点介绍使用 Glimpse ASP.NET MVC 和 EF 的包，但其他许多包可用。 在可能的情况将链接到相应[Glimpse docs](http://getglimpse.com/Docs/)我帮助维护。 Glimpse 是一个开放源代码项目，你也可以参与到源代码和文档。


- [安装概述](#ig)
- [为本地主机启用 Glimpse](#eg)
- [时间线选项卡](#Time)
- [模型绑定](#mb)
- [路由](#route)
- [在 Azure 上使用 Glimpse](#da)
- [其他资源](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>安装概述

你可以从 NuGet 包管理器控制台或安装 Glimpse**管理 NuGet 包**控制台。 对于此演示，我将安装 Mvc5 和 EF6 包：

![从 NuGet Dlg 安装概述](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

搜索*Glimpse.EF*

![从 NuGet 安装 dlg Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

通过选择**已安装的包**，可以看到安装 Glimpse 依赖模块：

![从 DLg 安装 Glimpse 包](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

以下命令从包管理器控制台安装 Glimpse MVC5 和 EF6 模块：

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>为本地主机启用 Glimpse

导航到http://localhost:&lt; 端口号&gt;/glimpse.axd，然后单击<strong>上打开 Glimpse</strong>按钮。

![Glimpse axd 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

如果必须显示在收藏夹栏，您可以拖放 Glimpse 按钮，将其添加为 bookmarklets:

![使用 Glimpse boookmarklets IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

你现在可以导航您的应用程序，并**Heads 平视显示**(HUD) 显示在页面底部。

![联系人管理器页的 HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

[Glimpse HUD 页](http://getglimpse.com/Docs/Heads-up-Display)详细介绍上面所示的计时信息。 非介入式性能数据 HUD 显示可以立即发出通知的问题的测试周期到开始之前。 单击&quot;g&quot;在右下角将显示概述面板：

![概述面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

在上面，图像中[选项卡执行](http://getglimpse.com/Docs/Execution-Tab)选择后，管道中显示的操作和筛选器的计时详细信息。 您可以看到我[停止监视筛选器计时器](http://www.nuget.org/packages/StopWatch/)开始管道阶段 6。 虽然我轻量计时器可提供有用的配置文件/计时数据，它未命中数和在授权中所用的呈现视图的所有时间。 你可以阅读我在计时器[配置文件和时间在 ASP.NET MVC 应用程序到 Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。 [选项卡](http://getglimpse.com/Docs/Tabs)页提供有关每个选项卡的详细信息的链接。

<a id="Time"></a>
## <a name="the-timeline-tab"></a>时间线选项卡

我已修改 Tom Dykstra 的未完成[EF 6/MVC 5 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)用下面的代码将更改为讲师控制器：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

上面的代码可以在查询字符串中传入 (`eager`) 控制预先或显式加载的数据。 在下图中，使用显式加载和计时页面将显示每个注册中加载`Index`操作方法：

![Explicit Loading — 显式加载](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

在下面的代码中，指定预先，并且每个注册提取后`Index`视图称为：

![指定预先](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

你可以悬停在时间段，以获取详细的计时信息：

![悬停鼠标以查看详细的计时](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>模型绑定

[模型绑定选项卡](http://getglimpse.com/Docs/Model-Binding-Tab)提供了丰富的信息可帮助你了解如何绑定窗体变量，为什么某些不能绑定如所料。 下的图显示 **？** 图标，你可以单击以打开该功能的初步了解帮助页。

![大致了解模型绑定查看](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>路由

 大致了解路由选项卡将可以帮助你调试和了解路由。 下图中的产品路由选择 （和其显示为绿色，大致了解约定）。 ![所选的产品名称](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png)路由约束、 区域和数据令牌也会显示。 请参阅[大致了解路由](http://getglimpse.com/Docs/Routes-Tab)并[ASP.NET MVC 5 中的属性路由](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)有关详细信息。 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>在 Azure 上使用 Glimpse

大致了解默认安全策略只允许要在本地主机显示的大致了解数据。 您可以更改此安全策略，以便您可以查看此数据 （如 Azure 上的 web 应用） 的远程服务器上。 在 Azure 上的测试环境，将添加到底部的突出显示的标记*web.confg*文件以启用初步了解：

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

与此项更改就，任何用户可以在远程站点上查看你大致了解数据。 考虑将上面的标记添加到发布配置文件，因此它仅部署应用时使用该发布配置文件 (例如，在 Azure 测试 proifle。)若要限制大致了解数据，我们将添加`canViewGlimpseData`角色和仅允许此角色，以查看大致了解数据的用户。

删除从注释*GlimpseSecurityPolicy.cs*文件，并更改[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)从调用`Administrator`到`canViewGlimpseData`角色：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> 安全性-大致了解提供的丰富数据可能会暴露您的应用程序的安全性。 Microsoft 未执行安全审核的大致了解用于生产应用。


添加角色的信息，请参阅我[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 web 应用部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教程。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [Glimpse 配置](http://getglimpse.com/Docs/Configuration)-文档页上配置的选项卡中，运行时策略、 日志记录和的详细信息。
