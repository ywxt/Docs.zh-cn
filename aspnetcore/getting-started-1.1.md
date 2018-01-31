---
title: "ASP.NET Core 1.1 入门"
author: rick-anderson
description: "介绍如何使用 ASP.NET Core 1.1 创建并运行简单的 Hello World 应用的快速教程。"
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started-1.1
ms.openlocfilehash: 895e91efbba931923540e4cd182862cbc1851585
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="getting-started-with-aspnet-core-11"></a><span data-ttu-id="d4c97-103">ASP.NET Core 1.1 入门</span><span class="sxs-lookup"><span data-stu-id="d4c97-103">Getting Started with ASP.NET Core 1.1</span></span>

> [!NOTE]
> <span data-ttu-id="d4c97-104">这些说明适用于 ASP.NET Core 1.1。</span><span class="sxs-lookup"><span data-stu-id="d4c97-104">These instructions are for ASP.NET Core 1.1.</span></span> <span data-ttu-id="d4c97-105">在寻找最新版本？</span><span class="sxs-lookup"><span data-stu-id="d4c97-105">Looking for the latest version?</span></span> <span data-ttu-id="d4c97-106">请参阅[本教程的当前版本](xref:getting-started)。</span><span class="sxs-lookup"><span data-stu-id="d4c97-106">See [the current version of this tutorial](xref:getting-started).</span></span>

1. <span data-ttu-id="d4c97-107">从 [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 下载页面](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md)安装 SDK 1.0.4 的 .NET Core SDK 安装程序。</span><span class="sxs-lookup"><span data-stu-id="d4c97-107">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 downloads page](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md).</span></span>

2. <span data-ttu-id="d4c97-108">为新 .NET Core 项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="d4c97-108">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="d4c97-109">在 macOS 和 Linux 上，打开终端窗口。</span><span class="sxs-lookup"><span data-stu-id="d4c97-109">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="d4c97-110">在 Windows 上，打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="d4c97-110">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

2. <span data-ttu-id="d4c97-111">如果已计算机上安装了 SDK 的更高版本，则创建一个 global.json 文件以选择 1.0.4 SDK。</span><span class="sxs-lookup"><span data-stu-id="d4c97-111">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

2. <span data-ttu-id="d4c97-112">创建新的 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="d4c97-112">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```
   
3.  <span data-ttu-id="d4c97-113">还原程序包。</span><span class="sxs-lookup"><span data-stu-id="d4c97-113">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

4. <span data-ttu-id="d4c97-114">运行应用。</span><span class="sxs-lookup"><span data-stu-id="d4c97-114">Run the app.</span></span>

   <span data-ttu-id="d4c97-115">如有需要，`dotnet run` 命令会首先生成应用。</span><span class="sxs-lookup"><span data-stu-id="d4c97-115">The `dotnet run` command builds the app first if needed.</span></span>

   ```terminal
   dotnet run
   ```

5. <span data-ttu-id="d4c97-116">浏览到 `http://localhost:5000`</span><span class="sxs-lookup"><span data-stu-id="d4c97-116">Browse to `http://localhost:5000`</span></span>

<!-- H3 to avoid a single-entry internal TOC -->
### <a name="next-steps"></a><span data-ttu-id="d4c97-117">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d4c97-117">Next steps</span></span>

<span data-ttu-id="d4c97-118">有关入门教程，请参阅 [ASP.NET Core 教程](tutorials/index.md)</span><span class="sxs-lookup"><span data-stu-id="d4c97-118">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="d4c97-119">有关 ASP.NET Core 概念和体系结构的简介，请参阅 [ASP.NET Core 简介](index.md)和 [ASP.NET Core 基础知识](fundamentals/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d4c97-119">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="d4c97-120">ASP.NET Core 应用可使用 .NET Core 或.NET Framework 基类库和运行时。</span><span class="sxs-lookup"><span data-stu-id="d4c97-120">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="d4c97-121">有关详细信息，请参阅[在 .NET Core 和 .NET Framework 之间进行选择](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)。</span><span class="sxs-lookup"><span data-stu-id="d4c97-121">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
