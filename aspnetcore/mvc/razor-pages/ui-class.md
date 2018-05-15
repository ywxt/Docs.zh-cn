---
title: ASP.NET Core 的类库中的可重用 Razor UI
author: Rick-Anderson
description: 说明如何在类库中创建可重用 Razor UI。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/31/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: advanced
uid: mvc/razor-pages/ui-class
ms.openlocfilehash: 731d37a8f4983b18ded114f05470f8a408deb7cd
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-reusable-ui-using-the-razor-class-library-project-in-aspnet-core"></a><span data-ttu-id="1d4a1-103">使用 ASP.NET Core 中的 Razor 类库项目创建可重用 UI。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-103">Create reusable UI using the Razor Class Library project in ASP.NET Core.</span></span>

<span data-ttu-id="1d4a1-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1d4a1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1d4a1-105">Razor 视图、页面、控制器、页模型和数据模型可以创建在 Razor 类库 (RCL) 中。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-105">Razor views, pages, controllers, page models, and data models can be built into a Razor Class Library(RCL).</span></span> <span data-ttu-id="1d4a1-106">RCL 可以打包并重复使用。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-106">The RCL can be and packaged and reused.</span></span> <span data-ttu-id="1d4a1-107">应用程序可以包括 RCL，并重写其中包含的视图和页面。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-107">Applications can include the RCL and override the views and pages it contains.</span></span> <span data-ttu-id="1d4a1-108">如果在 Web 应用和 RCL 中都能找到视图、分部视图或 Razor 页面，则 Web 应用中的 Razor 标记（.cshtml 文件）优先。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-108">When a view, partial view, or Razor Page is found in both the web app and the RCL, the Razor markup (*.cshtml* file) in the web app takes precedence.</span></span>

<span data-ttu-id="1d4a1-109">此功能需要 [!INCLUDE[](~/includes/2.1-SDK.md)]</span><span class="sxs-lookup"><span data-stu-id="1d4a1-109">This feature requires [!INCLUDE[](~/includes/2.1-SDK.md)]</span></span>

[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="1d4a1-110">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="1d4a1-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="create-a-class-library-containing-razor-ui"></a><span data-ttu-id="1d4a1-111">创建一个包含 Razor UI 的类库</span><span class="sxs-lookup"><span data-stu-id="1d4a1-111">Create a class library containing Razor UI</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1d4a1-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d4a1-112">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="1d4a1-113">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-113">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="1d4a1-114">选择“ASP.NET Core Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-114">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="1d4a1-115">验证是否已选择 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-115">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="1d4a1-116">选择“Razor 类库” > “确定”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-116">Select **Razor Class Library** > **OK**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="1d4a1-117">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="1d4a1-117">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="1d4a1-118">从命令行中运行 `dotnet new razorclasslib`。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-118">From the commandline, run `dotnet new razorclasslib`.</span></span> <span data-ttu-id="1d4a1-119">例如:</span><span class="sxs-lookup"><span data-stu-id="1d4a1-119">For example:</span></span>

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
```

<span data-ttu-id="1d4a1-120">有关详细信息，请查看 [dotnet new](/dotnet/core/tools/dotnet-new)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-120">For more information, see [dotnet new](/dotnet/core/tools/dotnet-new).</span></span>

------
<span data-ttu-id="1d4a1-121">将 Razor 文件添加到 RCL。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-121">Add Razor files to the RCL.</span></span>

<span data-ttu-id="1d4a1-122">建议将 RCL 内容转至“区域”文件夹。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-122">We recommend RCL content go in the *Areas* folder.</span></span> 


## <a name="referencing-razor-class-library-content"></a><span data-ttu-id="1d4a1-123">引用 Razor 类库内容</span><span class="sxs-lookup"><span data-stu-id="1d4a1-123">Referencing Razor Class Library content</span></span>

<span data-ttu-id="1d4a1-124">可以通过以下方式引用 RCL：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-124">The RCL can be referenced by:</span></span>

* <span data-ttu-id="1d4a1-125">NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-125">NuGet package.</span></span> <span data-ttu-id="1d4a1-126">请参阅[创建 NuGet 包](/nuget/create-packages/creating-a-package)、[dotnet 添加包](/dotnet/core/tools/dotnet-add-package)和[创建和发布 NuGet 包](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-126">See [Creating NuGet packages](/nuget/create-packages/creating-a-package) and [dotnet add package](/dotnet/core/tools/dotnet-add-package) and [Create and publish a NuGet package](/nuget/quickstart/create-and-publish-a-package-using-visual-studio).</span></span>
* <span data-ttu-id="1d4a1-127">{ProjectName}.csproj。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-127">*{ProjectName}.csproj*.</span></span> <span data-ttu-id="1d4a1-128">请查看 [dotnet-add 引用](/dotnet/core/tools/dotnet-add-reference)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-128">See [dotnet-add reference](/dotnet/core/tools/dotnet-add-reference).</span></span>

### <a name="partial-files-access-in-the-rcl"></a><span data-ttu-id="1d4a1-129">RCL 中的分部文件访问</span><span class="sxs-lookup"><span data-stu-id="1d4a1-129">Partial files access in the RCL</span></span>

<span data-ttu-id="1d4a1-130">对于 RCL 之外的内容，ASP.NET Core 运行时不会搜索 RCL 中的分部文件。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-130">For content outside the RCL, the ASP.NET Core runtime does not search for partial files in the RCL.</span></span>

<span data-ttu-id="1d4a1-131">例如，在示例下载中，不能在 WebApp1\Pages\About.cshtml 中引用 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 分部视图。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-131">For example, in the sample download, the *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* partial view can **not** be referenced in *WebApp1\Pages\About.cshtml*.</span></span> <span data-ttu-id="1d4a1-132">然而 RCL (RazorUIClassLib/) 中的页面可以访问 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtm。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-132">However, pages in the RCL ( *RazorUIClassLib/* **can** access *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span>

## <a name="walkthrough-create-a-razor-class-library-project-and-use-from-a-razor-pages-project"></a><span data-ttu-id="1d4a1-133">演练：创建 Razor 类库项目并从 Razor 页面项目使用它</span><span class="sxs-lookup"><span data-stu-id="1d4a1-133">Walkthrough: Create a Razor Class Library project and use from a Razor Pages project</span></span>

<span data-ttu-id="1d4a1-134">可以下载并测试[完整项目](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)，无需创建项目。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-134">You can download the [complete project](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples) and test it rather than creating it.</span></span> <span data-ttu-id="1d4a1-135">示例下载包含附加代码和链接，以方便测试项目。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-135">The sample download contains additional code and links that make the project easy to test.</span></span> <span data-ttu-id="1d4a1-136">可以在[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6098)中留下反馈，评论下载示例和分步说明的对比。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-136">You can leave feedback in [this GitHub issue](https://github.com/aspnet/Docs/issues/6098) with your comments on download samples versus step-by-step instructions.</span></span>

### <a name="test-the-download-app"></a><span data-ttu-id="1d4a1-137">测试下载应用</span><span class="sxs-lookup"><span data-stu-id="1d4a1-137">Test the download app</span></span>

<span data-ttu-id="1d4a1-138">如果尚未下载已完成的应用，并更愿意创建演练项目，请跳转至[下一节](#create-a-razor-class-library)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-138">If you haven't downloaded the completed app and would rather create the walkthrough project, skip to the [next section](#create-a-razor-class-library).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1d4a1-139">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d4a1-139">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="1d4a1-140">在 Visual Studio 中打开 .sln 文件。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-140">Open the *.sln* file in Visual Studio.</span></span> <span data-ttu-id="1d4a1-141">运行应用。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-141">Run the app.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="1d4a1-142">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="1d4a1-142">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="1d4a1-143">在 cli 目录中的命令提示符下生成 RCL 和 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-143">From a command prompt in the *cli* directory, build the RCL and web app.</span></span>

``` CLI
dotnet build
```

<span data-ttu-id="1d4a1-144">移动至 WebApp1 目录，并运行应用：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-144">Move to the *WebApp1* directory and run the app:</span></span>

``` CLI
dotnet run
```
------

<span data-ttu-id="1d4a1-145">按“测试 Test WebApp1”中的说明进行操作[](#test)</span><span class="sxs-lookup"><span data-stu-id="1d4a1-145">Follow the instructions in [Test WebApp1](#test)</span></span>

## <a name="create-a-razor-class-library"></a><span data-ttu-id="1d4a1-146">创建 Razor 类库</span><span class="sxs-lookup"><span data-stu-id="1d4a1-146">Create a Razor Class Library</span></span>

<span data-ttu-id="1d4a1-147">本部分创建 Razor 类库 (RCL)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-147">In this section, a Razor Class Library (RCL) is created.</span></span> <span data-ttu-id="1d4a1-148">将 Razor 文件添加到 RCL。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-148">Razor files are added to the RCL.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1d4a1-149">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d4a1-149">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="1d4a1-150">创建 RCL 项目：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-150">Create the RCL project:</span></span>

* <span data-ttu-id="1d4a1-151">从 Visual Studio“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-151">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="1d4a1-152">选择“ASP.NET Core Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-152">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="1d4a1-153">将应用命名为 RazorUIClassLib。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-153">Name the app **RazorUIClassLib**.</span></span>
* <span data-ttu-id="1d4a1-154">验证是否已选择 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-154">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="1d4a1-155">选择“Razor 类库” > “确定”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-155">Select **Razor Class Library** > **OK**.</span></span>

<span data-ttu-id="1d4a1-156">创建 Razor 页面 Web 应用：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-156">Create the Razor Pages web app:</span></span>

* <span data-ttu-id="1d4a1-157">在解决方案资源管理器中，右键单击解决方案 >“添加” >  “新建项目”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-157">From **Solution Explorer**, right-click the solution > **Add** >  **New Project**.</span></span>
* <span data-ttu-id="1d4a1-158">选择“ASP.NET Core Web 应用程序”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-158">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="1d4a1-159">将应用命名为 WebApp1。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-159">Name the app **WebApp1**.</span></span>
* <span data-ttu-id="1d4a1-160">验证是否已选择 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-160">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="1d4a1-161">选择“Web 应用程序” > “确定”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-161">Select **Web Application** > **OK**.</span></span>

### <a name="add-razor-files-and-folders-to-the-project"></a><span data-ttu-id="1d4a1-162">将 Razor 文件和文件夹添加到该项目。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-162">Add Razor files and folders to the project.</span></span>

* <span data-ttu-id="1d4a1-163">添加一个名为 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 的 Razor 分部视图文件。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-163">Add a Razor partial view file named *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span>
* <span data-ttu-id="1d4a1-164">使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 中的标记：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-164">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* <span data-ttu-id="1d4a1-165">将 WebApp1 项目中的 _ViewStart.cshtml 文件复制到 RazorUIClassLib/Areas/MyFeature/Pages/_ViewStart.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-165">Copy the *_ViewStart.cshtml* file from the WebApp1 project to  *RazorUIClassLib/Areas/MyFeature/Pages/_ViewStart.cshtml*.</span></span>

  <span data-ttu-id="1d4a1-166">使用 Razor 页面项目的布局需要 [Viewstart](xref:mvc/views/layout#running-code-before-each-view) 文件。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-166">The [viewstart](xref:mvc/views/layout#running-code-before-each-view) file is required to use the layout of the Razor Pages project.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="1d4a1-167">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="1d4a1-167">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="1d4a1-168">从命令行运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-168">From the command line, run the following:</span></span>

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
dotnet new page -n _Message -np -o RazorUIClassLib/Areas/MyFeature/Pages/Shared
dotnet new viewstart -o RazorUIClassLib/Areas/MyFeature/Pages
```

<span data-ttu-id="1d4a1-169">前面的命令：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-169">The preceding commands:</span></span>

* <span data-ttu-id="1d4a1-170">创建 `RazorUIClassLib` Razor 类库 (RCL)。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-170">Creates the `RazorUIClassLib` Razor Class Library (RCL).</span></span>
* <span data-ttu-id="1d4a1-171">创建 Razor _Message 页面，并将其添加至 RCL。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-171">Creates a Razor _Message page, and adds it to the RCL.</span></span> <span data-ttu-id="1d4a1-172">`-np` 参数创建不含 `PageModel` 的页面。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-172">The `-np` parameter creates the page without a `PageModel`.</span></span>
* <span data-ttu-id="1d4a1-173">创建 [viewstart](xref:mvc/views/layout#running-code-before-each-view) 文件并将其添加到 RCL。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-173">Creates a [viewstart](xref:mvc/views/layout#running-code-before-each-view) file and adds it to the RCL.</span></span>

<span data-ttu-id="1d4a1-174">使用 Razor 页面项目的布局需要 Viewstart 文件（将在下一节中添加）。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-174">The viewstart file is required to use the layout of the Razor Pages project (which is added in the next section).</span></span>

<span data-ttu-id="1d4a1-175">更新 Razor 页面：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-175">Update the Razor Pages:</span></span>

* <span data-ttu-id="1d4a1-176">使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 中的标记：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-176">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* <span data-ttu-id="1d4a1-177">使用以下代码替换 RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml 中的标记：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-177">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml)]

<span data-ttu-id="1d4a1-178">使用分步视图 (`<partial name="_Message" />`) 需要 `@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-178">`@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers` is required to use the partial view (`<partial name="_Message" />`).</span></span> <span data-ttu-id="1d4a1-179">可以添加一个 _ViewImports.cshtml 文件，无需包含 `@addTagHelper` 指令。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-179">Rather than including the `@addTagHelper` directive, you can add a *_ViewImports.cshtml* file.</span></span> <span data-ttu-id="1d4a1-180">例如:</span><span class="sxs-lookup"><span data-stu-id="1d4a1-180">For example:</span></span>

``` CLI
dotnet new viewimports -o RazorUIClassLib/Areas/MyFeature/Pages
```

<span data-ttu-id="1d4a1-181">有关 Viewimports 的详细信息，请参阅[导入共享指令](xref:mvc/views/layout#importing-shared-directives)</span><span class="sxs-lookup"><span data-stu-id="1d4a1-181">For more information on viewimports, see [Importing Shared Directives](xref:mvc/views/layout#importing-shared-directives)</span></span>

* <span data-ttu-id="1d4a1-182">生成类库以验证是否不存在编译器错误：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-182">Build the class library to verify there are no compiler errors:</span></span>

``` CLI
dotnet build RazorUIClassLib
```

<span data-ttu-id="1d4a1-183">生成输出内容包含 RazorUIClassLib.dll 和 RazorUIClassLib.Views.dll。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-183">The build output contains *RazorUIClassLib.dll* and *RazorUIClassLib.Views.dll*.</span></span> <span data-ttu-id="1d4a1-184">RazorUIClassLib.Views.dll 包含已编译的 Razor 内容。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-184">*RazorUIClassLib.Views.dll* contains the compiled Razor content.</span></span>

------

### <a name="use-the-razor-ui-library-from-a-razor-pages-project"></a><span data-ttu-id="1d4a1-185">从 Razor 页面项目使用 Razor UI 库</span><span class="sxs-lookup"><span data-stu-id="1d4a1-185">Use the Razor UI library from a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1d4a1-186">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d4a1-186">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="1d4a1-187">在解决方案资源管理器中，右键单击“WebApp1”，然后选择“设为启动项目”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-187">From **Solution Explorer**, right-click on **WebApp1** and select **Set as StartUp Project**.</span></span>
* <span data-ttu-id="1d4a1-188">在解决方案资源管理器中，右键单击“WebApp1”，然后选择“生成依赖项” > “项目依赖项”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-188">From **Solution Explorer**, right-click on **WebApp1** and select **Build Dependencies** > **Project Dependencies**.</span></span>
* <span data-ttu-id="1d4a1-189">将 RazorUIClassLib 勾选为 WebApp1 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-189">Check **RazorUIClassLib** as a dependency of **WebApp1**.</span></span>
* <span data-ttu-id="1d4a1-190">在解决方案资源管理器中，右键单击“WebApp1”，选择“添加” > “引用”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-190">From **Solution Explorer**, right-click on **WebApp1** and select **Add** > **Reference**.</span></span>
* <span data-ttu-id="1d4a1-191">在“引用管理器”对话框中勾选“RazorUIClassLib” > “确定”。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-191">In the **Reference Manager** dialog, check **RazorUIClassLib** > **OK**.</span></span>

<span data-ttu-id="1d4a1-192">运行应用。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-192">Run the app.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="1d4a1-193">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="1d4a1-193">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="1d4a1-194">创建 Razor 页面 Web 应用和包含 Razor 页面应用和 Razor 类库的解决方案文件：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-194">Create a Razor Pages web app and a solution file containing the Razor Pages app and the Razor Class Library:</span></span>

``` CLI
dotnet new razor -o WebApp1
dotnet new sln
dotnet sln add WebApp1
dotnet sln add RazorUIClassLib
dotnet add WebApp1 reference RazorUIClassLib
```

<span data-ttu-id="1d4a1-195">生成并运行 Web 应用：</span><span class="sxs-lookup"><span data-stu-id="1d4a1-195">Build and run the web app:</span></span>

``` CLI
cd WebApp1
dotnet run
```

------

<a name="test"></a>

### <a name="test-webapp1"></a><span data-ttu-id="1d4a1-196">测试 WebApp1</span><span class="sxs-lookup"><span data-stu-id="1d4a1-196">Test WebApp1</span></span>

<span data-ttu-id="1d4a1-197">验证正在使用的 Razor UI 类库。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-197">Verify the Razor UI class library is being used.</span></span>

* <span data-ttu-id="1d4a1-198">浏览到 `/MyFeature/Page1`。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-198">Browse to `/MyFeature/Page1`.</span></span>

## <a name="override-views-partial-views-and-pages"></a><span data-ttu-id="1d4a1-199">重写视图、分部视图和页面</span><span class="sxs-lookup"><span data-stu-id="1d4a1-199">Override views, partial views, and pages</span></span>

<span data-ttu-id="1d4a1-200">如果在 Web 应用和 Razor 类库中都能找到视图、分部视图或 Razor 页面，则 Web 应用中的 Razor 标记（.cshtml 文件）优先。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-200">When a view, partial view, or Razor Page is found in both the web app and the Razor Class Library, the Razor markup (*.cshtml* file) in the web app takes precedence.</span></span> <span data-ttu-id="1d4a1-201">例如，将 WebApp1/Areas/MyFeature/Pages/Page1.cshtml 添加到 WebApp1，则 WebApp1 中的 Page1 会优先于 Razor 类库中的 Page1。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-201">For example, add *WebApp1/Areas/MyFeature/Pages/Page1.cshtml* to WebApp1, and Page1 in the WebApp1 will take precedence over Page1in the Razor Class Library.</span></span>

<span data-ttu-id="1d4a1-202">在示例下载中，将 WebApp1/Areas/MyFeature2 重命名为 WebApp1/Areas/MyFeature 来测试优先级。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-202">In the sample download, rename *WebApp1/Areas/MyFeature2* to *WebApp1/Areas/MyFeature* to test precedence.</span></span>

<span data-ttu-id="1d4a1-203">将 RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml 分部视图复制到 WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-203">Copy the *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* partial view to *WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span> <span data-ttu-id="1d4a1-204">更新标记以指示新的位置。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-204">Update the markup to indicate the new location.</span></span> <span data-ttu-id="1d4a1-205">生成并运行应用，验证使用部分的应用版本。</span><span class="sxs-lookup"><span data-stu-id="1d4a1-205">Build and run the app to verify the app's version of the partial is being used.</span></span>
