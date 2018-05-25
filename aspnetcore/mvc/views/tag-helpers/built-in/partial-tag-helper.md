---
title: ASP.NET Core 中的部分标记帮助程序
author: scottaddie
description: 发现 ASP.NET Core 部分标记帮助程序以及每个属性在呈现分部视图时所扮演的角色。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 04/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
ms.openlocfilehash: 786c333980db89a9a5a60dc70c0bd1998ca159cd
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="partial-tag-helper-in-aspnet-core"></a>ASP.NET Core 中的部分标记帮助程序

作者：[Scott Addie](https://github.com/scottaddie)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="overview"></a>概述

Partial 标记帮助程序用于在 Razor 页面和 MVC 应用中呈现[分部视图](xref:mvc/views/partial)。 请考虑：

* 需要 ASP.NET Core 2.1 或更高版本。
* 是 [HTML 帮助程序语法](xref:mvc/views/partial#referencing-a-partial-view)的替代方法。
* 以异步方式呈现分部视图。

用于呈现分部视图的 HTML 帮助程序选项包括：

* [@await Html.PartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [@await Html.RenderPartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

本文档中的示例均使用产品模型：

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

以下是分部标记帮助程序属性的清单。

## <a name="name"></a>name

需要 `name` 属性。 它指示要呈现的分部视图的名称或路径。 提供分部视图名称时，会启动[视图发现](xref:mvc/views/overview#view-discovery)进程。 提供显式路径时，将绕过该进程。

以下标记使用显式路径，指示要从共享文件夹加载 _ProductPartial.cshtml。 使用 [for](#for) 属性，将模型传递给分部视图进行绑定。

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## <a name="for"></a>for

`for` 属性分配要根据当前模型评估的 [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression)。 `ModelExpression` 推断 `@Model.` 语法。 例如，可使用 `for="Product"` 而非 `for="@Model.Product"`。 通过使用 `@` 符号定义内联表达式来替代此默认推理行为。 `for` 属性不能与 [model](#model) 属性一起使用。

以下标记加载 _ProductPartial.cshtml：

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_For)]

分部视图绑定到关联页模型的 `Product` 属性：

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## <a name="model"></a>model

`model` 属性分配模型实例，以传递到分部视图。 `model` 属性不能与 [for](#for) 属性一起使用。

在以下标记中，实例化新的 `Product` 对象并将其传递给 `model` 属性进行绑定：

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Model)]

## <a name="view-data"></a>view-data

`view-data` 属性分配 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)，以传递到分部视图。 以下标记使整个 ViewData 集合可访问分部视图：

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

在前面的代码中，`IsNumberReadOnly` 键值设置为 `true` 并添加到 ViewData 集合中。 因此，在以下分部视图中可访问 `ViewData["IsNumberReadOnly"]`：

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

在此示例中，`ViewData["IsNumberReadOnly"]` 的值确定 Number 字段是否显示为只读。

## <a name="additional-resources"></a>其他资源

* [部分视图](xref:mvc/views/partial)
* [弱类型数据（ViewData、ViewData 属性和 ViewBag）](xref:mvc/views/overview#weakly-typed-data-viewdata-viewdata-attribute-and-viewbag)
