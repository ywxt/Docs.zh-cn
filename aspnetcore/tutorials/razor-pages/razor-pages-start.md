---
title: 在 ASP.NET Core 中开始使用 Razor Pages
author: rick-anderson
description: 了解构建 ASP.NET Core Razor 页面 Web 应用的基础知识。 Razor 页面推荐用于 ASP.NET Core 中的 Web 工作负载。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 12/22/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: caf4376c0a02931eeec85e5067a082b37ef9da68
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="fcd27-104">在 ASP.NET Core 中开始使用 Razor Pages</span><span class="sxs-lookup"><span data-stu-id="fcd27-104">Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="fcd27-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fcd27-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fcd27-106">本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="fcd27-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="fcd27-107">Razor Pages 是在 ASP.NET Core 中为 Web 应用生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="fcd27-107">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="fcd27-108">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="fcd27-108">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="fcd27-109">Windows：本教程</span><span class="sxs-lookup"><span data-stu-id="fcd27-109">Windows: This tutorial</span></span>
* <span data-ttu-id="fcd27-110">MacOS：[借助 Visual Studio for Mac 开始使用 Razor Pages](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="fcd27-110">MacOS: [Get started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="fcd27-111">macOS、Linux 和 Windows：[在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="fcd27-111">macOS, Linux, and Windows: [Get started with ASP.NET Core Razor Pages in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="fcd27-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="fcd27-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcd27-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="fcd27-113">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="fcd27-114">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="fcd27-114">Create a Razor web app</span></span>

* <span data-ttu-id="fcd27-115">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="fcd27-115">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="fcd27-116">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fcd27-116">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="fcd27-117">将项目命名为“RazorPagesMovie”。</span><span class="sxs-lookup"><span data-stu-id="fcd27-117">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="fcd27-118">将项目命名为“RazorPagesMovie”，以便命名空间在你复制/粘贴代码时相互匹配。</span><span class="sxs-lookup"><span data-stu-id="fcd27-118">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="fcd27-119">![新建 ASP.NET Core Web 应用程序](../../mvc/razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="fcd27-119">![new ASP.NET Core Web Application](../../mvc/razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="fcd27-120">在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="fcd27-120">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE [install 2.0](../../includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="fcd27-121">Visual Studio 模板创建初学者项目：</span><span class="sxs-lookup"><span data-stu-id="fcd27-121">The Visual Studio template creates a starter project:</span></span>

![“解决方案资源管理器”](razor-pages-start/_static/se.png)

<span data-ttu-id="fcd27-123">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在运行（不附加调试器）</span><span class="sxs-lookup"><span data-stu-id="fcd27-123">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![主页或索引页](razor-pages-start/_static/home.png)

* <span data-ttu-id="fcd27-125">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行你的应用。</span><span class="sxs-lookup"><span data-stu-id="fcd27-125">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="fcd27-126">地址栏显示 `localhost:port#`，而不显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="fcd27-126">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="fcd27-127">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="fcd27-127">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="fcd27-128">Localhost 仅为来自本地计算机的 Web 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="fcd27-128">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="fcd27-129">Visual Studio 创建 Web 项目时，为 Web 服务器使用随机端口。</span><span class="sxs-lookup"><span data-stu-id="fcd27-129">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="fcd27-130">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="fcd27-130">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="fcd27-131">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="fcd27-131">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="fcd27-132">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="fcd27-132">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="fcd27-133">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="fcd27-133">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

> [!div class="step-by-step"]
> [<span data-ttu-id="fcd27-134">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="fcd27-134">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
