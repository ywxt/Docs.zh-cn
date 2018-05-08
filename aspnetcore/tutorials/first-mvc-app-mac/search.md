---
title: 将搜索添加到 ASP.NET Core MVC 应用
author: rick-anderson
description: 演示如何将搜索添加到简单的 ASP.NET Core MVC 应用
manager: wpickett
ms.author: riande
ms.date: 04/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-mac/search
ms.openlocfilehash: 3f648bc6c6d095b9fe8b6ac65bf5f51741938ed1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
[!INCLUDE [adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="5cd62-103">请注意：SQLlite 区分大小写，因此需搜索“Ghost”而非“ghost”。</span><span class="sxs-lookup"><span data-stu-id="5cd62-103">Note: SQLlite is case sensitive, so you'll need to search for "Ghost" and not "ghost".</span></span>

[!INCLUDE [adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="5cd62-104">在“Views\movie\Index.cshtml”Razor 视图中更改 `<form>` 标记以指定 `method="get"`：</span><span class="sxs-lookup"><span data-stu-id="5cd62-104">Change the `<form>` tag in the *Views\movie\Index.cshtml* Razor view to specify `method="get"`:</span></span>

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE [adding-model](../../includes/mvc-intro/search3.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="5cd62-105">[上一篇 - 控制器方法和视图](controller-methods-views.md)
> [下一篇 - 添加字段](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="5cd62-105">[Previous - Controller methods and views](controller-methods-views.md)
[Next - Add a field](new-field.md)</span></span>
