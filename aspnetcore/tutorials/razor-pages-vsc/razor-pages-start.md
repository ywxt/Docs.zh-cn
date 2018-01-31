---
title: "利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面"
author: rick-anderson
description: "利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面"
manager: wpickett
ms.author: riande
ms.date: 08/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages-vsc/razor-pages-start
ms.openlocfilehash: 7c01d802e59951281c86c8eab64b7c6b9d646fbf
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="getting-started-with-razor-pages-in-aspnet-core-with-visual-studio-code"></a><span data-ttu-id="4c894-103">利用 Visual Studio Code 在 ASP.NET Core 中开始使用 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="4c894-103">Getting started with Razor Pages in ASP.NET Core with Visual Studio Code</span></span>

<span data-ttu-id="4c894-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4c894-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4c894-105">本教程介绍构建 ASP.NET Core Razor 页面 Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4c894-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="4c894-106">我们建议在学习本教程前先阅读 [Razor 页面介绍](xref:mvc/razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="4c894-106">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="4c894-107">Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="4c894-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c894-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="4c894-108">Prerequisites</span></span>

<span data-ttu-id="4c894-109">安装以下组件：</span><span class="sxs-lookup"><span data-stu-id="4c894-109">Install the following:</span></span>

* <span data-ttu-id="4c894-110">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) 或更高版本</span><span class="sxs-lookup"><span data-stu-id="4c894-110">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* [<span data-ttu-id="4c894-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4c894-111">Visual Studio Code</span></span>](https://code.visualstudio.com)
* <span data-ttu-id="4c894-112">VS Code [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span><span class="sxs-lookup"><span data-stu-id="4c894-112">VS Code [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)</span></span> 

## <a name="create-a-razor-web-app"></a><span data-ttu-id="4c894-113">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="4c894-113">Create a Razor web app</span></span>

<span data-ttu-id="4c894-114">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="4c894-114">From a terminal, run the following commands:</span></span>

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="4c894-115">上述命令使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="4c894-115">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="4c894-116">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c894-116">Open a browser to http://localhost:5000 to view the application.</span></span>

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="4c894-118">打开项目</span><span class="sxs-lookup"><span data-stu-id="4c894-118">Open the project</span></span>

<span data-ttu-id="4c894-119">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c894-119">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="4c894-120">在 Visual Studio Code (VS Code) 中，选择“文件”>“打开文件夹”，然后选择“RazorPagesMovie”文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c894-120">From Visual Studio Code (VS Code), select **File > Open Folder**, and then select the *RazorPagesMovie* folder.</span></span>

- <span data-ttu-id="4c894-121">对警告消息“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”选择“是”</span><span class="sxs-lookup"><span data-stu-id="4c894-121">Select **Yes** to the **Warn** message "Required assets to build and debug are missing from 'RazorPagesMovie'.</span></span> <span data-ttu-id="4c894-122">。</span><span class="sxs-lookup"><span data-stu-id="4c894-122">Add them?"</span></span>
- <span data-ttu-id="4c894-123">对信息性消息“存在未解析的依赖项”选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="4c894-123">Select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="4c894-124">启动应用</span><span class="sxs-lookup"><span data-stu-id="4c894-124">Launch the app</span></span>

<span data-ttu-id="4c894-125">按 Ctrl+F5 启动应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="4c894-125">Press Ctrl+F5 to start the app without debugging.</span></span> <span data-ttu-id="4c894-126">或者，从“调试”菜单中选择“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="4c894-126">Alternatively, from the **Debug** menu, select **Start Without Debugging**.</span></span>

<span data-ttu-id="4c894-127">在下一个教程中，我们将向项目添加模型。</span><span class="sxs-lookup"><span data-stu-id="4c894-127">In the next tutorial, we add a model to the project.</span></span> 

>[!div class="step-by-step"]
[<span data-ttu-id="4c894-128">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="4c894-128">Next: Adding a model</span></span>](xref:tutorials/razor-pages-vsc/model)  
