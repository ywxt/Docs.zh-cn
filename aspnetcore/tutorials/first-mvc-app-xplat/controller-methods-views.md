---
title: ASP.NET Core 中的控制器方法和视图
author: rick-anderson
description: 了解如何在 ASP.NET Core 中使用控制器方法、视图和 DataAnnotations。
ms.author: riande
ms.date: 04/07/2017
uid: tutorials/first-mvc-app-xplat/controller-methods-views
ms.openlocfilehash: 7cf42807eaba356cd090a08bba9357c3ec237087
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278435"
---
# <a name="controller-methods-and-views-in-aspnet-core"></a>ASP.NET Core 中的控制器方法和视图

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

我们的电影应用有个不错的开始，但是展示效果还不够理想。 我们不希望看到时间（如下图所示的 12:00:00 AM），并且“ReleaseDate”应为两个词。

![索引视图：Release Date 为一个词（没有空格），每个电影发行日期都显示时间中午 12 点](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

打开 Models/Movie.cs 文件，并添加以下代码中突出显示的行：

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

生成并运行应用。

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE [adding-model](../../includes/mvc-intro/controller-methods-views.md)]

> [!div class="step-by-step"]
> [上一篇 - 使用 SQLite](working-with-sql.md)
> [下一篇 - 添加搜索](search.md)  
