---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 编程 ASP.NET 网页 (Razor) 使用 Visual Studio |Microsoft Docs
author: Rick-Anderson
description: 本附录介绍了如何使用 Visual Studio 2010 或 Visual Web Developer 2010 速成版到程序 ASP.NET Web Pages with Razor syntax。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 5b8df17ec1021d133579e23cb4f5b0d0f67d4c7c
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020450"
---
<a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>编程使用 Visual Studio 的 ASP.NET Web Pages (Razor)
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 Visual Studio 或 Visual Web Developer 速成版到程序 ASP.NET Web Pages (Razor) 网站。
>
> 学习内容
>
> - 需要安装 （如果有的话），以便在你的 Visual Studio 版本中使用 ASP.NET Web Pages。
> - 如何将支持适用于 ASP.NET 网页添加到 Visual Web Developer 2010 Express。
> - 如何使用 Visual Studio 中的功能以使用 ASP.NET Razor 页面，包括 IntelliSense 和调试程序。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
>
> - ASP.NET 网页 (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> 本教程也适用于 ASP.NET Web Pages 2、 Visual Studio 2012、 Visual Studio 2010 中，和 WebMatrix 2。


您可以使用 Razor 语法使用 WebMatrix 或许多其他代码编辑器中编写的 ASP.NET Web pages。 此外可以使用 Microsoft Visual Studio 是一个全功能集成的开发环境 (IDE)，用于创建许多类型的应用程序 （而不仅仅是网站） 提供一组强大的工具。 若要使用 ASP.NET Razor 页面，可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

Visual Studio 提供了使用 ASP.NET Razor web 页面进行编程的两个特别有用功能是：

- *IntelliSense*。 Visual Studio 中内置的 IntelliSense 功能并更全面比在 WebMatrix 中的 IntelliSense。
- *调试器*。 调试程序，可通过停止程序，而是运行、 检查变量和单步执行代码逐行排查代码。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Visual Studio 中使用不同版本的 ASP.NET 网页

若要开发 Visual Studio 2017 中的 ASP.NET web 应用程序，安装**ASP.NET 和 web 开发**工作负荷。

Visual Studio 2012 和 Visual Studio 2013 包括支持适用于 ASP.NET 网页。 （为了支持 ASP.NET Web Pages 需要安装包时安装 Visual Studio。）

Visual Studio 2010 不包括支持默认情况下为 ASP.NET Web Pages。 若要使用 Visual Studio 2010 中使用 ASP.NET Web Pages，必须安装 ASP.NET MVC 包。 若要获取 ASP.NET Web Pages 2，你安装 ASP.NET MVC 4。

下表总结了不同版本的 Visual Studio 中的支持为 ASP.NET Web Pages。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 网页 2** | 安装 ASP.NET MVC 4 | （包含） | （包含） |
| **ASP.NET 网页 3** |  | 更新到 ASP.NET Web Pages 3 通过 NuGet | （包含） |

若要使用 Visual Studio 2010，请参阅[安装支持的 ASP.NET Web Pages Visual Studio 2010 中](#vs2010support)。

## <a name="launching-visual-studio-from-webmatrix"></a>启动 Visual Studio 中的从 WebMatrix

如果你在 WebMatrix 中启动项目，并想要切换到 Visual Studio，WebMatrix 提供了用于轻松地在 Visual Studio 中打开项目的按钮。 必须具有 Visual Studio 安装在计算机中的此按钮才可用。 下图显示在 WebMatrix 中的按钮。

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

当单击按钮时，在 Visual Studio 中打开该项目。 您可以来回切换 WebMatrix 和 Visual Studio 之间没有任何问题。 如果任何文件在其他环境中已更改并且需要重新加载以获取最新更改，你将收到通知。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>在 Visual Studio 中创建 ASP.NET Razor 站点

在 Visual Studio 中创建 ASP.NET Razor 网站：

1. 打开 Visual Studio。
2. 在中**文件**菜单上，单击**新的 Web 站点**。

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 在中**新的 Web 站点**对话框框中，选择要使用 （Visual C# 或 Visual Basic） 的语言。
4. 选择**ASP.NET Web 站点 (Razor)** 模板。

    ![razor 站点](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. 单击 **“确定”**。

新的项目存在，并填入一些默认 web 页，以帮助您入门。

### <a name="using-intellisense"></a>Using IntelliSense

现在，已创建一个站点，您可以看到在 Visual Studio 中的 IntelliSense 工作原理。

1. 在刚刚创建的网站，打开*Default.cshtml*页。
2. 之后`<h3>`标记在页中，键入`@ServerInfo.`（包含句点）。 请注意 IntelliSense 如何在显示的可用方法`ServerInfo`下拉列表中的帮助程序。

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 选择`GetHtml`方法从列表中，然后按 Enter。 IntelliSense 会自动填充该方法。 (如 C# 中的任何方法，则你必须添加`()`方法之后的字符。)已完成的代码`GetHtml`方法看起来如下例所示：

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 按 Ctrl + F5 以运行该页。 这是页面看起来像时显示在浏览器中：

    ![在浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 关闭浏览器。

### <a name="using-the-debugger"></a>使用调试器

1. 在顶部*Default.cshtml*页上，开头的行后`Page.Title`，添加以下代码行：

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 在左侧的代码编辑器的灰色边距中，单击此新行的旁边以添加*断点*。 断点是一个标记，通知调试器停止在该点运行该程序，以便您可以看到发生了什么情况。

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 删除对调用`ServerInfo.GetHtml`方法，并添加对调用`@myTime`变量在其原位置。 此调用显示新的代码行返回的当前时间值。
4. 按 F5 以在调试器中运行该页。 页面设置的断点处停止。 下图显示了页面外观在编辑器中使用断点 （用黄色）。

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 在调试工具栏中，单击**单步执行**按钮 （或按 F11） 以运行下的一行代码。 每次单击此按钮，则在前进执行到下一行代码。

    ![单步执行按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 检查的值`myTime`变量在其上停留鼠标指针或通过检查中显示的值**局部变量**并**调用堆栈**windows。 Visual Studio 显示变量的值。

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 完成检查变量和单步执行代码时，按 F5 继续运行而无需停止在每个行的页。 已完成逐步调试所有代码，浏览器显示的页面。

若要了解有关调试器以及如何在 Visual Studio 中调试代码的详细信息，请参阅[演练： 在 Visual Web Developer 中调试 Web Pages](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>在使用 Visual Studio 的 ASP.NET MVC 项目中使用 Razor

Razor 语法还在 ASP.NET MVC 项目中广泛使用。 MVC 是功能强大、 基于模式的方式来构建动态网站。 如果你的 ASP.NET Web Pages 站点变得难以维护，您可能需要考虑将其转换为 ASP.NET MVC 应用程序。 创建 MVC 应用程序的示例，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>在 Visual Studio 2010 中安装 ASP.NET Web pages 支持

本部分演示如何安装 Visual Web Developer 学习版 2010年和 ASP.NET Web Pages Tools for Visual Studio。

1. 如果还没有 Web 平台安装程序，请从以下 URL 下载：

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 运行 Web 平台安装程序。
3. 单击**产品**选项卡。

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 搜索**ASP.NET MVC 4** （适用于 ASP.NET Web Pages 2)，然后单击**添加**。 这些产品包括 Visual Studio 工具，用于构建 ASP.NET Razor 网站。

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 单击**安装**以完成安装。
