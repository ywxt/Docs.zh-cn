---
title: "Mac、Linux 或 Windows 上的 ASP.NET Core MVC 简介"
author: rick-anderson
description: "Mac、Linux 和 Windows 上的 ASP.NET Core MVC 和 Visual Studio Code 入门"
manager: wpickett
ms.author: riande
ms.date: 07/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-xplat/start-mvc
ms.openlocfilehash: 4771555b66f328a819f17a32eb3959f9ecf33d44
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="getting-started-with-aspnet-core-mvc--on-mac-linux-or-windows"></a><span data-ttu-id="de97b-103">Mac、Linux 或 Windows 上的 ASP.NET Core MVC 入门</span><span class="sxs-lookup"><span data-stu-id="de97b-103">Getting started with ASP.NET Core MVC  on Mac, Linux, or Windows</span></span>

<span data-ttu-id="de97b-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="de97b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="de97b-105">本教程将介绍基础知识，指导你使用 [Visual Studio Code](https://code.visualstudio.com) (VS Code) 构建 ASP.NET Core MVC Web 应用。</span><span class="sxs-lookup"><span data-stu-id="de97b-105">This tutorial will teach you the basics of building an ASP.NET Core MVC web app using [Visual Studio Code](https://code.visualstudio.com) (VS Code).</span></span> <span data-ttu-id="de97b-106">本教程假定用户熟悉 VS Code。</span><span class="sxs-lookup"><span data-stu-id="de97b-106">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="de97b-107">有关详细信息，请参阅 [VS Code 入门](https://code.visualstudio.com/docs) 和 [Visual Studio Code 帮助](#visual-studio-code-help)。</span><span class="sxs-lookup"><span data-stu-id="de97b-107">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span> 

[!INCLUDE[consider RP](../../includes/razor.md)]

<span data-ttu-id="de97b-108">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="de97b-108">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="de97b-109">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="de97b-109">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="de97b-110">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="de97b-110">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="de97b-111">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="de97b-111">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span> 

## <a name="install-vs-code-and-net-core"></a><span data-ttu-id="de97b-112">安装 VS Code 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="de97b-112">Install VS Code and .NET Core</span></span>

<span data-ttu-id="de97b-113">本教程需要 [.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="de97b-113">This tutorial requires the [.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later.</span></span> <span data-ttu-id="de97b-114">请参阅适用于 ASP.NET Core 1.1 版本的 [PDF](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/first-mvc-app-mac/start-mvc/8-23-17.pdf)。</span><span class="sxs-lookup"><span data-stu-id="de97b-114">See [the pdf](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/first-mvc-app-mac/start-mvc/8-23-17.pdf) for the ASP.NET Core 1.1 version.</span></span>

<span data-ttu-id="de97b-115">安装以下组件：</span><span class="sxs-lookup"><span data-stu-id="de97b-115">Install the following:</span></span>

* <span data-ttu-id="de97b-116">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="de97b-116">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later.</span></span>
* [<span data-ttu-id="de97b-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="de97b-117">Visual Studio Code</span></span>](https://code.visualstudio.com)
* <span data-ttu-id="de97b-118">VS Code [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="de97b-118">VS Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span> 

## <a name="create-a-web-app-with-dotnet"></a><span data-ttu-id="de97b-119">通过 dotnet 创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="de97b-119">Create a web app with dotnet</span></span>

<span data-ttu-id="de97b-120">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="de97b-120">From a terminal, run the following commands:</span></span>

```console
mkdir MvcMovie
cd MvcMovie
dotnet new mvc
```

<span data-ttu-id="de97b-121">在 Visual Studio Code (VS Code) 中打开“MvcMovie”文件夹并选择“Startup.cs”文件。</span><span class="sxs-lookup"><span data-stu-id="de97b-121">Open the *MvcMovie* folder in Visual Studio Code (VS Code) and select the *Startup.cs* file.</span></span>

- <span data-ttu-id="de97b-122">对于警告消息 -“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”，。</span><span class="sxs-lookup"><span data-stu-id="de97b-122">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'MvcMovie'.</span></span> <span data-ttu-id="de97b-123">请选择“是”</span><span class="sxs-lookup"><span data-stu-id="de97b-123">Add them?"</span></span>
- <span data-ttu-id="de97b-124">对于信息性消息 -“存在未解析的依赖项”，请选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="de97b-124">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

![带有“"MvcMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”](../web-api-vsc/_static/vsc_restore.png)

<span data-ttu-id="de97b-128">按“调试”(F5) 生成并运行程序。</span><span class="sxs-lookup"><span data-stu-id="de97b-128">Press **Debug** (F5) to build and run the program.</span></span>

![正在运行的应用](../first-mvc-app/start-mvc/_static/1.png)

<span data-ttu-id="de97b-130">VS Code 启动 [Kestrel](xref:fundamentals/servers/kestrel) Web 服务器并运行应用。</span><span class="sxs-lookup"><span data-stu-id="de97b-130">VS Code starts the [Kestrel](xref:fundamentals/servers/kestrel) web server and runs your app.</span></span> <span data-ttu-id="de97b-131">请注意，地址栏显示 `localhost:5000` 而非 `example.com` 等内容。</span><span class="sxs-lookup"><span data-stu-id="de97b-131">Notice that the address bar shows `localhost:5000` and not something like `example.com`.</span></span> <span data-ttu-id="de97b-132">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="de97b-132">That's because `localhost` is the standard hostname for your local computer.</span></span>

<span data-ttu-id="de97b-133">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="de97b-133">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="de97b-134">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="de97b-134">The browser image above doesn't show these links.</span></span> <span data-ttu-id="de97b-135">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="de97b-135">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](../first-mvc-app/start-mvc/_static/2.png)

<span data-ttu-id="de97b-137">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="de97b-137">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

## <a name="visual-studio-code-help"></a><span data-ttu-id="de97b-138">Visual Studio Code 帮助</span><span class="sxs-lookup"><span data-stu-id="de97b-138">Visual Studio Code help</span></span>

- [<span data-ttu-id="de97b-139">入门</span><span class="sxs-lookup"><span data-stu-id="de97b-139">Getting started</span></span>](https://code.visualstudio.com/docs)
- [<span data-ttu-id="de97b-140">调试</span><span class="sxs-lookup"><span data-stu-id="de97b-140">Debugging</span></span>](https://code.visualstudio.com/docs/editor/debugging)
- [<span data-ttu-id="de97b-141">集成终端</span><span class="sxs-lookup"><span data-stu-id="de97b-141">Integrated terminal</span></span>](https://code.visualstudio.com/docs/editor/integrated-terminal)
- [<span data-ttu-id="de97b-142">键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="de97b-142">Keyboard shortcuts</span></span>](https://code.visualstudio.com/docs/getstarted/keybindings#_keyboard-shortcuts-reference)

  - [<span data-ttu-id="de97b-143">Mac 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="de97b-143">Mac keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
  - [<span data-ttu-id="de97b-144">Linux 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="de97b-144">Linux keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
  - [<span data-ttu-id="de97b-145">Windows 键盘快捷键</span><span class="sxs-lookup"><span data-stu-id="de97b-145">Windows keyboard shortcuts</span></span>](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

>[!div class="step-by-step"]
[<span data-ttu-id="de97b-146">下一篇 - 添加控制器</span><span class="sxs-lookup"><span data-stu-id="de97b-146">Next - Add a controller</span></span>](adding-controller.md)
