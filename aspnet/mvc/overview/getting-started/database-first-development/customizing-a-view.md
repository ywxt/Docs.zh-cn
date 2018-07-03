---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 自定义视图 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: bfbcfd39dd1cf0abe89a00d2958ca010f0e5e109
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376493"
---
<a name="ef-database-first-with-aspnet-mvc-customizing-a-view"></a>第一种使用 ASP.NET MVC 的 EF 数据库： 自定义视图
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。
> 
> 本系列的此部分重点介绍更改的自动生成的视图，以增强此演示文稿。


## <a name="add-enrolled-courses-to-student-details"></a>将已注册的课程添加到学生详细信息

生成的代码为应用程序提供很好的起点，但它不一定提供全部所需应用程序中的功能。 可以自定义代码来满足你的应用程序的特定要求。 目前，你的应用程序不显示所选学生的已注册的课程。 在本部分中，您将添加已注册的课程到每个学生**详细信息**学生的视图。

打开**Students/Details.cshtml**，和最后一个下方&lt;/dl&gt;选项卡上，但在关闭前&lt;/div&gt;标记中，添加以下代码。

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

此代码将创建所选学生 Enrollment 表中显示为每个记录的行的表。 **显示**方法表示表达式的对象 (modelItem) 将呈现 HTML。 使用 Display 方法 （而不是只需在代码中嵌入的属性值） 以确保设置的值格式正确基于其类型和该类型的模板。 在此示例中，从当前记录在循环中，每个表达式返回的单个属性和值是基元类型的呈现为文本。

再次浏览到学生/索引视图并选择**详细信息**一个学生。 你将看到在视图中包含了已注册的课程。

![与注册的学生](customizing-a-view/_static/image1.png)

> [!div class="step-by-step"]
> [上一页](changing-the-database.md)
> [下一页](enhancing-data-validation.md)
