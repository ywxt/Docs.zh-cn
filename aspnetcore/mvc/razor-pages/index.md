---
title: ASP.NET Core 中的 Razor 页面介绍
author: Rick-Anderson
description: 了解 ASP.NET Core 中的 Razor 页面如何使基于页面的编码方式比使用 MVC 更简单高效。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 5/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: mvc/razor-pages/index
ms.openlocfilehash: 651d47ce20f3269340f0796f487e2f1a2a155710
ms.sourcegitcommit: 0063338c2e130409081bb60fcffa0c3f190cd46a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a><span data-ttu-id="a909e-103">ASP.NET Core 中的 Razor 页面介绍</span><span class="sxs-lookup"><span data-stu-id="a909e-103">Introduction to Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="a909e-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Ryan Nowak](https://github.com/rynowak)</span><span class="sxs-lookup"><span data-stu-id="a909e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Ryan Nowak](https://github.com/rynowak)</span></span>

<span data-ttu-id="a909e-105">Razor 页面是 ASP.NET Core MVC 的一个新特性，它可以使基于页面的编码方式更简单高效。</span><span class="sxs-lookup"><span data-stu-id="a909e-105">Razor Pages is a new aspect of ASP.NET Core MVC that makes coding page-focused scenarios easier and more productive.</span></span>

<span data-ttu-id="a909e-106">若要查找使用模型视图控制器方法的教程，请参阅 [ASP.NET Core MVC 入门](xref:tutorials/first-mvc-app/start-mvc)。</span><span class="sxs-lookup"><span data-stu-id="a909e-106">If you're looking for a tutorial that uses the Model-View-Controller approach, see [Get started with ASP.NET Core MVC](xref:tutorials/first-mvc-app/start-mvc).</span></span>

<span data-ttu-id="a909e-107">本文档介绍 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-107">This document provides an introduction to Razor Pages.</span></span> <span data-ttu-id="a909e-108">它并不是分步教程。</span><span class="sxs-lookup"><span data-stu-id="a909e-108">It's not a step by step tutorial.</span></span> <span data-ttu-id="a909e-109">如果认为某些部分过于复杂，请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="a909e-109">If you find some of the sections too advanced, see [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="a909e-110">有关 ASP.NET Core 的概述，请参阅 [ASP.NET Core 简介](xref:index)。</span><span class="sxs-lookup"><span data-stu-id="a909e-110">For an overview of ASP.NET Core, see the [Introduction to ASP.NET Core](xref:index).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a909e-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="a909e-111">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a><span data-ttu-id="a909e-112">创建 Razor 页面项目</span><span class="sxs-lookup"><span data-stu-id="a909e-112">Creating a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a909e-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a909e-113">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="a909e-114">请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)，获取关于如何使用 Visual Studio 创建 Razor 页面项目的详细说明。</span><span class="sxs-lookup"><span data-stu-id="a909e-114">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start) for detailed instructions on how to create a Razor Pages project using Visual Studio.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a909e-115">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="a909e-115">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="a909e-116">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="a909e-116">Run `dotnet new razor` from the command line.</span></span>

<span data-ttu-id="a909e-117">在 Visual Studio for Mac 中打开生成的 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="a909e-117">Open the generated *.csproj* file from Visual Studio for Mac.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a909e-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a909e-118">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="a909e-119">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="a909e-119">Run `dotnet new razor` from the command line.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="a909e-120">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a909e-120">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="a909e-121">在命令行中运行 `dotnet new razor`。</span><span class="sxs-lookup"><span data-stu-id="a909e-121">Run `dotnet new razor` from the command line.</span></span>

---

## <a name="razor-pages"></a><span data-ttu-id="a909e-122">Razor 页面</span><span class="sxs-lookup"><span data-stu-id="a909e-122">Razor Pages</span></span>

<span data-ttu-id="a909e-123">Startup.cs 中已启用 Razor 页面：</span><span class="sxs-lookup"><span data-stu-id="a909e-123">Razor Pages is enabled in *Startup.cs*:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

<span data-ttu-id="a909e-124">请考虑一个基本页面：<a name="OnGet"></a></span><span class="sxs-lookup"><span data-stu-id="a909e-124">Consider a basic page: <a name="OnGet"></a></span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

<span data-ttu-id="a909e-125">上述代码看上去类似于一个 Razor 视图文件。</span><span class="sxs-lookup"><span data-stu-id="a909e-125">The preceding code looks a lot like a Razor view file.</span></span> <span data-ttu-id="a909e-126">不同之处在于 `@page` 指令。</span><span class="sxs-lookup"><span data-stu-id="a909e-126">What makes it different is the `@page` directive.</span></span> <span data-ttu-id="a909e-127">`@page` 使文件转换为一个 MVC 操作 ，这意味着它将直接处理请求，而无需通过控制器处理。</span><span class="sxs-lookup"><span data-stu-id="a909e-127">`@page` makes the file into an MVC action - which means that it handles requests directly, without going through a controller.</span></span> <span data-ttu-id="a909e-128">`@page` 必须是页面上的第一个 Razor 指令。</span><span class="sxs-lookup"><span data-stu-id="a909e-128">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="a909e-129">`@page` 将影响其他 Razor 构造的行为。</span><span class="sxs-lookup"><span data-stu-id="a909e-129">`@page` affects the behavior of other Razor constructs.</span></span>

<span data-ttu-id="a909e-130">将在以下两个文件中显示使用 `PageModel` 类的类似页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-130">A similar page, using a `PageModel` class, is shown in the following two files.</span></span> <span data-ttu-id="a909e-131">Pages/Index2.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-131">The *Pages/Index2.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

<span data-ttu-id="a909e-132">Pages/Index2.cshtml.cs 页面模型：</span><span class="sxs-lookup"><span data-stu-id="a909e-132">The *Pages/Index2.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

<span data-ttu-id="a909e-133">按照惯例，`PageModel` 类文件的名称与追加 .cs 的 Razor 页面文件名称相同。</span><span class="sxs-lookup"><span data-stu-id="a909e-133">By convention, the `PageModel` class file has the same name as the Razor Page file with *.cs* appended.</span></span> <span data-ttu-id="a909e-134">例如，前面的 Razor 页面的名称为 Pages/Index2.cshtml。</span><span class="sxs-lookup"><span data-stu-id="a909e-134">For example, the previous Razor Page is *Pages/Index2.cshtml*.</span></span> <span data-ttu-id="a909e-135">包含 `PageModel` 类的文件的名称为 Pages/Index2.cshtml.cs。</span><span class="sxs-lookup"><span data-stu-id="a909e-135">The file containing the `PageModel` class is named *Pages/Index2.cshtml.cs*.</span></span>

<span data-ttu-id="a909e-136">页面的 URL 路径的关联由页面在文件系统中的位置决定。</span><span class="sxs-lookup"><span data-stu-id="a909e-136">The associations of URL paths to pages are determined by the page's location in the file system.</span></span> <span data-ttu-id="a909e-137">下表显示了 Razor 页面路径及匹配的 URL：</span><span class="sxs-lookup"><span data-stu-id="a909e-137">The following table shows a Razor Page path and the matching URL:</span></span>

| <span data-ttu-id="a909e-138">文件名和路径</span><span class="sxs-lookup"><span data-stu-id="a909e-138">File name and path</span></span>               | <span data-ttu-id="a909e-139">匹配的 URL</span><span class="sxs-lookup"><span data-stu-id="a909e-139">matching URL</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="a909e-140">*/Pages/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="a909e-140">*/Pages/Index.cshtml*</span></span> | <span data-ttu-id="a909e-141">`/` 或 `/Index`</span><span class="sxs-lookup"><span data-stu-id="a909e-141">`/` or `/Index`</span></span> |
| <span data-ttu-id="a909e-142">*/Pages/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="a909e-142">*/Pages/Contact.cshtml*</span></span> | `/Contact` |
| <span data-ttu-id="a909e-143">*/Pages/Store/Contact.cshtml*</span><span class="sxs-lookup"><span data-stu-id="a909e-143">*/Pages/Store/Contact.cshtml*</span></span> | `/Store/Contact` |
| <span data-ttu-id="a909e-144">*/Pages/Store/Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="a909e-144">*/Pages/Store/Index.cshtml*</span></span> | <span data-ttu-id="a909e-145">`/Store` 或 `/Store/Index`</span><span class="sxs-lookup"><span data-stu-id="a909e-145">`/Store` or `/Store/Index`</span></span> |

<span data-ttu-id="a909e-146">注意：</span><span class="sxs-lookup"><span data-stu-id="a909e-146">Notes:</span></span>

* <span data-ttu-id="a909e-147">默认情况下，运行时在“Pages”文件夹中查找 Razor 页面文件。</span><span class="sxs-lookup"><span data-stu-id="a909e-147">The runtime looks for Razor Pages files in the *Pages* folder by default.</span></span>
* <span data-ttu-id="a909e-148">URL 未包含页面时，`Index` 为默认页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-148">`Index` is the default page when a URL doesn't include a page.</span></span>

## <a name="writing-a-basic-form"></a><span data-ttu-id="a909e-149">编写基本窗体</span><span class="sxs-lookup"><span data-stu-id="a909e-149">Writing a basic form</span></span>

<span data-ttu-id="a909e-150">由于 Razor 页面的设计，在构建应用时可轻松实施用于 Web 浏览器的常用模式。</span><span class="sxs-lookup"><span data-stu-id="a909e-150">Razor Pages is designed to make common patterns used with web browsers easy to implement when building an app.</span></span> <span data-ttu-id="a909e-151">[模型绑定](xref:mvc/models/model-binding)、[标记帮助程序](xref:mvc/views/tag-helpers/intro)和 HTML 帮助程序均只可用于 Razor 页面类中定义的属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-151">[Model binding](xref:mvc/models/model-binding), [Tag Helpers](xref:mvc/views/tag-helpers/intro), and HTML helpers all *just work* with the properties defined in a Razor Page class.</span></span> <span data-ttu-id="a909e-152">请参考为 `Contact` 模型实现基本的“联系我们”窗体的页面：</span><span class="sxs-lookup"><span data-stu-id="a909e-152">Consider a page that implements a basic "contact us" form for the `Contact` model:</span></span>

<span data-ttu-id="a909e-153">在本文档中的示例中，`DbContext` 在 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 文件中进行初始化。</span><span class="sxs-lookup"><span data-stu-id="a909e-153">For the samples in this document, the `DbContext` is initialized in the [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) file.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

<span data-ttu-id="a909e-154">数据模型：</span><span class="sxs-lookup"><span data-stu-id="a909e-154">The data model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

<span data-ttu-id="a909e-155">数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="a909e-155">The db context:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

<span data-ttu-id="a909e-156">Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-156">The *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

<span data-ttu-id="a909e-157">Pages/Create.cshtml.cs 页面模型：</span><span class="sxs-lookup"><span data-stu-id="a909e-157">The *Pages/Create.cshtml.cs* page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

<span data-ttu-id="a909e-158">按照惯例，`PageModel` 类命名为 `<PageName>Model`并且它与页面位于同一个命名空间中。</span><span class="sxs-lookup"><span data-stu-id="a909e-158">By convention, the `PageModel` class is called `<PageName>Model` and is in the same namespace as the page.</span></span>

<span data-ttu-id="a909e-159">使用 `PageModel` 类，可以将页面的逻辑与其展示分离开来。</span><span class="sxs-lookup"><span data-stu-id="a909e-159">The `PageModel` class allows separation of the logic of a page from its presentation.</span></span> <span data-ttu-id="a909e-160">它定义了页面处理程序，用于处理发送到页面的请求和用于呈现页面的数据。</span><span class="sxs-lookup"><span data-stu-id="a909e-160">It defines page handlers for requests sent to the page and the data used to render the page.</span></span> <span data-ttu-id="a909e-161">借助这种分离，可以通过[依赖关系注入](xref:fundamentals/dependency-injection)管理页面依赖关系，并对页面执行[单元测试](xref:testing/razor-pages-testing)。</span><span class="sxs-lookup"><span data-stu-id="a909e-161">This separation allows you to manage page dependencies through [dependency injection](xref:fundamentals/dependency-injection) and to [unit test](xref:testing/razor-pages-testing) the pages.</span></span>

<span data-ttu-id="a909e-162">页面包含 `OnPostAsync` 处理程序方法，它在 `POST` 请求上运行（当用户发布窗体时）。</span><span class="sxs-lookup"><span data-stu-id="a909e-162">The page has an `OnPostAsync` *handler method*, which runs on `POST` requests (when a user posts the form).</span></span> <span data-ttu-id="a909e-163">可以为任何 HTTP 谓词添加处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="a909e-163">You can add handler methods for any HTTP verb.</span></span> <span data-ttu-id="a909e-164">最常见的处理程序是：</span><span class="sxs-lookup"><span data-stu-id="a909e-164">The most common handlers are:</span></span>

* <span data-ttu-id="a909e-165">`OnGet`，用于初始化页面所需的状态。</span><span class="sxs-lookup"><span data-stu-id="a909e-165">`OnGet` to initialize state needed for the page.</span></span> <span data-ttu-id="a909e-166">[OnGet](#OnGet) 示例。</span><span class="sxs-lookup"><span data-stu-id="a909e-166">[OnGet](#OnGet) sample.</span></span>
* <span data-ttu-id="a909e-167">`OnPost`，用于处理窗体提交。</span><span class="sxs-lookup"><span data-stu-id="a909e-167">`OnPost` to handle form submissions.</span></span>

<span data-ttu-id="a909e-168">`Async` 命名后缀为可选，但是按照惯例通常会将它用于异步函数。</span><span class="sxs-lookup"><span data-stu-id="a909e-168">The `Async` naming suffix is optional but is often used by convention for asynchronous functions.</span></span> <span data-ttu-id="a909e-169">前面示例中的 `OnPostAsync` 代码看上去与通常在控制器中编写的内容相似。</span><span class="sxs-lookup"><span data-stu-id="a909e-169">The `OnPostAsync` code in the preceding example looks similar to what you would normally write in a controller.</span></span> <span data-ttu-id="a909e-170">前面的代码通常用于 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-170">The preceding code is typical for Razor Pages.</span></span> <span data-ttu-id="a909e-171">多数 MVC 基元（例如[模型绑定](xref:mvc/models/model-binding)、[验证](xref:mvc/models/validation)和操作结果）都是共享的。</span><span class="sxs-lookup"><span data-stu-id="a909e-171">Most of the MVC primitives like [model binding](xref:mvc/models/model-binding), [validation](xref:mvc/models/validation), and action results are shared.</span></span>  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

<span data-ttu-id="a909e-172">之前的 `OnPostAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="a909e-172">The previous `OnPostAsync` method:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="a909e-173">`OnPostAsync` 的基本流：</span><span class="sxs-lookup"><span data-stu-id="a909e-173">The basic flow of `OnPostAsync`:</span></span>

<span data-ttu-id="a909e-174">检查验证错误。</span><span class="sxs-lookup"><span data-stu-id="a909e-174">Check for validation errors.</span></span>

*  <span data-ttu-id="a909e-175">如果没有错误，则保存数据并重定向。</span><span class="sxs-lookup"><span data-stu-id="a909e-175">If there are no errors, save the data and redirect.</span></span>
*  <span data-ttu-id="a909e-176">如果有错误，则再次显示页面并附带验证消息。</span><span class="sxs-lookup"><span data-stu-id="a909e-176">If there are errors, show the page again with validation messages.</span></span> <span data-ttu-id="a909e-177">客户端验证与传统的 ASP.NET Core MVC 应用程序相同。</span><span class="sxs-lookup"><span data-stu-id="a909e-177">Client-side validation is identical to traditional ASP.NET Core MVC applications.</span></span> <span data-ttu-id="a909e-178">很多情况下，都会在客户端上检测到验证错误，并且从不将它们提交到服务器。</span><span class="sxs-lookup"><span data-stu-id="a909e-178">In many cases, validation errors would be detected on the client, and never submitted to the server.</span></span>

<span data-ttu-id="a909e-179">成功输入数据后，`OnPostAsync` 处理程序方法调用 `RedirectToPage` 帮助程序方法来返回 `RedirectToPageResult` 的实例。</span><span class="sxs-lookup"><span data-stu-id="a909e-179">When the data is entered successfully, the `OnPostAsync` handler method calls the `RedirectToPage` helper method to return an instance of `RedirectToPageResult`.</span></span> <span data-ttu-id="a909e-180">`RedirectToPage` 是新的操作结果，类似于 `RedirectToAction` 或 `RedirectToRoute`，但是已针对页面进行自定义。</span><span class="sxs-lookup"><span data-stu-id="a909e-180">`RedirectToPage` is a new action result, similar to `RedirectToAction` or `RedirectToRoute`, but customized for pages.</span></span> <span data-ttu-id="a909e-181">在前面的示例中，它将重定向到根索引页 (`/Index`)。</span><span class="sxs-lookup"><span data-stu-id="a909e-181">In the preceding sample, it redirects to the root Index page (`/Index`).</span></span> <span data-ttu-id="a909e-182">[页面 URL 生成](#url_gen)部分中详细介绍了 `RedirectToPage`。</span><span class="sxs-lookup"><span data-stu-id="a909e-182">`RedirectToPage` is detailed in the [URL generation for Pages](#url_gen) section.</span></span>

<span data-ttu-id="a909e-183">提交的窗体存在（已传递到服务器的）验证错误时，`OnPostAsync` 处理程序方法调用 `Page` 帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="a909e-183">When the submitted form has validation errors (that are passed to the server), the`OnPostAsync` handler method calls the `Page` helper method.</span></span> <span data-ttu-id="a909e-184">`Page` 返回 `PageResult` 的实例。</span><span class="sxs-lookup"><span data-stu-id="a909e-184">`Page` returns an instance of `PageResult`.</span></span> <span data-ttu-id="a909e-185">返回 `Page` 的过程与控制器中的操作返回 `View` 的过程相似。</span><span class="sxs-lookup"><span data-stu-id="a909e-185">Returning `Page` is similar to how actions in controllers return `View`.</span></span> <span data-ttu-id="a909e-186">`PageResult` 是处理程序方法的默认 <!-- Review  --> 返回类型。</span><span class="sxs-lookup"><span data-stu-id="a909e-186">`PageResult` is the default <!-- Review  --> return type for a handler method.</span></span> <span data-ttu-id="a909e-187">返回 `void` 的处理程序方法将显示页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-187">A handler method that returns `void` renders the page.</span></span>

<span data-ttu-id="a909e-188">`Customer` 属性使用 `[BindProperty]` 特性来选择加入模型绑定。</span><span class="sxs-lookup"><span data-stu-id="a909e-188">The `Customer` property uses `[BindProperty]` attribute to opt in to model binding.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

<span data-ttu-id="a909e-189">默认情况下，Razor 页面只绑定带有非 GET 谓词的属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-189">Razor Pages, by default, bind properties only with non-GET verbs.</span></span> <span data-ttu-id="a909e-190">绑定属性可以减少需要编写的代码量。</span><span class="sxs-lookup"><span data-stu-id="a909e-190">Binding to properties can reduce the amount of code you have to write.</span></span> <span data-ttu-id="a909e-191">绑定通过使用相同的属性显示窗体字段 (`<input asp-for="Customer.Name" />`) 来减少代码，并接受输入。</span><span class="sxs-lookup"><span data-stu-id="a909e-191">Binding reduces code by using the same property to render form fields (`<input asp-for="Customer.Name" />`) and accept the input.</span></span>

> [!NOTE]
> <span data-ttu-id="a909e-192">出于安全原因，必须选择绑定 GET 请求数据以对模型属性进行分页。</span><span class="sxs-lookup"><span data-stu-id="a909e-192">For security reasons, you must opt in to binding GET request data to page model properties.</span></span> <span data-ttu-id="a909e-193">请在将用户输入映射到属性前对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="a909e-193">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="a909e-194">当处理依赖查询字符串或路由值的方案时，选择加入此行为非常有用。</span><span class="sxs-lookup"><span data-stu-id="a909e-194">Opting in to this behavior is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="a909e-195">若要将属性绑定在 GET 请求上，请将 `[BindProperty]` 特性的 `SupportsGet` 属性设置为 `true`：`[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="a909e-195">To bind a property on GET requests, set the `[BindProperty]` attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>

<span data-ttu-id="a909e-196">主页 (Index.cshtml)：</span><span class="sxs-lookup"><span data-stu-id="a909e-196">The home page (*Index.cshtml*):</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

<span data-ttu-id="a909e-197">Index.cshtml.cs 隐藏文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-197">The code behind *Index.cshtml.cs* file:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

<span data-ttu-id="a909e-198">Index.cshtml 文件包含以下标记来创建每个联系人项的编辑链接：</span><span class="sxs-lookup"><span data-stu-id="a909e-198">The *Index.cshtml* file contains the following markup to create an edit link for each contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

<span data-ttu-id="a909e-199">[定位点标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) 使用 `asp-route-{value}` 属性生成“编辑”页面的链接。</span><span class="sxs-lookup"><span data-stu-id="a909e-199">The [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) used the `asp-route-{value}` attribute to generate a link to the Edit page.</span></span> <span data-ttu-id="a909e-200">此链接包含路由数据及联系人 ID。</span><span class="sxs-lookup"><span data-stu-id="a909e-200">The link contains route data with the contact ID.</span></span> <span data-ttu-id="a909e-201">例如 `http://localhost:5000/Edit/1`。</span><span class="sxs-lookup"><span data-stu-id="a909e-201">For example, `http://localhost:5000/Edit/1`.</span></span>

<span data-ttu-id="a909e-202">Pages/Edit.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-202">The *Pages/Edit.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

<span data-ttu-id="a909e-203">第一行包含 `@page "{id:int}"` 指令。</span><span class="sxs-lookup"><span data-stu-id="a909e-203">The first line contains the `@page "{id:int}"` directive.</span></span> <span data-ttu-id="a909e-204">路由约束 `"{id:int}"` 告诉页面接受包含 `int` 路由数据的页面请求。</span><span class="sxs-lookup"><span data-stu-id="a909e-204">The routing constraint`"{id:int}"` tells the page to accept requests to the page that contain `int` route data.</span></span> <span data-ttu-id="a909e-205">如果页面请求未包含可转换为 `int` 的路由数据，则运行时返回 HTTP 404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="a909e-205">If a request to the page doesn't contain route data that can be converted to an `int`, the runtime returns an HTTP 404 (not found) error.</span></span> <span data-ttu-id="a909e-206">若要使 ID 可选，请将 `?` 追加到路由约束：</span><span class="sxs-lookup"><span data-stu-id="a909e-206">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

<span data-ttu-id="a909e-207">Pages/Edit.cshtml.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-207">The *Pages/Edit.cshtml.cs* file:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

<span data-ttu-id="a909e-208">Index.cshtml 文件还包含用于为每个客户联系人创建删除按钮的标记：</span><span class="sxs-lookup"><span data-stu-id="a909e-208">The *Index.cshtml* file also contains markup to create a delete button for each customer contact:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

<span data-ttu-id="a909e-209">删除按钮采用 HTML 呈现，其 `formaction` 包括参数：</span><span class="sxs-lookup"><span data-stu-id="a909e-209">When the delete button is rendered in HTML, its `formaction` includes parameters for:</span></span>

* <span data-ttu-id="a909e-210">`asp-route-id` 属性指定的客户联系人 ID。</span><span class="sxs-lookup"><span data-stu-id="a909e-210">The customer contact ID specified by the `asp-route-id` attribute.</span></span>
* <span data-ttu-id="a909e-211">`asp-page-handler` 属性指定的 `handler`。</span><span class="sxs-lookup"><span data-stu-id="a909e-211">The `handler` specified by the `asp-page-handler` attribute.</span></span>

<span data-ttu-id="a909e-212">下面是呈现的删除按钮的示例，其中客户联系人 ID 为 `1`：</span><span class="sxs-lookup"><span data-stu-id="a909e-212">Here is an example of a rendered delete button with a customer contact ID of `1`:</span></span>

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

<span data-ttu-id="a909e-213">选中按钮时，向服务器发送窗体 `POST` 请求。</span><span class="sxs-lookup"><span data-stu-id="a909e-213">When the button is selected, a form `POST` request is sent to the server.</span></span> <span data-ttu-id="a909e-214">按照惯例，根据方案 `OnPost[handler]Async` 基于 `handler` 参数的值来选择处理程序方法的名称。</span><span class="sxs-lookup"><span data-stu-id="a909e-214">By convention, the name of the handler method is selected based the value of the `handler` parameter according to the scheme `OnPost[handler]Async`.</span></span>

<span data-ttu-id="a909e-215">因为本示例中 `handler` 是 `delete`，因此 `OnPostDeleteAsync` 处理程序方法用于处理 `POST` 请求。</span><span class="sxs-lookup"><span data-stu-id="a909e-215">Because the `handler` is `delete` in this example, the `OnPostDeleteAsync` handler method is used to process the `POST` request.</span></span> <span data-ttu-id="a909e-216">如果 `asp-page-handler` 设置为不同值（如 `remove`），则选择名称为 `OnPostRemoveAsync` 的页面处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="a909e-216">If the `asp-page-handler` is set to a different value, such as `remove`, a page handler method with the name `OnPostRemoveAsync` is selected.</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

<span data-ttu-id="a909e-217">`OnPostDeleteAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="a909e-217">The `OnPostDeleteAsync` method:</span></span>

* <span data-ttu-id="a909e-218">接受来自查询字符串的 `id`。</span><span class="sxs-lookup"><span data-stu-id="a909e-218">Accepts the `id` from the query string.</span></span>
* <span data-ttu-id="a909e-219">使用 `FindAsync` 查询客户联系人的数据库。</span><span class="sxs-lookup"><span data-stu-id="a909e-219">Queries the database for the customer contact with `FindAsync`.</span></span>
* <span data-ttu-id="a909e-220">如果找到客户联系人，则从客户联系人列表将其删除。</span><span class="sxs-lookup"><span data-stu-id="a909e-220">If the customer contact is found, they're removed from the list of customer contacts.</span></span> <span data-ttu-id="a909e-221">数据库将更新。</span><span class="sxs-lookup"><span data-stu-id="a909e-221">The database is updated.</span></span>
* <span data-ttu-id="a909e-222">调用 `RedirectToPage`，重定向到根索引页 (`/Index`)。</span><span class="sxs-lookup"><span data-stu-id="a909e-222">Calls `RedirectToPage` to redirect to the root Index page (`/Index`).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-required"></a><span data-ttu-id="a909e-223">标记所需的页属性</span><span class="sxs-lookup"><span data-stu-id="a909e-223">Mark page properties required</span></span>

<span data-ttu-id="a909e-224">`PageModel` 上的属性可通过 [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) 特性进行修饰：</span><span class="sxs-lookup"><span data-stu-id="a909e-224">Properties on a `PageModel` can be decorated with the [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) attribute:</span></span>

<span data-ttu-id="a909e-225">[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]</span><span class="sxs-lookup"><span data-stu-id="a909e-225">[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]</span></span>

<span data-ttu-id="a909e-226">有关详细信息，请参阅[模型验证](xref:mvc/models/validation)。</span><span class="sxs-lookup"><span data-stu-id="a909e-226">See [Model validation](xref:mvc/models/validation) for more information.</span></span>

## <a name="manage-head-requests-with-the-onget-handler"></a><span data-ttu-id="a909e-227">使用 OnGet 处理程序管理 HEAD 请求</span><span class="sxs-lookup"><span data-stu-id="a909e-227">Manage HEAD requests with the OnGet handler</span></span>

<span data-ttu-id="a909e-228">通常，针对 HEAD 请求创建和调用 HEAD 处理程序：</span><span class="sxs-lookup"><span data-stu-id="a909e-228">Ordinarily, a HEAD handler is created and called for HEAD requests:</span></span>

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

<span data-ttu-id="a909e-229">如果未定义 HEAD 处理程序 (`OnHead`)，Razor 页面会回退以调用 ASP.NET Core 2.1 或更高版本中的 GET 页处理程序 (`OnGet`)。</span><span class="sxs-lookup"><span data-stu-id="a909e-229">If no HEAD handler (`OnHead`) is defined, Razor Pages falls back to calling the GET page handler (`OnGet`) in ASP.NET Core 2.1 or later.</span></span> <span data-ttu-id="a909e-230">使用 ASP.NET Core 2.1 到 2.x 版本 `Startup.Configure` 中的 [SetCompatibilityVersion 方法](xref:fundamentals/startup#setcompatibilityversion-for-aspnet-core-mvc)，选择加入此行为：</span><span class="sxs-lookup"><span data-stu-id="a909e-230">Opt in to this behavior with the [SetCompatibilityVersion method](xref:fundamentals/startup#setcompatibilityversion-for-aspnet-core-mvc) in `Startup.Configure` for ASP.NET Core 2.1 to 2.x:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

<span data-ttu-id="a909e-231">`SetCompatibilityVersion` 有效地将 Razor 页面选项 `AllowMappingHeadRequestsToGetHandler` 设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="a909e-231">`SetCompatibilityVersion` effectively sets the Razor Pages option `AllowMappingHeadRequestsToGetHandler` to `true`.</span></span>

<span data-ttu-id="a909e-232">可以显式地选择使用特定行为，而不是通过 `SetCompatibilityVersion` 选择使用所有 2.1 行为。</span><span class="sxs-lookup"><span data-stu-id="a909e-232">Rather than opting into all 2.1 behaviors with `SetCompatibilityVersion`, you can explicitly opt-in to specific behaviors.</span></span> <span data-ttu-id="a909e-233">以下代码选择使用将 HEAD 映射到 GET 处理程序这一行为。</span><span class="sxs-lookup"><span data-stu-id="a909e-233">The following code opts into the mapping HEAD requests to the GET handler.</span></span>


```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```
::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a><span data-ttu-id="a909e-234">XSRF/CSRF 和 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="a909e-234">XSRF/CSRF and Razor Pages</span></span>

<span data-ttu-id="a909e-235">无需为[防伪验证](xref:security/anti-request-forgery)编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="a909e-235">You don't have to write any code for [antiforgery validation](xref:security/anti-request-forgery).</span></span> <span data-ttu-id="a909e-236">Razor 页面自动将防伪标记生成过程和验证过程包含在内。</span><span class="sxs-lookup"><span data-stu-id="a909e-236">Antiforgery token generation and validation are automatically included in Razor Pages.</span></span>

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a><span data-ttu-id="a909e-237">将布局、分区、模板和标记帮助程序用于 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="a909e-237">Using Layouts, partials, templates, and Tag Helpers with Razor Pages</span></span>

<span data-ttu-id="a909e-238">页面可使用 Razor 视图引擎的所有功能。</span><span class="sxs-lookup"><span data-stu-id="a909e-238">Pages work with all the capabilities of the Razor view engine.</span></span> <span data-ttu-id="a909e-239">布局、分区、模板、标记帮助程序、_ViewStart.cshtml 和 _ViewImports.cshtml 的工作方式与它们在传统的 Razor 视图中的工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="a909e-239">Layouts, partials, templates, Tag Helpers, *_ViewStart.cshtml*, *_ViewImports.cshtml* work in the same way they do for conventional Razor views.</span></span>

<span data-ttu-id="a909e-240">让我们使用其中的一些功能来整理此页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-240">Let's declutter this page by taking advantage of some of those capabilities.</span></span>

<span data-ttu-id="a909e-241">向 Pages/_Layout.cshtml 添加[布局页面](xref:mvc/views/layout)：</span><span class="sxs-lookup"><span data-stu-id="a909e-241">Add a [layout page](xref:mvc/views/layout) to *Pages/_Layout.cshtml*:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

<span data-ttu-id="a909e-242">[布局](xref:mvc/views/layout)：</span><span class="sxs-lookup"><span data-stu-id="a909e-242">The [Layout](xref:mvc/views/layout):</span></span>

* <span data-ttu-id="a909e-243">控制每个页面的布局（页面选择退出布局时除外）。</span><span class="sxs-lookup"><span data-stu-id="a909e-243">Controls the layout of each page (unless the page opts out of layout).</span></span>
* <span data-ttu-id="a909e-244">导入 HTML 结构，例如 JavaScript 和样式表。</span><span class="sxs-lookup"><span data-stu-id="a909e-244">Imports HTML structures such as JavaScript and stylesheets.</span></span>

<span data-ttu-id="a909e-245">请参阅[布局页面](xref:mvc/views/layout)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="a909e-245">See [layout page](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="a909e-246">在 Pages/_ViewStart.cshtml 中设置 [Layout](xref:mvc/views/layout#specifying-a-layout) 属性：</span><span class="sxs-lookup"><span data-stu-id="a909e-246">The [Layout](xref:mvc/views/layout#specifying-a-layout) property is set in *Pages/_ViewStart.cshtml*:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

<span data-ttu-id="a909e-247">布局位于“页面”文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a909e-247">The layout is in the *Pages* folder.</span></span> <span data-ttu-id="a909e-248">页面按层次结构从当前页面的文件夹开始查找其他视图（布局、模板、分区）。</span><span class="sxs-lookup"><span data-stu-id="a909e-248">Pages look for other views (layouts, templates, partials) hierarchically, starting in the same folder as the current page.</span></span> <span data-ttu-id="a909e-249">可以从“页面”文件夹下的任意 Razor 页面使用“页面”文件夹中的布局。</span><span class="sxs-lookup"><span data-stu-id="a909e-249">A layout in the *Pages* folder can be used from any Razor page under the *Pages* folder.</span></span>

<span data-ttu-id="a909e-250">建议不要将布局文件放在“视图/共享”文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a909e-250">We recommend you **not** put the layout file in the *Views/Shared* folder.</span></span> <span data-ttu-id="a909e-251">视图/共享 是一种 MVC 视图模式。</span><span class="sxs-lookup"><span data-stu-id="a909e-251">*Views/Shared* is an MVC views pattern.</span></span> <span data-ttu-id="a909e-252">Razor 页面旨在依赖文件夹层次结构，而非路径约定。</span><span class="sxs-lookup"><span data-stu-id="a909e-252">Razor Pages are meant to rely on folder hierarchy, not path conventions.</span></span>

<span data-ttu-id="a909e-253">Razor 页面中的视图搜索包含“页面”文件夹。</span><span class="sxs-lookup"><span data-stu-id="a909e-253">View search from a Razor Page includes the *Pages* folder.</span></span> <span data-ttu-id="a909e-254">用于 MVC 控制器和传统 Razor 视图的布局、模板和分区可直接工作。</span><span class="sxs-lookup"><span data-stu-id="a909e-254">The layouts, templates, and partials you're using with MVC controllers and conventional Razor views *just work*.</span></span>

<span data-ttu-id="a909e-255">添加 Pages/_ViewImports.cshtml 文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-255">Add a *Pages/_ViewImports.cshtml* file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

<span data-ttu-id="a909e-256">本教程的后续部分中将介绍 `@namespace`。</span><span class="sxs-lookup"><span data-stu-id="a909e-256">`@namespace` is explained later in the tutorial.</span></span> <span data-ttu-id="a909e-257">`@addTagHelper` 指令将[内置标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/Index)引入“页面”文件夹中的所有页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-257">The `@addTagHelper` directive brings in the [built-in Tag Helpers](xref:mvc/views/tag-helpers/builtin-th/Index) to all the pages in the *Pages* folder.</span></span>

<a name="namespace"></a>

<span data-ttu-id="a909e-258">页面上显式使用 `@namespace` 指令后：</span><span class="sxs-lookup"><span data-stu-id="a909e-258">When the `@namespace` directive is used explicitly on a page:</span></span>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

<span data-ttu-id="a909e-259">此指令将为页面设置命名空间。</span><span class="sxs-lookup"><span data-stu-id="a909e-259">The directive sets the namespace for the page.</span></span> <span data-ttu-id="a909e-260">`@model` 指令无需包含命名空间。</span><span class="sxs-lookup"><span data-stu-id="a909e-260">The `@model` directive doesn't need to include the namespace.</span></span>

<span data-ttu-id="a909e-261">_ViewImports.cshtml 中包含 `@namespace` 指令后，指定的命名空间将为在导入 `@namespace` 指令的页面中生成的命名空间提供前缀。</span><span class="sxs-lookup"><span data-stu-id="a909e-261">When the `@namespace` directive is contained in *_ViewImports.cshtml*, the specified namespace supplies the prefix for the generated namespace in the Page that imports the `@namespace` directive.</span></span> <span data-ttu-id="a909e-262">生成的命名空间的剩余部分（后缀部分）是包含 _ViewImports.cshtml 的文件夹与包含页面的文件夹之间以点分隔的相对路径。</span><span class="sxs-lookup"><span data-stu-id="a909e-262">The rest of the generated namespace (the suffix portion) is the dot-separated relative path between the folder containing *_ViewImports.cshtml* and the folder containing the page.</span></span>

<span data-ttu-id="a909e-263">例如，代码隐藏文件 Pages/Customers/Edit.cshtml.cs 显式设置命名空间：</span><span class="sxs-lookup"><span data-stu-id="a909e-263">For example, the code behind file *Pages/Customers/Edit.cshtml.cs* explicitly sets the namespace:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

<span data-ttu-id="a909e-264">Pages/_ViewImports.cshtml 文件设置以下命名空间：</span><span class="sxs-lookup"><span data-stu-id="a909e-264">The *Pages/_ViewImports.cshtml* file sets the following namespace:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

<span data-ttu-id="a909e-265">为 Pages/Customers/Edit.cshtml Razor 页面生成的命名空间与代码隐藏文件相同.</span><span class="sxs-lookup"><span data-stu-id="a909e-265">The generated namespace for the *Pages/Customers/Edit.cshtml* Razor Page is the same as the code behind file.</span></span> <span data-ttu-id="a909e-266">已对 `@namespace` 指令进行设计，因此添加到项目的 C# 类和页面生成的代码可直接工作，而无需添加代码隐藏文件的 `@using` 指令。</span><span class="sxs-lookup"><span data-stu-id="a909e-266">The `@namespace` directive was designed so the C# classes added to a project and pages-generated code *just work* without having to add an `@using` directive for the code behind file.</span></span>

<span data-ttu-id="a909e-267">`@namespace` 也可用于传统的 Razor 视图。</span><span class="sxs-lookup"><span data-stu-id="a909e-267">`@namespace` *also works with conventional Razor views.*</span></span>

<span data-ttu-id="a909e-268">原始的 Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-268">The original *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

<span data-ttu-id="a909e-269">更新后的 Pages/Create.cshtml 视图文件：</span><span class="sxs-lookup"><span data-stu-id="a909e-269">The updated *Pages/Create.cshtml* view file:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

<span data-ttu-id="a909e-270">[Razor 页面初学者项目](#rpvs17)包含 Pages/_ValidationScriptsPartial.cshtml，它与客户端验证联合。</span><span class="sxs-lookup"><span data-stu-id="a909e-270">The [Razor Pages starter project](#rpvs17) contains the *Pages/_ValidationScriptsPartial.cshtml*, which hooks up client-side validation.</span></span>

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a><span data-ttu-id="a909e-271">页面的 URL 生成</span><span class="sxs-lookup"><span data-stu-id="a909e-271">URL generation for Pages</span></span>

<span data-ttu-id="a909e-272">之前显示的 `Create` 页面使用 `RedirectToPage`：</span><span class="sxs-lookup"><span data-stu-id="a909e-272">The `Create` page, shown previously, uses `RedirectToPage`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

<span data-ttu-id="a909e-273">应用具有以下文件/文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="a909e-273">The app has the following file/folder structure:</span></span>

* <span data-ttu-id="a909e-274">/Pages</span><span class="sxs-lookup"><span data-stu-id="a909e-274">*/Pages*</span></span>

  * <span data-ttu-id="a909e-275">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="a909e-275">*Index.cshtml*</span></span>
  * <span data-ttu-id="a909e-276">/Customers</span><span class="sxs-lookup"><span data-stu-id="a909e-276">*/Customers*</span></span>

    * <span data-ttu-id="a909e-277">Create.cshtml</span><span class="sxs-lookup"><span data-stu-id="a909e-277">*Create.cshtml*</span></span>
    * <span data-ttu-id="a909e-278">Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="a909e-278">*Edit.cshtml*</span></span>
    * <span data-ttu-id="a909e-279">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="a909e-279">*Index.cshtml*</span></span>

<span data-ttu-id="a909e-280">成功后，Pages/Customers/Create.cshtml 和 Pages/Customers/Edit.cshtml 页面将重定向到 Pages/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="a909e-280">The *Pages/Customers/Create.cshtml* and *Pages/Customers/Edit.cshtml* pages redirect to *Pages/Index.cshtml* after success.</span></span> <span data-ttu-id="a909e-281">字符串 `/Index` 是用于访问上一页的 URI 的组成部分。</span><span class="sxs-lookup"><span data-stu-id="a909e-281">The string `/Index` is part of the URI to access the preceding page.</span></span> <span data-ttu-id="a909e-282">可以使用字符串 `/Index` 生成 Pages/Index.cshtml 页面的 URI。</span><span class="sxs-lookup"><span data-stu-id="a909e-282">The string `/Index` can be used to generate URIs to the *Pages/Index.cshtml* page.</span></span> <span data-ttu-id="a909e-283">例如:</span><span class="sxs-lookup"><span data-stu-id="a909e-283">For example:</span></span>

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

<span data-ttu-id="a909e-284">页面名称是从根“/Pages”文件夹到页面的路径（包含前导 `/`，例如 `/Index`）。</span><span class="sxs-lookup"><span data-stu-id="a909e-284">The page name is the path to the page from the root */Pages* folder including a leading `/` (for example, `/Index`).</span></span> <span data-ttu-id="a909e-285">与硬编码 URL 相比，前面的 URL 生成示例提供了改进的选项和功能。</span><span class="sxs-lookup"><span data-stu-id="a909e-285">The preceding URL generation samples offer enhanced options and functional capabilities over hardcoding a URL.</span></span> <span data-ttu-id="a909e-286">URL 生成使用[路由](xref:mvc/controllers/routing)，并且可以根据目标路径定义路由的方式生成参数并对参数编码。</span><span class="sxs-lookup"><span data-stu-id="a909e-286">URL generation uses [routing](xref:mvc/controllers/routing) and can generate and encode parameters according to how the route is defined in the destination path.</span></span>

<span data-ttu-id="a909e-287">页面的 URL 生成支持相对名称。</span><span class="sxs-lookup"><span data-stu-id="a909e-287">URL generation for pages supports relative names.</span></span> <span data-ttu-id="a909e-288">下表显示了 Pages/Customers/Create.cshtml 中不同的 `RedirectToPage` 参数选择的索引页：</span><span class="sxs-lookup"><span data-stu-id="a909e-288">The following table shows which Index page is selected with different `RedirectToPage` parameters from *Pages/Customers/Create.cshtml*:</span></span>

| <span data-ttu-id="a909e-289">RedirectToPage(x)</span><span class="sxs-lookup"><span data-stu-id="a909e-289">RedirectToPage(x)</span></span>| <span data-ttu-id="a909e-290">页</span><span class="sxs-lookup"><span data-stu-id="a909e-290">Page</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="a909e-291">RedirectToPage("/Index")</span><span class="sxs-lookup"><span data-stu-id="a909e-291">RedirectToPage("/Index")</span></span> | <span data-ttu-id="a909e-292">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="a909e-292">*Pages/Index*</span></span> |
| <span data-ttu-id="a909e-293">RedirectToPage("./Index");</span><span class="sxs-lookup"><span data-stu-id="a909e-293">RedirectToPage("./Index");</span></span> | <span data-ttu-id="a909e-294">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="a909e-294">*Pages/Customers/Index*</span></span> |
| <span data-ttu-id="a909e-295">RedirectToPage("../Index")</span><span class="sxs-lookup"><span data-stu-id="a909e-295">RedirectToPage("../Index")</span></span> | <span data-ttu-id="a909e-296">*Pages/Index*</span><span class="sxs-lookup"><span data-stu-id="a909e-296">*Pages/Index*</span></span> |
| <span data-ttu-id="a909e-297">RedirectToPage("Index")</span><span class="sxs-lookup"><span data-stu-id="a909e-297">RedirectToPage("Index")</span></span>  | <span data-ttu-id="a909e-298">*Pages/Customers/Index*</span><span class="sxs-lookup"><span data-stu-id="a909e-298">*Pages/Customers/Index*</span></span> |

<span data-ttu-id="a909e-299">`RedirectToPage("Index")`、`RedirectToPage("./Index")` 和 `RedirectToPage("../Index")` 是相对名称。</span><span class="sxs-lookup"><span data-stu-id="a909e-299">`RedirectToPage("Index")`, `RedirectToPage("./Index")`, and `RedirectToPage("../Index")`  are <em>relative names</em>.</span></span> <span data-ttu-id="a909e-300">结合 `RedirectToPage` 参数与当前页的路径来计算目标页面的名称。</span><span class="sxs-lookup"><span data-stu-id="a909e-300">The `RedirectToPage` parameter is <em>combined</em> with the path of the current page to compute the name of the destination page.</span></span>  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

<span data-ttu-id="a909e-301">构建结构复杂的站点时，相对名称链接很有用。</span><span class="sxs-lookup"><span data-stu-id="a909e-301">Relative name linking is useful when building sites with a complex structure.</span></span> <span data-ttu-id="a909e-302">如果使用相对名称链接文件夹中的页面，则可以重命名该文件夹。</span><span class="sxs-lookup"><span data-stu-id="a909e-302">If you use relative names to link between pages in a folder, you can rename that folder.</span></span> <span data-ttu-id="a909e-303">所有链接仍然有效（因为这些链接未包含此文件夹名称）。</span><span class="sxs-lookup"><span data-stu-id="a909e-303">All the links still work (because they didn't include the folder name).</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="viewdata-attribute"></a><span data-ttu-id="a909e-304">ViewData 特性</span><span class="sxs-lookup"><span data-stu-id="a909e-304">ViewData attribute</span></span>

<span data-ttu-id="a909e-305">可以通过 [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute) 将数据传递到页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-305">Data can be passed to a page with [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="a909e-306">控制器或 Razor 页面模型上使用 `[ViewData]` 修饰的属性将其值存储在 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 中并从此处进行加载。</span><span class="sxs-lookup"><span data-stu-id="a909e-306">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary).</span></span>

<span data-ttu-id="a909e-307">在下面的示例中，`AboutModel` 包含使用 `[ViewData]` 修饰的 `Title` 属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-307">In the following example, the `AboutModel` contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="a909e-308">`Title` 属性设置为“关于”页面的标题：</span><span class="sxs-lookup"><span data-stu-id="a909e-308">The `Title` property is set to the title of the About page:</span></span>

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

<span data-ttu-id="a909e-309">在“关于”页面中，以模型属性的形式访问 `Title` 属性：</span><span class="sxs-lookup"><span data-stu-id="a909e-309">In the About page, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="a909e-310">在布局中，从 ViewData 字典读取标题：</span><span class="sxs-lookup"><span data-stu-id="a909e-310">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```
::: moniker-end

## <a name="tempdata"></a><span data-ttu-id="a909e-311">TempData</span><span class="sxs-lookup"><span data-stu-id="a909e-311">TempData</span></span>

<span data-ttu-id="a909e-312">ASP.NET 在[控制器](/dotnet/api/microsoft.aspnetcore.mvc.controller)上公开了 [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-312">ASP.NET Core exposes the [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](/dotnet/api/microsoft.aspnetcore.mvc.controller).</span></span> <span data-ttu-id="a909e-313">此属性存储未读取的数据。</span><span class="sxs-lookup"><span data-stu-id="a909e-313">This property stores data until it's read.</span></span> <span data-ttu-id="a909e-314">`Keep` 和 `Peek` 方法可用于检查数据，而不执行删除。</span><span class="sxs-lookup"><span data-stu-id="a909e-314">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="a909e-315">多个请求需要数据时，`TempData` 有助于进行重定向。</span><span class="sxs-lookup"><span data-stu-id="a909e-315">`TempData` is  useful for redirection, when data is needed for more than a single request.</span></span>

<span data-ttu-id="a909e-316">`[TempData]` 是 ASP.NET Core 2.0 中的新属性，在控制器和页面上受支持。</span><span class="sxs-lookup"><span data-stu-id="a909e-316">The `[TempData]` attribute is new in ASP.NET Core 2.0 and is supported on controllers and pages.</span></span>

<span data-ttu-id="a909e-317">下面的代码使用 `TempData` 设置 `Message` 的值：</span><span class="sxs-lookup"><span data-stu-id="a909e-317">The following code sets the value of `Message` using `TempData`:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

<span data-ttu-id="a909e-318">Pages/Customers/Index.cshtml 文件中的以下标记使用 `TempData` 显示 `Message` 的值。</span><span class="sxs-lookup"><span data-stu-id="a909e-318">The following markup in the *Pages/Customers/Index.cshtml* file displays the value of `Message` using `TempData`.</span></span>

```cshtml
<h3>Msg: @Model.Message</h3>
```

<span data-ttu-id="a909e-319">Pages/Customers/Index.cshtml.cs 页面模型将 `[TempData]` 属性应用到 `Message` 属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-319">The *Pages/Customers/Index.cshtml.cs* page model applies the `[TempData]` attribute to the `Message` property.</span></span>

```cs
[TempData]
public string Message { get; set; }
```

<span data-ttu-id="a909e-320">请参阅 [TempData](xref:fundamentals/app-state#tempdata) 了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="a909e-320">See [TempData](xref:fundamentals/app-state#tempdata) for more information.</span></span>

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a><span data-ttu-id="a909e-321">针对一个页面的多个处理程序</span><span class="sxs-lookup"><span data-stu-id="a909e-321">Multiple handlers per page</span></span>

<span data-ttu-id="a909e-322">以下页面使用 `asp-page-handler` 标记帮助程序为两个页面处理程序生成标记：</span><span class="sxs-lookup"><span data-stu-id="a909e-322">The following page generates markup for two page handlers using the `asp-page-handler` Tag Helper:</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

<span data-ttu-id="a909e-323">前面示例中的窗体包含两个提交按钮，每个提交按钮均使用 `FormActionTagHelper` 提交到不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="a909e-323">The form in the preceding example has two submit buttons, each using the `FormActionTagHelper` to submit to a different URL.</span></span> <span data-ttu-id="a909e-324">`asp-page-handler` 是 `asp-page` 的配套属性。</span><span class="sxs-lookup"><span data-stu-id="a909e-324">The `asp-page-handler` attribute is a companion to `asp-page`.</span></span> <span data-ttu-id="a909e-325">`asp-page-handler` 生成提交到页面定义的各个处理程序方法的 URL。</span><span class="sxs-lookup"><span data-stu-id="a909e-325">`asp-page-handler` generates URLs that submit to each of the handler methods defined by a page.</span></span> <span data-ttu-id="a909e-326">未指定 `asp-page`，因为示例已链接到当前页面。</span><span class="sxs-lookup"><span data-stu-id="a909e-326">`asp-page` isn't specified because the sample is linking to the current page.</span></span>

<span data-ttu-id="a909e-327">页面模型：</span><span class="sxs-lookup"><span data-stu-id="a909e-327">The page model:</span></span>

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

<span data-ttu-id="a909e-328">前面的代码使用已命名处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="a909e-328">The preceding code uses *named handler methods*.</span></span> <span data-ttu-id="a909e-329">已命名处理程序方法通过采用名称中 `On<HTTP Verb>` 之后及 `Async` 之前的文本（如果有）创建。</span><span class="sxs-lookup"><span data-stu-id="a909e-329">Named handler methods are created by taking the text in the name after `On<HTTP Verb>` and before `Async` (if present).</span></span> <span data-ttu-id="a909e-330">在前面的示例中，页面方法是 OnPost**JoinList**Async 和 OnPost**JoinListUC**Async。</span><span class="sxs-lookup"><span data-stu-id="a909e-330">In the preceding example, the page methods are OnPost**JoinList**Async and OnPost**JoinListUC**Async.</span></span> <span data-ttu-id="a909e-331">删除 OnPost 和 Async 后，处理程序名称为 `JoinList` 和 `JoinListUC`。</span><span class="sxs-lookup"><span data-stu-id="a909e-331">With *OnPost* and *Async* removed, the handler names are `JoinList` and `JoinListUC`.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

<span data-ttu-id="a909e-332">使用前面的代码时，提交到 `OnPostJoinListAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`。</span><span class="sxs-lookup"><span data-stu-id="a909e-332">Using the preceding code, the URL path that submits to `OnPostJoinListAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinList`.</span></span> <span data-ttu-id="a909e-333">提交到 `OnPostJoinListUCAsync` 的 URL 路径为 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`。</span><span class="sxs-lookup"><span data-stu-id="a909e-333">The URL path that submits to `OnPostJoinListUCAsync` is `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`.</span></span>



## <a name="customizing-routing"></a><span data-ttu-id="a909e-334">自定义路由</span><span class="sxs-lookup"><span data-stu-id="a909e-334">Customizing Routing</span></span>

<span data-ttu-id="a909e-335">如果你不喜欢 URL 中的查询字符串 `?handler=JoinList`，可以更改路由，将处理程序名称放在 URL 的路径部分。</span><span class="sxs-lookup"><span data-stu-id="a909e-335">If you don't like the query string `?handler=JoinList` in the URL, you can change the route to put the handler name in the path portion of the URL.</span></span> <span data-ttu-id="a909e-336">可以通过在 `@page` 指令后面添加使用双引号括起来的路由模板来自定义路由。</span><span class="sxs-lookup"><span data-stu-id="a909e-336">You can customize the route by adding a route template enclosed in double quotes after the `@page` directive.</span></span>

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

<span data-ttu-id="a909e-337">前面的路由将处理程序放在了 URL 路径中，而不是查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="a909e-337">The preceding route puts the handler name in the URL path instead of the query string.</span></span> <span data-ttu-id="a909e-338">`handler` 前面的 `?` 表示路由参数为可选。</span><span class="sxs-lookup"><span data-stu-id="a909e-338">The `?` following `handler` means the route parameter is optional.</span></span>

<span data-ttu-id="a909e-339">可以使用 `@page` 将其他段和参数添加到页面的路由中。</span><span class="sxs-lookup"><span data-stu-id="a909e-339">You can use `@page` to add additional segments and parameters to a page's route.</span></span> <span data-ttu-id="a909e-340">其中的任何内容均会被追加到页面的默认路由中。</span><span class="sxs-lookup"><span data-stu-id="a909e-340">Whatever's there's **appended** to the default route of the page.</span></span> <span data-ttu-id="a909e-341">不支持使用绝对路径或虚拟路径更改页面的路由（如 `"~/Some/Other/Path"`）。</span><span class="sxs-lookup"><span data-stu-id="a909e-341">Using an absolute or virtual path to change the page's route (like `"~/Some/Other/Path"`) isn't supported.</span></span>

## <a name="configuration-and-settings"></a><span data-ttu-id="a909e-342">配置和设置</span><span class="sxs-lookup"><span data-stu-id="a909e-342">Configuration and settings</span></span>

<span data-ttu-id="a909e-343">若要配置高级选项，请在 MVC 生成器上使用 `AddRazorPagesOptions` 扩展方法：</span><span class="sxs-lookup"><span data-stu-id="a909e-343">To configure advanced options, use the extension method `AddRazorPagesOptions` on the MVC builder:</span></span>

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

<span data-ttu-id="a909e-344">目前，可以使用 `RazorPagesOptions` 设置页面的根目录，或者为页面添加应用程序模型约定。</span><span class="sxs-lookup"><span data-stu-id="a909e-344">Currently you can use the `RazorPagesOptions` to set the root directory for pages, or add application model conventions for pages.</span></span> <span data-ttu-id="a909e-345">通过这种方式，我们在将来会实现更多扩展功能。</span><span class="sxs-lookup"><span data-stu-id="a909e-345">We'll enable more extensibility this way in the future.</span></span>

<span data-ttu-id="a909e-346">若要预编译视图，请参阅 [Razor 视图编译](xref:mvc/views/view-compilation)。</span><span class="sxs-lookup"><span data-stu-id="a909e-346">To precompile views, see [Razor view compilation](xref:mvc/views/view-compilation) .</span></span>

<span data-ttu-id="a909e-347">[下载或查看示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span><span class="sxs-lookup"><span data-stu-id="a909e-347">[Download or view sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample).</span></span>

<span data-ttu-id="a909e-348">请参阅 [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)，这篇文章以本文为基础编写。</span><span class="sxs-lookup"><span data-stu-id="a909e-348">See [Get started with Razor Pages](xref:tutorials/razor-pages/razor-pages-start), which builds on this introduction.</span></span>

### <a name="specify-that-razor-pages-are-at-the-content-root"></a><span data-ttu-id="a909e-349">指定 Razor 页面位于内容根目录中</span><span class="sxs-lookup"><span data-stu-id="a909e-349">Specify that Razor Pages are at the content root</span></span>

<span data-ttu-id="a909e-350">默认情况下，Razor 页面位于 /Pages 目录的根位置。</span><span class="sxs-lookup"><span data-stu-id="a909e-350">By default, Razor Pages are rooted in the */Pages* directory.</span></span> <span data-ttu-id="a909e-351">向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot)，以指定 Razor 页面位于应用的内容根目录 ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) 中：</span><span class="sxs-lookup"><span data-stu-id="a909e-351">Add [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at the content root ([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath)) of the app:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a><span data-ttu-id="a909e-352">指定 Razor 页面位于自定义根目录中</span><span class="sxs-lookup"><span data-stu-id="a909e-352">Specify that Razor Pages are at a custom root directory</span></span>

<span data-ttu-id="a909e-353">向 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 添加 [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot)，以指定 Razor 页面位于应用中自定义根目录位置（提供相对路径）：</span><span class="sxs-lookup"><span data-stu-id="a909e-353">Add [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot) to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_) to specify that your Razor Pages are at a custom root directory in the app (provide a relative path):</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="see-also"></a><span data-ttu-id="a909e-354">请参阅</span><span class="sxs-lookup"><span data-stu-id="a909e-354">See also</span></span>

* [<span data-ttu-id="a909e-355">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="a909e-355">Introduction to ASP.NET Core</span></span>](xref:index)
* [<span data-ttu-id="a909e-356">Razor 语法</span><span class="sxs-lookup"><span data-stu-id="a909e-356">Razor syntax</span></span>](xref:mvc/views/razor)
* [<span data-ttu-id="a909e-357">Razor 页面入门</span><span class="sxs-lookup"><span data-stu-id="a909e-357">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="a909e-358">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="a909e-358">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
* [<span data-ttu-id="a909e-359">Razor 页面自定义路由和页面模型提供程序</span><span class="sxs-lookup"><span data-stu-id="a909e-359">Razor Pages custom route and page model providers</span></span>](xref:mvc/razor-pages/razor-pages-conventions)
* [<span data-ttu-id="a909e-360">Razor 页面单位与集成测试</span><span class="sxs-lookup"><span data-stu-id="a909e-360">Razor Pages unit and integration tests</span></span>](xref:testing/razor-pages-testing)
