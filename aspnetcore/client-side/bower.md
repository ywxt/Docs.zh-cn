---
title: 管理 ASP.NET Core 中的 Bower 的客户端包
author: rick-anderson
description: 管理 Bower 的客户端包。
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: client-side/bower
ms.openlocfilehash: ada8120189baf036296b83f91d20b364ee90d074
ms.sourcegitcommit: 07903a1be39a99dcf538d57981161592d0e658b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/20/2018
---
# <a name="manage-client-side-packages-with-bower-in-aspnet-core"></a><span data-ttu-id="648fd-103">管理 ASP.NET Core 中的 Bower 的客户端包</span><span class="sxs-lookup"><span data-stu-id="648fd-103">Manage client-side packages with Bower in ASP.NET Core</span></span>

<span data-ttu-id="648fd-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)，[了米](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)，和[Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="648fd-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), and [Scott Addie](https://scottaddie.com)</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="648fd-105">而维持 Bower，其 maintainer 建议使用另一种解决方案。</span><span class="sxs-lookup"><span data-stu-id="648fd-105">While Bower is maintained, its maintainers recommend using a different solution.</span></span> <span data-ttu-id="648fd-106">[库管理器](https://blogs.msdn.microsoft.com/webdev/2018/04/18/what-happened-to-bower/)(简称 LibMan) 是 Visual Studio 的新客户端的静态内容管理系统。</span><span class="sxs-lookup"><span data-stu-id="648fd-106">[Library Manager](https://blogs.msdn.microsoft.com/webdev/2018/04/18/what-happened-to-bower/) (LibMan for short) is Visual Studio's new client-side static content management system.</span></span> <span data-ttu-id="648fd-107">与 Webpack yarn 是一个常用的替代项为其[迁移说明](https://bower.io/blog/2017/how-to-migrate-away-from-bower/)可用。</span><span class="sxs-lookup"><span data-stu-id="648fd-107">Yarn with Webpack is one popular alternative for which [migration instructions](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) are available.</span></span>

<span data-ttu-id="648fd-108">[Bower](https://bower.io/)调用自身"web 程序包管理器"。</span><span class="sxs-lookup"><span data-stu-id="648fd-108">[Bower](https://bower.io/) calls itself "A package manager for the web".</span></span> <span data-ttu-id="648fd-109">内部.NET 生态系统，它将填入 void 留下的 NuGet 的无法传送静态内容的文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-109">Within the .NET ecosystem, it fills the void left by NuGet's inability to deliver static content files.</span></span> <span data-ttu-id="648fd-110">对于 ASP.NET Core 项目，这些静态文件，则所固有的客户端库，如[jQuery](http://jquery.com/)和[Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="648fd-110">For ASP.NET Core projects, these static files are inherent to client-side libraries like [jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="648fd-111">对于.NET 库，你仍然使用[NuGet](https://www.nuget.org/)程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="648fd-111">For .NET libraries, you still use [NuGet](https://www.nuget.org/) package manager.</span></span>

<span data-ttu-id="648fd-112">设置客户端的 ASP.NET Core 项目模板创建的新项目生成过程。</span><span class="sxs-lookup"><span data-stu-id="648fd-112">New projects created with the ASP.NET Core project templates set up the client-side build process.</span></span> <span data-ttu-id="648fd-113">[jQuery](http://jquery.com/)和[Bootstrap](http://getbootstrap.com/)安装，并支持 Bower。</span><span class="sxs-lookup"><span data-stu-id="648fd-113">[jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/) are installed, and Bower is supported.</span></span>

<span data-ttu-id="648fd-114">在列出客户端包*bower.json*文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-114">Client-side packages are listed in the *bower.json* file.</span></span> <span data-ttu-id="648fd-115">ASP.NET 核心项目模板配置*bower.json* jQuery、 jQuery 验证与 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="648fd-115">The ASP.NET Core project templates configures *bower.json* with jQuery, jQuery validation, and Bootstrap.</span></span>

<span data-ttu-id="648fd-116">在本教程中，我们将添加对支持[字体出色](http://fontawesome.io)。</span><span class="sxs-lookup"><span data-stu-id="648fd-116">In this tutorial, we'll add support for [Font Awesome](http://fontawesome.io).</span></span> <span data-ttu-id="648fd-117">可以使用安装 bower 包**管理 Bower 包**UI 或手动在*bower.json*文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-117">Bower packages can be installed with the **Manage Bower Packages** UI or manually in the *bower.json* file.</span></span>

### <a name="installation-via-manage-bower-packages-ui"></a><span data-ttu-id="648fd-118">通过管理 Bower 包 UI 的安装</span><span class="sxs-lookup"><span data-stu-id="648fd-118">Installation via Manage Bower Packages UI</span></span>

* <span data-ttu-id="648fd-119">创建新的 ASP.NET 核心 Web 应用程序与**ASP.NET 核心 Web 应用程序 (.NET Core)** 模板。</span><span class="sxs-lookup"><span data-stu-id="648fd-119">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="648fd-120">选择**Web 应用程序**和**无身份验证**。</span><span class="sxs-lookup"><span data-stu-id="648fd-120">Select **Web Application** and **No Authentication**.</span></span>

* <span data-ttu-id="648fd-121">右键单击解决方案资源管理器中的项目并选择**管理 Bower 包**(或者从主菜单中，**项目** > **管理 Bower 包**).</span><span class="sxs-lookup"><span data-stu-id="648fd-121">Right-click the project in Solution Explorer and select **Manage Bower Packages** (alternatively from the main menu, **Project** > **Manage Bower Packages**).</span></span>

* <span data-ttu-id="648fd-122">在**Bower:\<项目名称\>** 窗口中，单击"浏览"选项卡，并输入，然后筛选包列表`font-awesome`的搜索框中：</span><span class="sxs-lookup"><span data-stu-id="648fd-122">In the **Bower: \<project name\>** window, click the "Browse" tab, and then filter the packages list by entering `font-awesome` in the search box:</span></span>

  ![管理 bower 包](bower/_static/manage-bower-packages.png)

* <span data-ttu-id="648fd-124">确认"保存更改为*bower.json*"复选框已选中。</span><span class="sxs-lookup"><span data-stu-id="648fd-124">Confirm that the "Save changes to *bower.json*" checkbox is checked.</span></span> <span data-ttu-id="648fd-125">从下拉列表中选择一个版本，然后单击**安装**按钮。</span><span class="sxs-lookup"><span data-stu-id="648fd-125">Select a version from the drop-down list and click the **Install** button.</span></span> <span data-ttu-id="648fd-126">**输出**窗口显示的安装详细信息。</span><span class="sxs-lookup"><span data-stu-id="648fd-126">The **Output** window shows the installation details.</span></span>

### <a name="manual-installation-in-bowerjson"></a><span data-ttu-id="648fd-127">手动安装在 bower.json</span><span class="sxs-lookup"><span data-stu-id="648fd-127">Manual installation in bower.json</span></span>

<span data-ttu-id="648fd-128">打开*bower.json*文件并添加到的依赖项的"字体出色"。</span><span class="sxs-lookup"><span data-stu-id="648fd-128">Open the *bower.json* file and add "font-awesome" to the dependencies.</span></span> <span data-ttu-id="648fd-129">IntelliSense 会显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="648fd-129">IntelliSense shows the available packages.</span></span> <span data-ttu-id="648fd-130">某个包被选中，将显示可用的版本。</span><span class="sxs-lookup"><span data-stu-id="648fd-130">When a package is selected, the available versions are displayed.</span></span> <span data-ttu-id="648fd-131">下面的映像不较旧，并不会匹配你看到的内容。</span><span class="sxs-lookup"><span data-stu-id="648fd-131">The images below are older and won't match what you see.</span></span>

![Bower 包资源管理器的智能感知](bower/_static/add-package.png)

![bower 版本 IntelliSense](bower/_static/version-intelliSense.png)

<span data-ttu-id="648fd-134">Bower 使用[语义版本控制](http://semver.org/)来组织依赖关系。</span><span class="sxs-lookup"><span data-stu-id="648fd-134">Bower uses [semantic versioning](http://semver.org/) to organize dependencies.</span></span> <span data-ttu-id="648fd-135">语义版本控制，也称为 SemVer，标识包的编号方案\<主要 >。\<次要 >。\<修补程序 >。</span><span class="sxs-lookup"><span data-stu-id="648fd-135">Semantic versioning, also known as SemVer, identifies packages with the numbering scheme \<major>.\<minor>.\<patch>.</span></span> <span data-ttu-id="648fd-136">IntelliSense 显示仅几个常用的选项，从而简化了语义版本控制。</span><span class="sxs-lookup"><span data-stu-id="648fd-136">IntelliSense simplifies semantic versioning by showing only a few common choices.</span></span> <span data-ttu-id="648fd-137">IntelliSense 列表 (在上面的示例 4.6.3) 中的顶级项被视为包的最新稳定版本。</span><span class="sxs-lookup"><span data-stu-id="648fd-137">The top item in the IntelliSense list (4.6.3 in the example above) is considered the latest stable version of the package.</span></span> <span data-ttu-id="648fd-138">脱字号 (^) 符号匹配的最新的主版本和波形符 （~） 与最新次要版本匹配。</span><span class="sxs-lookup"><span data-stu-id="648fd-138">The caret (^) symbol matches the most recent major version and the tilde (~) matches the most recent minor version.</span></span>

<span data-ttu-id="648fd-139">保存*bower.json*文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-139">Save the *bower.json* file.</span></span> <span data-ttu-id="648fd-140">Visual Studio 监视*bower.json*文件的更改。</span><span class="sxs-lookup"><span data-stu-id="648fd-140">Visual Studio watches the *bower.json* file for changes.</span></span> <span data-ttu-id="648fd-141">保存后， *bower 安装*执行命令。</span><span class="sxs-lookup"><span data-stu-id="648fd-141">Upon saving, the *bower install* command is executed.</span></span> <span data-ttu-id="648fd-142">请参见输出窗口**Bower/npm**视图执行的确切命令。</span><span class="sxs-lookup"><span data-stu-id="648fd-142">See the Output window's **Bower/npm** view for the exact command executed.</span></span>

<span data-ttu-id="648fd-143">打开 *.bowerrc*文件下*bower.json*。</span><span class="sxs-lookup"><span data-stu-id="648fd-143">Open the *.bowerrc* file under *bower.json*.</span></span> <span data-ttu-id="648fd-144">`directory`属性设置为*wwwroot/lib*指示的位置 Bower 将安装包资产。</span><span class="sxs-lookup"><span data-stu-id="648fd-144">The `directory` property is set to *wwwroot/lib* which indicates the location Bower will install the package assets.</span></span>

```json
{
 "directory": "wwwroot/lib"
}
```

<span data-ttu-id="648fd-145">在解决方案资源管理器搜索框中可用于查找并显示字体出色的包。</span><span class="sxs-lookup"><span data-stu-id="648fd-145">You can use the search box in Solution Explorer to find and display the font-awesome package.</span></span>

<span data-ttu-id="648fd-146">打开*views/shared\_Layout.cshtml*文件并将字体出色的 CSS 文件添加到环境[标记帮助器](xref:mvc/views/tag-helpers/intro)为`Development`。</span><span class="sxs-lookup"><span data-stu-id="648fd-146">Open the *Views\Shared\_Layout.cshtml* file and add the font-awesome CSS file to the environment [Tag Helper](xref:mvc/views/tag-helpers/intro) for `Development`.</span></span> <span data-ttu-id="648fd-147">从解决方案资源管理器，将拖*字体 awesome.css*内`<environment names="Development">`元素。</span><span class="sxs-lookup"><span data-stu-id="648fd-147">From Solution Explorer, drag and drop *font-awesome.css* inside the `<environment names="Development">` element.</span></span>

[!code-html[](bower/sample/_Layout.cshtml?highlight=4&range=9-13)]

<span data-ttu-id="648fd-148">在生产应用程序会添加*字体 awesome.min.css*到环境标记帮助器`Staging,Production`。</span><span class="sxs-lookup"><span data-stu-id="648fd-148">In a production app you would add *font-awesome.min.css* to the environment tag helper for `Staging,Production`.</span></span>

<span data-ttu-id="648fd-149">内容替换*Views\Home\About.cshtml* Razor 文件替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="648fd-149">Replace the contents of the *Views\Home\About.cshtml* Razor file with the following markup:</span></span>

[!code-html[](bower/sample/About.cshtml)]

<span data-ttu-id="648fd-150">运行应用程序并导航到关于视图，以验证字体出色包正常运行。</span><span class="sxs-lookup"><span data-stu-id="648fd-150">Run the app and navigate to the About view to verify the font-awesome package works.</span></span>

## <a name="exploring-the-client-side-build-process"></a><span data-ttu-id="648fd-151">浏览客户端生成过程</span><span class="sxs-lookup"><span data-stu-id="648fd-151">Exploring the client-side build process</span></span>

<span data-ttu-id="648fd-152">大多数 ASP.NET Core 项目模板已配置为使用 Bower。</span><span class="sxs-lookup"><span data-stu-id="648fd-152">Most ASP.NET Core project templates are already configured to use Bower.</span></span> <span data-ttu-id="648fd-153">此下一个演练中创建空的 ASP.NET Core 项目启动，并手动添加每个部分，以便您可以如何在项目中使用 Bower 获取获得感觉。</span><span class="sxs-lookup"><span data-stu-id="648fd-153">This next walkthrough starts with an empty ASP.NET Core project and adds each piece manually, so you can get a feel for how Bower is used in a project.</span></span> <span data-ttu-id="648fd-154">你可以查看到的项目结构和运行时，输出会和每个配置更改会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="648fd-154">You can see what happens to the project structure and the runtime output as each configuration change is made.</span></span>

<span data-ttu-id="648fd-155">将客户端生成过程用于 Bower 的常规步骤如下：</span><span class="sxs-lookup"><span data-stu-id="648fd-155">The general steps to use the client-side build process with Bower are:</span></span>

* <span data-ttu-id="648fd-156">定义项目中使用的包。</span><span class="sxs-lookup"><span data-stu-id="648fd-156">Define packages used in your project.</span></span> <!-- once defined, you don't need to download them, VS does -->
* <span data-ttu-id="648fd-157">从 web 页面的引用包。</span><span class="sxs-lookup"><span data-stu-id="648fd-157">Reference packages from your web pages.</span></span>

### <a name="define-packages"></a><span data-ttu-id="648fd-158">定义包</span><span class="sxs-lookup"><span data-stu-id="648fd-158">Define packages</span></span>

<span data-ttu-id="648fd-159">一旦列表中的包*bower.json*文件，Visual Studio 将下载它们。</span><span class="sxs-lookup"><span data-stu-id="648fd-159">Once you list packages in the *bower.json* file, Visual Studio will download them.</span></span> <span data-ttu-id="648fd-160">下面的示例使用 Bower 加载 jQuery 和引导定向到*wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="648fd-160">The following example uses Bower to load jQuery and Bootstrap to the *wwwroot* folder.</span></span>

* <span data-ttu-id="648fd-161">创建新的 ASP.NET 核心 Web 应用程序与**ASP.NET 核心 Web 应用程序 (.NET Core)** 模板。</span><span class="sxs-lookup"><span data-stu-id="648fd-161">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="648fd-162">选择**空**项目模板，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="648fd-162">Select the **Empty** project template and click **OK**.</span></span>

* <span data-ttu-id="648fd-163">在解决方案资源管理器，右键单击项目 >**添加新项**和选择**Bower 配置文件**。</span><span class="sxs-lookup"><span data-stu-id="648fd-163">In Solution Explorer, right-click the project > **Add New Item** and select **Bower Configuration File**.</span></span> <span data-ttu-id="648fd-164">注意： A *.bowerrc*还添加文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-164">Note: A *.bowerrc* file is also added.</span></span>

* <span data-ttu-id="648fd-165">打开*bower.json*，并添加 jquery 和引导到`dependencies`部分。</span><span class="sxs-lookup"><span data-stu-id="648fd-165">Open *bower.json*, and add jquery and bootstrap to the `dependencies` section.</span></span> <span data-ttu-id="648fd-166">生成*bower.json*文件将如下所示下面的示例。</span><span class="sxs-lookup"><span data-stu-id="648fd-166">The resulting *bower.json* file will look like the following example.</span></span> <span data-ttu-id="648fd-167">版本将会发生更改，并且可能不匹配下图所示。</span><span class="sxs-lookup"><span data-stu-id="648fd-167">The versions will change over time and may not match the image below.</span></span>

[!code-json[](bower/sample/bower.json?highlight=5,6)]

* <span data-ttu-id="648fd-168">保存*bower.json*文件。</span><span class="sxs-lookup"><span data-stu-id="648fd-168">Save the *bower.json* file.</span></span>

  <span data-ttu-id="648fd-169">验证该项目包括*bootstrap*和*jQuery*中的目录*wwwroot/lib*。</span><span class="sxs-lookup"><span data-stu-id="648fd-169">Verify the project includes the *bootstrap* and *jQuery* directories in *wwwroot/lib*.</span></span> <span data-ttu-id="648fd-170">Bower 使用 *.bowerrc*文件以安装中的资产*wwwroot/lib*。</span><span class="sxs-lookup"><span data-stu-id="648fd-170">Bower uses the *.bowerrc* file to install the assets in *wwwroot/lib*.</span></span>

  <span data-ttu-id="648fd-171">注意:"管理 Bower 包"UI 提供手动文件编辑的替代方法。</span><span class="sxs-lookup"><span data-stu-id="648fd-171">Note: The "Manage Bower Packages" UI provides an alternative to manual file editing.</span></span>

### <a name="enable-static-files"></a><span data-ttu-id="648fd-172">启用静态文件</span><span class="sxs-lookup"><span data-stu-id="648fd-172">Enable static files</span></span>

* <span data-ttu-id="648fd-173">添加`Microsoft.AspNetCore.StaticFiles`到项目的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="648fd-173">Add the `Microsoft.AspNetCore.StaticFiles` NuGet package to the project.</span></span>
* <span data-ttu-id="648fd-174">启用静态文件提供与[静态文件中间件](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions)。</span><span class="sxs-lookup"><span data-stu-id="648fd-174">Enable static files to be served with the [Static file middleware](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions).</span></span> <span data-ttu-id="648fd-175">添加对的调用[UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions)到`Configure`方法`Startup`。</span><span class="sxs-lookup"><span data-stu-id="648fd-175">Add a call to [UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions) to the `Configure` method of `Startup`.</span></span>

[!code-csharp[](bower/sample/Startup.cs?highlight=9)]

### <a name="reference-packages"></a><span data-ttu-id="648fd-176">引用包</span><span class="sxs-lookup"><span data-stu-id="648fd-176">Reference packages</span></span>

<span data-ttu-id="648fd-177">在本部分中，你将创建 HTML 页以验证它可以访问已部署的包。</span><span class="sxs-lookup"><span data-stu-id="648fd-177">In this section, you will create an HTML page to verify it can access the deployed packages.</span></span>

* <span data-ttu-id="648fd-178">添加一个名为的新 HTML 页*Index.html*到*wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="648fd-178">Add a new HTML page named *Index.html* to the *wwwroot* folder.</span></span> <span data-ttu-id="648fd-179">注意： 你必须将添加到的 HTML 文件*wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="648fd-179">Note: You must add the HTML file to the *wwwroot* folder.</span></span> <span data-ttu-id="648fd-180">默认情况下，静态内容无法提供外部*wwwroot*。</span><span class="sxs-lookup"><span data-stu-id="648fd-180">By default, static content cannot be served outside *wwwroot*.</span></span> <span data-ttu-id="648fd-181">请参阅[使用静态文件](xref:fundamentals/static-files)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="648fd-181">See [Work with static files](xref:fundamentals/static-files) for more information.</span></span>

  <span data-ttu-id="648fd-182">内容替换*Index.html*替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="648fd-182">Replace the contents of *Index.html* with the following markup:</span></span>

[!code-html[](bower/sample/Index.html)]

* <span data-ttu-id="648fd-183">运行应用程序并导航到`http://localhost:<port>/Index.html`。</span><span class="sxs-lookup"><span data-stu-id="648fd-183">Run the app and navigate to `http://localhost:<port>/Index.html`.</span></span> <span data-ttu-id="648fd-184">或者，使用*Index.html*打开，按`Ctrl+Shift+W`。</span><span class="sxs-lookup"><span data-stu-id="648fd-184">Alternatively, with *Index.html* opened, press `Ctrl+Shift+W`.</span></span> <span data-ttu-id="648fd-185">验证应用 jumbotron 样式，jQuery 代码响应时单击该按钮，以及启动按钮更改状态。</span><span class="sxs-lookup"><span data-stu-id="648fd-185">Verify that the jumbotron styling is applied, the jQuery code responds when the button is clicked, and that the Bootstrap button changes state.</span></span>

  ![应用的 jumbotron 样式](bower/_static/jumbotron.png)
