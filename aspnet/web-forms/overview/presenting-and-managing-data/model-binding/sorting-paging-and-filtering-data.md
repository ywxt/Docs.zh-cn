---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 排序、 分页和筛选数据与模型绑定和 web 窗体 |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: 86ddedb68b8d18057cd2f7d68e795efda33734b1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834703"
---
<a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>排序、 分页和筛选数据与模型绑定和 web 窗体
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 本教程演示如何添加排序、 分页和筛选数据，通过模型绑定。
> 
> 本教程基于第一个中创建的项目[一部分](retrieving-data.md)在本系列。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。


## <a name="what-youll-build"></a>你将生成

在本教程中，你将：

1. 启用排序和分页的数据
2. 启用基于用户选择的数据的筛选

## <a name="add-sorting"></a>添加排序

启用在 GridView 中排序是非常简单。 在 Student.aspx 文件中，只需将设置**AllowSorting**到**true** GridView 中。 不需要设置**SortExpression**自动使用数据字段值的每个列。 GridView 修改查询以包含所选值对数据进行排序。 以下突出显示的代码显示如何添加你需要进行启用排序。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

运行 web 应用程序，并测试排序学生记录不同列中的值。

![排序学生](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>添加分页

启用分页也是非常简单。 在 GridView 中，将**AllowPaging**属性设置为**true**并设置**PageSize**属性设置为你想要在每个页上显示的记录数。 在本教程中，可以将其设置为 4。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

运行 web 应用程序，并请注意，现在与在单页上显示不超过 4 个记录，通过多个页面分割记录。

![添加分页](sorting-paging-and-filtering-data/_static/image4.png)

延迟的执行查询可以提高应用程序效率。 而不是检索整个数据集，GridView 修改查询以检索仅为当前页的记录。

## <a name="filter-records-by-user-selection"></a>按用户所选内容筛选记录

模型绑定将添加几个属性使您能够指定如何在模型绑定方法中设置某个参数的值。 这些属性位于**System.Web.ModelBinding**命名空间。 它们包括：

- 控件
- Cookie
- 窗体
- 配置文件
- QueryString
- RouteData
- 会话
- 用户配置文件
- 视图状态

在本教程中，您将使用控件的值来筛选 GridView 中显示的记录。 您将添加**控制**属性为先前创建的查询方法。 在中[更高版本](using-query-string-values-to-retrieve-data.md)教程中，您将应用**QueryString**属性用于指定参数值来自查询字符串值的参数。

首先，上面 ValidationSummary，添加一个下拉列表筛选显示的学生。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

在代码隐藏文件中，修改选择的方法，以接收来自控件的值和参数的名称设置为提供的值的控件的名称。

必须添加**使用**语句**System.Web.ModelBinding**要解析的控件属性命名空间。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

下面的代码演示重新致力于筛选返回的数据基于值的下拉列表选择方法。 参数指定此参数的值来自具有相同名称的控件之前，将添加的控件属性。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

运行 web 应用程序，并从下拉列表以筛选学生列表中选择不同的值。

![筛选器学生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>结束语

在本教程中，您将启用排序和分页的数据。 你还启用了通过将控件的值筛选数据。

在接下来[教程](integrating-jquery-ui.md)将将 JQuery UI 小组件集成到动态数据模板来增强 UI。

> [!div class="step-by-step"]
> [上一页](updating-deleting-and-creating-data.md)
> [下一页](integrating-jquery-ui.md)
