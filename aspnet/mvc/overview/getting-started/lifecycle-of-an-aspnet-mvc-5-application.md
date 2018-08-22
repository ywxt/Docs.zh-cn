---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 应用程序生命周期 |Microsoft Docs
author: cephalin
description: 下载 PDF 文档绘制图表的一个 ASP.NET MVC 5 应用程序生命周期。 此生命周期文档提供 MVC 生命周期的高级视图...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: 5523217ae5674ac4e5898a150f9e5f0ae3a70d26
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824645"
---
<a name="lifecycle-of-an-aspnet-mvc-5-application"></a>ASP.NET MVC 5 应用程序生命周期
====================
通过[Cephas Lin](https://github.com/cephalin)

[下载 PDF 文档](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

此处，您可以下载 PDF 文档的图表的生命周期的每个 ASP.NET MVC 5 应用程序，接收 HTTP 请求发送的 HTTP 响应回客户端。 它旨在为那些不熟悉 ASP.NET MVC 的学习工具，而且还为那些需要深入了解应用程序的特定方面的参考。 PDF 文档具有以下功能：

- 相关[HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)阶段以帮助您了解 MVC 生地[ASP.NET 应用程序生命周期](https://msdn.microsoft.com/library/bb470252.aspx)。
- 在 MVC 应用程序生命周期，其中您可以了解每个 MVC 应用程序通过在请求处理管道中的主要阶段的高级视图。  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- 显示向下钻取，请求处理管道的详细信息的详细信息视图。 您可以比较高级的视图和详细信息视图以查看如何生命周期的详细信息将收集到的各个阶段。 [下载 PDF](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)若要查看可查看大图。
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- 定位以及所有可重写方法的目的[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx)请求处理管道中的对象。 您可能会或可能需要重写任何一种方法，但很重要，以便了解在应用程序生命周期中的角色，使您可以在适当的生命周期阶段的预期的效果编写代码。
- 解决问题向上关系图显示每个筛选器类型 （身份验证、 授权、 操作和结果） 的调用方式。
- 从每个点的详细信息视图中的相关链接到帮助性文章或博客。


## <a name="next-steps"></a>后续步骤

本文档是否满足您的需求？ 我们将不胜感激您的反馈。 如果你在应用程序中有任何问题的 ASP.NET MVC 生命周期[Stackoverflow](http://stackoverflow.com/help)并[ASP.NET MVC 论坛](https://forums.asp.net/1146.aspx)所提出的好地方。 请按照[我](https://twitter.com/Cephas_MSFT)twitter 这样您就获得更新的我最新教程。
