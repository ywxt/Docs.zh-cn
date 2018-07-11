---
title: ASP.NET Core 中的分部视图
author: ardalis
description: 了解分部视图是如何呈现在另一视图中，以及何时应在 ASP.NET Core 应用中使用它们。
ms.author: riande
ms.custom: mvc
ms.date: 07/06/2018
uid: mvc/views/partial
ms.openlocfilehash: 9f90ce39929d0dbc216b47d76d652c1fca866ec2
ms.sourcegitcommit: a09820f91e71a7d98b7347bf93210abb9e995e22
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2018
ms.locfileid: "37889111"
---
# <a name="partial-views-in-aspnet-core"></a>ASP.NET Core 中的分部视图

作者：[Steve Smith](https://ardalis.com/)、[Maher JENDOUBI](https://twitter.com/maherjend)、[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Scott Sauber](https://twitter.com/scottsauber)

ASP.NET Core MVC 支持分部视图，它们可用于在不同的视图中共享网页的可重用部分。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-are-partial-views"></a>什么是分部视图

分部视图是指在其他视图内呈现的视图。 通过执行分部视图生成的 HTML 输出在调用视图（或父视图）中呈现。 和视图一样，分部视图也使用 *.cshtml* 文件扩展名。

例如，ASP.NET Core 2.1 Web 应用程序项目模板包括 _CookieConsentPartial.cshtml 分部视图。 分部视图从 _Layout.cshtml 内加载：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_Layout.cshtml?name=snippet_CookieConsentPartial)]

## <a name="when-to-use-partial-views"></a>何时使用分部视图

分部视图是将大型视图分解为较小组件的有效方法。 它们可减少视图内容的重复并使视图元素得以重复使用。 常见布局元素应在 [_Layout.cshtml](xref:mvc/views/layout) 中指定。 非布局可重用内容可封装到分部视图中。

在由多个逻辑部分组成的复杂页面中，将每个部分用作它自己的分部视图十分有用。 在页面的其余部分可以单独查看页面的每个部分。 页面本身的视图会变得更简单，因为它仅包含整体页面结构，并且通过调用来呈现分部视图。

> [!TIP]
> 在视图中遵守[不要自我重复原则](https://deviq.com/don-t-repeat-yourself/)。

## <a name="declare-partial-views"></a>声明分部视图

分部视图的创建方式与常规视图类似：在 Views 文件夹内创建 .cshtml 文件。 分部视图和常规视图之间没有语义差异-，但呈现方式不同。 用户可拥有直接从控制器的 [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult) 返回的视图，并可将同一视图用作分部视图。 视图和分部视图的主要呈现方式差异在于分部视图不运行 _ViewStart.cshtml。 常规视图却要运行 _ViewStart.cshtml。 详细了解 [Layout](xref:mvc/views/layout)) 中的 _ViewStart.cshtml。

按照约定，分部视图的文件名通常以 `_` 开头。 虽然未强制要求遵从此命名约定，但它有助于直观地将分部视图与常规视图区分开来。

## <a name="reference-a-partial-view"></a>引用分部视图

在视图页中，有多种方法可呈现分部视图。 最佳做法是使用异步呈现。

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a>分部标记帮助程序

分部标记帮助程序要求 ASP.NET Core 2.1 或更高版本。 它以异步方式呈现，并使用类似于 HTML 的语法：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_PartialTagHelper)]

有关更多信息，请参见<xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>。

::: moniker-end

### <a name="asynchronous-html-helper"></a>异步 HTML 帮助程序

使用 HTML 帮助程序时，最佳做法是使用[PartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync#Microsoft_AspNetCore_Mvc_Rendering_HtmlHelperPartialExtensions_PartialAsync_Microsoft_AspNetCore_Mvc_Rendering_IHtmlHelper_System_String_)。 它返回包装在 `Task` 中的 [IHtmlContent](/dotnet/api/microsoft.aspnetcore.html.ihtmlcontent) 类型。 通过在调用前添加 `@` 前缀来引用该方法：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_PartialAsync)]

或者，也可以使用 [RenderPartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync) 呈现分部视图。 此方法不返回结果。 它将呈现的输出直接流式传输到响应。 因为该方法不返回结果，所以必须在 Razor 代码块内调用它：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

由于它直接流式传输结果，所以 `RenderPartialAsync` 在某些情况下可能会表现更佳。 但是，建议使用 `PartialAsync`。

### <a name="synchronous-html-helper"></a>同步 HTML 帮助程序

[Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial) 和 [RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial) 分别是 `PartialAsync` 和 `RenderPartialAsync` 的同步等效项。 但不建议使用同步等效项，因为可能会出现死锁的情况。 未来版本将不包含同步方法。

> [!IMPORTANT]
> 如果视图需要执行代码，请使用[视图组件](xref:mvc/views/view-components)，而不要使用分部视图。

::: moniker range=">= aspnetcore-2.1"

在 ASP.NET Core 2.1 或更高版本中，调用 `Partial` 或 `RenderPartial` 会导致分析器警告。 例如，使用 `Partial` 会产生以下警告消息：

> 使用 IHtmlHelper.Partial 可能会导致应用程序死锁。 请考虑使用`<partial>` 标记帮助程序或 `IHtmlHelper.PartialAsync`。

将对 `@Html.Partial` 的调用替换为 `@await Html.PartialAsync` 或分部标记帮助程序。 有关分部标记帮助程序迁移的详细信息，请参阅[从 HTML 帮助程序迁移](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper)。

::: moniker-end

## <a name="partial-view-discovery"></a>分部视图发现

引用分部视图时，可通过多种方式引用其位置。 例如:

::: moniker range=">= aspnetcore-2.1"

```cshtml
// Uses a view in current folder with this name.
// If none is found, searches the Shared folder.
<partial name="_ViewName" />

// A view with this name must be in the same folder
<partial name="_ViewName.cshtml" />

// Locate the view based on the app root.
// Paths that start with "/" or "~/" refer to the app root.
<partial name="~/Views/Folder/_ViewName.cshtml" />
<partial name="/Views/Folder/_ViewName.cshtml" />

// Locate the view using a relative path
<partial name="../Account/_LoginPartial.cshtml" />
```

上述示例使用分部标记帮助程序，它需要 ASP.NET Core 2.1 或更高版本。 以下示例使用异步 HTML 帮助程序完成相同任务。

::: moniker-end

```cshtml
// Uses a view in current folder with this name.
// If none is found, searches the Shared folder.
@await Html.PartialAsync("_ViewName")

// A view with this name must be in the same folder
@await Html.PartialAsync("_ViewName.cshtml")

// Locate the view based on the app root.
// Paths that start with "/" or "~/" refer to the app root.
@await Html.PartialAsync("~/Views/Folder/_ViewName.cshtml")
@await Html.PartialAsync("/Views/Folder/_ViewName.cshtml")

// Locate the view using a relative path
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

不同视图文件夹中可以存在具有相同文件名的不同分部视图。 按名称（不带文件扩展名）引用视图时，每个文件夹中的视图都会使用与其位于同一文件夹中的分部视图。 还可指定要使用的默认分部视图，将其放在 *Shared* 文件夹中。 任何没有属于自己版本的分部视图的视图均可使用共享分部视图。 可设置默认分部视图（位于 *Shared* 中），该视图被与父视图位于同一文件夹并具有相同名称的分部视图替代。

分部视图可以链接在一起 &mdash; 分部视图可调用其他分部视图（只要未创建循环）。 在每个视图或分部视图内，相对路径始终相对于该视图，而不相对于根视图或父视图。

> [!NOTE]
> 分部视图中定义的 [Razor](xref:mvc/views/razor) `section` 对父视图不可见。 `section` 仅对定义它时所在的分部视图可见。

## <a name="access-data-from-partial-views"></a>通过分部视图访问数据

实例化分部视图时，它会获得父视图的 `ViewData` 字典的副本。 在分部视图内对数据所做的更新不会保存到父视图中。 在分部视图中的 `ViewData` 更改会在分部视图返回时丢失。

可将 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 的实例传递到分部视图：

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

还可将模型传入分部视图。 该模型可以是页面的视图模型或自定义对象。 可将模型传递到 `PartialAsync` 或 `RenderPartialAsync`：

```cshtml
@await Html.PartialAsync("_PartialName", viewModel)
```

可将 `ViewDataDictionary` 的实例和视图模型传递到分部视图：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_PartialAsync)]

以下标记显示包含两个分部视图的 *Views/Articles/Read.cshtml* 视图。 第二个分部视图将模型和 `ViewData` 传入分部视图。 使用突出显示的 `ViewDataDictionary` 构造函数可传递新 `ViewData` 字典，同时保留现有的 `ViewData` 字典。

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=17-20)]

Views/Shared/_AuthorPartial：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

*_ArticleSection* 分部视图：

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

在运行时，分部视图在父视图中呈现，而父视图本身在共享的 _Layout.cshtml 内呈现。

![分部视图输出](partial/_static/output.png)

## <a name="additional-resources"></a>其他资源

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>

::: moniker-end