---
title: "布局"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/layout
ms.openlocfilehash: 3e9e5949d8940a33508e24f0da015b49b7ba468c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="layout"></a><span data-ttu-id="f74f8-102">布局</span><span class="sxs-lookup"><span data-stu-id="f74f8-102">Layout</span></span>

<span data-ttu-id="f74f8-103">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="f74f8-103">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="f74f8-104">视图经常共享可视和编程元素。</span><span class="sxs-lookup"><span data-stu-id="f74f8-104">Views frequently share visual and programmatic elements.</span></span> <span data-ttu-id="f74f8-105">本文介绍如何在 ASP.NET 应用中呈现视图之前，使用通用布局、共享指令和运行常见代码。</span><span class="sxs-lookup"><span data-stu-id="f74f8-105">In this article, you'll learn how to use common layouts, share directives, and run common code before rendering views in your ASP.NET app.</span></span>

## <a name="what-is-a-layout"></a><span data-ttu-id="f74f8-106">什么是布局</span><span class="sxs-lookup"><span data-stu-id="f74f8-106">What is a Layout</span></span>

<span data-ttu-id="f74f8-107">大多数 Web 应用都有一个通用布局，可在页面间切换时为用户提供一致体验。</span><span class="sxs-lookup"><span data-stu-id="f74f8-107">Most web apps have a common layout that provides the user with a consistent experience as they navigate from page to page.</span></span> <span data-ttu-id="f74f8-108">该布局通常包括应用标头、导航或菜单元素以及页脚等常见的用户界面元素。</span><span class="sxs-lookup"><span data-stu-id="f74f8-108">The layout typically includes common user interface elements such as the app header, navigation or menu elements, and footer.</span></span>

![页面布局示例](layout/_static/page-layout.png)

<span data-ttu-id="f74f8-110">应用中的许多页面也经常使用脚本和样式表等常用的 HTML 结构。</span><span class="sxs-lookup"><span data-stu-id="f74f8-110">Common HTML structures such as scripts and stylesheets are also frequently used by many pages within an app.</span></span> <span data-ttu-id="f74f8-111">所有这些共享元素均可在布局文件中进行定义，应用内使用的任何视图随后均可引用此文件。</span><span class="sxs-lookup"><span data-stu-id="f74f8-111">All of these shared elements may be defined in a *layout* file, which can then be referenced by any view used within the app.</span></span> <span data-ttu-id="f74f8-112">布局可减少视图中的重复代码，帮助它们遵循[不要自我重复 (DRY) 原则](http://deviq.com/don-t-repeat-yourself/)。</span><span class="sxs-lookup"><span data-stu-id="f74f8-112">Layouts reduce duplicate code in views, helping them follow the [Don't Repeat Yourself (DRY) principle](http://deviq.com/don-t-repeat-yourself/).</span></span>

<span data-ttu-id="f74f8-113">按照约定，ASP.NET 应用的默认布局名为 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="f74f8-113">By convention, the default layout for an ASP.NET app is named `_Layout.cshtml`.</span></span> <span data-ttu-id="f74f8-114">Visual Studio ASP.NET Core MVC 项目模板在 `Views/Shared` 文件夹中包含此布局文件：</span><span class="sxs-lookup"><span data-stu-id="f74f8-114">The Visual Studio ASP.NET Core MVC project template includes this layout file in the `Views/Shared` folder:</span></span>

![解决方案资源管理器中的视图文件夹](layout/_static/web-project-views.png)

<span data-ttu-id="f74f8-116">此布局为应用中的视图定义顶级模板。</span><span class="sxs-lookup"><span data-stu-id="f74f8-116">This layout defines a top level template for views in the app.</span></span> <span data-ttu-id="f74f8-117">应用不需要布局，它们可以定义多个布局，并且不同的视图指定不同的布局。</span><span class="sxs-lookup"><span data-stu-id="f74f8-117">Apps don't require a layout, and apps can define more than one layout, with different views specifying different layouts.</span></span>

<span data-ttu-id="f74f8-118">示例 `_Layout.cshtml`：</span><span class="sxs-lookup"><span data-stu-id="f74f8-118">An example `_Layout.cshtml`:</span></span>

[!code-html[Main](../../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=42,66)]

## <a name="specifying-a-layout"></a><span data-ttu-id="f74f8-119">指定布局</span><span class="sxs-lookup"><span data-stu-id="f74f8-119">Specifying a Layout</span></span>

<span data-ttu-id="f74f8-120">Razor 视图具有 `Layout` 属性。</span><span class="sxs-lookup"><span data-stu-id="f74f8-120">Razor views have a `Layout` property.</span></span> <span data-ttu-id="f74f8-121">单个视图通过设置此属性来指定布局：</span><span class="sxs-lookup"><span data-stu-id="f74f8-121">Individual views specify a layout by setting this property:</span></span>

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewStart.cshtml?highlight=2)]

<span data-ttu-id="f74f8-122">指定的布局可以使用完整路径（例如：`/Views/Shared/_Layout.cshtml`）或部分名称（例如：`_Layout`）。</span><span class="sxs-lookup"><span data-stu-id="f74f8-122">The layout specified can use a full path (example: `/Views/Shared/_Layout.cshtml`) or a partial name (example: `_Layout`).</span></span> <span data-ttu-id="f74f8-123">如果提供部分名称，Razor 视图引擎将使用其标准发现过程来搜索布局文件。</span><span class="sxs-lookup"><span data-stu-id="f74f8-123">When a partial name is provided, the Razor view engine will search for the layout file using its standard discovery process.</span></span> <span data-ttu-id="f74f8-124">首先搜索与控制器关联的文件夹，然后搜索 `Shared` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="f74f8-124">The controller-associated folder is searched first, followed by the `Shared` folder.</span></span> <span data-ttu-id="f74f8-125">此发现过程与用于发现[分部视图](partial.md)的过程相同。</span><span class="sxs-lookup"><span data-stu-id="f74f8-125">This discovery process is identical to the one used to discover [partial views](partial.md).</span></span>

<span data-ttu-id="f74f8-126">默认情况下，每个布局必须调用 `RenderBody`。</span><span class="sxs-lookup"><span data-stu-id="f74f8-126">By default, every layout must call `RenderBody`.</span></span> <span data-ttu-id="f74f8-127">无论在何处调用 `RenderBody`，都会呈现视图的内容。</span><span class="sxs-lookup"><span data-stu-id="f74f8-127">Wherever the call to `RenderBody` is placed, the contents of the view will be rendered.</span></span>

<a name="layout-sections-label"></a>

### <a name="sections"></a><span data-ttu-id="f74f8-128">部分</span><span class="sxs-lookup"><span data-stu-id="f74f8-128">Sections</span></span>

<span data-ttu-id="f74f8-129">布局可以通过调用 `RenderSection` 来选择引用一个或多个节。</span><span class="sxs-lookup"><span data-stu-id="f74f8-129">A layout can optionally reference one or more *sections*, by calling `RenderSection`.</span></span> <span data-ttu-id="f74f8-130">节提供一种方法来组织某些页面元素应当放置的位置。</span><span class="sxs-lookup"><span data-stu-id="f74f8-130">Sections provide a way to organize where certain page elements should be placed.</span></span> <span data-ttu-id="f74f8-131">对 `RenderSection` 的每次调用均可指定该节是必需的还是可选的。</span><span class="sxs-lookup"><span data-stu-id="f74f8-131">Each call to `RenderSection` can specify whether that section is required or optional.</span></span> <span data-ttu-id="f74f8-132">如果找不到所需的节，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="f74f8-132">If a required section isn't found, an exception will be thrown.</span></span> <span data-ttu-id="f74f8-133">单个视图使用 `@section` Razor 语法指定要在节中呈现的内容。</span><span class="sxs-lookup"><span data-stu-id="f74f8-133">Individual views specify the content to be rendered within a section using the `@section` Razor syntax.</span></span> <span data-ttu-id="f74f8-134">如果视图定义某个节，则必须呈现该节（否则会发生错误）。</span><span class="sxs-lookup"><span data-stu-id="f74f8-134">If a view defines a section, it must be rendered (or an error will occur).</span></span>

<span data-ttu-id="f74f8-135">视图中的示例 `@section` 定义：</span><span class="sxs-lookup"><span data-stu-id="f74f8-135">An example `@section` definition in a view:</span></span>

```html
@section Scripts {
     <script type="text/javascript" src="/scripts/main.js"></script>
   }
   ```

<span data-ttu-id="f74f8-136">在上面的代码中，验证脚本添加到了视图（包含窗体）上的 `scripts` 节。</span><span class="sxs-lookup"><span data-stu-id="f74f8-136">In the code above, validation scripts are added to the `scripts` section on a view that includes a form.</span></span> <span data-ttu-id="f74f8-137">同一应用程序中的其他视图可能不需要任何其他脚本，因此无需定义脚本节。</span><span class="sxs-lookup"><span data-stu-id="f74f8-137">Other views in the same application might not require any additional scripts, and so wouldn't need to define a scripts section.</span></span>

<span data-ttu-id="f74f8-138">视图中定义的节仅在其即时布局页面中可用。</span><span class="sxs-lookup"><span data-stu-id="f74f8-138">Sections defined in a view are available only in its immediate layout page.</span></span> <span data-ttu-id="f74f8-139">不能从部分、视图组件或视图系统的其他部分引用它们。</span><span class="sxs-lookup"><span data-stu-id="f74f8-139">They cannot be referenced from partials, view components, or other parts of the view system.</span></span>

### <a name="ignoring-sections"></a><span data-ttu-id="f74f8-140">忽略节</span><span class="sxs-lookup"><span data-stu-id="f74f8-140">Ignoring sections</span></span>

<span data-ttu-id="f74f8-141">默认情况下，必须由布局页面呈现内容页中的正文和所有节。</span><span class="sxs-lookup"><span data-stu-id="f74f8-141">By default, the body and all sections in a content page must all be rendered by the layout page.</span></span> <span data-ttu-id="f74f8-142">Razor 视图引擎通过跟踪是否已呈现正文和每个节来强制执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f74f8-142">The Razor view engine enforces this by tracking whether the body and each section have been rendered.</span></span>

<span data-ttu-id="f74f8-143">要让视图引擎忽略正文或节，请调用 `IgnoreBody` 和 `IgnoreSection` 方法。</span><span class="sxs-lookup"><span data-stu-id="f74f8-143">To instruct the view engine to ignore the body or sections, call the `IgnoreBody` and `IgnoreSection` methods.</span></span>

<span data-ttu-id="f74f8-144">必须呈现或忽略 Razor 页面中的正文和每个节。</span><span class="sxs-lookup"><span data-stu-id="f74f8-144">The body and every section in a Razor page must be either rendered or ignored.</span></span>

<a name="viewimports"></a>

## <a name="importing-shared-directives"></a><span data-ttu-id="f74f8-145">导入共享指令</span><span class="sxs-lookup"><span data-stu-id="f74f8-145">Importing Shared Directives</span></span>

<span data-ttu-id="f74f8-146">视图可以使用 Razor 指令来执行许多操作，例如导入命名空间或执行[依赖关系注入](dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="f74f8-146">Views can use Razor directives to do many things, such as importing namespaces or performing [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="f74f8-147">可在一个共同的 `_ViewImports.cshtml` 文件中指定由许多视图共享的指令。</span><span class="sxs-lookup"><span data-stu-id="f74f8-147">Directives shared by many views may be specified in a common `_ViewImports.cshtml` file.</span></span> <span data-ttu-id="f74f8-148">`_ViewImports` 文件支持以下指令：</span><span class="sxs-lookup"><span data-stu-id="f74f8-148">The `_ViewImports` file supports the following directives:</span></span>

* `@addTagHelper`

* `@removeTagHelper`

* `@tagHelperPrefix`

* `@using`

* `@model`

* `@inherits`

* `@inject`

<span data-ttu-id="f74f8-149">该文件不支持函数和节定义等其他 Razor 功能。</span><span class="sxs-lookup"><span data-stu-id="f74f8-149">The file doesn't support other Razor features, such as functions and section definitions.</span></span>

<span data-ttu-id="f74f8-150">示例 `_ViewImports.cshtml` 文件：</span><span class="sxs-lookup"><span data-stu-id="f74f8-150">A sample `_ViewImports.cshtml` file:</span></span>

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewImports.cshtml)]

<span data-ttu-id="f74f8-151">针对 ASP.NET Core MVC 应用的 `_ViewImports.cshtml` 文件通常放置在 `Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f74f8-151">The `_ViewImports.cshtml` file for an ASP.NET Core MVC app is typically placed in the `Views` folder.</span></span> <span data-ttu-id="f74f8-152">`_ViewImports.cshtml` 文件可以放置在任何文件夹中，在这种情况下，它仅适用于该文件夹及其子文件夹中的视图。</span><span class="sxs-lookup"><span data-stu-id="f74f8-152">A `_ViewImports.cshtml` file can be placed within any folder, in which case it will only be applied to views within that folder and its subfolders.</span></span> <span data-ttu-id="f74f8-153">由于从根级别开始处理 `_ViewImports` 文件，然后处理视图本身的位置之前的每个文件夹，因此在根级别指定的设置可能会覆盖在文件夹级别。</span><span class="sxs-lookup"><span data-stu-id="f74f8-153">`_ViewImports` files are processed starting at the root level, and then for each folder leading up to the location of the view itself, so settings specified at the root level may be overridden at the folder level.</span></span>

<span data-ttu-id="f74f8-154">例如，如果根级别 `_ViewImports.cshtml` 文件指定 `@model` 和 `@addTagHelper`，在该视图的控制器关联文件夹中，另一个 `_ViewImports.cshtml` 文件指定不同的 `@model` 并添加另一个 `@addTagHelper`，该视图将有权访问这两个标记帮助程序，并将使用后一个 `@model`。</span><span class="sxs-lookup"><span data-stu-id="f74f8-154">For example, if a root level `_ViewImports.cshtml` file specifies `@model` and `@addTagHelper`, and another `_ViewImports.cshtml` file in the controller-associated folder of the view specifies a different `@model` and adds another `@addTagHelper`, the view will have access to both tag helpers and will use the latter `@model`.</span></span>

<span data-ttu-id="f74f8-155">如果对一个视图运行多个 `_ViewImports.cshtml` 文件，那么包含在 `ViewImports.cshtml` 文件中的指令的组合行为如下所示：</span><span class="sxs-lookup"><span data-stu-id="f74f8-155">If multiple `_ViewImports.cshtml` files are run for a view, combined behavior of the directives included in the `ViewImports.cshtml` files will be as follows:</span></span>

* <span data-ttu-id="f74f8-156">`@addTagHelper``@removeTagHelper`：按顺序全部运行</span><span class="sxs-lookup"><span data-stu-id="f74f8-156">`@addTagHelper`, `@removeTagHelper`: all run, in order</span></span>

* <span data-ttu-id="f74f8-157">`@tagHelperPrefix`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="f74f8-157">`@tagHelperPrefix`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="f74f8-158">`@model`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="f74f8-158">`@model`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="f74f8-159">`@inherits`：最接近视图的文件会替代任何其他文件</span><span class="sxs-lookup"><span data-stu-id="f74f8-159">`@inherits`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="f74f8-160">`@using`：全部包括在内；忽略重复项</span><span class="sxs-lookup"><span data-stu-id="f74f8-160">`@using`: all are included; duplicates are ignored</span></span>

* <span data-ttu-id="f74f8-161">`@inject`：针对每个属性，最接近视图的属性会替代具有相同属性名的任何其他属性</span><span class="sxs-lookup"><span data-stu-id="f74f8-161">`@inject`: for each property, the closest one to the view overrides any others with the same property name</span></span>

<a name="viewstart"></a>

## <a name="running-code-before-each-view"></a><span data-ttu-id="f74f8-162">在呈现每个视图之前运行代码</span><span class="sxs-lookup"><span data-stu-id="f74f8-162">Running Code Before Each View</span></span>

<span data-ttu-id="f74f8-163">如果有需要在呈现每个视图之前运行的代码，应将其置于 `_ViewStart.cshtml` 文件中。</span><span class="sxs-lookup"><span data-stu-id="f74f8-163">If you have code you need to run before every view, this should be placed in the `_ViewStart.cshtml` file.</span></span> <span data-ttu-id="f74f8-164">按照约定，`_ViewStart.cshtml` 文件位于 `Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f74f8-164">By convention, the `_ViewStart.cshtml` file is located in the `Views` folder.</span></span> <span data-ttu-id="f74f8-165">在呈现每个完整视图（不是布局，也不是分部视图）之前运行 `_ViewStart.cshtml` 中列出的语句。</span><span class="sxs-lookup"><span data-stu-id="f74f8-165">The statements listed in `_ViewStart.cshtml` are run before every full view (not layouts, and not partial views).</span></span> <span data-ttu-id="f74f8-166">与 [ViewImports.cshtml](xref:mvc/views/layout#viewimports) 一样，`_ViewStart.cshtml` 是分层的。</span><span class="sxs-lookup"><span data-stu-id="f74f8-166">Like [ViewImports.cshtml](xref:mvc/views/layout#viewimports), `_ViewStart.cshtml` is hierarchical.</span></span> <span data-ttu-id="f74f8-167">如果在控制器关联的视图文件夹中定义了 `_ViewStart.cshtml` 文件，则将在 `Views` 文件夹根目录中定义的文件（如有）之后运行该文件。</span><span class="sxs-lookup"><span data-stu-id="f74f8-167">If a `_ViewStart.cshtml` file is defined in the controller-associated view folder, it will be run after the one defined in the root of the `Views` folder (if any).</span></span>

<span data-ttu-id="f74f8-168">示例 `_ViewStart.cshtml` 文件：</span><span class="sxs-lookup"><span data-stu-id="f74f8-168">A sample `_ViewStart.cshtml` file:</span></span>

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewStart.cshtml)]

<span data-ttu-id="f74f8-169">上述文件指定所有视图都将使用 `_Layout.cshtml` 布局。</span><span class="sxs-lookup"><span data-stu-id="f74f8-169">The file above specifies that all views will use the `_Layout.cshtml` layout.</span></span>

> [!NOTE]
> <span data-ttu-id="f74f8-170">`_ViewStart.cshtml` 和 `_ViewImports.cshtml` 通常不会放置在 `/Views/Shared` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f74f8-170">Neither `_ViewStart.cshtml` nor `_ViewImports.cshtml` are typically placed in the `/Views/Shared` folder.</span></span> <span data-ttu-id="f74f8-171">这些应用级别版本的文件应直接放置在 `/Views` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f74f8-171">The app-level versions of these files should be placed directly in the `/Views` folder.</span></span>
