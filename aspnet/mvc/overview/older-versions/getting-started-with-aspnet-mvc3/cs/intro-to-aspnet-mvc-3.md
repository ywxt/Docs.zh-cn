---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) 简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: b0ff8da1911b36e6e74e5c7057f27d891ad57f61
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37832284"
---
<a name="intro-to-aspnet-mvc-3-c"></a>ASP.NET MVC 3 (C#) 简介
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。
> 
> 
> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。


## <a name="what-youll-build"></a>你将生成

将实现一个简单的电影列表应用程序支持创建、 编辑和列出数据库中的电影。 以下是你将生成的应用程序的两个屏幕快照。 它包括显示的数据库中的电影列表的页面：

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。 所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>你将学习的技能

下面是你将了解：

- 如何创建一个新的 ASP.NET MVC 项目。
- 如何创建 ASP.NET MVC 控制器和视图。
- 如何创建新的数据库使用 Entity Framework Code First 范例。
- 如何检索和显示数据。
- 了解如何编辑数据并启用数据验证。

## <a name="getting-started"></a>入门

首先运行 Visual Web Developer 2010 速成版 ("Visual Web Developer"简称)，然后选择**新的项目**从**启动**页。

Visual Web Developer 是一个 IDE 或集成的开发环境。 就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。 在 Visual Web Developer 是向您显示各种可用选项顶部的工具栏。 此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。 (例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以创建使用 Visual Basic 或 Visual C# 作为编程语言的应用程序。 选择 Visual C# 在左侧，然后选择**ASP.NET MVC 3 Web 应用程序**。 命名你的项目"MvcMovie"，然后单击**确定**。 (如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。)

![](intro-to-aspnet-mvc-3/_static/image5.png)

在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。 检查**使用 HTML5 标记**并保留**Razor**作为默认视图引擎。

![](intro-to-aspnet-mvc-3/_static/image6.png)

单击 **“确定”**。 Visual Web Developer 中刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！ 这是简单"Hello World ！" 项目和它的启动应用程序的好时机。

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-3/_static/image9.png)

请注意，若要开始调试的键盘快捷键 F5。

F5 会导致 Visual Web Developer 才能启动开发 web 服务器和运行 web 应用程序。 然后，visual Web Developer 启动浏览器并打开应用程序的主页。 请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。 这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。 Visual Web Developer 运行时 web 项目，一个随机端口用于 web 服务器。 下图中的随机端口号是 43246。 当您运行该应用程序时，您可能看到不同的端口号。

![](intro-to-aspnet-mvc-3/_static/image10.png)

即时可用的此默认模板提供两个页面访问和基本的登录页。 下一步是更改此应用程序的工作原理和了解有点 ASP.NET MVC 中的过程。 关闭浏览器并让我们更改某些代码。

> [!div class="step-by-step"]
> [下一篇](adding-a-controller.md)
