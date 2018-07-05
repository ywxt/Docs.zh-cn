---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建一个新的 ASP.NET MVC 项目 |Microsoft Docs
author: microsoft
description: 步骤 1 说明了如何制定基本 NerdDinner 应用程序结构。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 9f5e0b3f82d113fc72ab4002ec8d06ad8444dceb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374271"
---
<a name="create-a-new-aspnet-mvc-project"></a>创建一个新的 ASP.NET MVC 项目
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 1 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 1 说明了如何制定基本 NerdDinner 应用程序结构。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner 步骤 1： 文件-&gt;新项目

我们将首先选择我们 NerdDinner 的应用程序**文件-&gt;新建项目**Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 中的菜单项。

这将显示"新建项目"对话框。 若要创建新的 ASP.NET MVC 应用程序，我们将选择对话框左侧的"Web"节点，然后选择右侧"ASP.NET MVC Web 应用程序"项目模板：

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要说明： 请确保已下载并安装 ASP.NET MVC-否则为它不会显示在新建项目对话框。可以使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)如果您尚未安装程序 (ASP.NET MVC 是中提供"Web 平台的&gt;框架和运行时"部分)。*

我们将的项目命名为新我们要创建"NerdDinner"，然后单击"确定"按钮以创建它。

当我们单击"确定"时 Visual Studio 将显示其他对话框，提示我们根据需要创建新应用程序的单元测试项目。 此单元测试项目使我们能够创建自动的测试以验证功能和我们的应用程序的行为 (我们将介绍的内容如何更高版本在本教程中的待办事项)。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

上面的对话框中的"测试框架"下拉列表会填充所有可用 ASP.NET MVC 单元测试项目模板在计算机上安装。 可以为 NUnit、 MBUnit 和 XUnit 下载版本。 也支持内置的 Visual Studio 单元测试框架。

*注意： Visual Studio 单元测试框架才可用于 Visual Studio 2008 Professional 和更高版本。如果你使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express 需要先下载并安装 NUnit、 MBUnit 或 XUnit 扩展为 ASP.NET MVC 中要显示此对话框的顺序。如果没有安装任何测试框架，不会显示该对话框。*

我们将使用我们创建的测试项目的默认"NerdDinner.Tests"名称，并使用"Visual Studio 单元测试"框架选项。 当我们单击 Visual Studio 的"确定"按钮将具有两个项目中的一个 web 应用程序，以进行单元测试的另一个为我们创建一个解决方案：

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>检查 NerdDinner 目录结构

当使用 Visual Studio 创建新的 ASP.NET MVC 应用程序时，它自动将大量文件和目录添加到项目：

![](create-a-new-aspnet-mvc-project/_static/image4.png)

默认情况下的 ASP.NET MVC 项目具有六个顶级目录：

| **目录** | **目的** |
| --- | --- |
| **/ 控制器** | 处理 URL 请求的控制器类的放置位置 |
| **/ 模型** | 类表示和操作数据的放置位置 |
| **/ 视图** | 负责呈现输出的 UI 模板文件的放置位置 |
| **/Scripts** | JavaScript 库文件和脚本 (.js) 的放置位置 |
| **/Content** | CSS 和图像文件和其他非动态/非-JavaScript 内容的放置位置 |
| **/ 应用\_数据** | 存储数据文件在你想要读/写。 |

ASP.NET MVC 不需要此结构。 事实上，在大型应用程序上工作的开发人员将通常对应用程序分区注册跨多个项目，以使其更易于管理 (例如： 数据通常模型类可以在一个单独的类库项目中从 web 应用程序)。 默认项目结构，但是，提供可用于保留我们的应用程序主要关注干净的很好的默认目录约定。

当我们展开 /Controllers 目录我们会发现 Visual Studio 添加默认情况下两个控制器类 – HomeController 和 AccountController – 到项目：

![](create-a-new-aspnet-mvc-project/_static/image5.png)

当我们展开 /Views 目录时，我们会发现三个子目录 – /Home、 /Account /Shared – 以及其中的文件也默认情况下添加到项目的多个模板：

![](create-a-new-aspnet-mvc-project/_static/image6.png)

当我们展开 /Content 和 /Scripts 目录时，我们会发现用于设置所有 HTML 都样式在站点上的 Site.css 文件，以及可以启用 ASP.NET AJAX 和 jQuery JavaScript 库支持应用程序中：

![](create-a-new-aspnet-mvc-project/_static/image7.png)

我们展开 NerdDinner.Tests 项目时，我们将会包含单元测试为控制器类的两个类：

![](create-a-new-aspnet-mvc-project/_static/image8.png)

运行的应用程序的完成，但主页上，有关页、 帐户注册/注销/登录信息页和 （所有连接和现成的工作） 的未处理的错误页面中，由 Visual Studio 添加这些默认文件向我们提供的基本结构。

### <a name="running-the-nerddinner-application"></a>运行 NerdDinner 应用程序

我们可以通过选择运行该项目**调试-&gt;启动调试**或**调试-&gt;启动但不调试**菜单项：

![](create-a-new-aspnet-mvc-project/_static/image9.png)

这将启动内置 ASP.NET Web 服务器随附 Visual Studio 中，并运行我们的应用程序：

![](create-a-new-aspnet-mvc-project/_static/image10.png)

下面是我们的新项目的主页 (URL:"/") 运行时：

![](create-a-new-aspnet-mvc-project/_static/image11.png)

单击"关于"选项卡显示有关页面 (URL:"/ Home/关于"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

单击右上角的"登录"链接将我们带到登录页 (URL:"/ 帐户/登录")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

如果我们还没有登录帐户，我们可以单击注册链接 (URL:"/ 帐户/注册") 创建一个：

![](create-a-new-aspnet-mvc-project/_static/image14.png)

有关，实现上述主页、 代码和注销 / 注册功能默认情况下创建新项目时添加。 我们将使用它作为我们的应用程序的起始点。

### <a name="testing-the-nerddinner-application"></a>测试 NerdDinner 应用程序

如果我们使用专业版或更高版本的 Visual Studio 2008，我们可以使用内置测试 Visual Studio 中的 IDE 支持的单元测试项目：

![](create-a-new-aspnet-mvc-project/_static/image15.png)

选择上述选项之一，将打开"测试结果"窗格中的，在 IDE 中，并向我们提供我们新的项目中包含的、 介绍内置功能 27 单元测试的通过/失败状态：

![](create-a-new-aspnet-mvc-project/_static/image16.png)

本教程中稍后我们将详细介绍自动测试，并添加其他单元测试以涵盖应用程序功能，我们实现。

### <a name="next-step"></a>下一步

我们在位置现在有一个基本的应用程序结构。 让我们现在[创建一个数据库来存储应用程序数据](create-a-database.md)。

> [!div class="step-by-step"]
> [上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)
