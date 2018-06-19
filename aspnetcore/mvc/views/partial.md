---
title: ASP.NET Core 中的分部视图
author: ardalis
description: 了解分部视图是如何呈现在另一视图中，以及何时应在 ASP.NET Core 应用中使用它们。
manager: wpickett
ms.author: riande
ms.date: 03/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/partial
ms.openlocfilehash: 3deaaeb666e5443d0784f2ac6977e58e1b25d711
ms.sourcegitcommit: 71b93b42cbce8a9b1a12c4d88391e75a4dfb6162
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
ms.locfileid: "30000897"
---
# <a name="partial-views-in-aspnet-core"></a>ASP.NET Core 中的分部视图

作者：[Steve Smith](https://ardalis.com/)、[Maher JENDOUBI](https://twitter.com/maherjend)、[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Scott Sauber](https://twitter.com/scottsauber)

ASP.NET Core MVC 支持分部视图，如果拥有想要在不同视图之间共享的网页的可重用部分，分部视图十分有用。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-are-partial-views"></a>什么是分部视图？

分部视图是指在其他视图内呈现的视图。 通过执行分部视图生成的 HTML 输出在调用视图（或父视图）中呈现。 和视图一样，分部视图也使用 *.cshtml* 文件扩展名。

## <a name="when-should-i-use-partial-views"></a>应在何时使用分部视图？

分部视图是将大型视图分解为较小组件的有效方法。 它们可减少视图内容的重复并使视图元素得以重复使用。 常见布局元素应在 [_Layout.cshtml](layout.md) 中指定。 非布局可重用内容可封装到分部视图中。

如果拥有由多个逻辑部分组成的复杂页面，将每个部分用作其自己的分部视图十分有用。 页面的每个部分都可独立于页面的其余部分进行查看，且页面本身的视图也会变得更加简单，因为它仅包含整体页面结构以及用于呈现分部视图的调用。

提示：在视图中遵守[不要自我重复原则](http://deviq.com/don-t-repeat-yourself/)。

## <a name="declaring-partial-views"></a>声明分部视图

分部视图的创建方式与任何其他视图的创建方式类似：在 *Views* 文件夹内创建 *.cshtml* 文件。 分部视图和常规视图之间没有语义差异-，仅呈现方式不同。 可拥有直接从控制器的 `ViewResult` 返回的视图，并可将同一视图用作分部视图。 视图和分部视图的主要呈现方式差异在于分部视图不运行 *_ViewStart.cshtml*（而视图运行 — 有关 *_ViewStart.cshtml* 的详细信息，请参阅[布局](layout.md)）。

## <a name="referencing-a-partial-view"></a>引用分部视图

在视图页中，有多种方法可呈现分部视图。 最佳做法是使用 `Html.PartialAsync`，它会返回 `IHtmlString` 并可通过为调用添加 `@` 前缀进行引用：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=8)]

可使用 `RenderPartialAsync` 呈现分部视图。 此方法不返回结果；它将呈现的输出直接流式传输到响应。 因为它不返回结果，所以必须在 Razor 代码块内调用它：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=11-13)]

由于它直接流式传输结果，`RenderPartialAsync` 在某些情况下可能会表现更佳。 但是，建议使用 `PartialAsync`。

虽然存在 `Html.PartialAsync` (`Html.Partial`) 和 `Html.RenderPartialAsync` (`Html.RenderPartial`) 的同步等效项，但不建议使用同步等效项，因为可能会出现死锁的情况。 同步方法在将来版本中不可用。

> [!NOTE]
> 如果视图需要执行代码，建议模式为使用[视图组件](view-components.md)，而不要使用分部视图。

### <a name="partial-view-discovery"></a>分部视图发现

引用分部视图时，可通过多种方式引用其位置：

```cshtml
// Uses a view in current folder with this name
// If none is found, searches the Shared folder
@await Html.PartialAsync("ViewName")

// A view with this name must be in the same folder
@await Html.PartialAsync("ViewName.cshtml")

// Locate the view based on the application root
// Paths that start with "/" or "~/" refer to the application root
@await Html.PartialAsync("~/Views/Folder/ViewName.cshtml")
@await Html.PartialAsync("/Views/Folder/ViewName.cshtml")

// Locate the view using relative paths
@await Html.PartialAsync("../Account/LoginPartial.cshtml")
```

可在不同视图文件夹中拥有具有相同名称的不同分部视图。 按名称（不带文件扩展名）引用视图时，每个文件夹中的视图都会使用与其位于同一文件夹中的分部视图。 还可指定要使用的默认分部视图，将其放在 *Shared* 文件夹中。 任何没有属于自己的分部视图的视图则可使用共享分部视图。 可设置默认分部视图（位于 *Shared* 中），该视图被与父视图位于同一文件夹并具有相同名称的分部视图替代。

分部视图可*链接*。 也就是说，分部视图可调用其他分部视图（只要未创建循环）。 在每个视图或分部视图内，相对路径始终相对于该视图，而不相对于根视图或父视图。

> [!NOTE]
> 如果在分部视图中声明 [Razor](razor.md) `section`，它不会对其父对象可见；它会局限于分部视图。

## <a name="accessing-data-from-partial-views"></a>通过分部视图访问数据

实例化分部视图时，它会获得父视图的 `ViewData` 字典的副本。 在分部视图内对数据所做的更新不会保存到父视图中。 在分部视图中更改的 `ViewData` 会在分部视图返回时丢失。

可将 `ViewDataDictionary` 的实例传递到分部视图：

```cshtml
@await Html.PartialAsync("PartialName", customViewData)
```

还可将模型传入分部视图。 该模型可以是页面的视图模型或自定义对象。 可将模型传递到 `PartialAsync` 或 `RenderPartialAsync`：

```cshtml
@await Html.PartialAsync("PartialName", viewModel)
```

可将 `ViewDataDictionary` 的实例和视图模型传递到分部视图：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml?range=15-16)]

以下标记显示包含两个分部视图的 *Views/Articles/Read.cshtml* 视图。 第二个分部视图将模型和 `ViewData` 传入分部视图。 如果使用下方突出显示的 `ViewDataDictionary` 的构造函数重载，则可在传递新 `ViewData` 字典的同时保留现有的 `ViewData`：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml)]

*Views/Shared/AuthorPartial*：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Shared/AuthorPartial.cshtml)]

*ArticleSection* 分部视图：

[!code-cshtml[](partial/sample/src/PartialViewsSample/Views/Articles/ArticleSection.cshtml)]

在运行时，分部视图在父视图中呈现，而父视图本身在共享的 *_Layout.cshtml* 内呈现

![分部视图输出](partial/_static/output.png)
