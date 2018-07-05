---
title: 将搜索添加到 ASP.NET Core MVC 应用
author: rick-anderson
description: 演示如何将搜索添加到简单的 ASP.NET Core MVC 应用
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-mac/search
ms.openlocfilehash: aca0835340977605cc84fad1970ac30fa1a9872a
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961537"
---
[!INCLUDE [adding-model](../../includes/mvc-intro/search1.md)]

请注意：SQLlite 区分大小写，因此需搜索“Ghost”而非“ghost”。

[!INCLUDE [adding-model](../../includes/mvc-intro/search2.md)]

在“Views\movie\Index.cshtml”Razor 视图中更改 `<form>` 标记以指定 `method="get"`：

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE [adding-model](../../includes/mvc-intro/search3.md)]

> [!div class="step-by-step"]
> [上一篇 - 控制器方法和视图](controller-methods-views.md)
> [下一篇 - 添加字段](new-field.md)
