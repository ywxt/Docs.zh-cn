---
title: "ASP.NET Core MVC 和 Visual Studio 入门"
author: rick-anderson
description: "ASP.NET Core MVC 和 Visual Studio 入门"
ms.author: riande
manager: wpickett
ms.date: 10/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: a55b0b2a52856755b89e8ae6a2598c713f1d436d
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="ac0e4-103">ASP.NET Core MVC 和 Visual Studio 入门</span><span class="sxs-lookup"><span data-stu-id="ac0e4-103">Getting started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="ac0e4-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ac0e4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[consider RP](../../includes/razor.md)]

<span data-ttu-id="ac0e4-105">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-105">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="ac0e4-106">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="ac0e4-106">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="ac0e4-107">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="ac0e4-107">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="ac0e4-108">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="ac0e4-108">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="ac0e4-109">安装 Visual Studio 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="ac0e4-109">Install Visual Studio and .NET Core</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ac0e4-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ac0e4-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ac0e4-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ac0e4-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ac0e4-112">安装 Visual Studio Community 2017。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-112">Install Visual Studio Community 2017.</span></span> <span data-ttu-id="ac0e4-113">选择社区下载。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-113">Select the Community download.</span></span> <span data-ttu-id="ac0e4-114">如果已安装 Visual Studio 2017，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-114">Skip this step if you have Visual Studio 2017 installed.</span></span>

* [<span data-ttu-id="ac0e4-115">Visual Studio 2017 主页安装程序</span><span class="sxs-lookup"><span data-stu-id="ac0e4-115">Visual Studio 2017 Home page installer</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="ac0e4-116">运行安装程序，然后选择以下工作负荷：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-116">Run the installer and select the following workloads:</span></span>

* <span data-ttu-id="ac0e4-117">“ASP.NET 和 Web 开发”（位于“Web 和云”下）</span><span class="sxs-lookup"><span data-stu-id="ac0e4-117">**ASP.NET and web development** (under **Web & Cloud**)</span></span>
* <span data-ttu-id="ac0e4-118">“.NET Core 跨平台开发”（位于“其他工具集”下）</span><span class="sxs-lookup"><span data-stu-id="ac0e4-118">**.NET Core cross-platform development** (under **Other Toolsets**)</span></span>

![**ASP.NET 和 Web 开发**（位于“Web 和云”下）](start-mvc/_static/web_workload.png)

![**.NET Core 跨平台开发**（位于“其他工具集”下）](start-mvc/_static/x_plat_wl.png)

---

## <a name="create-a-web-app"></a><span data-ttu-id="ac0e4-121">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="ac0e4-121">Create a web app</span></span>

<span data-ttu-id="ac0e4-122">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-122">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="ac0e4-124">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-124">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="ac0e4-125">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-125">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="ac0e4-126">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-126">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="ac0e4-127">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="ac0e4-127">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="ac0e4-128">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-128">Tap **OK**</span></span>

![<span data-ttu-id="ac0e4-129">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="ac0e4-129">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ac0e4-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ac0e4-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ac0e4-131">完成“新建 ASP.NET 核心 Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-131">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="ac0e4-132">在版本选择器下拉框中选择“ASP.NET Core 2.-”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-132">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="ac0e4-133">选择“Web 应用程序(Model-View-Controller)”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-133">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="ac0e4-134">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-134">Tap **OK**.</span></span>

![<span data-ttu-id="ac0e4-135">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="ac0e4-135">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ac0e4-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ac0e4-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ac0e4-137">完成“新建 ASP.NET 核心 Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-137">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="ac0e4-138">在版本选择器下拉框中，点击“ASP.NET Core 1.1”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-138">In the version selector drop-down box tap **ASP.NET Core 1.1**</span></span>
* <span data-ttu-id="ac0e4-139">点击“Web 应用程序”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-139">Tap **Web Application**</span></span>
* <span data-ttu-id="ac0e4-140">保留默认的“无身份验证”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-140">Keep the default **No Authentication**</span></span>
* <span data-ttu-id="ac0e4-141">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="ac0e4-141">Tap **OK**.</span></span>

![新建 ASP.NET Core Web 应用](start-mvc/_static/p3.png)

---

<span data-ttu-id="ac0e4-143">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-143">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="ac0e4-144">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-144">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="ac0e4-145">这是一个简单的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-145">This is a simple starter project, and it's a good place to start,</span></span>

<span data-ttu-id="ac0e4-146">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-146">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![运行应用](start-mvc/_static/1.png)

* <span data-ttu-id="ac0e4-148">Visual Studio 启动 [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行你的应用。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-148">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="ac0e4-149">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-149">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="ac0e4-150">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-150">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="ac0e4-151">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-151">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="ac0e4-152">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-152">In the image above, the port number is 5000.</span></span> <span data-ttu-id="ac0e4-153">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-153">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="ac0e4-154">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-154">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="ac0e4-155">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-155">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="ac0e4-156">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-156">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="ac0e4-157">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="ac0e4-157">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="ac0e4-159">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="ac0e4-159">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="ac0e4-161">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-161">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="ac0e4-162">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-162">The browser image above doesn't show these links.</span></span> <span data-ttu-id="ac0e4-163">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-163">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="ac0e4-165">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-165">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="ac0e4-166">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="ac0e4-166">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="ac0e4-167">下一篇</span><span class="sxs-lookup"><span data-stu-id="ac0e4-167">Next</span></span>](adding-controller.md)  
