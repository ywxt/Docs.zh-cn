---
title: 将从 ASP.NET MVC 迁移到 ASP.NET 核心 MVC
author: ardalis
description: 了解如何开始迁移到 ASP.NET 核心 MVC ASP.NET MVC 项目。
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/mvc
ms.openlocfilehash: b8c913c0a6f47a1c993d508f9baae54981327957
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="migrate-from-aspnet-mvc-to-aspnet-core-mvc"></a><span data-ttu-id="af2a1-103">将从 ASP.NET MVC 迁移到 ASP.NET 核心 MVC</span><span class="sxs-lookup"><span data-stu-id="af2a1-103">Migrate from ASP.NET MVC to ASP.NET Core MVC</span></span>

<span data-ttu-id="af2a1-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [Daniel Roth](https://github.com/danroth27)， [Steve Smith](https://ardalis.com/)，和[Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="af2a1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), [Steve Smith](https://ardalis.com/), and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="af2a1-105">这篇文章演示如何开始迁移到 ASP.NET MVC 项目[ASP.NET 核心 MVC](../mvc/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-105">This article shows how to get started migrating an ASP.NET MVC project to [ASP.NET Core MVC](../mvc/overview.md).</span></span> <span data-ttu-id="af2a1-106">在过程中，会突出显示许多已更改利用 ASP.NET MVC 的内容。</span><span class="sxs-lookup"><span data-stu-id="af2a1-106">In the process, it highlights many of the things that have changed from ASP.NET MVC.</span></span> <span data-ttu-id="af2a1-107">从 ASP.NET MVC 迁移是一个多步骤过程，本文涵盖初始安装程序、 基本控制器和视图、 静态内容和客户端依赖关系。</span><span class="sxs-lookup"><span data-stu-id="af2a1-107">Migrating from ASP.NET MVC is a multiple step process and this article covers the initial setup, basic controllers and views, static content, and client-side dependencies.</span></span> <span data-ttu-id="af2a1-108">其他文章涵盖迁移配置和标识代码在许多 ASP.NET MVC 项目中找到。</span><span class="sxs-lookup"><span data-stu-id="af2a1-108">Additional articles cover migrating configuration and identity code found in many ASP.NET MVC projects.</span></span>

> [!NOTE]
> <span data-ttu-id="af2a1-109">这些示例中的版本号可能不是最新。</span><span class="sxs-lookup"><span data-stu-id="af2a1-109">The version numbers in the samples might not be current.</span></span> <span data-ttu-id="af2a1-110">你可能需要相应地更新你的项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-110">You may need to update your projects accordingly.</span></span>

## <a name="create-the-starter-aspnet-mvc-project"></a><span data-ttu-id="af2a1-111">创建初学者 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="af2a1-111">Create the starter ASP.NET MVC project</span></span>

<span data-ttu-id="af2a1-112">为了演示升级，我们将开始通过创建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="af2a1-112">To demonstrate the upgrade, we'll start by creating a ASP.NET MVC app.</span></span> <span data-ttu-id="af2a1-113">创建同名*WebApp1*使命名空间匹配我们在下一步中创建 ASP.NET 核心项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-113">Create it with the name *WebApp1* so the namespace matches the ASP.NET Core project we create in the next step.</span></span>

![Visual Studio 的新项目对话框](mvc/_static/new-project.png)

![新建 Web 应用程序对话框： 在 ASP.NET 模板面板中选择 MVC 项目模板](mvc/_static/new-project-select-mvc-template.png)

<span data-ttu-id="af2a1-116">*可选：* 更改从解决方案的名称*WebApp1*到*Mvc5*。</span><span class="sxs-lookup"><span data-stu-id="af2a1-116">*Optional:* Change the name of the Solution from *WebApp1* to *Mvc5*.</span></span> <span data-ttu-id="af2a1-117">Visual Studio 将显示新的解决方案名称 (*Mvc5*)，从而更轻松地判断此项目从下一步的项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-117">Visual Studio displays the new solution name (*Mvc5*), which makes it easier to tell this project from the next project.</span></span>

## <a name="create-the-aspnet-core-project"></a><span data-ttu-id="af2a1-118">创建 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="af2a1-118">Create the ASP.NET Core project</span></span>

<span data-ttu-id="af2a1-119">创建一个新*空*ASP.NET Core 与以前的项目同名的 web 应用 (*WebApp1*) 以便将两个项目中的命名空间匹配。</span><span class="sxs-lookup"><span data-stu-id="af2a1-119">Create a new *empty* ASP.NET Core web app with the same name as the previous project (*WebApp1*) so the namespaces in the two projects match.</span></span> <span data-ttu-id="af2a1-120">使用相同的命名空间，可更轻松地复制两个项目之间的代码。</span><span class="sxs-lookup"><span data-stu-id="af2a1-120">Having the same namespace makes it easier to copy code between the two projects.</span></span> <span data-ttu-id="af2a1-121">你将需要在比以前的项目以使用相同的名称不同的目录中创建此项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-121">You'll have to create this project in a different directory than the previous project to use the same name.</span></span>

![“新建项目”对话框](mvc/_static/new_core.png)

![新建 ASP.NET Web 应用程序对话框： 在 ASP.NET 核心模板面板中选择的空项目模板](mvc/_static/new-project-select-empty-aspnet5-template.png)

* <span data-ttu-id="af2a1-124">*可选：* 创建新的 ASP.NET Core 应用使用*Web 应用程序*项目模板。</span><span class="sxs-lookup"><span data-stu-id="af2a1-124">*Optional:* Create a new ASP.NET Core app using the *Web Application* project template.</span></span> <span data-ttu-id="af2a1-125">将项目*WebApp1*，然后选择的一个身份验证选项**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="af2a1-125">Name the project *WebApp1*, and select an authentication option of **Individual User Accounts**.</span></span> <span data-ttu-id="af2a1-126">重命名此应用程序到*FullAspNetCore*。</span><span class="sxs-lookup"><span data-stu-id="af2a1-126">Rename this app to *FullAspNetCore*.</span></span> <span data-ttu-id="af2a1-127">在转换过程中创建此项目为您节省时间。</span><span class="sxs-lookup"><span data-stu-id="af2a1-127">Creating this project saves you time in the conversion.</span></span> <span data-ttu-id="af2a1-128">你可以查看若要查看的最终结果或将代码复制到转换项目模板生成的代码。</span><span class="sxs-lookup"><span data-stu-id="af2a1-128">You can look at the template-generated code to see the end result or to copy code to the conversion project.</span></span> <span data-ttu-id="af2a1-129">它也是很有帮助时遇到困难在转换步骤中，要与模板生成项目进行比较。</span><span class="sxs-lookup"><span data-stu-id="af2a1-129">It's also helpful when you get stuck on a conversion step to compare with the template-generated project.</span></span>

## <a name="configure-the-site-to-use-mvc"></a><span data-ttu-id="af2a1-130">配置站点以使用 MVC</span><span class="sxs-lookup"><span data-stu-id="af2a1-130">Configure the site to use MVC</span></span>

* <span data-ttu-id="af2a1-131">如果目标.NET 核心，将 ASP.NET Core metapackage 添加到项目中，调用`Microsoft.AspNetCore.All`默认情况下。</span><span class="sxs-lookup"><span data-stu-id="af2a1-131">When targeting .NET Core, the ASP.NET Core metapackage is added to the project, called `Microsoft.AspNetCore.All` by default.</span></span> <span data-ttu-id="af2a1-132">此程序包包含如`Microsoft.AspNetCore.Mvc`和`Microsoft.AspNetCore.StaticFiles`。</span><span class="sxs-lookup"><span data-stu-id="af2a1-132">This package contains packages like `Microsoft.AspNetCore.Mvc` and `Microsoft.AspNetCore.StaticFiles`.</span></span> <span data-ttu-id="af2a1-133">如果面向.NET Framework，包将引用需要 \*.csproj 文件中单独列出。</span><span class="sxs-lookup"><span data-stu-id="af2a1-133">If targeting .NET Framework, package references need to be listed individually in the \*.csproj file.</span></span>

<span data-ttu-id="af2a1-134">`Microsoft.AspNetCore.Mvc` 是 ASP.NET 核心 MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="af2a1-134">`Microsoft.AspNetCore.Mvc` is the ASP.NET Core MVC framework.</span></span> <span data-ttu-id="af2a1-135">`Microsoft.AspNetCore.StaticFiles` 是静态文件处理程序。</span><span class="sxs-lookup"><span data-stu-id="af2a1-135">`Microsoft.AspNetCore.StaticFiles` is the static file handler.</span></span> <span data-ttu-id="af2a1-136">ASP.NET 核心运行时是一个模块化，和中，你必须显式选择要为静态文件服务 (请参阅[静态文件](xref:fundamentals/static-files))。</span><span class="sxs-lookup"><span data-stu-id="af2a1-136">The ASP.NET Core runtime is modular, and you must explicitly opt in to serve static files (see [Static files](xref:fundamentals/static-files)).</span></span>

* <span data-ttu-id="af2a1-137">打开*Startup.cs*文件并将更改代码以匹配以下内容：</span><span class="sxs-lookup"><span data-stu-id="af2a1-137">Open the *Startup.cs* file and change the code to match the following:</span></span>

  [!code-csharp[](mvc/sample/Startup.cs?highlight=13,26-31)]

<span data-ttu-id="af2a1-138">`UseStaticFiles`扩展方法将添加静态文件处理程序。</span><span class="sxs-lookup"><span data-stu-id="af2a1-138">The `UseStaticFiles` extension method adds the static file handler.</span></span> <span data-ttu-id="af2a1-139">如前所述，ASP.NET 运行时是一个模块化，和中，你必须显式选择要为静态文件服务。</span><span class="sxs-lookup"><span data-stu-id="af2a1-139">As mentioned previously, the ASP.NET runtime is modular, and you must explicitly opt in to serve static files.</span></span> <span data-ttu-id="af2a1-140">`UseMvc`扩展方法将添加路由。</span><span class="sxs-lookup"><span data-stu-id="af2a1-140">The `UseMvc` extension method adds routing.</span></span> <span data-ttu-id="af2a1-141">有关详细信息，请参阅[应用程序启动](xref:fundamentals/startup)和[路由](xref:fundamentals/routing)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-141">For more information, see [Application Startup](xref:fundamentals/startup) and [Routing](xref:fundamentals/routing).</span></span>

## <a name="add-a-controller-and-view"></a><span data-ttu-id="af2a1-142">添加控制器和视图</span><span class="sxs-lookup"><span data-stu-id="af2a1-142">Add a controller and view</span></span>

<span data-ttu-id="af2a1-143">在本部分中，你将添加一个最小控制器和视图，以用作占位符的 ASP.NET MVC 控制器和视图将在下一部分中迁移。</span><span class="sxs-lookup"><span data-stu-id="af2a1-143">In this section, you'll add a minimal controller and view to serve as placeholders for the ASP.NET MVC controller and views you'll migrate in the next section.</span></span>

* <span data-ttu-id="af2a1-144">添加*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-144">Add a *Controllers* folder.</span></span>

* <span data-ttu-id="af2a1-145">添加**控制器类**名为*HomeController.cs*到*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-145">Add a **Controller Class** named *HomeController.cs* to the *Controllers* folder.</span></span>

![“添加新项”对话框](mvc/_static/add_mvc_ctl.png)

* <span data-ttu-id="af2a1-147">添加*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-147">Add a *Views* folder.</span></span>

* <span data-ttu-id="af2a1-148">添加*视图/主页*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-148">Add a *Views/Home* folder.</span></span>

* <span data-ttu-id="af2a1-149">添加**Razor 视图**名为*Index.cshtml*到*视图/主页*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-149">Add a **Razor View** named *Index.cshtml* to the *Views/Home* folder.</span></span>

![“添加新项”对话框](mvc/_static/view.png)

<span data-ttu-id="af2a1-151">项目结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="af2a1-151">The project structure is shown below:</span></span>

![显示文件和文件夹的 WebApp1 的解决方案资源管理器](mvc/_static/project-structure-controller-view.png)

<span data-ttu-id="af2a1-153">内容替换*Views/Home/Index.cshtml*替换为以下文件：</span><span class="sxs-lookup"><span data-stu-id="af2a1-153">Replace the contents of the *Views/Home/Index.cshtml* file with the following:</span></span>

```html
<h1>Hello world!</h1>
```

<span data-ttu-id="af2a1-154">运行应用。</span><span class="sxs-lookup"><span data-stu-id="af2a1-154">Run the app.</span></span>

![Web 应用在 Microsoft Edge 中打开](mvc/_static/hello-world.png)

<span data-ttu-id="af2a1-156">请参阅[控制器](xref:mvc/controllers/actions)和[视图](xref:mvc/views/overview)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="af2a1-156">See [Controllers](xref:mvc/controllers/actions) and [Views](xref:mvc/views/overview) for more information.</span></span>

<span data-ttu-id="af2a1-157">现在，我们已最小的工作 ASP.NET Core 项目，我们可以开始从 ASP.NET MVC 项目迁移功能。</span><span class="sxs-lookup"><span data-stu-id="af2a1-157">Now that we have a minimal working ASP.NET Core project, we can start migrating functionality from the ASP.NET MVC project.</span></span> <span data-ttu-id="af2a1-158">我们需要将以下：</span><span class="sxs-lookup"><span data-stu-id="af2a1-158">We need to move the following:</span></span>

* <span data-ttu-id="af2a1-159">客户端内容 （CSS、 字体和脚本）</span><span class="sxs-lookup"><span data-stu-id="af2a1-159">client-side content (CSS, fonts, and scripts)</span></span>

* <span data-ttu-id="af2a1-160">控制器</span><span class="sxs-lookup"><span data-stu-id="af2a1-160">controllers</span></span>

* <span data-ttu-id="af2a1-161">视图</span><span class="sxs-lookup"><span data-stu-id="af2a1-161">views</span></span>

* <span data-ttu-id="af2a1-162">模型</span><span class="sxs-lookup"><span data-stu-id="af2a1-162">models</span></span>

* <span data-ttu-id="af2a1-163">绑定</span><span class="sxs-lookup"><span data-stu-id="af2a1-163">bundling</span></span>

* <span data-ttu-id="af2a1-164">筛选器</span><span class="sxs-lookup"><span data-stu-id="af2a1-164">filters</span></span>

* <span data-ttu-id="af2a1-165">输入/输出的日志，标识 （这是在下一步的教程。）</span><span class="sxs-lookup"><span data-stu-id="af2a1-165">Log in/out, Identity (This is done in the next tutorial.)</span></span>

## <a name="controllers-and-views"></a><span data-ttu-id="af2a1-166">控制器和视图</span><span class="sxs-lookup"><span data-stu-id="af2a1-166">Controllers and views</span></span>

* <span data-ttu-id="af2a1-167">将每个方法复制利用 ASP.NET MVC`HomeController`对新`HomeController`。</span><span class="sxs-lookup"><span data-stu-id="af2a1-167">Copy each of the methods from the ASP.NET MVC `HomeController` to the new `HomeController`.</span></span> <span data-ttu-id="af2a1-168">请注意，在 ASP.NET MVC 内置模板的控制器操作方法的返回类型[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult(v=vs.118).aspx); 在 ASP.NET 核心 MVC，操作方法返回`IActionResult`相反。</span><span class="sxs-lookup"><span data-stu-id="af2a1-168">Note that in ASP.NET MVC, the built-in template's controller action method return type is [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult(v=vs.118).aspx); in ASP.NET Core MVC, the action methods return `IActionResult` instead.</span></span> <span data-ttu-id="af2a1-169">`ActionResult` 实现`IActionResult`，因此无需更改你的操作方法的返回类型。</span><span class="sxs-lookup"><span data-stu-id="af2a1-169">`ActionResult` implements `IActionResult`, so there's no need to change the return type of your action methods.</span></span>

* <span data-ttu-id="af2a1-170">复制*About.cshtml*， *Contact.cshtml*，和*Index.cshtml* Razor 视图文件从 ASP.NET MVC 项目添加到 ASP.NET 核心项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-170">Copy the *About.cshtml*, *Contact.cshtml*, and *Index.cshtml* Razor view files from the ASP.NET MVC project to the ASP.NET Core project.</span></span>

* <span data-ttu-id="af2a1-171">运行 ASP.NET Core 应用和测试每个方法。</span><span class="sxs-lookup"><span data-stu-id="af2a1-171">Run the ASP.NET Core app and test each method.</span></span> <span data-ttu-id="af2a1-172">我们尚未尚未进行迁移的布局文件或样式，因此呈现的视图仅包含视图文件中的内容。</span><span class="sxs-lookup"><span data-stu-id="af2a1-172">We haven't migrated the layout file or styles yet, so the rendered views only contain the content in the view files.</span></span> <span data-ttu-id="af2a1-173">不会有的布局生成文件链接`About`和`Contact`视图，因此你将需要从浏览器中调用它们 (替换**4492**与你的项目中使用的端口号)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-173">You won't have the layout file generated links for the `About` and `Contact` views, so you'll have to invoke them from the browser (replace **4492** with the port number used in your project).</span></span>

  * `http://localhost:4492/home/about`

  * `http://localhost:4492/home/contact`

![联系人页面](mvc/_static/contact-page.png)

<span data-ttu-id="af2a1-175">请注意在缺乏样式和菜单项。</span><span class="sxs-lookup"><span data-stu-id="af2a1-175">Note the lack of styling and menu items.</span></span> <span data-ttu-id="af2a1-176">此问题将在下一部分得以解决。</span><span class="sxs-lookup"><span data-stu-id="af2a1-176">We'll fix that in the next section.</span></span>

## <a name="static-content"></a><span data-ttu-id="af2a1-177">静态内容</span><span class="sxs-lookup"><span data-stu-id="af2a1-177">Static content</span></span>

<span data-ttu-id="af2a1-178">在以前版本的 ASP.NET MVC，静态内容已承载 web 项目的根目录中，已使用服务器端文件混合。</span><span class="sxs-lookup"><span data-stu-id="af2a1-178">In previous versions of ASP.NET MVC, static content was hosted from the root of the web project and was intermixed with server-side files.</span></span> <span data-ttu-id="af2a1-179">在 ASP.NET Core 静态内容承载于*wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-179">In ASP.NET Core, static content is hosted in the *wwwroot* folder.</span></span> <span data-ttu-id="af2a1-180">你将想要复制的静态内容从旧 ASP.NET MVC 应用程序到*wwwroot* ASP.NET Core 项目文件夹中的。</span><span class="sxs-lookup"><span data-stu-id="af2a1-180">You'll want to copy the static content from your old ASP.NET MVC app to the *wwwroot* folder in your ASP.NET Core project.</span></span> <span data-ttu-id="af2a1-181">在此示例转换：</span><span class="sxs-lookup"><span data-stu-id="af2a1-181">In this sample conversion:</span></span>

* <span data-ttu-id="af2a1-182">复制*favicon.ico*文件从旧的 MVC 项目到*wwwroot* ASP.NET Core 项目文件夹中的。</span><span class="sxs-lookup"><span data-stu-id="af2a1-182">Copy the *favicon.ico* file from the old MVC project to the *wwwroot* folder in the ASP.NET Core project.</span></span>

<span data-ttu-id="af2a1-183">旧 ASP.NET MVC 项目使用[Bootstrap](https://getbootstrap.com/)其 Bootstrap 文件中的样式和存储*内容*和*脚本*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-183">The old ASP.NET MVC project uses [Bootstrap](https://getbootstrap.com/) for its styling and stores the Bootstrap files in the *Content* and *Scripts* folders.</span></span> <span data-ttu-id="af2a1-184">该模板后，生成旧的 ASP.NET MVC 项目，该引用布局文件中的 Bootstrap (*Views/Shared/_Layout.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-184">The template, which generated the old ASP.NET MVC project, references Bootstrap in the layout file (*Views/Shared/_Layout.cshtml*).</span></span> <span data-ttu-id="af2a1-185">你也可以将复制*bootstrap.js*和*bootstrap.css*文件从 ASP.NET MVC 项目合并为*wwwroot*在新项目中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-185">You could copy the *bootstrap.js* and *bootstrap.css* files from the ASP.NET MVC project to the *wwwroot* folder in the new project.</span></span> <span data-ttu-id="af2a1-186">相反，我们将添加 Bootstrap 的支持 （和其他客户端库），它在下一节中使用 Cdn。</span><span class="sxs-lookup"><span data-stu-id="af2a1-186">Instead, we'll add support for Bootstrap (and other client-side libraries) using CDNs in the next section.</span></span>

## <a name="migrate-the-layout-file"></a><span data-ttu-id="af2a1-187">迁移布局文件</span><span class="sxs-lookup"><span data-stu-id="af2a1-187">Migrate the layout file</span></span>

* <span data-ttu-id="af2a1-188">复制 *_ViewStart.cshtml*文件从旧的 ASP.NET MVC 项目*视图*文件夹导入到 ASP.NET 核心项目*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-188">Copy the *_ViewStart.cshtml* file from the old ASP.NET MVC project's *Views* folder into the ASP.NET Core project's *Views* folder.</span></span> <span data-ttu-id="af2a1-189">*_ViewStart.cshtml*文件未更改 ASP.NET 核心 mvc。</span><span class="sxs-lookup"><span data-stu-id="af2a1-189">The *_ViewStart.cshtml* file has not changed in ASP.NET Core MVC.</span></span>

* <span data-ttu-id="af2a1-190">创建*视图/共享*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-190">Create a *Views/Shared* folder.</span></span>

* <span data-ttu-id="af2a1-191">*可选：* 复制 *_ViewImports.cshtml*从*FullAspNetCore* MVC 项目*视图*文件夹导入到 ASP.NET 核心项目*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-191">*Optional:* Copy *_ViewImports.cshtml* from the *FullAspNetCore* MVC project's *Views* folder into the ASP.NET Core project's *Views* folder.</span></span> <span data-ttu-id="af2a1-192">删除中的任何命名空间声明 *_ViewImports.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="af2a1-192">Remove any namespace declaration in the *_ViewImports.cshtml* file.</span></span> <span data-ttu-id="af2a1-193">*_ViewImports.cshtml*文件对于视图的所有文件提供命名空间，并使[标记帮助程序](xref:mvc/views/tag-helpers/intro)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-193">The *_ViewImports.cshtml* file provides namespaces for all the view files and brings in [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span> <span data-ttu-id="af2a1-194">新的布局文件中使用标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="af2a1-194">Tag Helpers are used in the new layout file.</span></span> <span data-ttu-id="af2a1-195">*_ViewImports.cshtml*文件是用于 ASP.NET 核心新功能。</span><span class="sxs-lookup"><span data-stu-id="af2a1-195">The *_ViewImports.cshtml* file is new for ASP.NET Core.</span></span>

* <span data-ttu-id="af2a1-196">复制 *_Layout.cshtml*文件从旧的 ASP.NET MVC 项目*视图/共享*文件夹导入到 ASP.NET 核心项目*视图/共享*文件夹。</span><span class="sxs-lookup"><span data-stu-id="af2a1-196">Copy the *_Layout.cshtml* file from the old ASP.NET MVC project's *Views/Shared* folder into the ASP.NET Core project's *Views/Shared* folder.</span></span>

<span data-ttu-id="af2a1-197">打开 *_Layout.cshtml*文件并进行以下更改 （已完成的代码下面显示）：</span><span class="sxs-lookup"><span data-stu-id="af2a1-197">Open *_Layout.cshtml* file and make the following changes (the completed code is shown below):</span></span>

* <span data-ttu-id="af2a1-198">替换`@Styles.Render("~/Content/css")`与`<link>`元素加载*bootstrap.css* （见下文）。</span><span class="sxs-lookup"><span data-stu-id="af2a1-198">Replace `@Styles.Render("~/Content/css")` with a `<link>` element to load *bootstrap.css* (see below).</span></span>

* <span data-ttu-id="af2a1-199">删除 `@Scripts.Render("~/bundles/modernizr")`。</span><span class="sxs-lookup"><span data-stu-id="af2a1-199">Remove `@Scripts.Render("~/bundles/modernizr")`.</span></span>

* <span data-ttu-id="af2a1-200">注释掉`@Html.Partial("_LoginPartial")`行 (括在一行时与`@*...*@`)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-200">Comment out the `@Html.Partial("_LoginPartial")` line (surround the line with `@*...*@`).</span></span> <span data-ttu-id="af2a1-201">在将来的教程，我们会返回到它。</span><span class="sxs-lookup"><span data-stu-id="af2a1-201">We'll return to it in a future tutorial.</span></span>

* <span data-ttu-id="af2a1-202">替换`@Scripts.Render("~/bundles/jquery")`与`<script>`元素 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="af2a1-202">Replace `@Scripts.Render("~/bundles/jquery")` with a `<script>` element (see below).</span></span>

* <span data-ttu-id="af2a1-203">替换`@Scripts.Render("~/bundles/bootstrap")`与`<script>`元素 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="af2a1-203">Replace `@Scripts.Render("~/bundles/bootstrap")` with a `<script>` element (see below).</span></span>

<span data-ttu-id="af2a1-204">Bootstrap CSS 包含替换标记：</span><span class="sxs-lookup"><span data-stu-id="af2a1-204">The replacement markup for Bootstrap CSS inclusion:</span></span>

```html
<link rel="stylesheet"
    href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
    integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u"
    crossorigin="anonymous">
```

<span data-ttu-id="af2a1-205">JQuery 和 Bootstrap JavaScript 包含的替换标记：</span><span class="sxs-lookup"><span data-stu-id="af2a1-205">The replacement markup for jQuery and Bootstrap JavaScript inclusion:</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"
    integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
```

<span data-ttu-id="af2a1-206">已更新 *_Layout.cshtml*文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="af2a1-206">The updated *_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[](mvc/sample/Views/Shared/_Layout.cshtml?highlight=7-10,29,41-44)]

<span data-ttu-id="af2a1-207">在浏览器中查看站点。</span><span class="sxs-lookup"><span data-stu-id="af2a1-207">View the site in the browser.</span></span> <span data-ttu-id="af2a1-208">它应现在正确加载，以就地预期的样式。</span><span class="sxs-lookup"><span data-stu-id="af2a1-208">It should now load correctly, with the expected styles in place.</span></span>

* <span data-ttu-id="af2a1-209">*可选：* 可能想要尝试使用新的布局文件。</span><span class="sxs-lookup"><span data-stu-id="af2a1-209">*Optional:* You might want to try using the new layout file.</span></span> <span data-ttu-id="af2a1-210">对于此项目中，你可以复制中的布局文件*FullAspNetCore*项目。</span><span class="sxs-lookup"><span data-stu-id="af2a1-210">For this project you can copy the layout file from the *FullAspNetCore* project.</span></span> <span data-ttu-id="af2a1-211">新的布局文件使用[标记帮助程序](xref:mvc/views/tag-helpers/intro)并且具有其他的改进功能。</span><span class="sxs-lookup"><span data-stu-id="af2a1-211">The new layout file uses [Tag Helpers](xref:mvc/views/tag-helpers/intro) and has other improvements.</span></span>

## <a name="configure-bundling-and-minification"></a><span data-ttu-id="af2a1-212">配置绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="af2a1-212">Configure bundling and minification</span></span>

<span data-ttu-id="af2a1-213">有关如何配置绑定和缩减的信息，请参阅[捆绑和缩减](../client-side/bundling-and-minification.md)。</span><span class="sxs-lookup"><span data-stu-id="af2a1-213">For information about how to configure bundling and minification, see [Bundling and Minification](../client-side/bundling-and-minification.md).</span></span>

## <a name="solve-http-500-errors"></a><span data-ttu-id="af2a1-214">解决 HTTP 500 错误</span><span class="sxs-lookup"><span data-stu-id="af2a1-214">Solve HTTP 500 errors</span></span>

<span data-ttu-id="af2a1-215">有许多问题的包含没有关于此问题的源的信息可能会导致 HTTP 500 错误消息。</span><span class="sxs-lookup"><span data-stu-id="af2a1-215">There are many problems that can cause a HTTP 500 error message that contain no information on the source of the problem.</span></span> <span data-ttu-id="af2a1-216">例如，如果*Views/_ViewImports.cshtml*文件包含在你的项目中不存在的命名空间，你将收到 HTTP 500 错误。</span><span class="sxs-lookup"><span data-stu-id="af2a1-216">For example, if the *Views/_ViewImports.cshtml* file contains a namespace that doesn't exist in your project, you'll get a HTTP 500 error.</span></span> <span data-ttu-id="af2a1-217">默认情况下，在 ASP.NET Core 应用中，`UseDeveloperExceptionPage`扩展添加到`IApplicationBuilder`和执行在配置后*开发*。</span><span class="sxs-lookup"><span data-stu-id="af2a1-217">By default in ASP.NET Core apps, the `UseDeveloperExceptionPage` extension is added to the `IApplicationBuilder` and executed when the configuration is *Development*.</span></span> <span data-ttu-id="af2a1-218">这将在下面的代码中详细说明：</span><span class="sxs-lookup"><span data-stu-id="af2a1-218">This is detailed in the following code:</span></span>

[!code-csharp[](mvc/sample/Startup.cs?highlight=19-22)]

<span data-ttu-id="af2a1-219">ASP.NET 核心将在 web 应用程序中未经处理的异常转换为 HTTP 500 错误响应。</span><span class="sxs-lookup"><span data-stu-id="af2a1-219">ASP.NET Core converts unhandled exceptions in a web app into HTTP 500 error responses.</span></span> <span data-ttu-id="af2a1-220">通常情况下，错误详细信息不包括在这些响应来防止有关服务器的潜在敏感信息被披露。</span><span class="sxs-lookup"><span data-stu-id="af2a1-220">Normally, error details aren't included in these responses to prevent disclosure of potentially sensitive information about the server.</span></span> <span data-ttu-id="af2a1-221">请参阅**使用开发人员异常页**中[处理错误](../fundamentals/error-handling.md)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="af2a1-221">See **Using the Developer Exception Page** in [Handle errors](../fundamentals/error-handling.md) for more information.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af2a1-222">其他资源</span><span class="sxs-lookup"><span data-stu-id="af2a1-222">Additional resources</span></span>

* [<span data-ttu-id="af2a1-223">客户端开发</span><span class="sxs-lookup"><span data-stu-id="af2a1-223">Client-side development</span></span>](xref:client-side/index)
* [<span data-ttu-id="af2a1-224">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="af2a1-224">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
