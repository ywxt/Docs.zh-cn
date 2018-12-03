---
title: ASP.NET Core MVC 和 Visual Studio 入门
author: rick-anderson
description: 了解如何开始使用 ASP.NET Core MVC 和 Visual Studio。
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 9d50607899058c887597a3d73198552d3ef5b020
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710083"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a>ASP.NET Core MVC 和 Visual Studio 入门

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

本教程提供 3 个版本：

* macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)
* macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)

> [!NOTE]
> 我们要测试所建议的新的 ASP.NET Core 目录结构是否可用。  如果你有几分钟时间进行练习，来了解当前目录或所建议目录中的 7 个不同主题，请[单击此处来参与调查](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5)。

## <a name="install-visual-studio-and-net-core"></a>安装 Visual Studio 和 .NET Core

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-web-app"></a>创建 Web 应用

在 Visual Studio 中，选择“文件”>“新建”>“项目”。

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

填写“新建项目”对话框：

* 在左侧窗格中，点击“.NET Core”
* 在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”
* 将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）
* 点击“确定”

![新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web ](start-mvc/_static/new_project2-21.png)

完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：

* 在版本选择器下拉框中选择“ASP.NET Core 2.1”
* 选择“Web 应用(模型-视图-控制器)”
* 点击“确定”

![新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web ](start-mvc/_static/new_project22-21.png)

Visual Studio 为刚刚创建的 MVC 项目使用默认模板。 输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。 这是一个基本的初学者项目，适合入门使用。

点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)

* Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。 请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。 这是因为 `localhost` 是本地计算机的标准主机名。 Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。 在上图中，端口号为 5000。 浏览器中的 URL 显示 `localhost:5000`。 运行应用时，将看到不同的端口号。
* 使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。 许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。
* 可以从“调试”菜单项中以调试或非调试模式启动应用：

![调试菜单](start-mvc/_static/debug_menu.png)

* 可以通过点击“IIS Express”按钮来调试应用

![IIS Express](start-mvc/_static/iis_express.png)

默认模板提供可用的“主页”、“关于”和“联系”链接。 上面的浏览器图像未显示这些链接。 根据浏览器的大小，可能需要单击导航图标才能显示这些链接。

![右上角的导航图标](start-mvc/_static/2.png)

如果正在调试模式下运行，点击“Shift-F5”以停止调试。

在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-web-app"></a>创建 Web 应用

在 Visual Studio 中，选择“文件”>“新建”>“项目”。

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

填写“新建项目”对话框：

* 在左侧窗格中，点击“.NET Core”
* 在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”
* 将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）
* 点击“确定”

![新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web ](start-mvc/_static/new_project2.png)

完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：

* 在版本选择器下拉框中选择“ASP.NET Core 2.-”
* 选择“Web 应用程序(Model-View-Controller)”
* 点击“确定”

![新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web ](start-mvc/_static/new_project22.png)

Visual Studio 为刚刚创建的 MVC 项目使用默认模板。 输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。 这是一个基本的初学者项目，适合入门使用。

点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)

* Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。 请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。 这是因为 `localhost` 是本地计算机的标准主机名。 Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。 在上图中，端口号为 5000。 浏览器中的 URL 显示 `localhost:5000`。 运行应用时，将看到不同的端口号。
* 使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。 许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。
* 可以从“调试”菜单项中以调试或非调试模式启动应用：

![调试菜单](start-mvc/_static/debug_menu.png)

* 可以通过点击“IIS Express”按钮来调试应用

![IIS Express](start-mvc/_static/iis_express.png)

默认模板提供可用的“主页”、“关于”和“联系”链接。 上面的浏览器图像未显示这些链接。 根据浏览器的大小，可能需要单击导航图标才能显示这些链接。

![右上角的导航图标](start-mvc/_static/2.png)

如果正在调试模式下运行，点击“Shift-F5”以停止调试。

在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。

::: moniker-end

> [!div class="step-by-step"]
> [下一篇](adding-controller.md)  
