---
title: ASP.NET Core 中的布局
author: ardalis
description: 了解如何在 ASP.NET Core 应用中呈现视图之前，使用通用布局、共享指令和运行常见代码。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/layout
ms.openlocfilehash: 8e89c8e6cf18c47abb6bf432cdc6bb6b97e8aeb0
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="layout-in-aspnet-core"></a><span data-ttu-id="bf002-103">ASP.NET Core 中的布局</span><span class="sxs-lookup"><span data-stu-id="bf002-103">Layout in ASP.NET Core</span></span>

<span data-ttu-id="bf002-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="bf002-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="bf002-105">视图经常共享可视和编程元素。</span><span class="sxs-lookup"><span data-stu-id="bf002-105">Views frequently share visual and programmatic elements.</span></span> <span data-ttu-id="bf002-106">本文介绍如何在 ASP.NET 应用中呈现视图之前，使用通用布局、共享指令和运行常见代码。</span><span class="sxs-lookup"><span data-stu-id="bf002-106">In this article, you'll learn how to use common layouts, share directives, and run common code before rendering views in your ASP.NET app.</span></span>

## <a name="what-is-a-layout"></a><span data-ttu-id="bf002-107">什么是布局</span><span class="sxs-lookup"><span data-stu-id="bf002-107">What is a Layout</span></span>

<span data-ttu-id="bf002-108">大多数 Web 应用都有一个通用布局，可在页面间切换时为用户提供一致体验。</span><span class="sxs-lookup"><span data-stu-id="bf002-108">Most web apps have a common layout that provides the user with a consistent experience as they navigate from page to page.</span></span> <span data-ttu-id="bf002-109">该布局通常包括应用标头、导航或菜单元素以及页脚等常见的用户界面元素。</span><span class="sxs-lookup"><span data-stu-id="bf002-109">The layout typically includes common user interface elements such as the app header, navigation or menu elements, and footer.</span></span>

![页面布局示例](layout/_static/page-layout.png)

<span data-ttu-id="bf002-111">应用中的许多页面也经常使用脚本和样式表等常用的 HTML 结构。</span><span class="sxs-lookup"><span data-stu-id="bf002-111">Common HTML structures such as scripts and stylesheets are also frequently used by many pages within an app.</span></span> <span data-ttu-id="bf002-112">所有这些共享元素均可在布局文件中进行定义，应用内使用的任何视图随后均可引用此文件。</span><span class="sxs-lookup"><span data-stu-id="bf002-112">All of these shared elements may be defined in a *layout* file, which can then be referenced by any view used within the app.</span></span> <span data-ttu-id="bf002-113">布局可减少视图中的重复代码，帮助它们遵循[不要自我重复 (DRY) 原则](http://deviq.com/don-t-repeat-yourself/)。</span><span class="sxs-lookup"><span data-stu-id="bf002-113">Layouts reduce duplicate code in views, helping them follow the [Don't Repeat Yourself (DRY) principle](http://deviq.com/don-t-repeat-yourself/).</span></span>

<span data-ttu-id="bf002-114">按照约定，ASP.NET 应用的默认布局名为 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="bf002-114">By convention, the default layout for an ASP.NET app is named `_Layout.cshtml`.</span></span> <span data-ttu-id="bf002-115">Visual Studio ASP.NET Core MVC 项目模板在 `Views/Shared` 文件夹中包含此布局文件：</span><span class="sxs-lookup"><span data-stu-id="bf002-115">The Visual Studio ASP.NET Core MVC project template includes this layout file in the `Views/Shared` folder:</span></span>

![解决方案资源管理器中的视图文件夹](layout/_static/web-project-views.png)

<span data-ttu-id="bf002-117">此布局为应用中的视图定义顶级模板。</span><span class="sxs-lookup"><span data-stu-id="bf002-117">This layout defines a top level template for views in the app.</span></span> <span data-ttu-id="bf002-118">应用不需要布局，它们可以定义多个布局，并且不同的视图指定不同的布局。</span><span class="sxs-lookup"><span data-stu-id="bf002-118">Apps don't require a layout, and apps can define more than one layout, with different views specifying different layouts.</span></span>

<span data-ttu-id="bf002-119">示例 `_Layout.cshtml`：</span><span class="sxs-lookup"><span data-stu-id="bf002-119">An example `_Layout.cshtml`:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=42,66)]

## <a name="specifying-a-layout"></a><span data-ttu-id="bf002-120">指定布局</span><span class="sxs-lookup"><span data-stu-id="bf002-120">Specifying a Layout</span></span>

<span data-ttu-id="bf002-121">Razor 视图具有 `Layout` 属性。</span><span class="sxs-lookup"><span data-stu-id="bf002-121">Razor views have a `Layout` property.</span></span> <span data-ttu-id="bf002-122">单个视图通过设置此属性来指定布局：</span><span class="sxs-lookup"><span data-stu-id="bf002-122">Individual views specify a layout by setting this property:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml?highlight=2)]

<span data-ttu-id="bf002-123">指定的布局可以使用完整路径（例如：`/Views/Shared/_Layout.cshtml`）或部分名称（例如：`_Layout`）。</span><span class="sxs-lookup"><span data-stu-id="bf002-123">The layout specified can use a full path (example: `/Views/Shared/_Layout.cshtml`) or a partial name (example: `_Layout`).</span></span> <span data-ttu-id="bf002-124">如果提供部分名称，Razor 视图引擎将使用其标准发现过程来搜索布局文件。</span><span class="sxs-lookup"><span data-stu-id="bf002-124">When a partial name is provided, the Razor view engine will search for the layout file using its standard discovery process.</span></span> <span data-ttu-id="bf002-125">首先搜索与控制器关联的文件夹，然后搜索 `Shared` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="bf002-125">The controller-associated folder is searched first, followed by the `Shared` folder.</span></span> <span data-ttu-id="bf002-126">此发现过程与用于发现[分部视图](partial.md)的过程相同。</span><span class="sxs-lookup"><span data-stu-id="bf002-126">This discovery process is identical to the one used to discover [partial views](partial.md).</span></span>

<span data-ttu-id="bf002-127">默认情况下，每个布局必须调用 `RenderBody`。</span><span class="sxs-lookup"><span data-stu-id="bf002-127">By default, every layout must call `RenderBody`.</span></span> <span data-ttu-id="bf002-128">无论在何处调用 `RenderBody`，都会呈现视图的内容。</span><span class="sxs-lookup"><span data-stu-id="bf002-128">Wherever the call to `RenderBody` is placed, the contents of the view will be rendered.</span></span>

<a name="layout-sections-label"></a>

### <a name="sections"></a><span data-ttu-id="bf002-129">部分</span><span class="sxs-lookup"><span data-stu-id="bf002-129">Sections</span></span>

<span data-ttu-id="bf002-130">布局可以通过调用 `RenderSection` 来选择引用一个或多个节。</span><span class="sxs-lookup"><span data-stu-id="bf002-130">A layout can optionally reference one or more *sections*, by calling `RenderSection`.</span></span> <span data-ttu-id="bf002-131">节提供一种方法来组织某些页面元素应当放置的位置。</span><span class="sxs-lookup"><span data-stu-id="bf002-131">Sections provide a way to organize where certain page elements should be placed.</span></span> <span data-ttu-id="bf002-132">对 `RenderSection` 的每次调用均可指定该节是必需的还是可选的。</span><span class="sxs-lookup"><span data-stu-id="bf002-132">Each call to `RenderSection` can specify whether that section is required or optional.</span></span> <span data-ttu-id="bf002-133">如果找不到所需的节，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="bf002-133">If a required section isn't found, an exception will be thrown.</span></span> <span data-ttu-id="bf002-134">单个视图使用 `@section` Razor 语法指定要在节中呈现的内容。</span><span class="sxs-lookup"><span data-stu-id="bf002-134">Individual views specify the content to be rendered within a section using the `@section` Razor syntax.</span></span> <span data-ttu-id="bf002-135">如果视图定义某个节，则必须呈现该节（否则会发生错误）。</span><span class="sxs-lookup"><span data-stu-id="bf002-135">If a view defines a section, it must be rendered (or an error will occur).</span></span>

<span data-ttu-id="bf002-136">视图中的示例 `@section` 定义：</span><span class="sxs-lookup"><span data-stu-id="bf002-136">An example `@section` definition in a view:</span></span>

```html
@section Scripts {
     <script type="text/javascript" src="/scripts/main.js"></script>
   }
   ```

<span data-ttu-id="bf002-137">在上面的代码中，验证脚本添加到了视图（包含窗体）上的 `scripts` 节。</span><span class="sxs-lookup"><span data-stu-id="bf002-137">In the code above, validation scripts are added to the `scripts` section on a view that includes a form.</span></span> <span data-ttu-id="bf002-138">同一应用程序中的其他视图可能不需要任何其他脚本，因此无需定义脚本节。</span><span class="sxs-lookup"><span data-stu-id="bf002-138">Other views in the same application might not require any additional scripts, and so wouldn't need to define a scripts section.</span></span>

<span data-ttu-id="bf002-139">视图中定义的节仅在其即时布局页面中可用。</span><span class="sxs-lookup"><span data-stu-id="bf002-139">Sections defined in a view are available only in its immediate layout page.</span></span> <span data-ttu-id="bf002-140">不能从部分、视图组件或视图系统的其他部分引用它们。</span><span class="sxs-lookup"><span data-stu-id="bf002-140">They cannot be referenced from partials, view components, or other parts of the view system.</span></span>

### <a name="ignoring-sections"></a><span data-ttu-id="bf002-141">忽略节</span><span class="sxs-lookup"><span data-stu-id="bf002-141">Ignoring sections</span></span>

<span data-ttu-id="bf002-142">默认情况下，必须由布局页面呈现内容页中的正文和所有节。</span><span class="sxs-lookup"><span data-stu-id="bf002-142">By default, the body and all sections in a content page must all be rendered by the layout page.</span></span> <span data-ttu-id="bf002-143">Razor 视图引擎通过跟踪是否已呈现正文和每个节来强制执行此操作。</span><span class="sxs-lookup"><span data-stu-id="bf002-143">The Razor view engine enforces this by tracking whether the body and each section have been rendered.</span></span>

<span data-ttu-id="bf002-144">要让视图引擎忽略正文或节，请调用 `IgnoreBody` 和 `IgnoreSection` 方法。</span><span class="sxs-lookup"><span data-stu-id="bf002-144">To instruct the view engine to ignore the body or sections, call the `IgnoreBody` and `IgnoreSection` methods.</span></span>

<span data-ttu-id="bf002-145">必须呈现或忽略 Razor 页面中的正文和每个节。</span><span class="sxs-lookup"><span data-stu-id="bf002-145">The body and every section in a Razor page must be either rendered or ignored.</span></span>

<a name="viewimports"></a>

## <a name="importing-shared-directives"></a><span data-ttu-id="bf002-146">导入共享指令</span><span class="sxs-lookup"><span data-stu-id="bf002-146">Importing Shared Directives</span></span>

<span data-ttu-id="bf002-147">视图可以使用 Razor 指令来执行许多操作，例如导入命名空间或执行[依赖关系注入](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="bf002-147">Views can use Razor directives to do many things, such as importing namespaces or performing [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="bf002-148">可在一个共同的 `_ViewImports.cshtml` 文件中指定由许多视图共享的指令。</span><span class="sxs-lookup"><span data-stu-id="bf002-148">Directives shared by many views may be specified in a common `_ViewImports.cshtml` file.</span></span> <span data-ttu-id="bf002-149">`_ViewImports` 文件支持以下指令：</span><span class="sxs-lookup"><span data-stu-id="bf002-149">The `_ViewImports` file supports the following directives:</span></span>

* `@addTagHelper`

* `@removeTagHelper`

* `@tagHelperPrefix`

* `@using`

* `@model`

* `@inherits`

* `@inject`

<span data-ttu-id="bf002-150">该文件不支持函数和节定义等其他 Razor 功能。</span><span class="sxs-lookup"><span data-stu-id="bf002-150">The file doesn't support other Razor features, such as functions and section definitions.</span></span>

<span data-ttu-id="bf002-151">示例 `_ViewImports.cshtml` 文件：</span><span class="sxs-lookup"><span data-stu-id="bf002-151">A sample `_ViewImports.cshtml` file:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewImports.cshtml)]

<span data-ttu-id="bf002-152">针对 ASP.NET Core MVC 应用的 `_ViewImports.cshtml` 文件通常放置在 `Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bf002-152">The `_ViewImports.cshtml` file for an ASP.NET Core MVC app is typically placed in the `Views` folder.</span></span> <span data-ttu-id="bf002-153">`_ViewImports.cshtml` 文件可以放置在任何文件夹中，在这种情况下，它仅适用于该文件夹及其子文件夹中的视图。</span><span class="sxs-lookup"><span data-stu-id="bf002-153">A `_ViewImports.cshtml` file can be placed within any folder, in which case it will only be applied to views within that folder and its subfolders.</span></span> <span data-ttu-id="bf002-154">由于从根级别开始处理 `_ViewImports` 文件，然后处理视图本身的位置之前的每个文件夹，因此在根级别指定的设置可能会覆盖在文件夹级别。</span><span class="sxs-lookup"><span data-stu-id="bf002-154">`_ViewImports` files are processed starting at the root level, and then for each folder leading up to the location of the view itself, so settings specified at the root level may be overridden at the folder level.</span></span>

<span data-ttu-id="bf002-155">例如，如果根级别 `_ViewImports.cshtml` 文件指定 `@model` 和 `@addTagHelper`，在该视图的控制器关联文件夹中，另一个 `_ViewImports.cshtml` 文件指定不同的 `@model` 并添加另一个 `@addTagHelper`，该视图将有权访问这两个标记帮助程序，并将使用后一个 `@model`。</span><span class="sxs-lookup"><span data-stu-id="bf002-155">For example, if a root level `_ViewImports.cshtml` file specifies `@model` and `@addTagHelper`, and another `_ViewImports.cshtml` file in the controller-associated folder of the view specifies a different `@model` and adds another `@addTagHelper`, the view will have access to both tag helpers and will use the latter `@model`.</span></span>

<span data-ttu-id="bf002-156">如果对一个视图运行多个 `_ViewImports.cshtml` 文件，那么包含在 `ViewImports.cshtml` 文件中的指令的组合行为如下所示：</span><span class="sxs-lookup"><span data-stu-id="bf002-156">If multiple `_ViewImports.cshtml` files are run for a view, combined behavior of the directives included in the `ViewImports.cshtml` files will be as follows:</span></span>

* <span data-ttu-id="bf002-157">`@addTagHelper``@removeTagHelper`：按顺序全部运行</span><span class="sxs-lookup"><span data-stu-id="bf002-157">`@addTagHelper`, `@removeTagHelper`: all run, in order</span></span>

* <span data-ttu-id="bf002-158">`@tagHelperPrefix`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="bf002-158">`@tagHelperPrefix`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="bf002-159">`@model`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="bf002-159">`@model`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="bf002-160">`@inherits`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="bf002-160">`@inherits`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="bf002-161">`@using`：全部包括在内；忽略重复项</span><span class="sxs-lookup"><span data-stu-id="bf002-161">`@using`: all are included; duplicates are ignored</span></span>

* <span data-ttu-id="bf002-162">`@inject`：针对每个属性，最接近视图的属性会替代具有相同属性名的任何其他属性</span><span class="sxs-lookup"><span data-stu-id="bf002-162">`@inject`: for each property, the closest one to the view overrides any others with the same property name</span></span>

<a name="viewstart"></a>

## <a name="running-code-before-each-view"></a><span data-ttu-id="bf002-163">在呈现每个视图之前运行代码</span><span class="sxs-lookup"><span data-stu-id="bf002-163">Running Code Before Each View</span></span>

<span data-ttu-id="bf002-164">如果有需要在呈现每个视图之前运行的代码，应将其置于 `_ViewStart.cshtml` 文件中。</span><span class="sxs-lookup"><span data-stu-id="bf002-164">If you have code you need to run before every view, this should be placed in the `_ViewStart.cshtml` file.</span></span> <span data-ttu-id="bf002-165">按照约定，`_ViewStart.cshtml` 文件位于 `Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bf002-165">By convention, the `_ViewStart.cshtml` file is located in the `Views` folder.</span></span> <span data-ttu-id="bf002-166">在呈现每个完整视图（不是布局，也不是分部视图）之前运行 `_ViewStart.cshtml` 中列出的语句。</span><span class="sxs-lookup"><span data-stu-id="bf002-166">The statements listed in `_ViewStart.cshtml` are run before every full view (not layouts, and not partial views).</span></span> <span data-ttu-id="bf002-167">与 [ViewImports.cshtml](xref:mvc/views/layout#viewimports) 一样，`_ViewStart.cshtml` 是分层的。</span><span class="sxs-lookup"><span data-stu-id="bf002-167">Like [ViewImports.cshtml](xref:mvc/views/layout#viewimports), `_ViewStart.cshtml` is hierarchical.</span></span> <span data-ttu-id="bf002-168">如果在控制器关联的视图文件夹中定义了 `_ViewStart.cshtml` 文件，则将在 `Views` 文件夹根目录中定义的文件（如有）之后运行该文件。</span><span class="sxs-lookup"><span data-stu-id="bf002-168">If a `_ViewStart.cshtml` file is defined in the controller-associated view folder, it will be run after the one defined in the root of the `Views` folder (if any).</span></span>

<span data-ttu-id="bf002-169">示例 `_ViewStart.cshtml` 文件：</span><span class="sxs-lookup"><span data-stu-id="bf002-169">A sample `_ViewStart.cshtml` file:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml)]

<span data-ttu-id="bf002-170">上述文件指定所有视图都将使用 `_Layout.cshtml` 布局。</span><span class="sxs-lookup"><span data-stu-id="bf002-170">The file above specifies that all views will use the `_Layout.cshtml` layout.</span></span>

> [!NOTE]
> <span data-ttu-id="bf002-171">`_ViewStart.cshtml` 和 `_ViewImports.cshtml` 通常不会放置在 `/Views/Shared` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bf002-171">Neither `_ViewStart.cshtml` nor `_ViewImports.cshtml` are typically placed in the `/Views/Shared` folder.</span></span> <span data-ttu-id="bf002-172">这些应用级别版本的文件应直接放置在 `/Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bf002-172">The app-level versions of these files should be placed directly in the `/Views` folder.</span></span>
