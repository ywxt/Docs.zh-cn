---
title: "利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面"
author: rick-anderson
description: "利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: 727c3d5c8bed0aef3094816b7e5f0a940aea654c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-razor-pages-in-aspnet-core-with-visual-studio-code"></a><span data-ttu-id="ce0c1-103">利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="ce0c1-103">Getting started with Razor Pages in ASP.NET Core with Visual Studio Code</span></span>

<span data-ttu-id="ce0c1-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ce0c1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ce0c1-105">本教程介绍构建 ASP.NET Core Razor 页面 Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="ce0c1-106">我们建议在学习本教程前先阅读 [Razor 页面介绍](xref:mvc/razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-106">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="ce0c1-107">Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce0c1-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="ce0c1-108">Prerequisites</span></span>

<span data-ttu-id="ce0c1-109">安装以下组件：</span><span class="sxs-lookup"><span data-stu-id="ce0c1-109">Install the following:</span></span>

* <span data-ttu-id="ce0c1-110">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ce0c1-110">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* [<span data-ttu-id="ce0c1-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ce0c1-111">Visual Studio Code</span></span>](https://code.visualstudio.com)
* <span data-ttu-id="ce0c1-112">VS Code [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="ce0c1-112">VS Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span> 

## <a name="create-a-razor-web-app"></a><span data-ttu-id="ce0c1-113">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="ce0c1-113">Create a Razor web app</span></span>

<span data-ttu-id="ce0c1-114">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="ce0c1-114">From a terminal, run the following commands:</span></span>

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="ce0c1-115">上述命令使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-115">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="ce0c1-116">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-116">Open a browser to http://localhost:5000 to view the application.</span></span>

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="ce0c1-118">打开项目</span><span class="sxs-lookup"><span data-stu-id="ce0c1-118">Open the project</span></span>

<span data-ttu-id="ce0c1-119">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-119">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="ce0c1-120">在 Visual Studio Code (VS Code) 中，选择“文件”>“打开文件夹”，然后选择“RazorPagesMovie”文件夹。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-120">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="ce0c1-121">对警告消息“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”选择“是”</span><span class="sxs-lookup"><span data-stu-id="ce0c1-121">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="ce0c1-122">。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-122">Add them?"</span></span>
- <span data-ttu-id="ce0c1-123">对信息性消息“存在未解析的依赖项”选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-123">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="ce0c1-124">启动应用</span><span class="sxs-lookup"><span data-stu-id="ce0c1-124">Launch the app</span></span>

<span data-ttu-id="ce0c1-125">按 Ctrl+F5 启动应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-125">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="ce0c1-126">或者，从“调试”菜单中选择“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-126">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="ce0c1-127">在下一个教程中，我们将向项目添加模型。</span><span class="sxs-lookup"><span data-stu-id="ce0c1-127">In the next tutorial, we add a model to the project.</span></span> 

>[!div class="step-by-step"]
[<span data-ttu-id="ce0c1-128">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="ce0c1-128">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
