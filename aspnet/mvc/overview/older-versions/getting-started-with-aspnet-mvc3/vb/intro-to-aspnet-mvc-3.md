---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (VB) 简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: f596dbfb534a64169767fb77fb15ecc867466c74
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577179"
---
<a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 (VB) 简介
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您愿意 C#，切换到[C# 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。


本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：

- [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）

如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

可随附于此项目具有 VB 源代码的 Visual Web Developer 项目。 [下载的 VB 版本](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。 如果您愿意 CSharp，切换到[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。

## <a name="what-youll-build"></a>你将生成

将实现一个简单的电影列表应用程序支持创建、 编辑和列出数据库中的电影。 以下是你将生成的应用程序的两个屏幕快照。 它包括显示的数据库中的电影列表的页面：

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。 所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>你将学习的技能

下面是你将了解：

- 如何创建一个新的 ASP.NET MVC 项目
- 如何创建使用 Entity Framework 代码优先的新数据库
- 如何创建 ASP.NET MVC 控制器和视图
- 如何检索和显示数据
- 如何编辑数据并启用数据验证

## <a name="getting-started"></a>入门

首先运行 Visual Web Developer 2010 速成版 (简称的"VWD")，然后选择**新的项目**从**启动**页。

Visual Web Developer 是一个 IDE 或集成的开发环境。 就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。 在 Visual Web Developer 是向您显示各种可用选项顶部的工具栏。 此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。 (例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以创建使用所选的 Visual Basic 或 Visual C# 作为编程语言的应用程序。 对于本教程中，在左侧，选择 Visual Basic，然后选择**ASP.NET MVC 3 Web 应用程序**。 命名你的项目"MvcMovie"，然后单击**确定**。

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。 将保留**Razor**作为默认视图引擎。

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

单击 **“确定”**。 Visual Web Developer 中刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！ 这是简单"Hello World ！" 项目和它的启动应用程序的好时机。

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-3/_static/image11.png)

请注意，若要开始调试的键盘快捷键 F5。

F5 会导致 Visual Web Developer 才能启动开发 web 服务器和运行 web 应用程序。 VWD 然后启动浏览器并打开应用程序的主页。 请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。 这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。 VWD 运行时 web 项目，项目使用一个随机端口。 下图中的随机端口号是 43246。 你的项目可能会使用不同的端口号。

![](intro-to-aspnet-mvc-3/_static/image12.png)

在初始状态下此默认模板提供了在两个页面访问和基本的登录页。 让我们更改此应用程序的工作原理，并了解有点 ASP.NET MVC 中的过程。 关闭浏览器并让我们更改某些代码。

> [!div class="step-by-step"]
> [下一篇](adding-a-controller.md)
