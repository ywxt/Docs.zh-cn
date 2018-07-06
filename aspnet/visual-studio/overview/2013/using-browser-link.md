---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用浏览器链接 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 9da93c279bfa2af614733e3234ba62429abf688a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822190"
---
<a name="using-browser-link-in-visual-studio-2013"></a>在 Visual Studio 2013 中使用浏览器链接
====================
通过[Mike Wasson](https://github.com/MikeWasson)

浏览器链接是创建开发环境和一个或多个 web 浏览器之间的通信通道的 Visual Studio 2013 中的新功能。 可以使用浏览器链接以刷新 web 应用程序在多个浏览器中的，这对于跨浏览器测试很有用。

- [刷新浏览器](#browser-refresh)
- [查看浏览器链接仪表板](#dashboard)
- [启用静态 HTML 文件的浏览器链接](#static-html)
- [禁用浏览器链接](#disabling)
- [它是如何工作的？](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>刷新浏览器

使用浏览器刷新，可以刷新已连接到 Visual Studio 中通过浏览器链接的多个浏览器。

若要使用浏览器刷新，首先创建 ASP.NET 应用程序，使用任何项目模板。 通过按 F5 或单击工具栏中的箭头图标来调试应用程序：

![](using-browser-link/_static/image1.png)

此外可以使用下拉列表中选择特定的浏览器进行调试。

![](using-browser-link/_static/image2.png)

若要使用多个浏览器进行调试，请选择**浏览方式**。 在中**浏览方式**对话框中，按住 CTRL 键以选择多个浏览器。 单击**浏览**使用所选的浏览器进行调试。 启动 Visual Studio 外部的浏览器并导航到应用程序 URL 也适用于浏览器链接。

![](using-browser-link/_static/image3.png)

浏览器链接控件位于具有循环的箭头图标在下拉列表中。 箭头图标**刷新**按钮。

![](using-browser-link/_static/image4.png)

若要查看哪些浏览器连接，将鼠标悬停**刷新**调试时的按钮。 在工具提示窗口中显示连接的浏览器。

![](using-browser-link/_static/image5.png)

若要刷新连接的浏览器，请单击**刷新**按钮或按 CTRL + ALT + ENTER。 例如，下面的屏幕截图显示了我使用 MVC 5 项目模板创建一个 ASP.NET 项目。 您可以看到在顶部的两个浏览器中运行的应用程序。 在底部，在 Visual Studio 中打开项目时。

![](using-browser-link/_static/image6.png)

在 Visual Studio 中，我更改了&lt;h1&gt;主页标题：

![](using-browser-link/_static/image7.png)

当我单击了**刷新**按钮，在这两个浏览器窗口中出现过更改：

![](using-browser-link/_static/image8.png)

**备注**

- 若要启用浏览器链接，请设置`debug=true`中[&lt;编译&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)项目的 Web.config 文件中的元素。
- 必须在 localhost 上运行应用程序。
- 该应用程序必须面向.NET 4.0 或更高版本。

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>查看浏览器链接仪表板

浏览器链接仪表板显示有关浏览器链接连接的信息。 若要查看仪表板，请选择浏览器链接下拉列表菜单 (下一步的小箭头**刷新**按钮)。 然后单击**浏览器链接仪表板**。

![](using-browser-link/_static/image9.png)

仪表板会列出连接的浏览器和每个浏览器导航到的 URL。

![](using-browser-link/_static/image10.png)

**先决条件**部分显示为该项目启用浏览器链接所需的任何步骤。 例如，以下屏幕截图显示了一个项目的"debug"设置为 false 的 Web.config 文件中。

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>启用静态 HTML 文件的浏览器链接

若要启用用于静态 HTML 文件浏览器链接，以下代码添加到 Web.config 文件。

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

出于性能原因，当你发布你的项目时删除此设置。

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>禁用浏览器链接

默认情况下会启用浏览器链接。 有几种方法，以禁用它：

- 在浏览器链接下拉列表菜单中，取消选中**启用浏览器链接**。 

    ![](using-browser-link/_static/image12.png)
- 在 Web.config 文件中，添加名为"vs: EnableBrowserLink"值"false"中的 appSettings 节的键。 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- 在 Web.config 文件中，设置为 false 的调试。 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>它是如何工作的？

使用浏览器链接[SignalR](../../../signalr/index.md)创建 Visual Studio 和浏览器之间的通信通道。 启用浏览器链接后，Visual Studio 将充当多个客户端 （浏览器） 可以连接到的 SignalR 服务器。 浏览器链接还会使用 ASP.NET 注册 HTTP 模块。 此模块将注入特殊&lt;脚本&gt;到每个页面请求来自服务器的引用。 通过在浏览器中选择"查看源"，可以看到脚本引用。

![](using-browser-link/_static/image13.png)

未修改的源文件。 HTTP 模块会动态注入脚本引用。

由于浏览器端代码是所有 JavaScript，它适用于所有浏览器的[SignalR 支持](../../../signalr/overview/getting-started/supported-platforms.md)，而无需任何浏览器插件。
