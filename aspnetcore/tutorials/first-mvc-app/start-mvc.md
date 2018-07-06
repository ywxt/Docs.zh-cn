---
title: ASP.NET Core MVC 和 Visual Studio 入门
author: rick-anderson
description: 了解如何开始使用 ASP.NET Core MVC 和 Visual Studio。
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 1fb3947023843341403f4355c6ae1e61d7e4f6b1
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275547"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="64d4c-103">ASP.NET Core MVC 和 Visual Studio 入门</span><span class="sxs-lookup"><span data-stu-id="64d4c-103">Get started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="64d4c-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="64d4c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="64d4c-105">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="64d4c-105">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="64d4c-106">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="64d4c-106">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="64d4c-107">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="64d4c-107">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="64d4c-108">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="64d4c-108">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="64d4c-109">安装 Visual Studio 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="64d4c-109">Install Visual Studio and .NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="64d4c-110">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="64d4c-110">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

## <a name="create-a-web-app"></a><span data-ttu-id="64d4c-111">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="64d4c-111">Create a web app</span></span>

<span data-ttu-id="64d4c-112">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="64d4c-112">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="64d4c-114">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="64d4c-114">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="64d4c-115">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="64d4c-115">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="64d4c-116">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="64d4c-116">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="64d4c-117">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="64d4c-117">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="64d4c-118">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="64d4c-118">Tap **OK**</span></span>

![<span data-ttu-id="64d4c-119">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="64d4c-119">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="64d4c-120">完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="64d4c-120">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="64d4c-121">在版本选择器下拉框中选择“ASP.NET Core 2.1”</span><span class="sxs-lookup"><span data-stu-id="64d4c-121">In the version selector drop-down box select **ASP.NET Core 2.1**</span></span>
* <span data-ttu-id="64d4c-122">选择“Web 应用程序(Model-View-Controller)”</span><span class="sxs-lookup"><span data-stu-id="64d4c-122">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="64d4c-123">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="64d4c-123">Tap **OK**.</span></span>

![<span data-ttu-id="64d4c-124">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="64d4c-124">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="64d4c-125">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="64d4c-125">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="64d4c-126">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-126">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="64d4c-127">这是一个基本的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-127">This is a basic starter project, and it's a good place to start,</span></span>

<span data-ttu-id="64d4c-128">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-128">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="64d4c-129"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="64d4c-129"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="64d4c-130">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-130">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="64d4c-131">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。</span><span class="sxs-lookup"><span data-stu-id="64d4c-131">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="64d4c-132">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="64d4c-132">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="64d4c-133">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="64d4c-133">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="64d4c-134">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="64d4c-134">In the image above, the port number is 5000.</span></span> <span data-ttu-id="64d4c-135">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="64d4c-135">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="64d4c-136">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="64d4c-136">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="64d4c-137">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="64d4c-137">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="64d4c-138">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="64d4c-138">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="64d4c-139">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="64d4c-139">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="64d4c-141">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="64d4c-141">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="64d4c-143">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-143">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="64d4c-144">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-144">The browser image above doesn't show these links.</span></span> <span data-ttu-id="64d4c-145">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-145">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="64d4c-147">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="64d4c-147">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="64d4c-148">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="64d4c-148">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="64d4c-149">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="64d4c-149">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="64d4c-150">[!INCLUDE [](~/includes/net-core-prereqs.md) [](~/includes/net-core-prereqs.md)]</span><span class="sxs-lookup"><span data-stu-id="64d4c-150">[!INCLUDE [](~/includes/net-core-prereqs.md) [](~/includes/net-core-prereqs.md)]</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="64d4c-151">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="64d4c-151">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="64d4c-152">安装 Visual Studio Community 2017。</span><span class="sxs-lookup"><span data-stu-id="64d4c-152">Install Visual Studio Community 2017.</span></span> <span data-ttu-id="64d4c-153">选择社区下载。</span><span class="sxs-lookup"><span data-stu-id="64d4c-153">Select the Community download.</span></span> <span data-ttu-id="64d4c-154">如果已安装 Visual Studio 2017，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="64d4c-154">Skip this step if you have Visual Studio 2017 installed.</span></span>

* [<span data-ttu-id="64d4c-155">Visual Studio 2017 主页安装程序</span><span class="sxs-lookup"><span data-stu-id="64d4c-155">Visual Studio 2017 Home page installer</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="64d4c-156">运行安装程序，然后选择以下工作负荷：</span><span class="sxs-lookup"><span data-stu-id="64d4c-156">Run the installer and select the following workloads:</span></span>

* <span data-ttu-id="64d4c-157">“ASP.NET 和 Web 开发”（位于“Web 和云”下）</span><span class="sxs-lookup"><span data-stu-id="64d4c-157">**ASP.NET and web development** (under **Web & Cloud**)</span></span>
* <span data-ttu-id="64d4c-158">“.NET Core 跨平台开发”（位于“其他工具集”下）</span><span class="sxs-lookup"><span data-stu-id="64d4c-158">**.NET Core cross-platform development** (under **Other Toolsets**)</span></span>

![**ASP.NET 和 Web 开发**（位于“Web 和云”下）](start-mvc/_static/web_workload.png)

![**.NET Core 跨平台开发**（位于“其他工具集”下）](start-mvc/_static/x_plat_wl.png)

---

## <a name="create-a-web-app"></a><span data-ttu-id="64d4c-161">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="64d4c-161">Create a web app</span></span>

<span data-ttu-id="64d4c-162">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="64d4c-162">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="64d4c-164">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="64d4c-164">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="64d4c-165">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="64d4c-165">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="64d4c-166">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="64d4c-166">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="64d4c-167">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="64d4c-167">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="64d4c-168">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="64d4c-168">Tap **OK**</span></span>

![<span data-ttu-id="64d4c-169">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="64d4c-169">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="64d4c-170">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="64d4c-170">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="64d4c-171">完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="64d4c-171">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="64d4c-172">在版本选择器下拉框中选择“ASP.NET Core 2.-”</span><span class="sxs-lookup"><span data-stu-id="64d4c-172">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="64d4c-173">选择“Web 应用程序(Model-View-Controller)”</span><span class="sxs-lookup"><span data-stu-id="64d4c-173">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="64d4c-174">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="64d4c-174">Tap **OK**.</span></span>

![<span data-ttu-id="64d4c-175">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="64d4c-175">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="64d4c-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="64d4c-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="64d4c-177">完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="64d4c-177">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="64d4c-178">在版本选择器下拉框中，点击“ASP.NET Core 1.1”</span><span class="sxs-lookup"><span data-stu-id="64d4c-178">In the version selector drop-down box tap **ASP.NET Core 1.1**</span></span>
* <span data-ttu-id="64d4c-179">点击“Web 应用程序”</span><span class="sxs-lookup"><span data-stu-id="64d4c-179">Tap **Web Application**</span></span>
* <span data-ttu-id="64d4c-180">保留默认的“无身份验证”</span><span class="sxs-lookup"><span data-stu-id="64d4c-180">Keep the default **No Authentication**</span></span>
* <span data-ttu-id="64d4c-181">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="64d4c-181">Tap **OK**.</span></span>

![新建 ASP.NET Core Web 应用](start-mvc/_static/p3.png)

---

<span data-ttu-id="64d4c-183">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="64d4c-183">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="64d4c-184">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-184">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="64d4c-185">这是一个基本的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-185">This is a basic starter project, and it's a good place to start,</span></span>

<span data-ttu-id="64d4c-186">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-186">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="64d4c-187"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="64d4c-187"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="64d4c-188">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="64d4c-188">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="64d4c-189">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。</span><span class="sxs-lookup"><span data-stu-id="64d4c-189">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="64d4c-190">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="64d4c-190">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="64d4c-191">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="64d4c-191">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="64d4c-192">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="64d4c-192">In the image above, the port number is 5000.</span></span> <span data-ttu-id="64d4c-193">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="64d4c-193">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="64d4c-194">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="64d4c-194">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="64d4c-195">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="64d4c-195">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="64d4c-196">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="64d4c-196">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="64d4c-197">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="64d4c-197">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="64d4c-199">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="64d4c-199">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="64d4c-201">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-201">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="64d4c-202">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-202">The browser image above doesn't show these links.</span></span> <span data-ttu-id="64d4c-203">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="64d4c-203">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="64d4c-205">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="64d4c-205">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="64d4c-206">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="64d4c-206">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end
> [!div class="step-by-step"]
> [<span data-ttu-id="64d4c-207">下一篇</span><span class="sxs-lookup"><span data-stu-id="64d4c-207">Next</span></span>](adding-controller.md)  
