---
title: "ASP.NET Core MVC 应用中的控制器方法和视图"
author: rick-anderson
description: "使用控制器方法、视图和 DataAnnotations"
ms.author: riande
manager: wpickett
ms.date: 04/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/controller-methods-views
ms.openlocfilehash: 1c58a3bbac227e06a36df0b0d3ed6c2455eb46c4
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="controller-methods-and-views-in-an-aspnet-core-mvc-app"></a><span data-ttu-id="84ca1-103">ASP.NET Core MVC 应用中的控制器方法和视图</span><span class="sxs-lookup"><span data-stu-id="84ca1-103">Controller methods and views in an ASP.NET Core MVC app</span></span>

<span data-ttu-id="84ca1-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="84ca1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="84ca1-105">我们的电影应用有个不错的开始，但是展示效果还不够理想。</span><span class="sxs-lookup"><span data-stu-id="84ca1-105">We have a good start to the movie app, but the presentation is not ideal.</span></span> <span data-ttu-id="84ca1-106">我们不希望看到时间（下图中的 12:00:00 AM），并且“ReleaseDate”应为两个词。</span><span class="sxs-lookup"><span data-stu-id="84ca1-106">We don't want to see the time (12:00:00 AM in the following image) and **ReleaseDate** should be two words.</span></span>

![索引视图：Release Date 为一个词（没有空格），每个电影发行日期都显示时间中午 12 点](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

<span data-ttu-id="84ca1-108">打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="84ca1-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

<span data-ttu-id="84ca1-109">生成并运行应用。</span><span class="sxs-lookup"><span data-stu-id="84ca1-109">Build and run the app.</span></span>

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
<span data-ttu-id="84ca1-110">[上一篇 - 使用 SQLite](working-with-sql.md)
[下一篇 - 添加搜索](search.md)</span><span class="sxs-lookup"><span data-stu-id="84ca1-110">[Previous - Working with SQLite](working-with-sql.md)
[Next - Add search](search.md)</span></span>
