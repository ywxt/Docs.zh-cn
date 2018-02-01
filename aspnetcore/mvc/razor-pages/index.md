---
title: "ASP.NET Core 中的 Razor 页面介绍"
author: Rick-Anderson
description: "ASP.NET Core Razor 页面教程。 包含 MVC Core、ASP.NET Core 2.x、web 开发介绍和 Visual Studio 2017。 本文档提供有关使用 ASP.NET Core 中的 Razor 页面轻松开发聚焦于页的方案概述。"
manager: wpickett
ms.author: riande
ms.date: 09/12/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: mvc/razor-pages/index
ms.openlocfilehash: c16959189448337b12dc4902300516b25c200eee
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="6bb40-105">ASP.NET Core 中的 Razor 页面介绍</span><span class="sxs-lookup"><span data-stu-id="6bb40-105">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="6bb40-106">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="6bb40-106">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="6bb40-107">Razor 页面是 ASP.NET Core MVC 的一个新功能，它可以使基于页面的编码方式更简单高效。</span><span class="sxs-lookup"><span data-stu-id="6bb40-107">Razor Pages is a new feature of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="6bb40-108">若要查找使用模型视图控制器方法的教程，请参阅 [ASP.NET Core MVC 入门](xref:tutorials/first-mvc-app/start-mvc)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-108">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Getting started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="6bb40-109">本文档介绍 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-109">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="6bb40-110">它并不是分步教程。</span><span class="sxs-lookup"><span data-stu-id="6bb40-110">It's not a step by step tutorial.</span></span> <span data-ttu-id="6bb40-111">如果认为某些部分难以理解，请参阅[Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-111">If you find some of the sections difficult to follow, see [Getting started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span>

<a name="prerequisites"></a>

## <a name="aspnet-core-20-prerequisites"></a><span data-ttu-id="6bb40-112">ASP.NET Core 2.0 必备组件</span><span class="sxs-lookup"><span data-stu-id="6bb40-112">ASP.NET Core 2.0 prerequisites</span></span>

<span data-ttu-id="6bb40-113">安装 [.NET Core](https://www.microsoft.com/net/core) 2.0.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6bb40-113">Install [.NET Core](https://www.microsoft.com/net/core) 2.0.0 or later.</span></span>

<span data-ttu-id="6bb40-114">如果在使用 Visual Studio，请使用以下工作负载安装 [Visual Studio](https://www.visualstudio.com/vs/) 2017 版本 15.3 或更高版本：</span><span class="sxs-lookup"><span data-stu-id="6bb40-114">If you're using Visual Studio, install [Visual Studio](https://www.visualstudio.com/vs/) 2017 version 15.3 or later with the following workloads:</span></span>

* <span data-ttu-id="6bb40-115">**ASP.NET 和 Web 开发**</span><span class="sxs-lookup"><span data-stu-id="6bb40-115">**ASP.NET and web development**</span></span>
* <span data-ttu-id="6bb40-116">**.NET Core 跨平台开发**</span><span class="sxs-lookup"><span data-stu-id="6bb40-116">**.NET Core cross-platform development**</span></span>

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a><span data-ttu-id="6bb40-117">创建 Razor 页面项目</span><span class="sxs-lookup"><span data-stu-id="6bb40-117">Creating a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="6bb40-118">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bb40-118">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="6bb40-119">请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)，获取关于如何使用 Visual Studio 创建 Razor 页面项目的详细说明。</span><span class="sxs-lookup"><span data-stu-id="6bb40-119">See [Getting started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project using Visual Studio.</span></span>

#   <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="6bb40-120">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="6bb40-120">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="6bb40-121">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-121">Run `dotnet new razor` from the command line.</span></span>

<span data-ttu-id="6bb40-122">在 Visual Studio for Mac 中打开生成的 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="6bb40-122">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="6bb40-123">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6bb40-123">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="6bb40-124">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-124">Run `dotnet new razor` from the command line.</span></span>

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="6bb40-125">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6bb40-125">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="6bb40-126">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-126">Run `dotnet new razor` from the command line.</span></span>

---

## <a name="razor-pages"></a><span data-ttu-id="6bb40-127">Razor 页面</span><span class="sxs-lookup"><span data-stu-id="6bb40-127">Razor Pages</span></span>

<span data-ttu-id="6bb40-128">Startup.cs 中已启用 Razor 页面：</span><span class="sxs-lookup"><span data-stu-id="6bb40-128">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[main](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="6bb40-129">请考虑一个基本页面：<a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="6bb40-129">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="6bb40-130">上述代码看上去类似于一个 Razor 视图文件。</span><span class="sxs-lookup"><span data-stu-id="6bb40-130">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="6bb40-131">不同之处在于 `@page` 指令。</span><span class="sxs-lookup"><span data-stu-id="6bb40-131">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="6bb40-132">`@page` 使文件转换为一个 MVC 操作 ，这意味着它将直接处理请求，而无需通过控制器处理。</span><span class="sxs-lookup"><span data-stu-id="6bb40-132">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="6bb40-133">`@page` 必须是页面上的第一个 Razor 指令。</span><span class="sxs-lookup"><span data-stu-id="6bb40-133">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="6bb40-134">`@page` 将影响其他 Razor 构造的行为。</span><span class="sxs-lookup"><span data-stu-id="6bb40-134">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="6bb40-135">将在以下两个文件中显示使用 `PageModel` 类的类似页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-135">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="6bb40-136">Pages/Index2.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-136">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="6bb40-137">Pages/Index2.cshtml.cs 页面模型：</span><span class="sxs-lookup"><span data-stu-id="6bb40-137">The *Pages/Index2.cshtml.cs* page model:</span></span>

[!code-cs[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="6bb40-138">按照惯例，`PageModel` 类文件的名称与追加 .cs 的 Razor 页面文件名称相同。</span><span class="sxs-lookup"><span data-stu-id="6bb40-138">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="6bb40-139">例如，前面的 Razor 页面的名称为 Pages/Index2.cshtml。</span><span class="sxs-lookup"><span data-stu-id="6bb40-139">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="6bb40-140">包含 `PageModel` 类的文件的名称为 Pages/Index2.cshtml.cs。</span><span class="sxs-lookup"><span data-stu-id="6bb40-140">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="6bb40-141">页面的 URL 路径的关联由页面在文件系统中的位置决定。</span><span class="sxs-lookup"><span data-stu-id="6bb40-141">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="6bb40-142">下表显示了 Razor 页面路径及匹配的 URL：</span><span class="sxs-lookup"><span data-stu-id="6bb40-142">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="6bb40-143">文件名和路径</span><span class="sxs-lookup"><span data-stu-id="6bb40-143">File name and path</span></span>               | <span data-ttu-id="6bb40-144">匹配的 URL</span><span class="sxs-lookup"><span data-stu-id="6bb40-144">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="6bb40-145">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6bb40-145">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="6bb40-146">`/` 或 `/Index`</span><span class="sxs-lookup"><span data-stu-id="6bb40-146">`/` or `/Index`</span></span> |
| <span data-ttu-id="6bb40-147">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6bb40-147">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="6bb40-148">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6bb40-148">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="6bb40-149">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="6bb40-149">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="6bb40-150">`/Store` 或 `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="6bb40-150">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="6bb40-151">注意：</span><span class="sxs-lookup"><span data-stu-id="6bb40-151">Notes:</span></span>

* <span data-ttu-id="6bb40-152">默认情况下，运行时在“页面”文件夹中查找 Razor 页面文件。</span><span class="sxs-lookup"><span data-stu-id="6bb40-152">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="6bb40-153">URL 未包含页面时，`Index` 为默认页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-153">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="writing-a-basic-form"></a><span data-ttu-id="6bb40-154">编写基本窗体</span><span class="sxs-lookup"><span data-stu-id="6bb40-154">Writing a basic form</span></span>

<span data-ttu-id="6bb40-155">Razor 页面功能旨在简化 Web 浏览器常用的模式。</span><span class="sxs-lookup"><span data-stu-id="6bb40-155">Razor Pages features are designed to make common patterns used with web browsers easy.</span></span> <span data-ttu-id="6bb40-156">[模型绑定](xref:mvc/models/model-binding)、[标记帮助程序](xref:mvc/views/tag-helpers/intro)和 HTML 帮助程序均只可用于 Razor 页面类中定义的属性。</span><span class="sxs-lookup"><span data-stu-id="6bb40-156">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="6bb40-157">请参考为 `Contact` 模型实现基本的“联系我们”窗体的页面：</span><span class="sxs-lookup"><span data-stu-id="6bb40-157">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="6bb40-158">在本文档中的示例中，`DbContext` 在 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 文件中进行初始化。</span><span class="sxs-lookup"><span data-stu-id="6bb40-158">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="6bb40-159">数据模型：</span><span class="sxs-lookup"><span data-stu-id="6bb40-159">The data model:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="6bb40-160">数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="6bb40-160">The db context:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="6bb40-161">Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-161">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="6bb40-162">Pages/Create.cshtml.cs 页面模型：</span><span class="sxs-lookup"><span data-stu-id="6bb40-162">The *Pages/Create.cshtml.cs* page model:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="6bb40-163">按照惯例，`PageModel` 类称为 `<PageName>Model`并且它与页面位于同一个命名空间中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-163">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="6bb40-164">使用 `PageModel` 类，可以将页面的逻辑与其展示分离开来。</span><span class="sxs-lookup"><span data-stu-id="6bb40-164">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="6bb40-165">它定义了页面处理程序，用于处理发送到页面的请求和用于呈现页面的数据。</span><span class="sxs-lookup"><span data-stu-id="6bb40-165">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="6bb40-166">借助这种分离，可以通过[依赖关系注入](xref:fundamentals/dependency-injection)管理页面依赖关系，并对页面执行[单元测试](xref:testing/razor-pages-testing)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-166">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:testing/razor-pages-testing) the pages.</span></span>

<span data-ttu-id="6bb40-167">页面包含 `OnPostAsync` 处理程序方法，它在 `POST` 请求上运行（当用户发布窗体时）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-167">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="6bb40-168">可以为任何 HTTP 谓词添加处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="6bb40-168">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="6bb40-169">最常见的处理程序是：</span><span class="sxs-lookup"><span data-stu-id="6bb40-169">The most common handlers are:</span></span>

* <span data-ttu-id="6bb40-170">`OnGet`，用于初始化页面所需的状态。</span><span class="sxs-lookup"><span data-stu-id="6bb40-170">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="6bb40-171">[OnGet](#OnGet) 示例。</span><span class="sxs-lookup"><span data-stu-id="6bb40-171">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="6bb40-172">`OnPost`，用于处理窗体提交。</span><span class="sxs-lookup"><span data-stu-id="6bb40-172">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="6bb40-173">`Async` 命名后缀为可选，但是按照惯例通常会将它用于异步函数。</span><span class="sxs-lookup"><span data-stu-id="6bb40-173">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="6bb40-174">前面示例中的 `OnPostAsync` 代码看上去与通常在控制器中编写的内容相似。</span><span class="sxs-lookup"><span data-stu-id="6bb40-174">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="6bb40-175">前面的代码通常用于 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-175">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="6bb40-176">多数 MVC 基元（例如[模型绑定](xref:mvc/models/model-binding)、[验证](xref:mvc/models/validation)和操作结果）都是共享的。</span><span class="sxs-lookup"><span data-stu-id="6bb40-176">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="6bb40-177">之前的 `OnPostAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="6bb40-177">The previous `OnPostAsync` method:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="6bb40-178">`OnPostAsync` 的基本流：</span><span class="sxs-lookup"><span data-stu-id="6bb40-178">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="6bb40-179">检查验证错误。</span><span class="sxs-lookup"><span data-stu-id="6bb40-179">Check for validation errors.</span></span>

*  <span data-ttu-id="6bb40-180">如果没有错误，则保存数据并重定向。</span><span class="sxs-lookup"><span data-stu-id="6bb40-180">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="6bb40-181">如果有错误，则再次显示页面并附带验证消息。</span><span class="sxs-lookup"><span data-stu-id="6bb40-181">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="6bb40-182">客户端验证与传统的 ASP.NET Core MVC 应用程序相同。</span><span class="sxs-lookup"><span data-stu-id="6bb40-182">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="6bb40-183">很多情况下，都会在客户端上检测到验证错误，并且从不将它们提交到服务器。</span><span class="sxs-lookup"><span data-stu-id="6bb40-183">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="6bb40-184">成功输入数据后，`OnPostAsync` 处理程序方法调用 `RedirectToPage` 帮助程序方法来返回 `RedirectToPageResult` 的实例。</span><span class="sxs-lookup"><span data-stu-id="6bb40-184">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="6bb40-185">`RedirectToPage` 是新的操作结果，类似于 `RedirectToAction` 或 `RedirectToRoute`，但是已针对页面进行自定义。</span><span class="sxs-lookup"><span data-stu-id="6bb40-185">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="6bb40-186">在前面的示例中，它将重定向到根索引页 (`/Index`)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-186">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="6bb40-187">[页面 URL 生成](#url_gen)部分中详细介绍了 `RedirectToPage`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-187">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="6bb40-188">提交的窗体存在（已传递到服务器的）验证错误时，`OnPostAsync` 处理程序方法调用 `Page` 帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="6bb40-188">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="6bb40-189">`Page` 返回 `PageResult` 的实例。</span><span class="sxs-lookup"><span data-stu-id="6bb40-189">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="6bb40-190">返回 `Page` 的过程与控制器中的操作返回 `View` 的过程相似。</span><span class="sxs-lookup"><span data-stu-id="6bb40-190">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="6bb40-191">`PageResult` 是处理程序方法的默认 <!-- Review  --> 返回类型。</span><span class="sxs-lookup"><span data-stu-id="6bb40-191">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="6bb40-192">返回 `void` 的处理程序方法将显示页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-192">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="6bb40-193">`Customer` 属性使用 `[BindProperty]` 特性来选择加入模型绑定。</span><span class="sxs-lookup"><span data-stu-id="6bb40-193">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="6bb40-194">默认情况下，Razor 页面只绑定带有非 GET 谓词的属性。</span><span class="sxs-lookup"><span data-stu-id="6bb40-194">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="6bb40-195">绑定属性可以减少需要编写的代码量。</span><span class="sxs-lookup"><span data-stu-id="6bb40-195">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="6bb40-196">绑定通过使用相同的属性显示窗体字段 (`<input asp-for="Customer.Name" />`) 来减少代码，并接受输入。</span><span class="sxs-lookup"><span data-stu-id="6bb40-196">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

<span data-ttu-id="6bb40-197">主页 (Index.cshtml)：</span><span class="sxs-lookup"><span data-stu-id="6bb40-197">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="6bb40-198">Index.cshtml.cs 隐藏文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-198">The code behind *Index.cshtml.cs* file:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="6bb40-199">Index.cshtml 文件包含以下标记来创建每个联系人项的编辑链接：</span><span class="sxs-lookup"><span data-stu-id="6bb40-199">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="6bb40-200">[定位点标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) 使用 `asp-route-{value}` 属性生成“编辑”页面的链接。</span><span class="sxs-lookup"><span data-stu-id="6bb40-200">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="6bb40-201">此链接包含路由数据及联系人 ID。</span><span class="sxs-lookup"><span data-stu-id="6bb40-201">The link contains route data with the contact ID.</span></span> <span data-ttu-id="6bb40-202">例如 `http://localhost:5000/Edit/1`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-202">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="6bb40-203">Pages/Edit.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-203">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="6bb40-204">第一行包含 `@page "{id:int}"` 指令。</span><span class="sxs-lookup"><span data-stu-id="6bb40-204">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="6bb40-205">路由约束 `"{id:int}"` 告诉页面接受包含 `int` 路由数据的页面请求。</span><span class="sxs-lookup"><span data-stu-id="6bb40-205">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="6bb40-206">如果页面请求未包含可转换为 `int` 的路由数据，则运行时返回 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="6bb40-206">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span>

<span data-ttu-id="6bb40-207">Pages/Edit.cshtml.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-207">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="6bb40-208">Index.cshtml 文件还包含用于为每个客户联系人创建删除按钮的标记：</span><span class="sxs-lookup"><span data-stu-id="6bb40-208">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="6bb40-209">删除按钮采用 HTML 呈现，其 `formaction` 包括参数：</span><span class="sxs-lookup"><span data-stu-id="6bb40-209">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="6bb40-210">`asp-route-id` 属性指定的客户联系人 ID。</span><span class="sxs-lookup"><span data-stu-id="6bb40-210">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="6bb40-211">`asp-page-handler` 属性指定的 `handler`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-211">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="6bb40-212">下面是呈现的删除按钮的示例，其中客户联系人 ID 为 `1`：</span><span class="sxs-lookup"><span data-stu-id="6bb40-212">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="6bb40-213">选中按钮时，向服务器发送窗体 `POST` 请求。</span><span class="sxs-lookup"><span data-stu-id="6bb40-213">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="6bb40-214">按照惯例，根据方案 `OnPost[handler]Async` 基于 `handler` 参数的值来选择处理程序方法的名称。</span><span class="sxs-lookup"><span data-stu-id="6bb40-214">By convention, the name of the handler method is selected based the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="6bb40-215">因为本示例中 `handler` 是 `delete`，因此 `OnPostDeleteAsync` 处理程序方法用于处理 `POST` 请求。</span><span class="sxs-lookup"><span data-stu-id="6bb40-215">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="6bb40-216">如果 `asp-page-handler` 设置为不同值（如 `remove`），则选择名称为 `OnPostRemoveAsync` 的页面处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="6bb40-216">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="6bb40-217">`OnPostDeleteAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="6bb40-217">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="6bb40-218">接受来自查询字符串的 `id`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-218">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="6bb40-219">使用 `FindAsync` 查询客户联系人的数据库。</span><span class="sxs-lookup"><span data-stu-id="6bb40-219">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="6bb40-220">如果找到客户联系人，则从客户联系人列表将其删除。</span><span class="sxs-lookup"><span data-stu-id="6bb40-220">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="6bb40-221">数据库将更新。</span><span class="sxs-lookup"><span data-stu-id="6bb40-221">The database is updated.</span></span>
* <span data-ttu-id="6bb40-222">调用 `RedirectToPage`，重定向到根索引页 (`/Index`)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-222">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="6bb40-223">XSRF/CSRF 和 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="6bb40-223">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="6bb40-224">无需为[防伪验证](xref:security/anti-request-forgery)编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="6bb40-224">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="6bb40-225">Razor 页面自动将防伪标记生成过程和验证过程包含在内。</span><span class="sxs-lookup"><span data-stu-id="6bb40-225">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="6bb40-226">将布局、分区、模板和标记帮助程序用于 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="6bb40-226">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="6bb40-227">页面可使用 Razor 视图引擎的所有功能。</span><span class="sxs-lookup"><span data-stu-id="6bb40-227">Pages work with all the features of the Razor view engine.</span></span> <span data-ttu-id="6bb40-228">布局、分区、模板、标记帮助程序、_ViewStart.cshtml 和 _ViewImports.cshtml 的工作方式与它们在传统的 Razor 视图中的工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="6bb40-228">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="6bb40-229">我们来使用其中的一些功能来整理此页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-229">Let's declutter this page by taking advantage of some of those features.</span></span>

<span data-ttu-id="6bb40-230">向 Pages/_Layout.cshtml 添加[布局页面](xref:mvc/views/layout)：</span><span class="sxs-lookup"><span data-stu-id="6bb40-230">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="6bb40-231">[布局](xref:mvc/views/layout)：</span><span class="sxs-lookup"><span data-stu-id="6bb40-231">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="6bb40-232">控制每个页面的布局（页面选择退出布局时除外）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-232">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="6bb40-233">导入 HTML 结构，例如 JavaScript 和样式表。</span><span class="sxs-lookup"><span data-stu-id="6bb40-233">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="6bb40-234">请参阅[布局页面](xref:mvc/views/layout)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="6bb40-234">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="6bb40-235">在 Pages/_ViewStart.cshtml 中设置 [Layout](xref:mvc/views/layout#specifying-a-layout) 属性：</span><span class="sxs-lookup"><span data-stu-id="6bb40-235">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

<span data-ttu-id="6bb40-236">注意：布局位于“页面”文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-236">**Note:** The layout is in the *Pages* folder.</span></span> <span data-ttu-id="6bb40-237">页面按层次结构从当前页面的文件夹开始查找其他视图（布局、模板、分区）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-237">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="6bb40-238">可以从“页面”文件夹下的任意 Razor 页面使用“页面”文件夹中的布局。</span><span class="sxs-lookup"><span data-stu-id="6bb40-238">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="6bb40-239">建议不要将布局文件放在“视图/共享”文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-239">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="6bb40-240">视图/共享 是一种 MVC 视图模式。</span><span class="sxs-lookup"><span data-stu-id="6bb40-240">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="6bb40-241">Razor 页面旨在依赖文件夹层次结构，而非路径约定。</span><span class="sxs-lookup"><span data-stu-id="6bb40-241">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="6bb40-242">Razor 页面中的视图搜索包含“页面”文件夹。</span><span class="sxs-lookup"><span data-stu-id="6bb40-242">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="6bb40-243">用于 MVC 控制器和传统 Razor 视图的布局、模板和分区可直接工作。</span><span class="sxs-lookup"><span data-stu-id="6bb40-243">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="6bb40-244">添加 Pages/_ViewImports.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-244">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="6bb40-245">本教程的后续部分中将介绍 `@namespace`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-245">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="6bb40-246">`@addTagHelper` 指令将[内置标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/Index)引入“页面”文件夹中的所有页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-246">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="6bb40-247">页面上显式使用 `@namespace` 指令后：</span><span class="sxs-lookup"><span data-stu-id="6bb40-247">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="6bb40-248">此指令将为页面设置命名空间。</span><span class="sxs-lookup"><span data-stu-id="6bb40-248">The directive sets the namespace for the page.</span></span> <span data-ttu-id="6bb40-249">`@model` 指令无需包含命名空间。</span><span class="sxs-lookup"><span data-stu-id="6bb40-249">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="6bb40-250">_ViewImports.cshtml 中包含 `@namespace` 指令后，指定的命名空间将为在导入 `@namespace` 指令的页面中生成的命名空间提供前缀。</span><span class="sxs-lookup"><span data-stu-id="6bb40-250">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="6bb40-251">生成的命名空间的剩余部分（后缀部分）是包含 _ViewImports.cshtml 的文件夹与包含页面的文件夹之间以点分隔的相对路径。</span><span class="sxs-lookup"><span data-stu-id="6bb40-251">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="6bb40-252">例如，代码隐藏文件 Pages/Customers/Edit.cshtml.cs 显式设置命名空间：</span><span class="sxs-lookup"><span data-stu-id="6bb40-252">For example, the code behind file *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="6bb40-253">Pages/_ViewImports.cshtml 文件设置以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="6bb40-253">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="6bb40-254">为 Pages/Customers/Edit.cshtml Razor 页面生成的命名空间与代码隐藏文件相同.</span><span class="sxs-lookup"><span data-stu-id="6bb40-254">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the code behind file.</span></span> <span data-ttu-id="6bb40-255">已对 `@namespace` 指令进行设计，因此添加到项目的 C# 类和页面生成的代码可直接工作，而无需添加代码隐藏文件的 `@using` 指令。</span><span class="sxs-lookup"><span data-stu-id="6bb40-255">The `@namespace` directive was designed so the C# classes added to a project and pages-generated code *just work* without having to add an `@using` directive for the code behind file.</span></span>

<span data-ttu-id="6bb40-256">注意：`@namespace` 也可用于传统的 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="6bb40-256">**Note:** `@namespace` also works with conventional Razor views.</span></span>

<span data-ttu-id="6bb40-257">原始的 Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-257">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="6bb40-258">更新后的 Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="6bb40-258">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="6bb40-259">[Razor 页面初学者项目](#rpvs17)包含 Pages/_ValidationScriptsPartial.cshtml，它与客户端验证联合。</span><span class="sxs-lookup"><span data-stu-id="6bb40-259">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="6bb40-260">页面的 URL 生成</span><span class="sxs-lookup"><span data-stu-id="6bb40-260">URL generation for Pages</span></span>

<span data-ttu-id="6bb40-261">之前显示的 `Create` 页面使用 `RedirectToPage`：</span><span class="sxs-lookup"><span data-stu-id="6bb40-261">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="6bb40-262">应用具有以下文件/文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="6bb40-262">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="6bb40-263">/Pages</span><span class="sxs-lookup"><span data-stu-id="6bb40-263">*/Pages*</span></span>

  * <span data-ttu-id="6bb40-264">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="6bb40-264">*Index.cshtml*</span></span>
  * <span data-ttu-id="6bb40-265">/Customer</span><span class="sxs-lookup"><span data-stu-id="6bb40-265">*/Customer*</span></span>

    * <span data-ttu-id="6bb40-266">Create.cshtml</span><span class="sxs-lookup"><span data-stu-id="6bb40-266">*Create.cshtml*</span></span>
    * <span data-ttu-id="6bb40-267">Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="6bb40-267">*Edit.cshtml*</span></span>
    * <span data-ttu-id="6bb40-268">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="6bb40-268">*Index.cshtml*</span></span>

<span data-ttu-id="6bb40-269">成功后，Pages/Customers/Create.cshtml 和 Pages/Customers/Edit.cshtml 页面将重定向到 Pages/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="6bb40-269">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="6bb40-270">字符串 `/Index` 是用于访问上一页的 URI 的组成部分。</span><span class="sxs-lookup"><span data-stu-id="6bb40-270">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="6bb40-271">可以使用字符串 `/Index` 生成 Pages/Index.cshtml 页面的 URI。</span><span class="sxs-lookup"><span data-stu-id="6bb40-271">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="6bb40-272">例如:</span><span class="sxs-lookup"><span data-stu-id="6bb40-272">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="6bb40-273">页面名称是从根“/Pages”文件夹到页面的路径（包含前导 `/`，例如 `/Index`）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-273">The page name is the path to the page from the root */Pages* folder (including a leading `/`, for example `/Index`).</span></span> <span data-ttu-id="6bb40-274">相较于仅对 URL 硬编码，前面的 URL 生成示例的功能更加强大。</span><span class="sxs-lookup"><span data-stu-id="6bb40-274">The preceding URL generation samples are much more feature rich than just hardcoding a URL.</span></span> <span data-ttu-id="6bb40-275">URL 生成使用[路由](xref:mvc/controllers/routing)，并且可以根据目标路径定义路由的方式生成参数并对参数编码。</span><span class="sxs-lookup"><span data-stu-id="6bb40-275">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="6bb40-276">页面的 URL 生成支持相对名称。</span><span class="sxs-lookup"><span data-stu-id="6bb40-276">URL generation for pages supports relative names.</span></span> <span data-ttu-id="6bb40-277">下表显示了 Pages/Customers/Create.cshtml 中不同的 `RedirectToPage` 参数选择的索引页：</span><span class="sxs-lookup"><span data-stu-id="6bb40-277">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="6bb40-278">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="6bb40-278">RedirectToPage(x)</span></span>| <span data-ttu-id="6bb40-279">页</span><span class="sxs-lookup"><span data-stu-id="6bb40-279">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="6bb40-280">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="6bb40-280">RedirectToPage("/Index")</span></span> | <span data-ttu-id="6bb40-281">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="6bb40-281">*Pages/Index*</span></span> |
| <span data-ttu-id="6bb40-282">RedirectToPage("./Index");</span><span class="sxs-lookup"><span data-stu-id="6bb40-282">RedirectToPage("./Index");</span></span> | <span data-ttu-id="6bb40-283">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="6bb40-283">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="6bb40-284">RedirectToPage("../Index")</span><span class="sxs-lookup"><span data-stu-id="6bb40-284">RedirectToPage("../Index")</span></span> | <span data-ttu-id="6bb40-285">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="6bb40-285">*Pages/Index*</span></span> |
| <span data-ttu-id="6bb40-286">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="6bb40-286">RedirectToPage("Index")</span></span>  | <span data-ttu-id="6bb40-287">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="6bb40-287">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="6bb40-288">`RedirectToPage("Index")`、`RedirectToPage("./Index")` 和 `RedirectToPage("../Index")` 是相对名称。</span><span class="sxs-lookup"><span data-stu-id="6bb40-288">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are *relative names*.</span></span> <span data-ttu-id="6bb40-289">结合 `RedirectToPage` 参数与当前页的路径来计算目标页面的名称。</span><span class="sxs-lookup"><span data-stu-id="6bb40-289">The `RedirectToPage` parameter is *combined* with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page. -- page name, not page path -->

<span data-ttu-id="6bb40-290">构建结构复杂的站点时，相对名称链接很有用。</span><span class="sxs-lookup"><span data-stu-id="6bb40-290">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="6bb40-291">如果使用相对名称链接文件夹中的页面，则可以重命名该文件夹。</span><span class="sxs-lookup"><span data-stu-id="6bb40-291">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="6bb40-292">所有链接仍然有效（因为这些链接未包含此文件夹名称）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-292">All the links still work (because they didn't include the folder name).</span></span>

## <a name="tempdata"></a><span data-ttu-id="6bb40-293">TempData</span><span class="sxs-lookup"><span data-stu-id="6bb40-293">TempData</span></span>

<span data-ttu-id="6bb40-294">ASP.NET 在[控制器](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller)上公开了 [TempData](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 属性。</span><span class="sxs-lookup"><span data-stu-id="6bb40-294">ASP.NET Core exposes the [TempData](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="6bb40-295">此属性存储未读取的数据。</span><span class="sxs-lookup"><span data-stu-id="6bb40-295">This property stores data until it's read.</span></span> <span data-ttu-id="6bb40-296">`Keep` 和 `Peek` 方法可用于检查数据，而不执行删除。</span><span class="sxs-lookup"><span data-stu-id="6bb40-296">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="6bb40-297">多个请求需要数据时，`TempData` 有助于进行重定向。</span><span class="sxs-lookup"><span data-stu-id="6bb40-297">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="6bb40-298">`[TempData]` 是 ASP.NET Core 2.0 中的新属性，在控制器和页面上受支持。</span><span class="sxs-lookup"><span data-stu-id="6bb40-298">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="6bb40-299">下面的代码使用 `TempData` 设置 `Message` 的值：</span><span class="sxs-lookup"><span data-stu-id="6bb40-299">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="6bb40-300">Pages/Customers/Index.cshtml 文件中的以下标记使用 `TempData` 显示 `Message` 的值。</span><span class="sxs-lookup"><span data-stu-id="6bb40-300">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="6bb40-301">Pages/Customers/Index.cshtml.cs 页面模型将 `[TempData]` 属性应用到 `Message` 属性。</span><span class="sxs-lookup"><span data-stu-id="6bb40-301">The *Pages/Customers/Index.cshtml.cs* page model applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="6bb40-302">请参阅 [TempData](xref:fundamentals/app-state#temp) 了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="6bb40-302">See [TempData](xref:fundamentals/app-state#temp) for more information.</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="6bb40-303">针对一个页面的多个处理程序</span><span class="sxs-lookup"><span data-stu-id="6bb40-303">Multiple handlers per page</span></span>

<span data-ttu-id="6bb40-304">以下页面使用 `asp-page-handler` 标记帮助程序为两个页面处理程序生成标记：</span><span class="sxs-lookup"><span data-stu-id="6bb40-304">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

<span data-ttu-id="6bb40-305">前面示例中的窗体包含两个提交按钮，每个提交按钮均使用 `FormActionTagHelper` 提交到不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="6bb40-305">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="6bb40-306">`asp-page-handler` 是 `asp-page` 的配套属性。</span><span class="sxs-lookup"><span data-stu-id="6bb40-306">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="6bb40-307">`asp-page-handler` 生成提交到页面定义的各个处理程序方法的 URL。</span><span class="sxs-lookup"><span data-stu-id="6bb40-307">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="6bb40-308">未指定 `asp-page`，因为示例已链接到当前页面。</span><span class="sxs-lookup"><span data-stu-id="6bb40-308">`asp-page` isn't specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="6bb40-309">页面模型：</span><span class="sxs-lookup"><span data-stu-id="6bb40-309">The page model:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="6bb40-310">前面的代码使用已命名处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="6bb40-310">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="6bb40-311">已命名处理程序方法通过采用名称中 `On<HTTP Verb>` 之后及 `Async` 之前的文本（如果有）创建。</span><span class="sxs-lookup"><span data-stu-id="6bb40-311">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="6bb40-312">在前面的示例中，页面方法是 OnPost**JoinList**Async 和 OnPost**JoinListUC**Async。</span><span class="sxs-lookup"><span data-stu-id="6bb40-312">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="6bb40-313">删除 OnPost 和 Async 后，处理程序名称为 `JoinList` 和 `JoinListUC`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-313">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="6bb40-314">使用前面的代码时，提交到 `OnPostJoinListAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-314">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="6bb40-315">提交到 `OnPostJoinListUCAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`。</span><span class="sxs-lookup"><span data-stu-id="6bb40-315">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>

## <a name="customizing-routing"></a><span data-ttu-id="6bb40-316">自定义路由</span><span class="sxs-lookup"><span data-stu-id="6bb40-316">Customizing Routing</span></span>

<span data-ttu-id="6bb40-317">如果你不喜欢 URL 中的查询字符串 `?handler=JoinList`，可以更改路由，将处理程序名称放在 URL 的路径部分。</span><span class="sxs-lookup"><span data-stu-id="6bb40-317">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="6bb40-318">可以通过在 `@page` 指令后面添加使用双引号括起来的路由模板来自定义路由。</span><span class="sxs-lookup"><span data-stu-id="6bb40-318">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="6bb40-319">前面的路由将处理程序放在了 URL 路径中，而不是查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-319">The preceding route puts the handler name in the URL path instead of the query string.</span></span> <span data-ttu-id="6bb40-320">`handler` 前面的 `?` 表示路由参数为可选。</span><span class="sxs-lookup"><span data-stu-id="6bb40-320">The `?` following `handler` means the route parameter is optional.</span></span>

<span data-ttu-id="6bb40-321">可以使用 `@page` 将其他段和参数添加到页面的路由中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-321">You can use `@page` to add additional segments and parameters to a page's route.</span></span> <span data-ttu-id="6bb40-322">其中的任何内容均会被追加到页面的默认路由中。</span><span class="sxs-lookup"><span data-stu-id="6bb40-322">Whatever's there's **appended** to the default route of the page.</span></span> <span data-ttu-id="6bb40-323">不支持使用绝对路径或虚拟路径更改页面的路由（如 `"~/Some/Other/Path"`）。</span><span class="sxs-lookup"><span data-stu-id="6bb40-323">Using an absolute or virtual path to change the page's route (like `"~/Some/Other/Path"`) isn't supported.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="6bb40-324">配置和设置</span><span class="sxs-lookup"><span data-stu-id="6bb40-324">Configuration and settings</span></span>

<span data-ttu-id="6bb40-325">若要配置高级选项，请在 MVC 生成器上使用 `AddRazorPagesOptions` 扩展方法：</span><span class="sxs-lookup"><span data-stu-id="6bb40-325">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[main](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="6bb40-326">目前，可以使用 `RazorPagesOptions` 设置页面的根目录，或者为页面添加应用程序模型约定。</span><span class="sxs-lookup"><span data-stu-id="6bb40-326">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="6bb40-327">通过这种方式，我们在将来会实现更多扩展功能。</span><span class="sxs-lookup"><span data-stu-id="6bb40-327">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="6bb40-328">若要预编译视图，请参阅 [Razor 视图编译](xref:mvc/views/view-compilation)。</span><span class="sxs-lookup"><span data-stu-id="6bb40-328">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="6bb40-329">[下载或查看示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="6bb40-329">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span></span>

<span data-ttu-id="6bb40-330">请参阅 [ASP.NET Core 中的 Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)，这篇文章以本文为基础编写。</span><span class="sxs-lookup"><span data-stu-id="6bb40-330">See [Getting started with Razor Pages in ASP.NET Core](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="6bb40-331">指定 Razor 页面位于内容根目录中</span><span class="sxs-lookup"><span data-stu-id="6bb40-331">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="6bb40-332">默认情况下，Razor 页面位于 /Pages 目录的根位置。</span><span class="sxs-lookup"><span data-stu-id="6bb40-332">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="6bb40-333">向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot)，以指定 Razor 页面位于应用的内容根目录 ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) 中：</span><span class="sxs-lookup"><span data-stu-id="6bb40-333">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="6bb40-334">指定 Razor 页面位于自定义根目录中</span><span class="sxs-lookup"><span data-stu-id="6bb40-334">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="6bb40-335">向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot)，以指定 Razor 页面位于应用中自定义根目录位置（提供相对路径）：</span><span class="sxs-lookup"><span data-stu-id="6bb40-335">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="see-also"></a><span data-ttu-id="6bb40-336">请参阅</span><span class="sxs-lookup"><span data-stu-id="6bb40-336">See also</span></span>

* [<span data-ttu-id="6bb40-337">Razor 页面入门</span><span class="sxs-lookup"><span data-stu-id="6bb40-337">Getting started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="6bb40-338">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="6bb40-338">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
* [<span data-ttu-id="6bb40-339">Razor 页面自定义路由和页面模型提供程序</span><span class="sxs-lookup"><span data-stu-id="6bb40-339">Razor Pages custom route and page model providers</span></span>](xref:mvc/razor-pages/razor-pages-convention-features)
* [<span data-ttu-id="6bb40-340">Razor 页面单位与集成测试</span><span class="sxs-lookup"><span data-stu-id="6bb40-340">Razor Pages unit and integration testing</span></span>](xref:testing/razor-pages-testing)
