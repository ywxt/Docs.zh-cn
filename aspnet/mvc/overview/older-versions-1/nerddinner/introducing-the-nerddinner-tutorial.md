---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 的简介教程 |Microsoft Docs
author: shanselman
description: 若要了解新框架的最佳方式是生成内容进行处理。 本教程将指导完成如何构建很小，但完成后，应用程序使用 ASP.NE...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 9188df1eca7f488502640bc17d5034f93f4ac82c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805105"
---
<a name="introducing-the-nerddinner-tutorial"></a>NerdDinner 的简介教程
====================
通过[Scott Hanselman](https://github.com/shanselman)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 若要了解新框架的最佳方式是生成内容进行处理。 本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 1 中，应用程序，并介绍了一些重要概念。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-tutorial"></a>NerdDinner 教程

若要了解新框架的最佳方式是生成内容进行处理。 本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 应用程序，并介绍了一些重要概念。

我们要生成应用程序被称为"NerdDinner"。 NerdDinner 提供方便人们查找和整理 dinners 联机：

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner，已注册的用户可以创建、 编辑和删除 dinners。 它在应用程序强制实施一组一致的验证和业务规则：

![](introducing-the-nerddinner-tutorial/_static/image2.png)

访问者可以使用基于 AJAX 的映射来搜索即将推出 dinners 接近的人们正在挂起：

![](introducing-the-nerddinner-tutorial/_static/image3.png)

单击 dinner 会将他们到详细信息页，以了解有关它的详细信息：

![](introducing-the-nerddinner-tutorial/_static/image4.png)

如果他们感兴趣参加 dinner 他们可以登录，或在网站注册：

![](introducing-the-nerddinner-tutorial/_static/image5.png)

然后，他们可以单击来参与活动的基于 AJAX 的 RSVP 链接：

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>实现 NerdDinner

我们将首先我们 NerdDinner 的应用程序使用的文件-&gt;Visual Studio 中的新项目命令以创建一个全新的 ASP.NET MVC 项目。 然后以增量方式将功能和特性。 在此过程中，我们将介绍：

1. [如何创建新的 ASP.NET MVC 项目](# "创建新的 ASP.NET MVC 项目")
2. [如何创建数据库](# "创建数据库")
3. [如何生成具有业务规则验证模型](# "生成具有业务规则验证功能的模型")
4. [如何使用控制器和视图实现列表/详细信息 UI](# "使用控制器和视图实现列表/详细信息 UI")
5. [如何提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持](# "提供 CRUD （创建、 读取、 更新、 删除） 数据窗体项支持")
6. [如何使用 ViewData 和实现 ViewModel 类](# "使用 ViewData 和实现 ViewModel 类")
7. [如何重新使用 UI 使用母版页和部分](# "重复使用 UI 使用母版页和部分")
8. [如何实现高效数据分页](# "实现高效数据分页")
9. [如何保护应用程序使用身份验证和授权](# "安全应用程序使用的身份验证和授权")
10. [如何使用 AJAX 提供动态更新](# "使用 AJAX 提供动态更新到")
11. [如何使用 AJAX 实现映射方案](# "使用 AJAX 实现映射方案")
12. [如何启用自动化的单元测试](# "启用自动单元测试")

您可以构建您自己的 NerdDinner 副本从零开始通过完成每个步骤我们的这一章中的演练。 或者，可以下载下面的源代码的完整的版本： [NerdDinner GitHub 上的](https://github.com/AspNetMVPSamples/NerdDinner)。 也可以选择性地[下载本教程的免费 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)如果你想要阅读教程脱机。

可以使用 Visual Studio 2008 或免费 Visual Web Developer 2008 速成版构建应用程序。 您可以使用 SQL Server 或免费 SQL Server Express 数据库。

你可以安装 ASP.NET MVC，Visual Web Developer 2008 速成版，和 SQL Server Express （所有免费） 使用 V2 的[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>现在让我们开始吧...

现在，我们已经介绍了 NerdDinner 的是，让我们卷起袖子，编写一些代码。

我们将首先使用文件-&gt;Visual Studio 创建 NerdDinner 应用程序中的新项目。

> [!div class="step-by-step"]
> [下一篇](create-a-new-aspnet-mvc-project.md)
