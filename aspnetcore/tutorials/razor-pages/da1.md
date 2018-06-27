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
# <a name="update-the-generated-pages-in-an-aspnet-core-app"></a><span data-ttu-id="fb2b7-103">在 ASP.NET Core 应用中更新生成的页面</span><span class="sxs-lookup"><span data-stu-id="fb2b7-103">Update the generated pages in an ASP.NET Core app</span></span>

<span data-ttu-id="fb2b7-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fb2b7-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fb2b7-105">我们的电影应用有个不错的开始，但是展示效果还不够理想。</span><span class="sxs-lookup"><span data-stu-id="fb2b7-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="fb2b7-106">我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为“Release Date”（两个词）。</span><span class="sxs-lookup"><span data-stu-id="fb2b7-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be **Release Date** (two words).</span></span>

![在 Chrome 中打开的显示电影数据的电影应用程序](sql/_static/m55.png)

## <a name="update-the-generated-code"></a><span data-ttu-id="fb2b7-108">更新生成的代码</span><span class="sxs-lookup"><span data-stu-id="fb2b7-108">Update the generated code</span></span>

<span data-ttu-id="fb2b7-109">打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="fb2b7-109">Open the *Models/Movie.cs* file and add the highlighted lines shown in the following code:</span></span>

::: moniker range="= aspnetcore-2.0"
<span data-ttu-id="fb2b7-110">[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]</span><span class="sxs-lookup"><span data-stu-id="fb2b7-110">[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="fb2b7-111">[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]</span><span class="sxs-lookup"><span data-stu-id="fb2b7-111">[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]</span></span>
::: moniker-end

<span data-ttu-id="fb2b7-112">右键单击红色波浪线，然后单击“快速操作和重构”。</span><span class="sxs-lookup"><span data-stu-id="fb2b7-112">Right click on a red squiggly line > **Quick Actions and Refactorings**.</span></span>

  ![上下文菜单中显示“快速操作和重构”。](da1/qa.png)

<span data-ttu-id="fb2b7-114">选择 `using System.ComponentModel.DataAnnotations;`</span><span class="sxs-lookup"><span data-stu-id="fb2b7-114">Select `using System.ComponentModel.DataAnnotations;`</span></span>

  ![使用列表顶部的 System.ComponentModel.DataAnnotations](da1/da.png)

  <span data-ttu-id="fb2b7-116">Visual studio 添加 `using System.ComponentModel.DataAnnotations;`。</span><span class="sxs-lookup"><span data-stu-id="fb2b7-116">Visual studio adds `using System.ComponentModel.DataAnnotations;`.</span></span>

[!INCLUDE [model1](~/includes/RP/da2.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="fb2b7-117">[上一篇：使用 SQL Server LocalDB](xref:tutorials/razor-pages/sql)
> [添加搜索](xref:tutorials/razor-pages/search)</span><span class="sxs-lookup"><span data-stu-id="fb2b7-117">[Previous: Working with SQL Server LocalDB](xref:tutorials/razor-pages/sql)
[Add search](xref:tutorials/razor-pages/search)</span></span>
