---
title: "ASP.NET Core MVC 和 Visual Studio 入门"
author: rick-anderson
description: "ASP.NET Core MVC 和 Visual Studio 入门"
keywords: ASP.NET Core, MVC
ms.author: riande
manager: wpickett
ms.date: 10/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 72852678a296107e6a2a146ed2324335a6e870ee
ms.sourcegitcommit: 77b8025c30ec2fd46d85ee2a2b497c44435d3009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="55335-104">ASP.NET Core MVC 和 Visual Studio 入门</span><span class="sxs-lookup"><span data-stu-id="55335-104">Getting started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="55335-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="55335-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[consider RP](../../includes/razor.md)]

<span data-ttu-id="55335-106">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="55335-106">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="55335-107">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="55335-107">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="55335-108">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="55335-108">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="55335-109">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="55335-109">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="55335-110">安装 Visual Studio 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="55335-110">Install Visual Studio and .NET Core</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="55335-111">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="55335-111">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="55335-112">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="55335-112">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="55335-113">安装 Visual Studio Community 2017。</span><span class="sxs-lookup"><span data-stu-id="55335-113">Install Visual Studio Community 2017.</span></span> <span data-ttu-id="55335-114">选择社区下载。</span><span class="sxs-lookup"><span data-stu-id="55335-114">Select the Community download.</span></span> <span data-ttu-id="55335-115">如果已安装 Visual Studio 2017，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="55335-115">Skip this step if you have Visual Studio 2017 installed.</span></span>

* [<span data-ttu-id="55335-116">Visual Studio 2017 主页安装程序</span><span class="sxs-lookup"><span data-stu-id="55335-116">Visual Studio 2017 Home page installer</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="55335-117">运行安装程序，然后选择以下工作负荷：</span><span class="sxs-lookup"><span data-stu-id="55335-117">Run the installer and select the following workloads:</span></span>

* <span data-ttu-id="55335-118">“ASP.NET 和 Web 开发”（位于“Web 和云”下）</span><span class="sxs-lookup"><span data-stu-id="55335-118">**ASP.NET and web development** (under **Web & Cloud**)</span></span>
* <span data-ttu-id="55335-119">“.NET Core 跨平台开发”（位于“其他工具集”下）</span><span class="sxs-lookup"><span data-stu-id="55335-119">**.NET Core cross-platform development** (under **Other Toolsets**)</span></span>

![**ASP.NET 和 Web 开发**（位于“Web 和云”下）](start-mvc/_static/web_workload.png)

![**.NET Core 跨平台开发**（位于“其他工具集”下）](start-mvc/_static/x_plat_wl.png)

---

## <a name="create-a-web-app"></a><span data-ttu-id="55335-122">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="55335-122">Create a web app</span></span>

<span data-ttu-id="55335-123">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="55335-123">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="55335-125">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="55335-125">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="55335-126">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="55335-126">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="55335-127">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="55335-127">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="55335-128">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="55335-128">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="55335-129">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="55335-129">Tap **OK**</span></span>

![<span data-ttu-id="55335-130">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="55335-130">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="55335-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="55335-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="55335-132">完成“新建 ASP.NET 核心 Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="55335-132">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="55335-133">在版本选择器下拉框中选择“ASP.NET Core 2.-”</span><span class="sxs-lookup"><span data-stu-id="55335-133">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="55335-134">选择“Web 应用程序(Model-View-Controller)”</span><span class="sxs-lookup"><span data-stu-id="55335-134">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="55335-135">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="55335-135">Tap **OK**.</span></span>

![<span data-ttu-id="55335-136">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="55335-136">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="55335-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="55335-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="55335-138">完成“新建 ASP.NET 核心 Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="55335-138">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="55335-139">在版本选择器下拉框中，点击“ASP.NET Core 1.1”</span><span class="sxs-lookup"><span data-stu-id="55335-139">In the version selector drop-down box tap **ASP.NET Core 1.1**</span></span>
* <span data-ttu-id="55335-140">点击“Web 应用程序”</span><span class="sxs-lookup"><span data-stu-id="55335-140">Tap **Web Application**</span></span>
* <span data-ttu-id="55335-141">保留默认的“无身份验证”</span><span class="sxs-lookup"><span data-stu-id="55335-141">Keep the default **No Authentication**</span></span>
* <span data-ttu-id="55335-142">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="55335-142">Tap **OK**.</span></span>

![新建 ASP.NET Core Web 应用](start-mvc/_static/p3.png)

---

<span data-ttu-id="55335-144">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="55335-144">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="55335-145">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="55335-145">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="55335-146">这是一个简单的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="55335-146">This is a simple starter project, and it's a good place to start,</span></span>

<span data-ttu-id="55335-147">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="55335-147">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![运行应用](start-mvc/_static/1.png)

* <span data-ttu-id="55335-149">Visual Studio 启动 [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行你的应用。</span><span class="sxs-lookup"><span data-stu-id="55335-149">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="55335-150">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="55335-150">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="55335-151">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="55335-151">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="55335-152">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="55335-152">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="55335-153">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="55335-153">In the image above, the port number is 5000.</span></span> <span data-ttu-id="55335-154">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="55335-154">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="55335-155">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="55335-155">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="55335-156">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="55335-156">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="55335-157">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="55335-157">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="55335-158">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="55335-158">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="55335-160">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="55335-160">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="55335-162">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="55335-162">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="55335-163">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="55335-163">The browser image above doesn't show these links.</span></span> <span data-ttu-id="55335-164">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="55335-164">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="55335-166">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="55335-166">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="55335-167">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="55335-167">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="55335-168">下一篇</span><span class="sxs-lookup"><span data-stu-id="55335-168">Next</span></span>](adding-controller.md)  
