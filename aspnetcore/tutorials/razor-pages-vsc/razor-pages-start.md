---
title: 在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面
author: rick-anderson
description: 了解使用 Visual Studio Code 生成 ASP.NET Core Razor 页面 Web 应用的基础知识。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: f18d0a8b3ce24c9844b02f8a0b6360f7e1b1bdb7
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244848"
---
# <a name="get-started-with-aspnet-core-razor-pages-in-visual-studio-code"></a><span data-ttu-id="94eec-103">在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面</span><span class="sxs-lookup"><span data-stu-id="94eec-103">Get started with ASP.NET Core Razor Pages in Visual Studio Code</span></span>

<span data-ttu-id="94eec-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="94eec-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="94eec-105">本教程介绍构建 ASP.NET Core Razor 页面 Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="94eec-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="94eec-106">我们建议在学习本教程前先阅读 [Razor 页面介绍](xref:razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="94eec-106">We recommend you complete [Introduction to Razor Pages](xref:razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="94eec-107">Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="94eec-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94eec-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="94eec-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="94eec-109">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="94eec-109">Create a Razor web app</span></span>

<span data-ttu-id="94eec-110">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="94eec-110">From a terminal, run the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

<span data-ttu-id="94eec-111">上述命令使用 [.NET Core CLI](/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="94eec-111">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="94eec-112">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="94eec-112">Open a browser to http://localhost:5000 to view the application.</span></span>

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="94eec-114">打开项目</span><span class="sxs-lookup"><span data-stu-id="94eec-114">Open the project</span></span>

<span data-ttu-id="94eec-115">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="94eec-115">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="94eec-116">在 Visual Studio Code (VS Code) 中，选择“文件”>“打开文件夹”，然后选择“RazorPagesMovie”文件夹。</span><span class="sxs-lookup"><span data-stu-id="94eec-116">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="94eec-117">对警告消息“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”选择“是”</span><span class="sxs-lookup"><span data-stu-id="94eec-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="94eec-118">。</span><span class="sxs-lookup"><span data-stu-id="94eec-118">Add them?"</span></span>
- <span data-ttu-id="94eec-119">对信息性消息“存在未解析的依赖项”选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="94eec-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="94eec-120">启动应用</span><span class="sxs-lookup"><span data-stu-id="94eec-120">Launch the app</span></span>

<span data-ttu-id="94eec-121">在“调试”菜单中，选择“启动但不调试”。</span><span class="sxs-lookup"><span data-stu-id="94eec-121">From the **Debug** menu, select **Start Without Debugging**.</span></span> <span data-ttu-id="94eec-122">或者，也可以按菜单选项旁边显示的键盘快捷键。</span><span class="sxs-lookup"><span data-stu-id="94eec-122">Alternatively, you can press the keyboard shortcut displayed next to the menu option.</span></span> <span data-ttu-id="94eec-123">此快捷键因操作系统而异。</span><span class="sxs-lookup"><span data-stu-id="94eec-123">This shortcut varies depending on your operating system.</span></span>

<span data-ttu-id="94eec-124">在下一个教程中，我们将向项目添加模型。</span><span class="sxs-lookup"><span data-stu-id="94eec-124">In the next tutorial, we add a model to the project.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="94eec-125">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="94eec-125">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
