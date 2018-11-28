---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门 |Microsoft Docs
author: Erikre
description: 此分步教程系列将指导您学习生成使用 ASP.NET 4.5 和 Microsoft Visual Studio 截止的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: b9ed6ce4ac13f047f53c56e183433cbd038ea15c
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450679"
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a>ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

此分步教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 

## <a name="introduction"></a>介绍

本系列教程将指导您完成创建适用于 Web 和 ASP.NET 4.5 中使用 Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序所需的步骤。

应用程序将创建名为**Wingtip Toys**。 它是销售项在线应用商店前端网站的简化的示例。 本系列教程重点介绍 ASP.NET 4.5 中提供的新功能。

注释是欢迎使用，并且我们将采取各种方法来更新本系列教程基于您的建议。

### <a name="download-completed-project"></a>下载已完成项目

您可以下载包含已完成本教程的 C# 项目。

- [开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a>通过执行相关的 ASP.NET Web 窗体测验查看的内容

完成本教程后，测试你的知识并通过采用加强关键概念[ASP.NET Web 窗体测验](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)。 此测验专门设计从本教程系列中包含的内容。 测验中的每个问题提供的附加指导的链接以及说明。

- [ASP.NET Web 窗体测验](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a>读者

本系列教程的目标的读者是经验丰富的开发人员的新 ASP.NET Web 窗体。 希望本系列教程的开发人员应具备以下技能：

- 熟悉对象面向编程 (OOP) 语言
- 熟悉 Web 开发概念 (HTML、 CSS、 JavaScript)
- 熟悉关系数据库概念
- 熟悉 n 层体系结构概念

如果您有兴趣查看上面列出的区域，请考虑查看以下内容：

- [Visual C# 入门](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web 开发](https://msdn.microsoft.com/beginner/bb308760.aspx)， [HTML、 CSS、 JavaScript、 SQL、 PHP、 JQuery](http://w3schools.com/)
- [关系数据库](http://en.wikipedia.org/wiki/Relational_database)
- [多层体系结构](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>应用程序功能

本系列中显示的 ASP.NET Web 窗体功能包括：

- Web 应用程序项目 （而不是网站项目）
- Web Forms — Web 窗体
- 母版页配置
- Bootstrap
- 实体框架代码优先，LocalDB
- 请求验证
- 强类型数据控件模型绑定数据批注和值提供程序
- SSL 和 OAuth
- ASP.NET 标识、 配置和授权
- 非介入式验证
- 路由
- ASP.NET 错误处理

### <a name="application-scenarios-and-tasks"></a>应用程序方案和任务

本系列教程中演示的任务包括：

- 创建、 查看和运行新的项目
- 创建的数据库结构
- 初始化和数据库的种子设定
- 自定义 UI 使用样式、 图形和母版页
- 添加页面和导航
- 显示菜单的详细信息和产品数据
- 创建购物车
- 添加 SSL 和 OAuth 支持
- 添加付款方式
- 包括一个管理员角色和用户访问应用程序
- 限制对特定页面和文件夹的访问
- 将文件上载到 web 应用程序
- 实施输入的验证
- 注册 web 应用程序路由
- 实现错误处理和错误日志记录

## <a name="overview"></a>概述

如果你不熟悉 ASP.NET Web 窗体编程概念的熟悉，但同时具备，则必须正确教程。 如果你已熟悉 ASP.NET Web 窗体，您可以受益于本系列教程的 ASP.NET 4.5 中提供的新功能。 如果您不熟悉编程概念和 ASP.NET Web 窗体，请参阅 Web 窗体中提供的其他教程[Getting Started](../../../index.md) ASP.NET 网站上的部分。

特定于**最新**ASP.NET 4.5 功能在此 Web 窗体中的系列教程包括以下：

- 用于创建一个简单的 UI 项目的产品/服务[支持多个 ASP.NET 框架](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)（Web 窗体、 MVC 和 Web API）。
- [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)，一个布局和主题的框架，提供响应式设计和主题功能。
- [ASP.NET 标识](../../../../identity/index.md)，新的 ASP.NET 成员资格系统的与 web 托管 IIS 之外的软件的工作方式在所有 ASP.NET 框架和工作原理相同。
- [实体框架 6](https://msdn.microsoft.com/data/ef.aspx)、 Entity framework，使你检索和操作数据作为强类型化对象、 访问数据以异步方式处理暂时性连接故障和日志的 SQL 语句。

ASP.NET 4.5 功能的完整列表，请参阅[ASP.NET 和 Web Tools for Visual Studio 2013 发行说明](../../../../visual-studio/overview/2013/release-notes.md)。

### <a name="the-wingtip-toys-sample-application"></a>Wingtip Toys 示例应用程序

以下屏幕截图提供将在本系列教程中创建 ASP.NET Web 窗体应用程序的快速视图。 运行时应用程序从 Visual Studio Express 2013 for Web，您将看到以下 web 主页。

![Wingtip Toys 的默认页](introduction-and-overview/_static/image1.png)

可以将注册为新用户，或现有用户身份登录。 导航由从数据库检索可用的产品提供顶部为每个产品类别。

通过选择的产品链接，你将能够查看所有可用产品的列表。

![Wingtip Toys 的产品](introduction-and-overview/_static/image2.png)

选择任何列出的产品，还可以查看各个产品的详细信息。

![Wingtip Toys 的产品详细信息](introduction-and-overview/_static/image3.png)

作为用户，可以注册和登录使用 Web 窗体模板的默认功能。 本教程还介绍如何使用现有的 Gmail 帐户登录。 此外，你可以登录以管理员身份添加和从数据库中删除产品。

![Wingtip Toys-登录](introduction-and-overview/_static/image4.png)

以用户身份登录，你可以将产品添加到购物车并使用 PayPal 结帐。 请注意此示例应用程序旨在 PayPal 的开发人员沙箱起作用。 没有实际资金事务会发生。

![Wingtip Toys 的购物车](introduction-and-overview/_static/image5.png)

PayPal 将确认你的帐户、 订单和付款信息。

![Wingtip Toys 的 PayPal](introduction-and-overview/_static/image6.png)

返回从 PayPal 后, 可以查看并完成你的订单。

![Wingtip Toys 的顺序查看](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>系统必备

在开始之前，请确保您已在计算机上安装以下软件：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 会自动安装.NET Framework。

本系列教程使用 Microsoft Visual Studio Express 2013 for Web。 可以使用 Microsoft Visual Studio Express 2013 for Web，或者 Microsoft Visual Studio 2013 来完成本系列教程。

> [!NOTE] 
> 
> Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常称为 Visual Studio 在整个教程系列中。


如果已安装了 Visual Studio 版本，安装过程将现有版本旁边安装 Visual Studio 2013 或 Microsoft Visual Studio Express 2013 for Web。 在早期版本中创建的网站中可以在 Visual Studio 2013 中打开，并继续在以前的版本中打开。

> [!NOTE] 
> 
> 本演练假定你所选*Web 开发*的设置集合，首次启动 Visual Studio。 有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。


## <a name="download-the-sample-application"></a>下载示例应用程序

在安装后系统必备组件，已准备好开始本教程系列中创建新的 Web 项目显示。 如果你想要**根据需要**运行本教程系列中创建的示例应用程序，你可以从下载 MSDN 示例网站。 此下载包含以下元素：

- 中的示例应用程序*WingtipToys*文件夹。
- 若要创建示例应用程序所使用的资源*WingtipToys 资产*中的文件夹*WingtipToys*文件夹。

#### <a name="download-the-file-from-msdn-samples-site"></a>从 MSDN 示例站点下载文件：

[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 

在下载<em>.zip</em>文件。 若要查看已完成本教程系列中创建的项目，找到并选择<em>C#</em>中的文件夹<em>.zip</em>文件。 保存<em>C#</em> folderto 使用以使用 Visual Studio 2013 项目的文件夹。 默认情况下，以下是 Visual Studio 2013 项目文件夹：

<strong>C:\Users&#92;</strong><strong><em>&lt;用户名&gt;</em></strong><strong>\Documents\Visual Studio 2013\Projects</strong>

重命名***C#*** 向文件夹***WingtipToys***。

> [!NOTE]
> 如果已有一个名为文件夹*WingtipToys*在项目文件夹中，暂时重命名该现有文件夹重命名前*C#* 文件夹*WingtipToys*。


若要运行已完成的项目，打开*WingtipToys*文件夹，然后双击*WingtipToys.sln*文件。 Visual Studio 2013 将打开的项目。 接下来，右键单击*Default.aspx*文件在解决方案资源管理器窗口中，右键单击菜单中单击视图中浏览器。

### <a name="tutorial-support-and-comments"></a>教程支持和提出的意见

使用随附的问题与解答部分[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)示例 (C#) 的任何问题或意见。

在本教程系列中的注释是欢迎使用，并更新本系列教程时将进行每项工作要考虑到帐户更正或建议的教程的注释中提供的改进。

在开发期间，发生错误，或者如果网站无法正常运行的错误消息可能会给问题的源提供复杂的线索或可能不说明如何修复此错误。 若要帮助您通过一些常见的问题方案，您可以使用[ASP.NET 论坛](https://forums.asp.net/)或附带的问题与解答部分[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 示例。 如果收到错误消息或某些操作无法在完成教程，，请务必检查上述位置。

> [!div class="step-by-step"]
> [下一篇](create-the-project.md)
