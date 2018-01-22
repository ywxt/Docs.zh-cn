---
title: "将搜索添加到 ASP.NET Core MVC 应用"
author: rick-anderson
description: "演示如何将搜索添加到简单的 ASP.NET Core MVC 应用"
ms.author: riande
manager: wpickett
ms.date: 04/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/search
ms.openlocfilehash: 76739cd3805d9e5ac8b4b0e672b8e7da6596492e
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="5539b-103">请注意：SQLlite 区分大小写，因此需搜索“Ghost”而非“ghost”。</span><span class="sxs-lookup"><span data-stu-id="5539b-103">Note: SQLlite is case sensitive, so you'll need to search for "Ghost" and not "ghost".</span></span>

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="5539b-104">在“Views\movie\Index.cshtml”Razor 视图中更改 `<form>` 标记以指定 `method="get"`：</span><span class="sxs-lookup"><span data-stu-id="5539b-104">Change the `<form>` tag in the *Views\movie\Index.cshtml* Razor view to specify `method="get"`:</span></span>

```html
<form asp-controller="Movies" asp-action="Index" method="get">
```

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
<span data-ttu-id="5539b-105">[上一篇 - 控制器方法和视图](controller-methods-views.md)
[下一篇 - 添加字段](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="5539b-105">[Previous - Controller methods and views](controller-methods-views.md)
[Next - Add a field](new-field.md)</span></span>
