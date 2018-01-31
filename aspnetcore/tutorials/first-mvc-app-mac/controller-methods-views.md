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
ms.openlocfilehash: 71cdf9f0a4a72f375af094c7c0a446278f8aeeb5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="controller-methods-and-views-in-an-aspnet-core-mvc-app"></a>ASP.NET Core MVC 应用中的控制器方法和视图

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

我们的电影应用有个不错的开始，但是展示效果还不够理想。 我们不希望看到时间（下图中的 12:00:00 AM），并且“ReleaseDate”应为两个词。

![索引视图：Release Date 为一个词（没有空格），每个电影发行日期都显示时间中午 12 点](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

生成并运行应用。

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
[上一篇 - 使用 SQLite](working-with-sql.md)
[下一篇 - 添加搜索](search.md)
