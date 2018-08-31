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
# <a name="introduction-to-aspnet-core-mvc-on-macos-linux-or-windows"></a><span data-ttu-id="443a3-103">macOS、Linux 或 Windows 上的 ASP.NET Core MVC 简介</span><span class="sxs-lookup"><span data-stu-id="443a3-103">Introduction to ASP.NET Core MVC on macOS, Linux, or Windows</span></span>

<span data-ttu-id="443a3-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="443a3-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="443a3-105">本教程将介绍基础知识，指导你使用 [Visual Studio Code](https://code.visualstudio.com) (VS Code) 构建 ASP.NET Core MVC Web 应用。</span><span class="sxs-lookup"><span data-stu-id="443a3-105">This tutorial will teach you the basics of building an ASP.NET Core MVC web app using [Visual Studio Code](https://code.visualstudio.com) (VS Code).</span></span> <span data-ttu-id="443a3-106">本教程假定用户熟悉 VS Code。</span><span class="sxs-lookup"><span data-stu-id="443a3-106">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="443a3-107">有关详细信息，请参阅 [VS Code 入门](https://code.visualstudio.com/docs) 和 [Visual Studio Code 帮助](#visual-studio-code-help)。</span><span class="sxs-lookup"><span data-stu-id="443a3-107">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span> 

[!INCLUDE [consider RP](../../includes/razor.md)]

<span data-ttu-id="443a3-108">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="443a3-108">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="443a3-109">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="443a3-109">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="443a3-110">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="443a3-110">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="443a3-111">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="443a3-111">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="443a3-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="443a3-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-web-app-with-dotnet"></a><span data-ttu-id="443a3-113">通过 dotnet 创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="443a3-113">Create a web app with dotnet</span></span>

<span data-ttu-id="443a3-114">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="443a3-114">From a terminal, run the following commands:</span></span>

```console
mkdir MvcMovie
cd MvcMovie
dotnet new mvc
```

<span data-ttu-id="443a3-115">在 Visual Studio Code (VS Code) 中打开“MvcMovie”文件夹并选择“Startup.cs”文件。</span><span class="sxs-lookup"><span data-stu-id="443a3-115">Open the *MvcMovie* folder in Visual Studio Code (VS Code) and select the *Startup.cs* file.</span></span>

- <span data-ttu-id="443a3-116">对于警告消息 -“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”，。</span><span class="sxs-lookup"><span data-stu-id="443a3-116">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'MvcMovie'.</span></span> <span data-ttu-id="443a3-117">请选择“是”</span><span class="sxs-lookup"><span data-stu-id="443a3-117">Add them?"</span></span>
- <span data-ttu-id="443a3-118">对于信息性消息 -“存在未解析的依赖项”，请选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="443a3-118">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

![带有“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”](../web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="443a3-122">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="443a3-122">Press **Debug** (F5) to build and run the program.</span></span>

![正在运行的应用](../first-mvc-app/start-mvc/_static/1.png)

<span data-ttu-id="443a3-124">VS Code 启动 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器并运行应用。</span><span class="sxs-lookup"><span data-stu-id="443a3-124">VS Code starts the [Kestrel](xref:fundamentals/servers/kestrel) web server and runs your app.</span></span> <span data-ttu-id="443a3-125">请注意，地址栏显示 `localhost:5000` 而非 `example.com` 等内容。</span><span class="sxs-lookup"><span data-stu-id="443a3-125">Notice that the address bar shows `localhost:5000` and not something like `example.com`.</span></span> <span data-ttu-id="443a3-126">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="443a3-126">That's because `localhost` is the standard hostname for your local computer.</span></span>

<span data-ttu-id="443a3-127">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="443a3-127">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="443a3-128">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="443a3-128">The browser image above doesn't show these links.</span></span> <span data-ttu-id="443a3-129">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="443a3-129">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](../first-mvc-app/start-mvc/_static/2.png)

<span data-ttu-id="443a3-131">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="443a3-131">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

## <a name="visual-studio-code-help"></a><span data-ttu-id="443a3-132">Visual Studio Code 帮助</span><span class="sxs-lookup"><span data-stu-id="443a3-132">Visual Studio Code help</span></span>

- [<span data-ttu-id="443a3-133">入门</span><span class="sxs-lookup"><span data-stu-id="443a3-133">Getting started</span></span>](https://code.visualstudio.com/docs)
- [<span data-ttu-id="443a3-134">调试</span><span class="sxs-lookup"><span data-stu-id="443a3-134">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
- [<span data-ttu-id="443a3-135">集成终端</span><span class="sxs-lookup"><span data-stu-id="443a3-135">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [<span data-ttu-id="443a3-136">键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="443a3-136">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [<span data-ttu-id="443a3-137">macOS 键盘快捷方式</span><span class="sxs-lookup"><span data-stu-id="443a3-137">macOS keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [<span data-ttu-id="443a3-138">Linux 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="443a3-138">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [<span data-ttu-id="443a3-139">Windows 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="443a3-139">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

> [!div class="step-by-step"]
> [<span data-ttu-id="443a3-140">下一篇 - 添加控制器</span><span class="sxs-lookup"><span data-stu-id="443a3-140">Next - Add a controller</span></span>](adding-controller.md)
