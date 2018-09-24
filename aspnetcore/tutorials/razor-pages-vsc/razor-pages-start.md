---
title: 在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面
author: rick-anderson
description: 了解使用 Visual Studio Code 生成 ASP.NET Core Razor 页面 Web 应用的基础知识。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: b7f6ca377a892fce912dc0ee9d4b7378f40fbf24
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2018
ms.locfileid: "46522922"
---
# <a name="get-started-with-aspnet-core-razor-pages-in-visual-studio-code"></a><span data-ttu-id="72934-103">在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面</span><span class="sxs-lookup"><span data-stu-id="72934-103">Get started with ASP.NET Core Razor Pages in Visual Studio Code</span></span>

<span data-ttu-id="72934-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="72934-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="72934-105">本教程介绍构建 ASP.NET Core Razor 页面 Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="72934-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="72934-106">我们建议在学习本教程前先阅读 [Razor 页面介绍](xref:razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="72934-106">We recommend you complete [Introduction to Razor Pages](xref:razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="72934-107">Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="72934-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72934-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="72934-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-vscode.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="72934-109">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="72934-109">Create a Razor web app</span></span>

<span data-ttu-id="72934-110">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="72934-110">From a terminal, run the following commands:</span></span>

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

<span data-ttu-id="72934-111">上述命令使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="72934-111">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="72934-112">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="72934-112">Open a browser to http://localhost:5000 to view the application.</span></span>

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="72934-114">打开项目</span><span class="sxs-lookup"><span data-stu-id="72934-114">Open the project</span></span>

<span data-ttu-id="72934-115">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="72934-115">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="72934-116">在 Visual Studio Code (VS Code) 中，选择“文件”>“打开文件夹”，然后选择“RazorPagesMovie”文件夹。</span><span class="sxs-lookup"><span data-stu-id="72934-116">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="72934-117">对警告消息“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”选择“是”</span><span class="sxs-lookup"><span data-stu-id="72934-117">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="72934-118">。</span><span class="sxs-lookup"><span data-stu-id="72934-118">Add them?"</span></span>
- <span data-ttu-id="72934-119">对信息性消息“存在未解析的依赖项”选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="72934-119">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="72934-120">启动应用</span><span class="sxs-lookup"><span data-stu-id="72934-120">Launch the app</span></span>

<span data-ttu-id="72934-121">按 Ctrl+F5 启动应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="72934-121">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="72934-122">或者，从“调试”菜单中选择“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="72934-122">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="72934-123">在下一个教程中，我们将向项目添加模型。</span><span class="sxs-lookup"><span data-stu-id="72934-123">In the next tutorial, we add a model to the project.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="72934-124">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="72934-124">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
