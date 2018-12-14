---
title: 在 ASP.NET Core 中开始使用 Razor Pages
author: rick-anderson
monikerRange: '>= aspnetcore-2.2'
description: 此系列教程演示了如何在 ASP.NET Core 中使用 Razor Pages。 了解如何创建模型、为 Razor Pages 生成代码、将 Entity Framework Core 和 SQL Server 用于数据访问、添加搜索功能、添加输入验证及使用迁移更新模型。
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 1152ebfcee48a46ecd28c941fce32d3fc1e05c41
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861623"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="1aef7-104">教程：在 ASP.NET Core 中开始使用 Razor Pages</span><span class="sxs-lookup"><span data-stu-id="1aef7-104">Tutorial: Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="1aef7-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1aef7-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1aef7-106">本教程介绍构建 ASP.NET Core Razor Pages Web 应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="1aef7-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span>

<span data-ttu-id="1aef7-107">该应用管理电影标题的数据库。</span><span class="sxs-lookup"><span data-stu-id="1aef7-107">The app manages a database of movie titles.</span></span> <span data-ttu-id="1aef7-108">您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="1aef7-108">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1aef7-109">创建 Razor 页面 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-109">Create a Razor Pages web app.</span></span>
> * <span data-ttu-id="1aef7-110">添加和构架模型。</span><span class="sxs-lookup"><span data-stu-id="1aef7-110">Add and scaffold a model.</span></span>
> * <span data-ttu-id="1aef7-111">使用数据库。</span><span class="sxs-lookup"><span data-stu-id="1aef7-111">Work with a database.</span></span>
> * <span data-ttu-id="1aef7-112">添加搜索和验证。</span><span class="sxs-lookup"><span data-stu-id="1aef7-112">Add search and validation.</span></span>

<span data-ttu-id="1aef7-113">在结束时，你会获得可以管理和显示电影标题项的应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-113">At the end, you have an app that can manage and display movie titles items.</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

## <a name="prerequisites"></a><span data-ttu-id="1aef7-114">系统必备</span><span class="sxs-lookup"><span data-stu-id="1aef7-114">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="1aef7-115">创建 Razor Web 应用</span><span class="sxs-lookup"><span data-stu-id="1aef7-115">Create a Razor web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1aef7-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aef7-116">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="1aef7-117">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="1aef7-117">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="1aef7-118">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1aef7-118">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="1aef7-119">将项目命名为“RazorPagesMovie”。</span><span class="sxs-lookup"><span data-stu-id="1aef7-119">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="1aef7-120">将项目命名为“RazorPagesMovie”，以便命名空间在你复制/粘贴代码时相互匹配。</span><span class="sxs-lookup"><span data-stu-id="1aef7-120">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="1aef7-121">![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="1aef7-121">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>

* <span data-ttu-id="1aef7-122">在下拉列表中选择“ASP.NET Core 2.2”，然后选择“Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="1aef7-122">Select **ASP.NET Core 2.2** in the dropdown, and then select **Web Application**.</span></span>

  ![新建 ASP.NET Core Web 应用程序](razor-pages-start/_static/np_2_2.2.png)

  <span data-ttu-id="1aef7-124">创建以下初学者项目：</span><span class="sxs-lookup"><span data-stu-id="1aef7-124">The following starter project is created:</span></span>

  ![“解决方案资源管理器”](razor-pages-start/_static/se2.2.png)

* <span data-ttu-id="1aef7-126">按 **Ctrl-F5** 以在不使用调试程序的情况下运行。</span><span class="sxs-lookup"><span data-stu-id="1aef7-126">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="1aef7-127">Visual Studio 启动 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 并运行应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-127">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="1aef7-128">地址栏显示 `localhost:port#`，而不是显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="1aef7-128">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="1aef7-129">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="1aef7-129">That's because `localhost` is the standard hostname for the local computer.</span></span> <span data-ttu-id="1aef7-130">Localhost 仅为来自本地计算机的 Web 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="1aef7-130">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="1aef7-131">Visual Studio 创建 Web 项目时，Web 服务器使用的是随机端口。</span><span class="sxs-lookup"><span data-stu-id="1aef7-131">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="1aef7-132">在上图中，端口号为 5001。</span><span class="sxs-lookup"><span data-stu-id="1aef7-132">In the preceding image, the port number is 5001.</span></span> <span data-ttu-id="1aef7-133">运行应用时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="1aef7-133">When you run the app, you'll see a different port number.</span></span>

  <span data-ttu-id="1aef7-134">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="1aef7-134">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="1aef7-135">许多开发人员更喜欢使用非调试模式刷新页面并查看更改。</span><span class="sxs-lookup"><span data-stu-id="1aef7-135">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="1aef7-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1aef7-136">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="1aef7-137">打开[集成终端](https://code.visualstudio.com/docs/editor/integrated-terminal)。</span><span class="sxs-lookup"><span data-stu-id="1aef7-137">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="1aef7-138">将目录更改为 (`cd`) 包含项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1aef7-138">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="1aef7-139">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="1aef7-139">Run the following command:</span></span>

   ```console
   dotnet new webapp -o RazorPagesMovie
   code -r RazorPagesMovie
   ```

  * <span data-ttu-id="1aef7-140">一个对话框随即出现，其中包含“"RazorPagesMovie" 中缺少进行生成和调试所需的资产。是否添加它们?”</span><span class="sxs-lookup"><span data-stu-id="1aef7-140">A dialog box appears with **Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?**</span></span>  <span data-ttu-id="1aef7-141">选择“是”</span><span class="sxs-lookup"><span data-stu-id="1aef7-141">Select **Yes**</span></span>

  * <span data-ttu-id="1aef7-142">`dotnet new webapp -o RazorPagesMovie`：在 RazorPagesMovie 文件夹中创建新的 Razor Pages 项目。</span><span class="sxs-lookup"><span data-stu-id="1aef7-142">`dotnet new webapp -o RazorPagesMovie`: creates a new Razor Pages project in the *RazorPagesMovie* folder.</span></span>
  * <span data-ttu-id="1aef7-143">`code -r RazorPagesMovie`：在 Visual Studio Code 中加载 RazorPagesMovie.csproj 项目文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-143">`code -r RazorPagesMovie`: Loads the *RazorPagesMovie.csproj* project file in Visual Studio Code.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="1aef7-144">启动应用</span><span class="sxs-lookup"><span data-stu-id="1aef7-144">Launch the app</span></span>

* <span data-ttu-id="1aef7-145">按 **Ctrl-F5** 以在不使用调试程序的情况下运行。</span><span class="sxs-lookup"><span data-stu-id="1aef7-145">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="1aef7-146">Visual Studio Code 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5001`。</span><span class="sxs-lookup"><span data-stu-id="1aef7-146">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span> <span data-ttu-id="1aef7-147">地址栏显示 `localhost:port:5001`，而不是显示 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="1aef7-147">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="1aef7-148">这是因为 `localhost` 是本地计算机的标准主机名。</span><span class="sxs-lookup"><span data-stu-id="1aef7-148">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="1aef7-149">Localhost 仅为来自本地计算机的 Web 请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="1aef7-149">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="1aef7-150">使用“Ctrl+F5”启动应用（非调试模式）后，可执行代码更改、保存文件、刷新浏览器和查看代码更改等操作。</span><span class="sxs-lookup"><span data-stu-id="1aef7-150">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="1aef7-151">许多开发人员更喜欢使用非调试模式刷新页面并查看更改。</span><span class="sxs-lookup"><span data-stu-id="1aef7-151">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="1aef7-152">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="1aef7-152">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="1aef7-153">从终端运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1aef7-153">From a terminal, run the following commands:</span></span>

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="1aef7-154">上述命令使用 [.NET Core CLI](/dotnet/core/tools/dotnet) 创建并运行 Razor 页面项目。</span><span class="sxs-lookup"><span data-stu-id="1aef7-154">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="1aef7-155">打开浏览器，转到 http://localhost:5000 查看应用程序。</span><span class="sxs-lookup"><span data-stu-id="1aef7-155">Open a browser to http://localhost:5000 to view the application.</span></span>

## <a name="open-the-project"></a><span data-ttu-id="1aef7-156">打开项目</span><span class="sxs-lookup"><span data-stu-id="1aef7-156">Open the project</span></span>

<span data-ttu-id="1aef7-157">按 Ctrl+C 关闭应用程序。</span><span class="sxs-lookup"><span data-stu-id="1aef7-157">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="1aef7-158">在 Visual Studio 中，选择“文件”>“打开”，然后选择“RazorPagesMovie.csproj”文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-158">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="1aef7-159">启动应用</span><span class="sxs-lookup"><span data-stu-id="1aef7-159">Launch the app</span></span>

<span data-ttu-id="1aef7-160">选择“运行”>“开始执行(不调试)”以启动应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-160">Select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="1aef7-161">Visual Studio 启动 [Kestrel](xref:fundamentals/servers/kestrel)，启动浏览器并导航到 `http://localhost:5001`。</span><span class="sxs-lookup"><span data-stu-id="1aef7-161">Visual Studio starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span>

<!-- End of VS tabs -->

---

* <span data-ttu-id="1aef7-162">选择“接受”以同意跟踪。</span><span class="sxs-lookup"><span data-stu-id="1aef7-162">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="1aef7-163">此应用不会跟踪个人信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-163">This app doesn't track personal information.</span></span> <span data-ttu-id="1aef7-164">模板生成的代码包含有助于符合[一般数据保护条例 (GDPR)](xref:security/gdpr) 的资产。</span><span class="sxs-lookup"><span data-stu-id="1aef7-164">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![主页或索引页](razor-pages-start/_static/homeGDPR2.2.png)

  <span data-ttu-id="1aef7-166">下图展示了接受跟踪后的应用：</span><span class="sxs-lookup"><span data-stu-id="1aef7-166">The following image shows the app after accepting tracking:</span></span>

  ![主页或索引页](razor-pages-start/_static/home2.2.png)

## <a name="project-files-and-folders"></a><span data-ttu-id="1aef7-168">项目文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="1aef7-168">Project files and folders</span></span>

<span data-ttu-id="1aef7-169">下表列出了项目中的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="1aef7-169">The following table lists the files and folders in the project.</span></span> <span data-ttu-id="1aef7-170">此时在本教程中，Startup.cs 是最有必要了解的文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-170">At this point in the tutorial, the *Startup.cs* file is the most important to understand.</span></span> <span data-ttu-id="1aef7-171">无需查看下面提供的每一个链接。</span><span class="sxs-lookup"><span data-stu-id="1aef7-171">You don't need to review each link provided below.</span></span> <span data-ttu-id="1aef7-172">需要详细了解项目中的某个文件或文件夹时，可参考此处提供的链接。</span><span class="sxs-lookup"><span data-stu-id="1aef7-172">The links are provided as a reference when you need more information on a file or folder in the project.</span></span>

| <span data-ttu-id="1aef7-173">文件或文件夹</span><span class="sxs-lookup"><span data-stu-id="1aef7-173">File or folder</span></span>              | <span data-ttu-id="1aef7-174">目标</span><span class="sxs-lookup"><span data-stu-id="1aef7-174">Purpose</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="1aef7-175">*wwwroot*</span><span class="sxs-lookup"><span data-stu-id="1aef7-175">*wwwroot*</span></span> | <span data-ttu-id="1aef7-176">包含静态文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-176">Contains static files.</span></span> <span data-ttu-id="1aef7-177">请参阅[静态文件](xref:fundamentals/static-files)。</span><span class="sxs-lookup"><span data-stu-id="1aef7-177">See [Static files](xref:fundamentals/static-files).</span></span> |
| <span data-ttu-id="1aef7-178">*页*</span><span class="sxs-lookup"><span data-stu-id="1aef7-178">*Pages*</span></span> | <span data-ttu-id="1aef7-179">[Razor Pages](xref:razor-pages/index)的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1aef7-179">Folder for [Razor Pages](xref:razor-pages/index).</span></span> |
| <span data-ttu-id="1aef7-180">*appsettings.json*</span><span class="sxs-lookup"><span data-stu-id="1aef7-180">*appsettings.json*</span></span> | [<span data-ttu-id="1aef7-181">配置</span><span class="sxs-lookup"><span data-stu-id="1aef7-181">Configuration</span></span>](xref:fundamentals/configuration/index) |
| <span data-ttu-id="1aef7-182">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="1aef7-182">*Program.cs*</span></span> | <span data-ttu-id="1aef7-183">[托管](xref:fundamentals/host/index) ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-183">[Hosts](xref:fundamentals/host/index) the ASP.NET Core app.</span></span>|
| <span data-ttu-id="1aef7-184">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="1aef7-184">*Startup.cs*</span></span> | <span data-ttu-id="1aef7-185">配置服务和请求管道。</span><span class="sxs-lookup"><span data-stu-id="1aef7-185">Configures services and the request pipeline.</span></span> <span data-ttu-id="1aef7-186">请参阅[启动](xref:fundamentals/startup)。</span><span class="sxs-lookup"><span data-stu-id="1aef7-186">See [Startup](xref:fundamentals/startup).</span></span>|

### <a name="the-pages-folder"></a><span data-ttu-id="1aef7-187">“页面”文件夹</span><span class="sxs-lookup"><span data-stu-id="1aef7-187">The Pages folder</span></span>

<span data-ttu-id="1aef7-188">_Layout.cshtml 文件包含常见的 HTML 元素（脚本和样式表），并设置应用程序的布局。</span><span class="sxs-lookup"><span data-stu-id="1aef7-188">The *_Layout.cshtml* file contains common HTML elements (scripts and stylesheets) and sets the layout for the application.</span></span> <span data-ttu-id="1aef7-189">例如，单击“RazorPagesMovie”、“主页”或“隐私”时，将看到相同的元素。</span><span class="sxs-lookup"><span data-stu-id="1aef7-189">For example, when you click on **RazorPagesMovie**, **Home**, or **Privacy**, you see the same elements.</span></span> <span data-ttu-id="1aef7-190">常见的元素包括顶部的导航菜单和窗口底部的标题。</span><span class="sxs-lookup"><span data-stu-id="1aef7-190">The common elements include the navigation menu on the top and the header on the bottom of the window.</span></span> <span data-ttu-id="1aef7-191">请参阅[布局](xref:mvc/views/layout)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-191">See [Layout](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="1aef7-192">_ViewImports.cshtml 文件包含要导入每个 Razor 页面的 Razor 指令。</span><span class="sxs-lookup"><span data-stu-id="1aef7-192">The *_ViewImports.cshtml* file contains Razor directives that are imported into each Razor Page.</span></span> <span data-ttu-id="1aef7-193">请参阅[导入共享指令](xref:mvc/views/layout#importing-shared-directives)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-193">See [Importing Shared Directives](xref:mvc/views/layout#importing-shared-directives) for more information.</span></span>

<span data-ttu-id="1aef7-194">*_ViewStart.cshtml*将 Razor Pages `Layout` 属性设置为使用 *_Layout.cshtml* 文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-194">The *_ViewStart.cshtml* sets the Razor Pages `Layout` property to use the *_Layout.cshtml* file.</span></span> <span data-ttu-id="1aef7-195">请参阅[布局](xref:mvc/views/layout)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-195">See [Layout](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="1aef7-196">_ValidationScriptsPartial.cshtml 文件提供对 [jQuery](https://jquery.com/) 验证脚本的引用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-196">The *_ValidationScriptsPartial.cshtml* file provides a reference to [jQuery](https://jquery.com/) validation scripts.</span></span> <span data-ttu-id="1aef7-197">在本教程的后续部分中添加 `Create` 和 `Edit` 页面时，会使用 _ValidationScriptsPartial.cshtml 文件。</span><span class="sxs-lookup"><span data-stu-id="1aef7-197">When the `Create` and `Edit` pages are added later in the tutorial, the *_ValidationScriptsPartial.cshtml* file will be used.</span></span>

<span data-ttu-id="1aef7-198">提供 `Index`、`Error` 和 `Privacy` 页面以用于：</span><span class="sxs-lookup"><span data-stu-id="1aef7-198">`Index`, `Error`, and `Privacy` pages are provided to:</span></span>

* <span data-ttu-id="1aef7-199">`Index`：启动应用。</span><span class="sxs-lookup"><span data-stu-id="1aef7-199">`Index`: Start an app.</span></span>
* <span data-ttu-id="1aef7-200">`Error`：显示错误信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-200">`Error`: Display error information.</span></span>
* <span data-ttu-id="1aef7-201">`Privacy`：指定有关站点隐私策略的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1aef7-201">`Privacy`: Specify details about the site's privacy policy.</span></span>

<span data-ttu-id="1aef7-202">对于本教程，不使用前面的页面。</span><span class="sxs-lookup"><span data-stu-id="1aef7-202">For this tutorial, the preceding pages are not used.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1aef7-203">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aef7-203">Visual Studio</span></span>](#tab/visual-studio)

<a name="f7"></a>
### <a name="use-f7-to-toggle-between-a-razor-page-and-the-pagemodel"></a><span data-ttu-id="1aef7-204">使用 F7 在 Razor 页面和 PageModel 之间切换</span><span class="sxs-lookup"><span data-stu-id="1aef7-204">Use F7 to toggle between a Razor Page and the PageModel</span></span>

<span data-ttu-id="1aef7-205">使用 F7 在 Razor 页面（\*.cshtml 文件）与 C# 文件 (\*.cshtml.cs) 之间切换。</span><span class="sxs-lookup"><span data-stu-id="1aef7-205">F7 toggles between a Razor Page (*\*.cshtml* file) and the C# file (*\*.cshtml.cs*).</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="1aef7-206">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1aef7-206">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!-- TODO review  Need something in these tabs -->

<span data-ttu-id="1aef7-207">按照约定，Razor 页面（\*.cshtml 文件）和关联 `PageModel` 具有相同的根文件名称。</span><span class="sxs-lookup"><span data-stu-id="1aef7-207">By convention, the Razor Page (*\*.cshtml* file) and the associated `PageModel` have the same root file name.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="1aef7-208">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="1aef7-208">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="1aef7-209">按照约定，Razor 页面（\*.cshtml 文件）和关联 `PageModel` 具有相同的根文件名称。</span><span class="sxs-lookup"><span data-stu-id="1aef7-209">By convention, the Razor Page (*\*.cshtml* file) and the associated `PageModel` have the same root file name.</span></span>

---

> [!div class="step-by-step"]
> [<span data-ttu-id="1aef7-210">下一篇：添加模型</span><span class="sxs-lookup"><span data-stu-id="1aef7-210">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)