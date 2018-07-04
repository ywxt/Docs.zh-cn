---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第 1 部分： 概述和文件-> 新建项目 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 1 部分介绍如何概述和文件-> 新项目。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: c03b62db2227c167c68ca5cf8174e4322658d39d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377884"
---
<a name="part-1-overview-and-file-new-project"></a>第 1 部分： 概述和文件-> 新建项目
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。  
>   
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 1 部分介绍了概述和文件-&gt;新项目。


## <a name="overview"></a>概述

MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Web Developer web 开发的分步教程应用程序。 我们将启动速度慢，因此初学者级别 web 开发体验也没关系。

我们将构建的应用程序是简单音乐应用商店。 有向应用程序的三个主要部分： 购物、 结帐和管理。

![](mvc-music-store-part-1/_static/image1.jpg)

访问者可以浏览按流派的唱片集：

![](mvc-music-store-part-1/_static/image2.jpg)

他们可以查看一个唱片集，并将其添加到其购物车：

![](mvc-music-store-part-1/_static/image3.jpg)

他们可以查看其购物车，删除它们不再需要任何的项：

![](mvc-music-store-part-1/_static/image4.jpg)

继续下的一步要签出将提示他们登录或注册一个用户帐户。

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

创建帐户后，他们可以通过填写传送和付款信息完成顺序。 为了简单起见，我们将运行令人惊叹的升级： 所有内容都是免费的如果输入促销代码"免费"！

![](mvc-music-store-part-1/_static/image5.jpg)

排序后，他们将看到简单确认屏幕：

![](mvc-music-store-part-1/_static/image6.jpg)

除了客户 faceing 页，我们还将生成一个管理员部分，其中显示了一系列唱片集从其管理员可以创建、 编辑、 并删除唱片集：

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1.文件-&gt;新项目

### <a name="installing-the-software"></a>安装软件

本教程将首先创建一个新的 ASP.NET MVC 3 项目使用免费的 Visual Web Developer 2010 Express （这是免费的），，然后我们将以增量方式添加功能，可创建一个完整的正常运行应用程序。 此过程中，我们将介绍数据库访问权限、 窗体发布方案、 数据验证、 使用母版页对于一致的页面布局，使用 AJAX 页面更新和验证、 用户登录名和的详细信息。

您可以照着操作步骤，也可以下载完整的应用程序从[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。

可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 速成版 SP1 （Visual Studio 2010 的免费版本） 生成应用程序。 我们将使用 SQL Server Compact （同样免费） 来承载数据库。 在开始之前，请确保已安装以下列出的先决条件。


- [Visual Studio Web Developer Express SP1 系统必备组件]
- [ASP.NET MVC 3 工具更新]
- [SQL Server Compact 4.0]-包括运行时和工具支持


### <a name="creating-a-new-aspnet-mvc-3-project"></a>创建新的 ASP.NET MVC 3 项目

我们将开始通过 Visual Web Developer 中的文件菜单中选择"新建项目"。 此时会打开新建项目对话框。

![](mvc-music-store-part-1/_static/image5.png)

我们将选择 Visual C#-&gt; Web 模板组在左侧，然后在中间栏中选择"ASP.NET MVC 3 Web 应用程序"模板。 为项目 MvcMusicStore 命名并按确定按钮。

![](mvc-music-store-part-1/_static/image8.jpg)

这将显示辅助对话框使我们可以使我们的项目中的某些 MVC 特定设置。 选择以下项：

项目模板-选择为空

视图引擎-选择 Razor

使用 HTML5 语义标记的检查

请验证你的设置是如下所示，然后按确定按钮。

![](mvc-music-store-part-1/_static/image9.jpg)

这将创建我们的项目。 让我们看看已添加到我们在右侧的解决方案资源管理器中的应用程序的文件夹。

![](mvc-music-store-part-1/_static/image10.jpg)

空 MVC 3 模板并没有完全为空，它将添加基本的文件夹结构：

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC 使用的一些基本的命名约定的文件夹名称：

| **文件夹** | **目的** |
| --- | --- |
| **/ 控制器** | 控制器响应从浏览器输入，决定要处理的问题，并向用户返回响应的内容。 |
| **/ 视图** | 视图保存我们的 UI 模板 |
| **/ 模型** | 模型保存和操作数据 |
| **/Content** | 此文件夹包含我们的图像、 CSS 和任何其他静态内容 |
| **/Scripts** | 此文件夹包含我们的 JavaScript 文件 |

这些文件夹包含即使在空的 ASP.NET MVC 应用程序，因为默认情况下的 ASP.NET MVC 框架使用"惯例优先于配置"的方法，并默认做了一些假设基于文件夹命名约定。 例如，控制器视图文件夹中的视图的默认情况下查找而无需显式指定此设置在代码中。 坚持使用的默认约定可以减少需要编写的代码量还可使其便于其他开发人员了解您的项目。 我们将介绍这些约定详细构建我们的应用程序。

> [!div class="step-by-step"]
> [下一篇](mvc-music-store-part-2.md)
