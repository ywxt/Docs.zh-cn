---
title: 添加搜索
author: rick-anderson
description: 演示如何将搜索添加到简单的 ASP.NET Core MVC 应用
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-xplat/search
ms.openlocfilehash: dc84eb38c0487d90451979ec9572bf1641571357
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276001"
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
