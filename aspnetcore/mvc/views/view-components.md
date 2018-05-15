---
title: ASP.NET Core 中的视图组件
author: rick-anderson
description: 了解如何在 ASP.NET Core 中使用视图组件，以及如何将其添加到应用中。
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-components
ms.openlocfilehash: a3614024c7f776e4502bc049180ae1c965e31db4
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="view-components-in-aspnet-core"></a><span data-ttu-id="98e3b-103">ASP.NET Core 中的视图组件</span><span class="sxs-lookup"><span data-stu-id="98e3b-103">View components in ASP.NET Core</span></span>

<span data-ttu-id="98e3b-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="98e3b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="98e3b-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="98e3b-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="introducing-view-components"></a><span data-ttu-id="98e3b-106">视图组件简介</span><span class="sxs-lookup"><span data-stu-id="98e3b-106">Introducing view components</span></span>

<span data-ttu-id="98e3b-107">作为 ASP.NET Core MVC 的新功能，视图组件与分部视图类似，但它们的功能更加强大。</span><span class="sxs-lookup"><span data-stu-id="98e3b-107">New to ASP.NET Core MVC, view components are similar to partial views, but they're much more powerful.</span></span> <span data-ttu-id="98e3b-108">视图组件不使用模型绑定，并且仅依赖调用时提供的数据。</span><span class="sxs-lookup"><span data-stu-id="98e3b-108">View components don't use model binding, and only depend on the data provided when calling into it.</span></span> <span data-ttu-id="98e3b-109">视图组件：</span><span class="sxs-lookup"><span data-stu-id="98e3b-109">A view component:</span></span>

* <span data-ttu-id="98e3b-110">呈现一个区块而不是整个响应。</span><span class="sxs-lookup"><span data-stu-id="98e3b-110">Renders a chunk rather than a whole response.</span></span>
* <span data-ttu-id="98e3b-111">包括控制器和视图间发现的相同关注点分离和可测试性优势。</span><span class="sxs-lookup"><span data-stu-id="98e3b-111">Includes the same separation-of-concerns and testability benefits found between a controller and view.</span></span>
* <span data-ttu-id="98e3b-112">可以有参数和业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="98e3b-112">Can have parameters and business logic.</span></span>
* <span data-ttu-id="98e3b-113">通常从布局页调用。</span><span class="sxs-lookup"><span data-stu-id="98e3b-113">Is typically invoked from a layout page.</span></span>

<span data-ttu-id="98e3b-114">视图组件可用于具有可重用呈现逻辑（对分部视图来说过于复杂）的任何位置，例如：</span><span class="sxs-lookup"><span data-stu-id="98e3b-114">View components are intended anywhere you have reusable rendering logic that's too complex for a partial view, such as:</span></span>

* <span data-ttu-id="98e3b-115">动态导航菜单</span><span class="sxs-lookup"><span data-stu-id="98e3b-115">Dynamic navigation menus</span></span>
* <span data-ttu-id="98e3b-116">标记云（查询数据库的位置）</span><span class="sxs-lookup"><span data-stu-id="98e3b-116">Tag cloud (where it queries the database)</span></span>
* <span data-ttu-id="98e3b-117">登录面板</span><span class="sxs-lookup"><span data-stu-id="98e3b-117">Login panel</span></span>
* <span data-ttu-id="98e3b-118">购物车</span><span class="sxs-lookup"><span data-stu-id="98e3b-118">Shopping cart</span></span>
* <span data-ttu-id="98e3b-119">最近发布的文章</span><span class="sxs-lookup"><span data-stu-id="98e3b-119">Recently published articles</span></span>
* <span data-ttu-id="98e3b-120">典型博客上的边栏内容</span><span class="sxs-lookup"><span data-stu-id="98e3b-120">Sidebar content on a typical blog</span></span>
* <span data-ttu-id="98e3b-121">一个登录面板，呈现在每页上并显示注销或登录链接，具体取决于用户的登录状态</span><span class="sxs-lookup"><span data-stu-id="98e3b-121">A login panel that would be rendered on every page and show either the links to log out or log in, depending on the log in state of the user</span></span>

<span data-ttu-id="98e3b-122">视图组件由两部分组成：类（通常派生自 [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)）及其返回的结果（通常为视图）。</span><span class="sxs-lookup"><span data-stu-id="98e3b-122">A view component consists of two parts: the class (typically derived from [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) and the result it returns (typically a view).</span></span> <span data-ttu-id="98e3b-123">与控制器一样，视图组件也可以是 POCO，但大多数开发人员都希望利用派生自 `ViewComponent` 的可用方法和属性。</span><span class="sxs-lookup"><span data-stu-id="98e3b-123">Like controllers, a view component can be a POCO, but most developers will want to take advantage of the methods and properties available by deriving from `ViewComponent`.</span></span>

## <a name="creating-a-view-component"></a><span data-ttu-id="98e3b-124">创建视图组件</span><span class="sxs-lookup"><span data-stu-id="98e3b-124">Creating a view component</span></span>

<span data-ttu-id="98e3b-125">本部分包含创建视图组件的高级别要求。</span><span class="sxs-lookup"><span data-stu-id="98e3b-125">This section contains the high-level requirements to create a view component.</span></span> <span data-ttu-id="98e3b-126">本文后续部分将详细检查每个步骤并创建视图组件。</span><span class="sxs-lookup"><span data-stu-id="98e3b-126">Later in the article, we'll examine each step in detail and create a view component.</span></span>

### <a name="the-view-component-class"></a><span data-ttu-id="98e3b-127">视图组件类</span><span class="sxs-lookup"><span data-stu-id="98e3b-127">The view component class</span></span>

<span data-ttu-id="98e3b-128">可通过以下任一方法创建视图组件类：</span><span class="sxs-lookup"><span data-stu-id="98e3b-128">A view component class can be created by any of the following:</span></span>

* <span data-ttu-id="98e3b-129">从 ViewComponent 派生</span><span class="sxs-lookup"><span data-stu-id="98e3b-129">Deriving from *ViewComponent*</span></span>
* <span data-ttu-id="98e3b-130">使用 `[ViewComponent]` 属性修饰类，或者从具有 `[ViewComponent]` 属性的类派生</span><span class="sxs-lookup"><span data-stu-id="98e3b-130">Decorating a class with the `[ViewComponent]` attribute, or deriving from a class with the `[ViewComponent]` attribute</span></span>
* <span data-ttu-id="98e3b-131">创建名称以 ViewComponent 后缀结尾的类</span><span class="sxs-lookup"><span data-stu-id="98e3b-131">Creating a class where the name ends with the suffix *ViewComponent*</span></span>

<span data-ttu-id="98e3b-132">与控制器一样，视图组件必须是公共、非嵌套和非抽象的类。</span><span class="sxs-lookup"><span data-stu-id="98e3b-132">Like controllers, view components must be public, non-nested, and non-abstract classes.</span></span> <span data-ttu-id="98e3b-133">视图组件名称是删除了“ViewComponent”后缀的类名。</span><span class="sxs-lookup"><span data-stu-id="98e3b-133">The view component name is the class name with the "ViewComponent" suffix removed.</span></span> <span data-ttu-id="98e3b-134">也可以使用 `ViewComponentAttribute.Name` 属性显式指定它。</span><span class="sxs-lookup"><span data-stu-id="98e3b-134">It can also be explicitly specified using the `ViewComponentAttribute.Name` property.</span></span>

<span data-ttu-id="98e3b-135">视图组件类：</span><span class="sxs-lookup"><span data-stu-id="98e3b-135">A view component class:</span></span>

* <span data-ttu-id="98e3b-136">完全支持构造函数[依赖关系注入](../../fundamentals/dependency-injection.md)</span><span class="sxs-lookup"><span data-stu-id="98e3b-136">Fully supports constructor [dependency injection](../../fundamentals/dependency-injection.md)</span></span>

* <span data-ttu-id="98e3b-137">不参与控制器生命周期，这意味着不能在视图组件中使用[筛选器](../controllers/filters.md)</span><span class="sxs-lookup"><span data-stu-id="98e3b-137">Doesn't take part in the controller lifecycle, which means you can't use [filters](../controllers/filters.md) in a view component</span></span>

### <a name="view-component-methods"></a><span data-ttu-id="98e3b-138">视图组件方法</span><span class="sxs-lookup"><span data-stu-id="98e3b-138">View component methods</span></span>

<span data-ttu-id="98e3b-139">视图组件以返回 `InvokeAsync` 的 `IViewComponentResult` 方法定义其逻辑。</span><span class="sxs-lookup"><span data-stu-id="98e3b-139">A view component defines its logic in an `InvokeAsync` method that returns an `IViewComponentResult`.</span></span> <span data-ttu-id="98e3b-140">参数直接来自视图组件的调用，而不是来自模型绑定。</span><span class="sxs-lookup"><span data-stu-id="98e3b-140">Parameters come directly from invocation of the view component, not from model binding.</span></span> <span data-ttu-id="98e3b-141">视图组件从不直接处理请求。</span><span class="sxs-lookup"><span data-stu-id="98e3b-141">A view component never directly handles a request.</span></span> <span data-ttu-id="98e3b-142">通常，视图组件通过调用 `View` 方法来初始化模型并将其传递到视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-142">Typically, a view component initializes a model and passes it to a view by calling the `View` method.</span></span> <span data-ttu-id="98e3b-143">总之，视图组件方法：</span><span class="sxs-lookup"><span data-stu-id="98e3b-143">In summary, view component methods:</span></span>

* <span data-ttu-id="98e3b-144">定义返回 `IViewComponentResult` 的 `InvokeAsync` 方法</span><span class="sxs-lookup"><span data-stu-id="98e3b-144">Define an `InvokeAsync` method that returns an `IViewComponentResult`</span></span>
* <span data-ttu-id="98e3b-145">一般通过调用 `ViewComponent` `View` 方法来初始化模型并将其传递到视图</span><span class="sxs-lookup"><span data-stu-id="98e3b-145">Typically initializes a model and passes it to a view by calling the `ViewComponent` `View` method</span></span>
* <span data-ttu-id="98e3b-146">参数来自调用方法，而不是 HTTP，没有模型绑定</span><span class="sxs-lookup"><span data-stu-id="98e3b-146">Parameters come from the calling method, not HTTP, there's no model binding</span></span>
* <span data-ttu-id="98e3b-147">不可直接作为 HTTP 终结点访问，它们从代码调用（通常在视图中）。</span><span class="sxs-lookup"><span data-stu-id="98e3b-147">Are not reachable directly as an HTTP endpoint, they're invoked from your code (usually in a view).</span></span> <span data-ttu-id="98e3b-148">视图组件从不处理请求</span><span class="sxs-lookup"><span data-stu-id="98e3b-148">A view component never handles a request</span></span>
* <span data-ttu-id="98e3b-149">在签名上重载，而不是当前 HTTP 请求的任何详细信息</span><span class="sxs-lookup"><span data-stu-id="98e3b-149">Are overloaded on the signature rather than any details from the current HTTP request</span></span>

### <a name="view-search-path"></a><span data-ttu-id="98e3b-150">视图搜索路径</span><span class="sxs-lookup"><span data-stu-id="98e3b-150">View search path</span></span>

<span data-ttu-id="98e3b-151">运行时在以下路径中搜索视图：</span><span class="sxs-lookup"><span data-stu-id="98e3b-151">The runtime searches for the view in the following paths:</span></span>

   * <span data-ttu-id="98e3b-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="98e3b-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span></span>
   * <span data-ttu-id="98e3b-153">Views/Shared/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="98e3b-153">Views/Shared/Components/\<view_component_name>/\<view_name></span></span>

<span data-ttu-id="98e3b-154">视图组件的默认视图名称为“默认”，这意味着视图文件通常命名为“Default.cshtml”。</span><span class="sxs-lookup"><span data-stu-id="98e3b-154">The default view name for a view component is *Default*, which means your view file will typically be named *Default.cshtml*.</span></span> <span data-ttu-id="98e3b-155">可以在创建视图组件结果或调用 `View` 方法时指定不同的视图名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-155">You can specify a different view name when creating the view component result or when calling the `View` method.</span></span>

<span data-ttu-id="98e3b-156">建议将视图文件命名为“Default.cshtml”并使用 Views/Shared/Components/\<view_component_name>/\<view_name> 路径。</span><span class="sxs-lookup"><span data-stu-id="98e3b-156">We recommend you name the view file *Default.cshtml* and use the *Views/Shared/Components/\<view_component_name>/\<view_name>* path.</span></span> <span data-ttu-id="98e3b-157">此示例中使用的 `PriorityList` 视图组件对视图组件视图使用 Views/Shared/Components/PriorityList/Default.cshtml。</span><span class="sxs-lookup"><span data-stu-id="98e3b-157">The `PriorityList` view component used in this sample uses *Views/Shared/Components/PriorityList/Default.cshtml* for the view component view.</span></span>

## <a name="invoking-a-view-component"></a><span data-ttu-id="98e3b-158">调用视图组件</span><span class="sxs-lookup"><span data-stu-id="98e3b-158">Invoking a view component</span></span>

<span data-ttu-id="98e3b-159">要使用视图组件，请在视图中调用以下内容：</span><span class="sxs-lookup"><span data-stu-id="98e3b-159">To use the view component, call the following inside a view:</span></span>

```cshtml
@Component.InvokeAsync("Name of view component", <anonymous type containing parameters>)
```

<span data-ttu-id="98e3b-160">参数将传递给 `InvokeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="98e3b-160">The parameters will be passed to the `InvokeAsync` method.</span></span> <span data-ttu-id="98e3b-161">本文中开发的 `PriorityList` 视图组件是从 Views/Todo/Index.cshtml 视图文件中调用的。</span><span class="sxs-lookup"><span data-stu-id="98e3b-161">The `PriorityList` view component developed in the article is invoked from the *Views/Todo/Index.cshtml* view file.</span></span> <span data-ttu-id="98e3b-162">在下例中，使用两个参数调用 `InvokeAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="98e3b-162">In the following, the `InvokeAsync` method is called with two parameters:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

## <a name="invoking-a-view-component-as-a-tag-helper"></a><span data-ttu-id="98e3b-163">调用视图组件作为标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="98e3b-163">Invoking a view component as a Tag Helper</span></span>

<span data-ttu-id="98e3b-164">对于 ASP.NET Core 1.1 及更高版本，可以调用视图组件作为[标记帮助程序](xref:mvc/views/tag-helpers/intro)：</span><span class="sxs-lookup"><span data-stu-id="98e3b-164">For ASP.NET Core 1.1 and higher, you can invoke a view component as a [Tag Helper](xref:mvc/views/tag-helpers/intro):</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="98e3b-165">标记帮助程序采用 Pascal 大小写格式的类和方法参数将转换为各自相应的[小写短横线格式](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101)。</span><span class="sxs-lookup"><span data-stu-id="98e3b-165">Pascal-cased class and method parameters for Tag Helpers are translated into their [lower kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="98e3b-166">要调用视图组件的标记帮助程序使用 `<vc></vc>` 元素。</span><span class="sxs-lookup"><span data-stu-id="98e3b-166">The Tag Helper to invoke a view component uses the `<vc></vc>` element.</span></span> <span data-ttu-id="98e3b-167">按如下方式指定视图组件：</span><span class="sxs-lookup"><span data-stu-id="98e3b-167">The view component is specified as follows:</span></span>

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

<span data-ttu-id="98e3b-168">注意：为了将视图组件用作标记帮助程序，必须使用 `@addTagHelper` 指令注册包含视图组件的程序集。</span><span class="sxs-lookup"><span data-stu-id="98e3b-168">Note: In order to use a View Component as a Tag Helper, you must register the assembly containing the View Component using the `@addTagHelper` directive.</span></span> <span data-ttu-id="98e3b-169">例如，如果视图组件位于名为“MyWebApp”的程序集中，请将以下指令添加到 `_ViewImports.cshtml` 文件：</span><span class="sxs-lookup"><span data-stu-id="98e3b-169">For example, if your View Component is in an assembly called "MyWebApp", add the following directive to the `_ViewImports.cshtml` file:</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="98e3b-170">可将视图组件作为标记帮助程序注册到任何引用视图组件的文件。</span><span class="sxs-lookup"><span data-stu-id="98e3b-170">You can register a View Component as a Tag Helper to any file that references the View Component.</span></span> <span data-ttu-id="98e3b-171">要详细了解如何注册标记帮助程序，请参阅[管理标记帮助程序作用域](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope)。</span><span class="sxs-lookup"><span data-stu-id="98e3b-171">See [Managing Tag Helper Scope](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) for more information on how to register Tag Helpers.</span></span>

<span data-ttu-id="98e3b-172">本教程中使用的 `InvokeAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="98e3b-172">The `InvokeAsync` method used in this tutorial:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="98e3b-173">在标记帮助程序标记中：</span><span class="sxs-lookup"><span data-stu-id="98e3b-173">In Tag Helper markup:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="98e3b-174">在以上示例中，`PriorityList` 视图组件变为 `priority-list`。</span><span class="sxs-lookup"><span data-stu-id="98e3b-174">In the sample above, the `PriorityList` view component becomes `priority-list`.</span></span> <span data-ttu-id="98e3b-175">视图组件的参数作为小写短横线格式的属性进行传递。</span><span class="sxs-lookup"><span data-stu-id="98e3b-175">The parameters to the view component are passed as attributes in lower kebab case.</span></span>

### <a name="invoking-a-view-component-directly-from-a-controller"></a><span data-ttu-id="98e3b-176">从控制器直接调用视图组件</span><span class="sxs-lookup"><span data-stu-id="98e3b-176">Invoking a view component directly from a controller</span></span>

<span data-ttu-id="98e3b-177">视图组件通常从视图调用，但你可以直接从控制器方法调用它们。</span><span class="sxs-lookup"><span data-stu-id="98e3b-177">View components are typically invoked from a view, but you can invoke them directly from a controller method.</span></span> <span data-ttu-id="98e3b-178">尽管视图组件不定义控制器等终结点，但你可以轻松实现返回 `ViewComponentResult` 内容的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="98e3b-178">While view components don't define endpoints like controllers, you can easily implement a controller action that returns the content of a `ViewComponentResult`.</span></span>

<span data-ttu-id="98e3b-179">在此示例中，视图组件直接从控制器调用：</span><span class="sxs-lookup"><span data-stu-id="98e3b-179">In this example, the view component is called directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a><span data-ttu-id="98e3b-180">演练：创建简单的视图组件</span><span class="sxs-lookup"><span data-stu-id="98e3b-180">Walkthrough: Creating a simple view component</span></span>

<span data-ttu-id="98e3b-181">[下载](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)、生成和测试起始代码。</span><span class="sxs-lookup"><span data-stu-id="98e3b-181">[Download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), build and test the starter code.</span></span> <span data-ttu-id="98e3b-182">它是一个带有 `Todo` 控制器的简单项目，该控制器显示 Todo 项的列表。</span><span class="sxs-lookup"><span data-stu-id="98e3b-182">It's a simple project with a `Todo` controller that displays a list of *Todo* items.</span></span>

![ToDo 列表](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a><span data-ttu-id="98e3b-184">添加 ViewComponent 类</span><span class="sxs-lookup"><span data-stu-id="98e3b-184">Add a ViewComponent class</span></span>

<span data-ttu-id="98e3b-185">创建一个 ViewComponents 文件夹并添加以下 `PriorityListViewComponent` 类：</span><span class="sxs-lookup"><span data-stu-id="98e3b-185">Create a *ViewComponents* folder and add the following `PriorityListViewComponent` class:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

<span data-ttu-id="98e3b-186">代码说明：</span><span class="sxs-lookup"><span data-stu-id="98e3b-186">Notes on the code:</span></span>

* <span data-ttu-id="98e3b-187">视图组件类可以包含在项目的任意文件夹中。</span><span class="sxs-lookup"><span data-stu-id="98e3b-187">View component classes can be contained in **any** folder in the project.</span></span>
* <span data-ttu-id="98e3b-188">因为类名 PriorityListViewComponent 以后缀 ViewComponent 结尾，所以运行时将在从视图引用类组件时使用字符串“PriorityList”。</span><span class="sxs-lookup"><span data-stu-id="98e3b-188">Because the class name PriorityList**ViewComponent** ends with the suffix **ViewComponent**, the runtime will use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="98e3b-189">我稍后将进行详细解释。</span><span class="sxs-lookup"><span data-stu-id="98e3b-189">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="98e3b-190">`[ViewComponent]` 属性可以更改用于引用视图组件的名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-190">The `[ViewComponent]` attribute can change the name used to reference a view component.</span></span> <span data-ttu-id="98e3b-191">例如，我们可以将类命名为 `XYZ` 并应用 `ViewComponent` 属性：</span><span class="sxs-lookup"><span data-stu-id="98e3b-191">For example, we could've named the class `XYZ` and applied the `ViewComponent` attribute:</span></span>

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* <span data-ttu-id="98e3b-192">上面的 `[ViewComponent]` 属性通知视图组件选择器在查找与组件相关联的视图时使用名称 `PriorityList`，以及在从视图引用类组件时使用字符串“PriorityList”。</span><span class="sxs-lookup"><span data-stu-id="98e3b-192">The `[ViewComponent]` attribute above tells the view component selector to use the name `PriorityList` when looking for the views associated with the component, and to use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="98e3b-193">我稍后将进行详细解释。</span><span class="sxs-lookup"><span data-stu-id="98e3b-193">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="98e3b-194">组件使用[依赖关系注入](../../fundamentals/dependency-injection.md)以使数据上下文可用。</span><span class="sxs-lookup"><span data-stu-id="98e3b-194">The component uses [dependency injection](../../fundamentals/dependency-injection.md) to make the data context available.</span></span>
* <span data-ttu-id="98e3b-195">`InvokeAsync` 公开可以从视图调用的方法，且可以采用任意数量的参数。</span><span class="sxs-lookup"><span data-stu-id="98e3b-195">`InvokeAsync` exposes a method which can be called from a view, and it can take an arbitrary number of arguments.</span></span>
* <span data-ttu-id="98e3b-196">`InvokeAsync` 方法返回满足 `isDone` 和 `maxPriority` 参数的 `ToDo` 项集。</span><span class="sxs-lookup"><span data-stu-id="98e3b-196">The `InvokeAsync` method returns the set of `ToDo` items that satisfy the `isDone` and `maxPriority` parameters.</span></span>

### <a name="create-the-view-component-razor-view"></a><span data-ttu-id="98e3b-197">创建视图组件 Razor 视图</span><span class="sxs-lookup"><span data-stu-id="98e3b-197">Create the view component Razor view</span></span>

* <span data-ttu-id="98e3b-198">创建 Views/Shared/Components 文件夹。</span><span class="sxs-lookup"><span data-stu-id="98e3b-198">Create the *Views/Shared/Components* folder.</span></span> <span data-ttu-id="98e3b-199">此文件夹 **必须** 命名为 *Components*。</span><span class="sxs-lookup"><span data-stu-id="98e3b-199">This folder **must** be named *Components*.</span></span>

* <span data-ttu-id="98e3b-200">创建 Views/Shared/Components/PriorityList 文件夹。</span><span class="sxs-lookup"><span data-stu-id="98e3b-200">Create the *Views/Shared/Components/PriorityList* folder.</span></span> <span data-ttu-id="98e3b-201">此文件夹名称必须与视图组件类的名称或类名去掉后缀（如果遵照约定并在类名中使用了“ViewComponent”后缀）的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="98e3b-201">This folder name must match the name of the view component class, or the name of the class minus the suffix (if we followed convention and used the *ViewComponent* suffix in the class name).</span></span> <span data-ttu-id="98e3b-202">如果使用了 `ViewComponent` 属性，则类名称需要匹配指定的属性。</span><span class="sxs-lookup"><span data-stu-id="98e3b-202">If you used the `ViewComponent` attribute, the class name would need to match the attribute designation.</span></span>

* <span data-ttu-id="98e3b-203">创建 Views/Shared/Components/PriorityList/Default.cshtml Razor 视图：[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="98e3b-203">Create a *Views/Shared/Components/PriorityList/Default.cshtml* Razor view: [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span></span>
    
   <span data-ttu-id="98e3b-204">Razor 视图获取并显示 `TodoItem` 列表。</span><span class="sxs-lookup"><span data-stu-id="98e3b-204">The Razor view takes a list of `TodoItem` and displays them.</span></span> <span data-ttu-id="98e3b-205">如果视图组件 `InvokeAsync` 方法不传递视图名称（如示例中所示），则按照约定使用“默认”作为视图名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-205">If the view component `InvokeAsync` method doesn't pass the name of the view (as in our sample), *Default* is used for the view name by convention.</span></span> <span data-ttu-id="98e3b-206">在本教程后面部分，我将演示如何传递视图名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-206">Later in the tutorial, I'll show you how to pass the name of the view.</span></span> <span data-ttu-id="98e3b-207">要替代特定控制器的默认样式，请将视图添加到控制器特定的视图文件夹（例如 Views/Todo/Components/PriorityList/Default.cshtml）。</span><span class="sxs-lookup"><span data-stu-id="98e3b-207">To override the default styling for a specific controller, add a view to the controller-specific view folder (for example *Views/Todo/Components/PriorityList/Default.cshtml)*.</span></span>
    
    <span data-ttu-id="98e3b-208">如果视图组件是控制器特定的，则可将其添加到控制器特定的文件夹 (Views/Todo/Components/PriorityList/Default.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="98e3b-208">If the view component is controller-specific, you can add it to the controller-specific folder (*Views/Todo/Components/PriorityList/Default.cshtml*).</span></span>

* <span data-ttu-id="98e3b-209">将包含优先级列表组件调用的 `div` 添加到 Views/Todo/index.cshtml 文件底部：</span><span class="sxs-lookup"><span data-stu-id="98e3b-209">Add a `div` containing a call to the priority list component to the bottom of the *Views/Todo/index.cshtml* file:</span></span>

    [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFirst.cshtml?range=34-38)]

<span data-ttu-id="98e3b-210">标记 `@await Component.InvokeAsync` 显示调用视图组件的语法。</span><span class="sxs-lookup"><span data-stu-id="98e3b-210">The markup `@await Component.InvokeAsync` shows the syntax for calling view components.</span></span> <span data-ttu-id="98e3b-211">第一个参数是要调用的组件的名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-211">The first argument is the name of the component we want to invoke or call.</span></span> <span data-ttu-id="98e3b-212">后续参数将传递给该组件。</span><span class="sxs-lookup"><span data-stu-id="98e3b-212">Subsequent parameters are passed to the component.</span></span> <span data-ttu-id="98e3b-213">`InvokeAsync` 可以采用任意数量的参数。</span><span class="sxs-lookup"><span data-stu-id="98e3b-213">`InvokeAsync` can take an arbitrary number of arguments.</span></span>

<span data-ttu-id="98e3b-214">测试应用。</span><span class="sxs-lookup"><span data-stu-id="98e3b-214">Test the app.</span></span> <span data-ttu-id="98e3b-215">下图显示 ToDo 列表和优先级项：</span><span class="sxs-lookup"><span data-stu-id="98e3b-215">The following image shows the ToDo list and the priority items:</span></span>

![Todo 列表和优先级项](view-components/_static/pi.png)

<span data-ttu-id="98e3b-217">也可直接从控制器调用视图组件：</span><span class="sxs-lookup"><span data-stu-id="98e3b-217">You can also call the view component directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![IndexVC 操作的优先级项](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a><span data-ttu-id="98e3b-219">指定视图名称</span><span class="sxs-lookup"><span data-stu-id="98e3b-219">Specifying a view name</span></span>

<span data-ttu-id="98e3b-220">在某些情况下，复杂的视图组件可能需要指定非默认视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-220">A complex view component might need to specify a non-default view under some conditions.</span></span> <span data-ttu-id="98e3b-221">以下代码显示如何从 `InvokeAsync` 方法指定“PVC”视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-221">The following code shows how to specify the "PVC" view  from the `InvokeAsync` method.</span></span> <span data-ttu-id="98e3b-222">更新 `PriorityListViewComponent` 类中的 `InvokeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="98e3b-222">Update the `InvokeAsync` method in the `PriorityListViewComponent` class.</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

<span data-ttu-id="98e3b-223">将 Views/Shared/Components/PriorityList/Default.cshtml 文件复制到名为 Views/Shared/Components/PriorityList/PVC.cshtml 的视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-223">Copy the *Views/Shared/Components/PriorityList/Default.cshtml* file to a view named *Views/Shared/Components/PriorityList/PVC.cshtml*.</span></span> <span data-ttu-id="98e3b-224">添加标题以指示正在使用 PVC 视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-224">Add a heading to indicate the PVC view is being used.</span></span>

[!code-cshtml[](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

<span data-ttu-id="98e3b-225">更新 Views/TodoList/Index.cshtml：</span><span class="sxs-lookup"><span data-stu-id="98e3b-225">Update *Views/TodoList/Index.cshtml*:</span></span>

<!-- Views/TodoList/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="98e3b-226">运行应用并验证 PVC 视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-226">Run the app and verify PVC view.</span></span>

![优先级视图组件](view-components/_static/pvc.png)

<span data-ttu-id="98e3b-228">如果不呈现 PVC 视图，请验证是否调用优先级为 4 或更高的视图组件。</span><span class="sxs-lookup"><span data-stu-id="98e3b-228">If the PVC view isn't rendered, verify you are calling the view component with a priority of 4 or higher.</span></span>

### <a name="examine-the-view-path"></a><span data-ttu-id="98e3b-229">检查视图路径</span><span class="sxs-lookup"><span data-stu-id="98e3b-229">Examine the view path</span></span>

* <span data-ttu-id="98e3b-230">将优先级参数更改为 3 或更低，从而不返回优先级视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-230">Change the priority parameter to three or less so the priority view isn't returned.</span></span>
* <span data-ttu-id="98e3b-231">将 Views/Todo/Components/PriorityList/Default.cshtml 暂时重命名为 1Default.cshtml。</span><span class="sxs-lookup"><span data-stu-id="98e3b-231">Temporarily rename the *Views/Todo/Components/PriorityList/Default.cshtml* to *1Default.cshtml*.</span></span>
* <span data-ttu-id="98e3b-232">测试应用，你将收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="98e3b-232">Test the app, you'll get the following error:</span></span>

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' wasn't found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* <span data-ttu-id="98e3b-233">将 Views/Todo/Components/PriorityList/1Default.cshtml 复制到 Views/Shared/Components/PriorityList/Default.cshtml。</span><span class="sxs-lookup"><span data-stu-id="98e3b-233">Copy *Views/Todo/Components/PriorityList/1Default.cshtml* to *Views/Shared/Components/PriorityList/Default.cshtml*.</span></span>
* <span data-ttu-id="98e3b-234">将一些标记添加到共享 Todo 视图组件视图以指示视图来自“Shared”文件夹。</span><span class="sxs-lookup"><span data-stu-id="98e3b-234">Add some markup to the *Shared* Todo view component view to indicate the view is from the *Shared* folder.</span></span>
* <span data-ttu-id="98e3b-235">测试“共享”组件视图。</span><span class="sxs-lookup"><span data-stu-id="98e3b-235">Test the **Shared** component view.</span></span>

![有共享组件视图的 ToDo 输出](view-components/_static/shared.png)

### <a name="avoiding-magic-strings"></a><span data-ttu-id="98e3b-237">避免魔幻字符串</span><span class="sxs-lookup"><span data-stu-id="98e3b-237">Avoiding magic strings</span></span>

<span data-ttu-id="98e3b-238">若要确保编译时的安全性，可以用类名替换硬编码的视图组件名称。</span><span class="sxs-lookup"><span data-stu-id="98e3b-238">If you want compile time safety, you can replace the hard-coded view component name with the class name.</span></span> <span data-ttu-id="98e3b-239">创建没有“ViewComponent”后缀的视图组件：</span><span class="sxs-lookup"><span data-stu-id="98e3b-239">Create the view component without the "ViewComponent" suffix:</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

<span data-ttu-id="98e3b-240">将 `using` 语句添加到 Razor 视图文件，并使用 `nameof` 运算符：</span><span class="sxs-lookup"><span data-stu-id="98e3b-240">Add a `using` statement to your Razor view file, and use the `nameof` operator:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexNameof.cshtml?range=1-6,35-)]

## <a name="additional-resources"></a><span data-ttu-id="98e3b-241">其他资源</span><span class="sxs-lookup"><span data-stu-id="98e3b-241">Additional resources</span></span>

* [<span data-ttu-id="98e3b-242">视图中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="98e3b-242">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
