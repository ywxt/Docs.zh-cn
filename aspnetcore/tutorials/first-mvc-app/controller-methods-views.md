---
title: ASP.NET Core 中的控制器方法和视图
author: rick-anderson
description: 了解如何在 ASP.NET Core 中使用控制器方法、视图和 DataAnnotations。
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/controller-methods-views
ms.openlocfilehash: 3f84d242a41bc482110d87ff342fa5b5d8c870ff
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729848"
---
# <a name="controller-methods-and-views-in-aspnet-core"></a><span data-ttu-id="cb7a8-103">ASP.NET Core 中的控制器方法和视图</span><span class="sxs-lookup"><span data-stu-id="cb7a8-103">Controller methods and views in ASP.NET Core</span></span>

<span data-ttu-id="cb7a8-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cb7a8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cb7a8-105">我们的电影应用有个不错的开始，但是展示效果还不够理想。</span><span class="sxs-lookup"><span data-stu-id="cb7a8-105">We have a good start to the movie app, but the presentation isn't ideal.</span></span> <span data-ttu-id="cb7a8-106">我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为两个词。</span><span class="sxs-lookup"><span data-stu-id="cb7a8-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![索引视图：Release Date 为一个词（没有空格），每个电影发行日期都显示时间中午 12 点](working-with-sql/_static/m55.png)

<span data-ttu-id="cb7a8-108">打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="cb7a8-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="cb7a8-109">[!code-csharp[](start-mvc/sample/MvcMovie21/Models/MovieDateFixed.cs?name=snippet_1&highlight=2,3,12-13,17)]</span><span class="sxs-lookup"><span data-stu-id="cb7a8-109">[!code-csharp[](start-mvc/sample/MvcMovie21/Models/MovieDateFixed.cs?name=snippet_1&highlight=2,3,12-13,17)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="cb7a8-110">[!code-csharp[](start-mvc/sample/MvcMovie/Models/MovieDateWithExtraUsings.cs?name=snippet_1&highlight=13-14)]</span><span class="sxs-lookup"><span data-stu-id="cb7a8-110">[!code-csharp[](start-mvc/sample/MvcMovie/Models/MovieDateWithExtraUsings.cs?name=snippet_1&highlight=13-14)]</span></span>
::: moniker-end

[!INCLUDE [adding-model](~/includes/mvc-intro/controller-methods-views.md)]

> [!div class="step-by-step"]
> <span data-ttu-id="cb7a8-111">[上一页](working-with-sql.md)
> [下一页](search.md)</span><span class="sxs-lookup"><span data-stu-id="cb7a8-111">[Previous](working-with-sql.md)
[Next](search.md)</span></span>  
