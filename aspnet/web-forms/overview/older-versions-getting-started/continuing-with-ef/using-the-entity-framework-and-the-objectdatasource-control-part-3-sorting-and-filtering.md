---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 使用实体框架 4.0 和 ObjectDataSource 控件，第 3 部分： 排序和筛选 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 48d859191877ba951e233f19873d52625fe180ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378905"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>使用实体框架 4.0 和 ObjectDataSource 控件，第 3 部分： 排序和筛选
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> 本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)系列教程。 如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。 此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。 如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。


上一教程中实现中使用实体框架的 n 层 web 应用程序的存储库模式和`ObjectDataSource`控件。 本教程演示如何执行排序和筛选和处理主-从方案。 你将添加到以下增强功能*Departments.aspx*页：

- 若要允许用户按名称选择部门文本框。
- 在网格中显示每个部门的课程列表。
- 通过单击列标题排序功能。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>将功能添加到 GridView 列进行排序

打开*Departments.aspx*页上，添加`SortParameterName="sortExpression"`归于`ObjectDataSource`控件命名为`DepartmentsObjectDataSource`。 (稍后将创建`GetDepartments`方法采用参数名为`sortExpression`。)现在，该控件的开始标记的标记类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

添加`AllowSorting="true"`属性的开始标记为`GridView`控件。 现在，该控件的开始标记的标记类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

在中*Departments.aspx.cs*，通过调用设置默认的排序顺序`GridView`控件的`Sort`方法从`Page_Load`方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

在业务逻辑类或存储库类中，可以添加对进行排序或筛选器的代码。 如果您执行此操作的业务逻辑类中，排序或筛选工作会执行从数据库检索数据之后由于业务逻辑类使用`IEnumerable`对象返回的存储库。 如果您添加排序和筛选存储库类中的代码和执行之前的 LINQ 表达式或对象查询转换为`IEnumerable`对象，你的命令将通过传递给数据库进行处理，通常效率更高。 将在本教程中实现排序和筛选将导致由数据库执行的处理的方式 — 也就是说，存储库中。

若要添加排序功能，必须将新方法添加到存储库接口和存储库类以及业务逻辑类中。 在中*ISchoolRepository.cs*文件中，添加一个新`GetDepartments`采用的方法`sortExpression`参数，它将用于排序返回部门列表：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression`参数将指定要作为排序依据的列和排序方向。

添加到新的方法的代码*SchoolRepository.cs*文件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

更改现有无参数`GetDepartments`方法调用新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

在测试项目中，添加以下新方法*MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

如果要创建依赖于此方法返回的已排序的列表的任何单元测试，您需要对列表返回之前对其进行排序。 你不需要创建测试类似的在本教程中，因此该方法只返回部门的未排序的列表。

在中*SchoolBL.cs*文件中，将以下新方法添加到业务逻辑类：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

此代码将排序参数传递给存储库方法。

运行*Departments.aspx*页。

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

现在可以单击任何列标题以按该列排序。 如果已对列进行排序，单击标题反转的排序方向。

## <a name="adding-a-search-box"></a>添加搜索框

将在本部分中添加搜索文本框中，将其链接至`ObjectDataSource`控制使用控件参数，并将方法添加到要支持筛选的业务逻辑类。

打开*Departments.aspx*页上，添加以下标记标题和第一个之间`ObjectDataSource`控件：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

在中`ObjectDataSource`名为控件`DepartmentsObjectDataSource`，执行以下操作：

- 添加`SelectParameters`名为的参数的元素`nameSearchString`获取中输入的值`SearchTextBox`控件。
- 更改`SelectMethod`属性值为`GetDepartmentsByName`。 （您将创建此方法更高版本。）

有关标记`ObjectDataSource`控件现在类似于下面的示例：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

在中*ISchoolRepository.cs*，添加`GetDepartmentsByName`方法采用两`sortExpression`和`nameSearchString`参数：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

在中*SchoolRepository.cs*，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

此代码使用`Where`方法来选择包含搜索字符串的项。 如果搜索字符串为空，将选择所有记录。 请注意，当您指定在此类的一个语句中一起调用的方法 (`Include`，然后`OrderBy`，然后`Where`)，则`Where`方法必须始终为最后一个。

更改现有`GetDepartments`方法采用`sortExpression`参数来调用新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

在中*MockSchoolRepository.cs*在测试项目中，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

在中*SchoolBL.cs*，添加以下新方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

运行*Departments.aspx*页，并输入搜索字符串以确保选择逻辑可以正常工作。 将文本框留空，请尝试搜索以确保将返回所有记录。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>为每个网格行中添加详细信息列

接下来，你想要查看所有右侧的网格单元中显示每个系的课程。 若要执行此操作，您将使用嵌套`GridView`控制和数据绑定将数据从它`Courses`导航属性`Department`实体。

打开*Departments.aspx*和中的标记`GridView`控制，请指定处理程序为`RowDataBound`事件。 现在，该控件的开始标记的标记类似于下面的示例。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

添加一个新`TemplateField`元素后的`Administrator`模板字段：

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

此标记创建嵌套`GridView`演示的课程编号和标题的课程列表的控件。 它不指定数据源，因为将数据绑定中的代码中`RowDataBound`处理程序。

打开*Departments.aspx.cs*并添加以下处理程序`RowDataBound`事件：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

此代码获取`Department`从事件参数中，实体将转换`Courses`导航属性设置为`List`集合和嵌套的 databinds`GridView`到集合。

打开*SchoolRepository.cs*文件，并指定预先加载`Courses`导航属性，通过调用`Include`方法中创建的对象查询中`GetDepartmentsByName`方法。 `return`中的语句`GetDepartmentsByName`方法现在类似于下面的示例。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

运行页。 排序和筛选你前面添加的功能，除了 GridView 控件现在显示每个部门的嵌套的课程详细信息。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

这将完成排序、 筛选，和母版-详细信息方案的简介。 在下一步的教程中，您将了解如何处理并发。

> [!div class="step-by-step"]
> [上一页](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [下一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
