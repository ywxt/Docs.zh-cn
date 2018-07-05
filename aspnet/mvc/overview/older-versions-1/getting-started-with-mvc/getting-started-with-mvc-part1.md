---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 简介 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 408256d116a7e73e01c34b0a11881e14c5b8401d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385727"
---
<a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 简介
====================
通过[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。 新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。
> 
> 
> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


让我们第一个 ASP.NET MVC Web 应用程序使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)。 我们将使一些电影列表应用程序，让我们将创建并列出电影。

## <a name="what-youll-build"></a>你将生成

以下是你将生成的应用程序的两个屏幕截图。 必须将影片的各个列的一个简单的表。

[![电影列表-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

您将得到创建窗体，因此我们可以向列表添加电影。

[![创建电影的 Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>你将学习的技能

本教程将讲述构建 ASP.NET MVC Web 应用程序使用 Visual Studio 的基础知识。 你将学习：

- 如何创建新的 ASP.NET MVC 项目
- 如何使用 SQL Server 创建一个新的数据库
- 如何创建 ASP.NET MVC 控制器和视图
- 如何检索和显示数据
- 如何编辑数据并启用数据验证
- 如何更新数据库架构

## <a name="get-started"></a>开始操作

通过从开始屏幕中运行 Visual Web Developer 2010 速成版 （我将称它"VWD"从现在起），然后选择新的项目启动。

Visual Web Developer 是一个 IDE 或集成开发环境。 就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。 没有显示各种可用选项，以及您还可以使用到选择的文件的菜单顶部的工具栏 |新项目。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以创建使用 Visual Basic 或 Visual C# 应用程序。 现在，选择 Visual C# 在左侧，然后选择"ASP.NET MVC 2 Web 应用程序"。 将项目命名为"Movies"并单击确定。

[![新项目](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

在右侧是解决方案资源管理器在应用程序中显示所有文件和文件夹。 在中间的大窗口是编辑你的代码和花费大部分时间的位置。 Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！ 这是简单的"Hello World ！ 项目中，也是如此开始我们的应用程序的好时机。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

选择工具栏上的"播放"按钮。

![开始调试](getting-started-with-mvc-part1/_static/image11.png)

它是一个绿色箭头向右将要编译你的程序和 web 浏览器中启动应用程序。

*注意： 您可以改为在键盘上按 F5 或选择调试-&gt;从"调试"菜单启动调试。*

这会导致 Visual Web Developer 启动开发 web 服务器并运行 （没有任何配置或启用此功能所需的手动步骤） 的 web 应用程序。 然后，它将启动浏览器并将其配置为浏览应用程序的主页。 请注意，下面的浏览器地址栏显示"localhost"而不是像 example.com。 这是因为 localhost 始终指向你自己的本地计算机-在这种情况下运行的是我们刚刚构建了应用程序。

[![主页](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

在初始状态下此默认模板提供了在两个页面访问和基本的登录页。 让我们更改此应用程序的工作原理，并了解有点 ASP.NET MVC 中的过程。 关闭浏览器并允许更改一些代码。

> [!div class="step-by-step"]
> [下一篇](getting-started-with-mvc-part2.md)
