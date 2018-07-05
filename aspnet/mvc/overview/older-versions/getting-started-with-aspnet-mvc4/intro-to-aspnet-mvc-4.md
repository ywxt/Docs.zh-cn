---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 简介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教程是此处使用 Visual Studio 2013 提供更新的版本。 新教程使用 ASP.NET MVC 5，可获得许多改进通过 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51e469e131b083325bc565530d91173887769ab0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395809"
---
<a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4 简介
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。 新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。
> 
> 本教程将教您构建使用 Microsoft 的 ASP.NET MVC 4 Web 应用程序的基础知识[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1。 建议使用 visual Studio 2012，无需安装任何要完成本教程的内容。 如果您使用的 Visual Studio 2010，则必须安装以下组件。 可以通过单击以下链接安装所有这些：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [为 ASP.NET MVC 4 WPI 安装程序](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
> 
> 如果您正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，安装[WPI 安装程序为 ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)和: [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。
> 
> 在本教程在 Visual Studio 中运行应用程序。 您还可以让应用程序访问 Internet 上通过将其部署到托管提供商。 Microsoft 提供了免费的 web 托管最多 10 个网站中有关[免费 Windows Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)。 有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的信息，请参阅[创建和部署 ASP.NET 网站和 SQL 数据库使用 Visual Studio](https://docs.microsoft.com/dotnet/azure/)。 该教程还演示如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Windows Azure SQL 数据库 (以前称为 SQL Azure)。
> 
> 本教程由 Rick Anderson 编写 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )。


## <a name="what-youll-build"></a>你将生成

> [!NOTE]
> 如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。 新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。


将实现一个简单的电影列表应用程序支持创建、 编辑、 搜索和列出数据库中的电影。 以下是你将生成的应用程序的两个屏幕快照。 它包括显示的数据库中的电影列表的页面：

![](intro-to-aspnet-mvc-4/_static/image1.png)

应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。 所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>入门

首先运行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express。 大部分屏幕快照中本系列，请使用 Visual Studio Express 2012 中，但你可以完成本教程使用 Visual Studio 2010 SP1、 Visual Studio 2012，Visual Studio Express 2012 或 Visual Web Developer 2010 Express。 选择**新的项目**从**启动**页。

Visual Studio 是一个 IDE 或集成的开发环境。 就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。 在 Visual Studio 中没有向您显示各种可用选项顶部的工具栏。 此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。 (例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以创建使用 Visual Basic 或 Visual C# 作为编程语言的应用程序。 选择 Visual C# 在左侧，然后选择**ASP.NET MVC 4 Web 应用程序**。 将项目命名&quot;MvcMovie&quot; ，然后单击**确定**。

![](intro-to-aspnet-mvc-4/_static/image4.png)

在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**。 将保留**Razor**作为默认视图引擎。

![](intro-to-aspnet-mvc-4/_static/image5.png)

单击 **“确定”**。 Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！ 这是一个简单&quot;Hello World ！&quot;项目中，和它的启动应用程序的好时机。

![](intro-to-aspnet-mvc-4/_static/image6.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-4/_static/image7.png)

请注意，若要开始调试的键盘快捷键 F5。

F5 导致 Visual Studio 启动 IIS Express 和运行 web 应用程序。 然后，visual Studio 启动浏览器并打开应用程序的主页。 请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。 这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。 Visual Studio 运行时 web 项目，一个随机端口用于 web 服务器。 下图中的端口号是 41788。 当您运行该应用程序时，您可能看到不同的端口号。

![](intro-to-aspnet-mvc-4/_static/image8.png)

即时可用的此默认模板也提供家庭、 联系人以及有关页面。 它还提供支持，以注册和登录，并链接到 Facebook 和 Twitter。 下一步是要更改此应用程序的工作方式有点了解 ASP.NET MVC。 关闭浏览器并让我们更改某些代码。

> [!div class="step-by-step"]
> [下一篇](adding-a-controller.md)
