---
title: macOS、Linux 或 Windows 上的 ASP.NET Core MVC 简介
author: rick-anderson
description: 了解如何在 macOS、Linux 和 Windows 上开始使用 ASP.NET Core MVC 和 Visual Studio Code
ms.author: riande
ms.date: 07/07/2017
uid: tutorials/first-mvc-app-xplat/start-mvc
ms.openlocfilehash: b25ee29541e345a3bf6700b67d992409c02b183a
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "36275270"
---
# <a name="introduction-to-aspnet-core-mvc-on-macos-linux-or-windows"></a>macOS、Linux 或 Windows 上的 ASP.NET Core MVC 简介

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本教程将介绍基础知识，指导你使用 [Visual Studio Code](https://code.visualstudio.com) (VS Code) 构建 ASP.NET Core MVC Web 应用。 本教程假定用户熟悉 VS Code。 有关详细信息，请参阅 [VS Code 入门](https://code.visualstudio.com/docs) 和 [Visual Studio Code 帮助](#visual-studio-code-help)。 

[!INCLUDE [consider RP](../../includes/razor.md)]

本教程提供 3 个版本：

* macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)
* macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc) 

## <a name="prerequisites"></a>系统必备

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-web-app-with-dotnet"></a>通过 dotnet 创建 Web 应用

从终端运行以下命令：

```console
mkdir MvcMovie
cd MvcMovie
dotnet new mvc
```

在 Visual Studio Code (VS Code) 中打开“MvcMovie”文件夹并选择“Startup.cs”文件。

- 对于警告消息 -“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”，。 请选择“是”
- 对于信息性消息 -“存在未解析的依赖项”，请选择“还原”。

![带有“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?” 警告的 VS Code “不再询问”、“稍后再说”、“是”以及“信息 - 存在未解决的依赖项”-“还原”-“关闭”](../web-api-vsc/_static/vsc_restore.png)

按“调试”(F5) 生成并运行程序。

![正在运行的应用](../first-mvc-app/start-mvc/_static/1.png)

VS Code 启动 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器并运行应用。 请注意，地址栏显示 `localhost:5000` 而非 `example.com` 等内容。 这是因为 `localhost` 是本地计算机的标准主机名。

默认模板提供可用的“主页”、“关于”和“联系”链接。 上面的浏览器图像未显示这些链接。 根据浏览器的大小，可能需要单击导航图标才能显示这些链接。

![右上角的导航图标](../first-mvc-app/start-mvc/_static/2.png)

在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。

## <a name="visual-studio-code-help"></a>Visual Studio Code 帮助

- [入门](https://code.visualstudio.com/docs)
- [调试](https://code.visualstudio.com/docs/editor/debugging)
- [集成终端](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [键盘快捷键](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [macOS 键盘快捷方式](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [Linux 键盘快捷键](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [Windows 键盘快捷键](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

> [!div class="step-by-step"]
> [下一篇 - 添加控制器](adding-controller.md)
