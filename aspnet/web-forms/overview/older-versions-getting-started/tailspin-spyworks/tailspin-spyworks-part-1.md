---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第 1 部分： 文件-> 新建项目 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 1 部分介绍了概述和文件/新项目。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: d2e4b36c9029e86eea9b09974839e96e9aa39ced
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830691"
---
<a name="part-1-file--new-project"></a>第 1 部分： 文件-> 新建项目
====================
通过[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。 它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。
> 
> 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 1 部分介绍了概述和文件/新项目。


## <a id="_Toc260221666"></a>  概述

本教程是 ASP.NET WebForms 的简介。 我们将启动速度慢，因此初学者级别 web 开发体验也没关系。

我们将构建的应用程序是简单的在线商店。

![](tailspin-spyworks-part-1/_static/image1.jpg)


访问者可以浏览产品按类别：

![](tailspin-spyworks-part-1/_static/image2.jpg)

他们可以查看一个产品，并将其添加到其购物车：

![](tailspin-spyworks-part-1/_static/image3.jpg)

他们可以查看其购物车，删除它们不再需要任何的项：

![](tailspin-spyworks-part-1/_static/image4.jpg)

继续下的一步要签出将提示他们到

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

排序后，他们将看到简单确认屏幕：

![](tailspin-spyworks-part-1/_static/image7.jpg)


我们将首先在 Visual Studio 2010 中，创建新的 ASP.NET WebForms 项目和我们将以增量方式添加功能，可创建一个完整的正常运行应用程序。 此过程中，我们将介绍数据库访问权限、 列表和网格视图、 数据更新页、 数据验证、 使用母版页提供一致的页面布局、 AJAX、 验证、 用户成员身份和的详细信息。

您可以照着操作步骤，也可以下载已完成的应用程序 [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)

可以使用 Visual Studio 2010 或免费的 Visual Web Developer 2010 从[ https://www.microsoft.com/express/Web/ ](https://www.microsoft.com/express/Web/)。 若要生成应用程序，可以使用 SQL Server 或免费 SQL Server Express 到主机数据库。

## <a id="_Toc260221667"></a>  文件 / 新建项目

我们将开始从 Visual Studio 中的文件菜单中选择新项目。 此时会打开新建项目对话框。

![](tailspin-spyworks-part-1/_static/image8.jpg)

我们将选择 Visual C# / Web 模板组在左侧，，然后在中间栏中选择"ASP.NET Web 应用程序"模板。 为项目 TailspinSpyworks 命名并按确定按钮。

![](tailspin-spyworks-part-1/_static/image9.jpg)

这将创建我们的项目。 让我们看看我们在右侧的解决方案资源管理器中的应用程序中包括的文件夹。

![](tailspin-spyworks-part-1/_static/image10.jpg)

空的解决方案并没有完全为空，它将添加基本的文件夹结构：

![](tailspin-spyworks-part-1/_static/image1.png)

请注意由 ASP.NET 4 默认项目模板实现的约定。

- "帐户"文件夹 asp 实现基本用户界面。NET 的成员资格子系统。
- 充当客户端 JavaScript 文件的存储库的"Scripts"文件夹和核心 jQuery.js 文件都可用的默认值。
- "样式"文件夹用于组织我们网站上的视觉对象 （CSS 样式表）

当我们按 F5 以运行我们的应用程序和呈现 default.aspx 页面时将看到以下信息。

![](tailspin-spyworks-part-1/_static/image11.jpg)

我们的第一个应用程序增强功能将使用的 CSS 类和关联的图像文件，将呈现我们想要我们 Tailspin Spyworks 的应用程序的 visual asthetics 替换默认 WebForms 模板中的 Style.css 文件。

执行此操作之后如下所示 default.aspx 页面。

![](tailspin-spyworks-part-1/_static/image12.jpg)

请注意，在顶部的图像链接的页面和已添加到母版页的菜单项。 仅"登录"和"帐户"链接指向的存在 （由默认模板生成） 的页面和我们将实现构建我们的应用程序的页面的其余部分。

我们还要将母版页重新定位到样式目录。 虽然这是首选项仅它可能会简化操作有点如果我们决定在将来执行我们的应用程序"skinable"。

这样我们将需要更改母版页后所有.aspx 文件中的引用生成默认情况下 ASP.NET WebForms 页。

> [!div class="step-by-step"]
> [下一篇](tailspin-spyworks-part-2.md)
