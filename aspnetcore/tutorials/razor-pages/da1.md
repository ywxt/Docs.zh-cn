---
title: 在 ASP.NET Core 应用中更新生成的页面
author: rick-anderson
description: 了解如何在 ASP.NET Core 应用中更新生成的页面。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/da1
ms.openlocfilehash: 55ff98712da314e28e50a1b1b1e04530d5b3fedd
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278065"
---
# <a name="update-the-generated-pages-in-an-aspnet-core-app"></a>在 ASP.NET Core 应用中更新生成的页面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

我们的电影应用有个不错的开始，但是展示效果还不够理想。 我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为“Release Date”（两个词）。

![在 Chrome 中打开的显示电影数据的电影应用程序](sql/_static/m55.png)

## <a name="update-the-generated-code"></a>更新生成的代码

打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：

::: moniker range="= aspnetcore-2.0"
[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]
::: moniker-end

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]
::: moniker-end

右键单击红色波浪线，然后单击“快速操作和重构”。

  ![上下文菜单中显示“快速操作和重构”。](da1/qa.png)

选择 `using System.ComponentModel.DataAnnotations;`

  ![使用列表顶部的 System.ComponentModel.DataAnnotations](da1/da.png)

  Visual studio 添加 `using System.ComponentModel.DataAnnotations;`。

[!INCLUDE [model1](~/includes/RP/da2.md)]

> [!div class="step-by-step"]
> [上一篇：使用 SQL Server LocalDB](xref:tutorials/razor-pages/sql)
> [添加搜索](xref:tutorials/razor-pages/search)
