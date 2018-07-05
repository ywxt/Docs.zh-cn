---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查询字符串值以使用模型绑定筛选数据和 web 窗体 |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 495489479ef912afcb89c267b56fb11e07f959ec
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374725"
---
<a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>模型绑定和 web 窗体中使用查询字符串值以筛选数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 本教程演示如何在查询字符串中传递一个值，并使用该值来通过模型绑定检索数据。
> 
> 本教程中创建的项目为基础[早期](retrieving-data.md)在本系列的部分。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。


## <a name="what-youll-build"></a>你将生成

在本教程中，你将：

1. 添加新的页显示已注册的课程的学生
2. 基于查询字符串中的值所选学生检索已注册的课程
3. 从网格视图中为超链接使用查询字符串值添加到新页面

本教程中的步骤是非常类似于你未在早期[教程](sorting-paging-and-filtering-data.md)以筛选根据用户选择下拉列表中显示的学生。 在该教程中，使用**控制**中选择的方法来指定参数值来自控件的属性。 在本教程中，你将使用**QueryString** select 方法来指定参数值来自查询字符串中的属性。

## <a name="add-new-page-for-displaying-a-students-courses"></a>添加用于显示学生的课程的新页面

添加使用 Site.master 母版页的新 web 窗体并将该页命名为**课程**。

在中**Courses.aspx**文件中，添加要显示所选学生的课程的网格视图。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>定义 select 方法

在中**Courses.aspx.cs**，将添加 select 方法使用网格视图中指定的名称**SelectMethod**属性。 在该方法中，将定义用于检索学生的课程，查询和指定参数来自具有相同名称作为参数的查询字符串值。

首先，必须添加以下**使用**语句。

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

然后，将以下代码添加到 Courses.aspx.cs:

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

查询字符串属性意味着，一个名为 StudentID 的查询字符串值自动分配给此方法中的参数。

## <a name="add-hyperlink-with-query-string-value"></a>添加超链接使用查询字符串值

在上 Students.aspx 网格视图中，您将添加超链接字段链接到新的课程页。 超链接将包含学生的 id 的查询字符串值。

在 Students.aspx，将以下字段添加到字段的正下方的网格视图列的总信用额度。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

运行应用程序，并注意到网格视图现在包含课程链接。

![添加超链接](using-query-string-values-to-retrieve-data/_static/image1.png)

当您单击的链接之一时，您将看到该学生的已注册的课程。

![显示课程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>结束语

在本教程中，您添加了使用查询字符串值的链接。 该查询字符串值用于在 select 方法的参数值。

在接下来[教程](adding-business-logic-layer.md)，会将代码隐藏文件的代码移动到业务逻辑层和数据访问层。

> [!div class="step-by-step"]
> [上一页](integrating-jquery-ui.md)
> [下一页](adding-business-logic-layer.md)
