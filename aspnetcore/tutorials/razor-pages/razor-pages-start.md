---
title: 在 ASP.NET Core 中开始使用 Razor Pages
author: rick-anderson
description: 了解构建 ASP.NET Core Razor 页面 Web 应用的基础知识。 Razor 页面推荐用于 ASP.NET Core 中的 Web 工作负载。
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 7148f2d944bd1978b1a83278dfed9051f192e4dd
ms.sourcegitcommit: 08f1a9baa97060da5168840b332c9c0805b5f901
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37144932"
---
# <a name="get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="eda9c-104">在 ASP.NET Core 中开始使用 Razor Pages</span><span class="sxs-lookup"><span data-stu-id="eda9c-104">Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="eda9c-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="eda9c-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="eda9c-106">建议学习本教程的 ASP.NET Core 2.1 版本。</span><span class="sxs-lookup"><span data-stu-id="eda9c-106">We recommend you follow the ASP.NET Core 2.1 version of this tutorial.</span></span> <span data-ttu-id="eda9c-107">该版本更易于学习并且涵盖更多功能。</span><span class="sxs-lookup"><span data-stu-id="eda9c-107">It's **much** easier to follow and covers more features.</span></span> <span data-ttu-id="eda9c-108">在版本选择器中选择“ASP.NET Core 2.1”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-108">Select **ASP.NET Core 2.1** in the version selector.</span></span>

![TOC 中的版本选择器](razor-pages-start/_static/v21.png)

::: moniker-end

<span data-ttu-id="eda9c-110">本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="eda9c-110">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="eda9c-111">Razor Pages 是在 ASP.NET Core 中为 Web 应用生成 UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="eda9c-111">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="eda9c-112">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="eda9c-112">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="eda9c-113">Windows：本教程</span><span class="sxs-lookup"><span data-stu-id="eda9c-113">Windows: This tutorial</span></span>
* <span data-ttu-id="eda9c-114">MacOS：[借助 Visual Studio for Mac 开始使用 Razor Pages](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="eda9c-114">MacOS: [Get started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="eda9c-115">macOS、Linux 和 Windows：[在 Visual Studio Code 中开始使用 ASP.NET Core Razor 页面](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="eda9c-115">macOS, Linux, and Windows: [Get started with ASP.NET Core Razor Pages in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="eda9c-116">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="eda9c-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="prerequisites"></a><span data-ttu-id="eda9c-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="eda9c-117">Prerequisites</span></span>

<span data-ttu-id="eda9c-118">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="eda9c-118">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

## <a name="create-a-razor-web-app"></a><span data-ttu-id="eda9c-119">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="eda9c-119">Create a Razor web app</span></span>

* <span data-ttu-id="eda9c-120">从 Visual Studio“文件”菜单中，选择“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-120">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="eda9c-121">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eda9c-121">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="eda9c-122">将项目命名为“RazorPagesMovie”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-122">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="eda9c-123">将项目命名为“RazorPagesMovie”，以便命名空间在你复制/粘贴代码时相互匹配。</span><span class="sxs-lookup"><span data-stu-id="eda9c-123">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="eda9c-124">![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="eda9c-124">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>
* <span data-ttu-id="eda9c-125">在下拉列表中选择“ASP.NET Core 2.1”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-125">Select **ASP.NET Core 2.1** in the dropdown, and then select **Web Application**.</span></span>

 ![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2_2.1.png)

<span data-ttu-id="eda9c-127">Visual Studio 模板创建初学者项目：</span><span class="sxs-lookup"><span data-stu-id="eda9c-127">The Visual Studio template creates a starter project:</span></span>

![“解决方案资源管理器”](razor-pages-start/_static/se2.1.png)

<span data-ttu-id="eda9c-129">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在不附加调试器的情况下运行。</span><span class="sxs-lookup"><span data-stu-id="eda9c-129">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span> <span data-ttu-id="eda9c-130">选择“接受”以同意跟踪。</span><span class="sxs-lookup"><span data-stu-id="eda9c-130">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="eda9c-131">此应用不会跟踪个人信息。</span><span class="sxs-lookup"><span data-stu-id="eda9c-131">This app doesn't track personal information.</span></span> <span data-ttu-id="eda9c-132">模板生成的代码包含有助于符合[一般数据保护条例 (GDPR)](xref:security/gdpr) 的资产。</span><span class="sxs-lookup"><span data-stu-id="eda9c-132">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

![主页或索引页](razor-pages-start/_static/homeGDPR.png)

<span data-ttu-id="eda9c-134">下图展示了接受跟踪后的应用：</span><span class="sxs-lookup"><span data-stu-id="eda9c-134">The following image shows the app after accepting tracking:</span></span>

![主页或索引页](razor-pages-start/_static/home2.1.png)

* <span data-ttu-id="eda9c-136">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="eda9c-136">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="eda9c-137">地址栏显示 `localhost:port#`，而不是显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="eda9c-137">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="eda9c-138">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="eda9c-138">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="eda9c-139">Localhost 仅为来自本地计算机的 Web 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="eda9c-139">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="eda9c-140">Visual Studio 创建 Web 项目时，为 Web 服务器使用随机端口。</span><span class="sxs-lookup"><span data-stu-id="eda9c-140">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="eda9c-141">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="eda9c-141">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="eda9c-142">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="eda9c-142">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="eda9c-143">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="eda9c-143">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="eda9c-144">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="eda9c-144">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="prerequisites"></a><span data-ttu-id="eda9c-145">系统必备</span><span class="sxs-lookup"><span data-stu-id="eda9c-145">Prerequisites</span></span>

<span data-ttu-id="eda9c-146">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="eda9c-146">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

## <a name="create-a-razor-web-app"></a><span data-ttu-id="eda9c-147">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="eda9c-147">Create a Razor web app</span></span>

* <span data-ttu-id="eda9c-148">从 Visual Studio“文件”菜单中，选择“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-148">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="eda9c-149">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eda9c-149">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="eda9c-150">将项目命名为“RazorPagesMovie”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-150">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="eda9c-151">将项目命名为“RazorPagesMovie”，以便命名空间在你复制/粘贴代码时相互匹配。</span><span class="sxs-lookup"><span data-stu-id="eda9c-151">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="eda9c-152">![新建 ASP.NET Core Web 应用程序](../../razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="eda9c-152">![new ASP.NET Core Web Application](../../razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="eda9c-153">在下拉列表中选择“ASP.NET Core 2.0”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="eda9c-153">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE [install 2.0](~/includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="eda9c-154">Visual Studio 模板创建初学者项目：</span><span class="sxs-lookup"><span data-stu-id="eda9c-154">The Visual Studio template creates a starter project:</span></span>

![“解决方案资源管理器”](razor-pages-start/_static/se.png)

<span data-ttu-id="eda9c-156">按 F5 在调试模式下运行应用，或按 Ctrl-F5 在运行（不附加调试器）</span><span class="sxs-lookup"><span data-stu-id="eda9c-156">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![主页或索引页](razor-pages-start/_static/home.png)

* <span data-ttu-id="eda9c-158">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行你的应用。</span><span class="sxs-lookup"><span data-stu-id="eda9c-158">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="eda9c-159">地址栏显示 `localhost:port#`，而不显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="eda9c-159">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="eda9c-160">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="eda9c-160">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="eda9c-161">Localhost 仅为来自本地计算机的 Web 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="eda9c-161">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="eda9c-162">Visual Studio 创建 Web 项目时，为 Web 服务器使用随机端口。</span><span class="sxs-lookup"><span data-stu-id="eda9c-162">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="eda9c-163">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="eda9c-163">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="eda9c-164">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="eda9c-164">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="eda9c-165">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="eda9c-165">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="eda9c-166">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="eda9c-166">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/razor-pages-start.md)]

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="eda9c-167">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="eda9c-167">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
