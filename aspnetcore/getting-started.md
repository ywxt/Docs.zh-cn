---
title: ASP.NET Core 入门
author: rick-anderson
description: 介绍如何使用 ASP.NET Core 创建并运行简单的 Hello World 应用的快速教程。
manager: wpickett
ms.author: riande
ms.date: 10/18/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: getting-started
ms.openlocfilehash: c2f18c69901a5a6503314d508a776e6985872681
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-aspnet-core"></a><span data-ttu-id="24621-103">ASP.NET Core 入门</span><span class="sxs-lookup"><span data-stu-id="24621-103">Get Started with ASP.NET Core</span></span>

> [!NOTE]
> <span data-ttu-id="24621-104">这些说明仅适用于 ASP.NET Core 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="24621-104">These instructions are for the latest version of ASP.NET Core.</span></span> <span data-ttu-id="24621-105">有关本文档 的1.1 版本，请参阅 [ASP.NET Core 1.1 入门](xref:getting-started-1.1)。</span><span class="sxs-lookup"><span data-stu-id="24621-105">See [Getting Started with ASP.NET Core 1.1](xref:getting-started-1.1) for the 1.1 version of this document.</span></span>

1. <span data-ttu-id="24621-106">安装 [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]。</span><span class="sxs-lookup"><span data-stu-id="24621-106">Install the [!INCLUDE [](~/includes/net-core-sdk-download-link.md)].</span></span>

2. <span data-ttu-id="24621-107">创建新的 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="24621-107">Create a new .NET Core project.</span></span>

   <span data-ttu-id="24621-108">在 macOS 和 Linux 上，打开终端窗口。</span><span class="sxs-lookup"><span data-stu-id="24621-108">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="24621-109">在 Windows 上，打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="24621-109">On Windows, open a command prompt.</span></span> <span data-ttu-id="24621-110">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="24621-110">Enter the following command:</span></span>

    ```terminal
    dotnet new razor -o aspnetcoreapp
    ```
    
3. <span data-ttu-id="24621-111">运行应用。</span><span class="sxs-lookup"><span data-stu-id="24621-111">Run the app.</span></span>

    <span data-ttu-id="24621-112">使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="24621-112">Use the following commands to run the app:</span></span>

    ```terminal
    cd aspnetcoreapp
    dotnet run
    ```

4. <span data-ttu-id="24621-113">浏览到 [http://localhost:5000](http://localhost:5000)</span><span class="sxs-lookup"><span data-stu-id="24621-113">Browse to [http://localhost:5000](http://localhost:5000)</span></span>

5. <span data-ttu-id="24621-114">打开 Pages/About.cshtml 并将页面修改为显示消息“Hello, world!</span><span class="sxs-lookup"><span data-stu-id="24621-114">Open <em>Pages/About.cshtml</em> and modify the page to display the message "Hello, world!</span></span> <span data-ttu-id="24621-115">The time on the server is @DateTime.Now”：</span><span class="sxs-lookup"><span data-stu-id="24621-115">The time on the server is @DateTime.Now ":</span></span>

    [!code-html[](getting-started/sample/getting-started/about.cshtml?highlight=9&range=1-9)]

6. <span data-ttu-id="24621-116">浏览到 [http://localhost:5000/About](http://localhost:5000/About) 并验证更改。</span><span class="sxs-lookup"><span data-stu-id="24621-116">Browse to [http://localhost:5000/About](http://localhost:5000/About) and verify the changes.</span></span>

### <a name="next-steps"></a><span data-ttu-id="24621-117">后续步骤</span><span class="sxs-lookup"><span data-stu-id="24621-117">Next steps</span></span>

<span data-ttu-id="24621-118">有关入门教程，请参阅 [ASP.NET Core 教程](tutorials/index.md)</span><span class="sxs-lookup"><span data-stu-id="24621-118">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="24621-119">有关 ASP.NET Core 概念和体系结构的简介，请参阅 [ASP.NET Core 简介](index.md)和 [ASP.NET Core 基础知识](fundamentals/index.md)。</span><span class="sxs-lookup"><span data-stu-id="24621-119">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="24621-120">ASP.NET Core 应用可使用 .NET Core 或.NET Framework 基类库和运行时。</span><span class="sxs-lookup"><span data-stu-id="24621-120">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="24621-121">有关详细信息，请参阅[在 .NET Core 和 .NET Framework 之间进行选择](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)。</span><span class="sxs-lookup"><span data-stu-id="24621-121">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
