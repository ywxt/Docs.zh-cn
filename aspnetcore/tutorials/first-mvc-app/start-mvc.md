---
title: ASP.NET Core MVC 和 Visual Studio 入门
author: rick-anderson
description: 了解如何开始使用 ASP.NET Core MVC 和 Visual Studio。
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 738c49272c2ae2b075866001f06ad09fe73969f9
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862195"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="04b2f-103">ASP.NET Core MVC 和 Visual Studio 入门</span><span class="sxs-lookup"><span data-stu-id="04b2f-103">Get started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="04b2f-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="04b2f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="04b2f-105">本教程提供 3 个版本：</span><span class="sxs-lookup"><span data-stu-id="04b2f-105">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="04b2f-106">macOS：[使用 Visual Studio for Mac 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="04b2f-106">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="04b2f-107">Windows：[使用 Visual Studio 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="04b2f-107">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="04b2f-108">macOS、Linux 和 Windows：[使用 Visual Studio Code 创建 ASP.NET Core MVC 应用](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="04b2f-108">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

> [!NOTE]
> <span data-ttu-id="04b2f-109">我们要测试所建议的新的 ASP.NET Core 目录结构是否可用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-109">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="04b2f-110">如果你有几分钟时间进行练习，来了解当前目录或所建议目录中的 7 个不同主题，请[单击此处来参与调查](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82)。</span><span class="sxs-lookup"><span data-stu-id="04b2f-110">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="04b2f-111">安装 Visual Studio 和 .NET Core</span><span class="sxs-lookup"><span data-stu-id="04b2f-111">Install Visual Studio and .NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="04b2f-112">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="04b2f-112">Create a web app</span></span>

<span data-ttu-id="04b2f-113">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="04b2f-113">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="04b2f-115">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="04b2f-115">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="04b2f-116">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="04b2f-116">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="04b2f-117">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="04b2f-117">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="04b2f-118">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="04b2f-118">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="04b2f-119">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="04b2f-119">Tap **OK**</span></span>

![<span data-ttu-id="04b2f-120">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="04b2f-120">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="04b2f-121">完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="04b2f-121">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="04b2f-122">在版本选择器下拉框中选择“ASP.NET Core 2.1”</span><span class="sxs-lookup"><span data-stu-id="04b2f-122">In the version selector drop-down box select **ASP.NET Core 2.1**</span></span>
* <span data-ttu-id="04b2f-123">选择“Web 应用(模型-视图-控制器)”</span><span class="sxs-lookup"><span data-stu-id="04b2f-123">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="04b2f-124">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="04b2f-124">Tap **OK**.</span></span>

![<span data-ttu-id="04b2f-125">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="04b2f-125">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="04b2f-126">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="04b2f-126">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="04b2f-127">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-127">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="04b2f-128">这是一个基本的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-128">This is a basic starter project, and it's a good place to start.</span></span>

<span data-ttu-id="04b2f-129">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-129">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="04b2f-130"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="04b2f-130"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="04b2f-131">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-131">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="04b2f-132">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。</span><span class="sxs-lookup"><span data-stu-id="04b2f-132">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="04b2f-133">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="04b2f-133">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="04b2f-134">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="04b2f-134">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="04b2f-135">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="04b2f-135">In the image above, the port number is 5000.</span></span> <span data-ttu-id="04b2f-136">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="04b2f-136">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="04b2f-137">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="04b2f-137">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="04b2f-138">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="04b2f-138">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="04b2f-139">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="04b2f-139">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="04b2f-140">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="04b2f-140">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="04b2f-142">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="04b2f-142">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="04b2f-144">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-144">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="04b2f-145">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-145">The browser image above doesn't show these links.</span></span> <span data-ttu-id="04b2f-146">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-146">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="04b2f-148">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="04b2f-148">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="04b2f-149">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="04b2f-149">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="04b2f-150">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="04b2f-150">Create a web app</span></span>

<span data-ttu-id="04b2f-151">在 Visual Studio 中，选择“文件”>“新建”>“项目”。</span><span class="sxs-lookup"><span data-stu-id="04b2f-151">From Visual Studio, select  **File > New > Project**.</span></span>

![“文件”>“新建”>“项目”](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="04b2f-153">填写“新建项目”对话框：</span><span class="sxs-lookup"><span data-stu-id="04b2f-153">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="04b2f-154">在左侧窗格中，点击“.NET Core”</span><span class="sxs-lookup"><span data-stu-id="04b2f-154">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="04b2f-155">在中间窗格中，点击“ASP.NET Core Web 应用程序(.NET Core)”</span><span class="sxs-lookup"><span data-stu-id="04b2f-155">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="04b2f-156">将项目命名为“MvcMovie”（请务必将项目命名为“MvcMovie”，以便在复制代码时可以与命名空间匹配。）</span><span class="sxs-lookup"><span data-stu-id="04b2f-156">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="04b2f-157">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="04b2f-157">Tap **OK**</span></span>

![<span data-ttu-id="04b2f-158">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="04b2f-158">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)

<span data-ttu-id="04b2f-159">完成“新建 ASP.NET Core Web 应用程序(.NET Core) - MvcMovie”对话框：</span><span class="sxs-lookup"><span data-stu-id="04b2f-159">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="04b2f-160">在版本选择器下拉框中选择“ASP.NET Core 2.-”</span><span class="sxs-lookup"><span data-stu-id="04b2f-160">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="04b2f-161">选择“Web 应用程序(Model-View-Controller)”</span><span class="sxs-lookup"><span data-stu-id="04b2f-161">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="04b2f-162">点击“确定”</span><span class="sxs-lookup"><span data-stu-id="04b2f-162">Tap **OK**.</span></span>

![<span data-ttu-id="04b2f-163">新项目对话框, 左侧窗格中的 .NET Core, ASP.NET Core Web</span><span class="sxs-lookup"><span data-stu-id="04b2f-163">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

<span data-ttu-id="04b2f-164">Visual Studio 为刚刚创建的 MVC 项目使用默认模板。</span><span class="sxs-lookup"><span data-stu-id="04b2f-164">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="04b2f-165">输入项目名称并选择几个选项后，就拥有了一个可正常运行的应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-165">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="04b2f-166">这是一个基本的初学者项目，适合入门使用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-166">This is a basic starter project, and it's a good place to start,</span></span>

<span data-ttu-id="04b2f-167">点击“F5”在调试模式下运行应用，或按“Ctrl-F5”在非调试模式下运行应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-167">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="04b2f-168"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![正在运行的应用](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="04b2f-168"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="04b2f-169">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="04b2f-169">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="04b2f-170">请注意，地址栏显示 `localhost:port#`，而不显示 `example.com` 之类的内容。</span><span class="sxs-lookup"><span data-stu-id="04b2f-170">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="04b2f-171">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="04b2f-171">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="04b2f-172">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="04b2f-172">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="04b2f-173">在上图中，端口号为 5000。</span><span class="sxs-lookup"><span data-stu-id="04b2f-173">In the image above, the port number is 5000.</span></span> <span data-ttu-id="04b2f-174">浏览器中的 URL 显示 `localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="04b2f-174">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="04b2f-175">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="04b2f-175">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="04b2f-176">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="04b2f-176">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="04b2f-177">许多开发人员更喜欢使用非调试模式快速启动应用并查看更改。</span><span class="sxs-lookup"><span data-stu-id="04b2f-177">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="04b2f-178">可以从“调试”菜单项中以调试或非调试模式启动应用：</span><span class="sxs-lookup"><span data-stu-id="04b2f-178">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![调试菜单](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="04b2f-180">可以通过点击“IIS Express”按钮来调试应用</span><span class="sxs-lookup"><span data-stu-id="04b2f-180">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="04b2f-182">默认模板提供可用的“主页”、“关于”和“联系”链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-182">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="04b2f-183">上面的浏览器图像未显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-183">The browser image above doesn't show these links.</span></span> <span data-ttu-id="04b2f-184">根据浏览器的大小，可能需要单击导航图标才能显示这些链接。</span><span class="sxs-lookup"><span data-stu-id="04b2f-184">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![右上角的导航图标](start-mvc/_static/2.png)

<span data-ttu-id="04b2f-186">如果正在调试模式下运行，点击“Shift-F5”以停止调试。</span><span class="sxs-lookup"><span data-stu-id="04b2f-186">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="04b2f-187">在本教程的下一部分中，我们将了解 MVC 并开始编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="04b2f-187">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="04b2f-188">下一页</span><span class="sxs-lookup"><span data-stu-id="04b2f-188">Next</span></span>](adding-controller.md)  
