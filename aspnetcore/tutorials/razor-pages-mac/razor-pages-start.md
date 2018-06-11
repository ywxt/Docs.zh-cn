---
title: 借助 Visual Studio for Mac 在 macOS 上的 ASP.NET Core 中开始使用 Razor 页面
author: rick-anderson
description: 了解如何借助 Visual Studio for Mac 在 ASP.NET Core 中开始使用 Razor 页面。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 07/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages-mac/razor-pages-start
ms.openlocfilehash: 29eb11d0195f483b144394e505dd63fb6016161b
ms.sourcegitcommit: 63fb07fb3f71b32daf2c9466e132f2e7cc617163
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2018
ms.locfileid: "35252329"
---
# <a name="get-started-with-razor-pages-in-aspnet-core-on-macos-with-visual-studio-for-mac"></a><span data-ttu-id="87f06-103">借助 Visual Studio for Mac 在 macOS 上的 ASP.NET Core 中开始使用 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="87f06-103">Get started with Razor Pages in ASP.NET Core on macOS with Visual Studio for Mac</span></span>

<span data-ttu-id="87f06-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="87f06-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="87f06-105">本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="87f06-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="87f06-106">建议在学习本教程前先查看 [Razor 页面介绍](xref:mvc/razor-pages/index)。</span><span class="sxs-lookup"><span data-stu-id="87f06-106">We recommend you review [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="87f06-107">Razor 页面是在 ASP.NET Core 中为 Web 应用程序生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="87f06-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87f06-108">系统必备</span><span class="sxs-lookup"><span data-stu-id="87f06-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-macos.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="87f06-109">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="87f06-109">Create a Razor web app</span></span>

<span data-ttu-id="87f06-110">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="87f06-110">From a terminal, run the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

<span data-ttu-id="87f06-112">上述命令使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="87f06-112">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="87f06-113">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="87f06-113">Open a browser to http://localhost:5000 to view the application.</span></span>

![主页或索引页](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="87f06-115">打开项目</span><span class="sxs-lookup"><span data-stu-id="87f06-115">Open the project</span></span>

<span data-ttu-id="87f06-116">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="87f06-116">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="87f06-117">在 Visual Studio 中，选择“文件”>“打开”，然后选择“RazorPagesMovie.csproj”文件。</span><span class="sxs-lookup"><span data-stu-id="87f06-117">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="87f06-118">启动应用</span><span class="sxs-lookup"><span data-stu-id="87f06-118">Launch the app</span></span>

<span data-ttu-id="87f06-119">在 Visual Studio 中，选择“运行”>“开始执行(不调试)”以启动应用。</span><span class="sxs-lookup"><span data-stu-id="87f06-119">In Visual Studio, select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="87f06-120">Visual Studio 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="87f06-120">Visual Studio starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5000`.</span></span>

<span data-ttu-id="87f06-121">在下一个教程中，我们将向项目添加模型。</span><span class="sxs-lookup"><span data-stu-id="87f06-121">In the next tutorial, we add a model to the project.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="87f06-122">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="87f06-122">Next: Adding a model</span></span>](xref:tutorials/razor-pages-mac/model)
