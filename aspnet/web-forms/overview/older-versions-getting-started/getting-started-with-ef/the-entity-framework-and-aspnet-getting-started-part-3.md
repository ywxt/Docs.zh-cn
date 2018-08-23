---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 3 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 162f93c0249d8fa11d67ea10c68bc2ca8bae7259
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832508"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 3 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="filtering-ordering-and-grouping-data"></a>筛选、 排序和分组数据

在上一教程使用了`EntityDataSource`控件来显示和编辑数据。 在本教程中将筛选、 排序和分组数据。 执行此操作时通过设置属性的`EntityDataSource`控件，语法是不同于其他数据源控件。 正如您将看到的但是，您可以使用`QueryExtender`控件以最大程度减少这些差异。

将更改*Students.aspx*页后，可以筛选学生，按名称排序，并对名称的搜索。 此外将更改*Courses.aspx*页后，可以按名称显示为所选的部门和搜索课程的课程。 最后，将添加到学生统计信息*About.aspx*页。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>使用 EntityDataSource"Where"属性来筛选数据

打开*Students.aspx*在上一教程中创建的页。 按当前配置，`GridView`页中的控件显示来自所有名称`People`实体集。 但是，你想要显示仅学生，你可以通过选择查找`Person`具有非 null 注册日期实体。

切换到**设计**查看和选择`EntityDataSource`控件。 在中**属性**窗口中，将`Where`属性设置为`it.EnrollmentDate is not null`。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

在中使用的语法`Where`属性的`EntityDataSource`控件是 Entity SQL。 Entity SQL 是类似于 TRANSACT-SQL，但与实体而不是数据库对象一起使用了自定义。 在表达式中`it.EnrollmentDate is not null`，word`it`表示查询所返回的实体的引用。 因此，`it.EnrollmentDate`是指`EnrollmentDate`的属性`Person`实体的`EntityDataSource`控制返回。

运行页。 学生列表现在包含仅学生。 (没有任何行，其中显示没有注册日期。)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>使用订单数据的 EntityDataSource"OrderBy"属性

你还想在首次显示时按姓名顺序将此列表。 与*Students.aspx*仍在中打开页面**设计**视图中，并使用`EntityDataSource`控件仍处于选中状态，在**属性**窗口中设置**OrderBy**属性设置为`it.LastName`。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

运行页。 学生列表现按姓氏的顺序。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>使用控件参数设置的"Where"属性

当与其他数据源控件，你可以通过参数值`Where`属性。 上*Courses.aspx*页上，在本教程的第 2 部分中创建，则可以使用此方法以显示与用户从下拉列表中选择的院系的课程。

打开*Courses.aspx* ，并切换到**设计**视图。 添加另一个`EntityDataSource`控制对页上，并将其命名`CoursesEntityDataSource`。 将其连接到`SchoolEntities`模型并选择`Courses`作为**EntitySetName**值。

在中**属性**窗口中，单击中的省略号**其中**属性框。 (请确保`CoursesEntityDataSource`仍处于选中控件状态在使用之前**属性**窗口。)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

**表达式编辑器**显示对话框。 在此对话框中，选择**自动生成 Where 表达式基于提供的参数**，然后单击**添加参数**。 将参数命名`DepartmentID`，选择**控制**作为**参数源**值，然后选择**DepartmentsDropDownList**作为**ControlID**值。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

单击**显示高级属性**，然后在**属性**窗口**表达式编辑器**对话框中，更改`Type`属性设置为`Int32`。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

完成后，单击**确定**。

下面的下拉列表中，添加`GridView`控制对页面并将其命名`CoursesGridView`。 将其连接到`CoursesEntityDataSource`数据源控件，单击**刷新架构**，单击**编辑列**，并删除`DepartmentID`列。 `GridView`控件标记将类似于下面的示例。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

当用户更改所选的系的下拉列表中时，你想要关联的课程，会自动更改的列表。 若要使它发生这种情况中，选择下拉列表中，然后在**属性**窗口中设置`AutoPostBack`属性设置为`True`。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

现在，完成使用设计器后，切换到**源**查看和替换`ConnectionString`并`DefaultContainer`命名的属性`CoursesEntityDataSource`控件，其`ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`属性。 完成后，该控件的标记将类似下面的示例。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

运行页面，并使用下拉列表选择不同的部门。 提供的所选系的课程将显示在`GridView`控件。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>使用对数据进行分组的 EntityDataSource"GroupBy"属性

假设 Contoso 大学想要在其关于页面上放置一些学生正文统计信息。 具体而言，它想要按用户注册日期显示学生人数的细分。

打开*About.aspx*，然后在**源**视图中，替换现有内容`BodyContent`之间使用"学生正文统计信息"来控制`h2`标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

在标题后添加`EntityDataSource`控制并将其命名`StudentStatisticsEntityDataSource`。 将其连接到`SchoolEntities`，选择`People`实体集，并保留**选择**框在向导中保持不变。 在中设置以下属性**属性**窗口：

- 若要筛选为仅学生，设置`Where`属性设置为`it.EnrollmentDate is not null`。
- 若要按注册日期对结果进行分组，设置`GroupBy`属性设置为`it.EnrollmentDate`。
- 若要选择的注册日期和学生的数量，请设置`Select`属性设置为`it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`。
- 若要按注册日期对结果进行排序，设置`OrderBy`属性设置为`it.EnrollmentDate`。

在**源**视图中，替换`ConnectionString`并`DefaultContainer`名称与属性`ContextTypeName`属性。 `EntityDataSource`控件标记现在类似于下面的示例。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

语法`Select`， `GroupBy`，并`Where`属性类似于 TRANSACT-SQL 除`it`指定当前实体的关键字。

添加以下标记以创建`GridView`控件来显示数据。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

运行页后，可以看到一个列表，显示按注册日期的学生数量。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>用于筛选和排序使用 QueryExtender 控件

`QueryExtender`控件提供了一种指定标记中筛选和排序方法。 语法是独立于正在使用数据库管理系统 (DBMS)。 它还是通常独立于实体框架中，使用的导航属性使用的语法是唯一的实体框架的异常。

在本教程的此部分将使用`QueryExtender`控件与筛选器和订单数据，并按字段中的一个将为导航属性。

(如果想要使用代码而不是标记扩展通过自动生成的查询`EntityDataSource`控件，您可以通过实现处理`QueryCreated`事件。 这是如何`QueryExtender`控件扩展`EntityDataSource`控件查询的数据源。)

打开*Courses.aspx*页上，和以前添加的标记，插入以下标记以创建标题，用于输入搜索字符串，搜索按钮、 文本框和一个`EntityDataSource`控件绑定到`Courses`实体集。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

请注意，`EntityDataSource`控件的`Include`属性设置为`Department`。 在数据库中，`Course`表不包含部门名称; 它包含`DepartmentID`外键列。 如果要查询数据库直接，以获取部门名称以及课程的数据，必须加入`Course`和`Department`表。 通过设置`Include`属性设置为`Department`，指定实体框架应执行的相关工作`Department`实体时它获取`Course`实体。 `Department`实体然后存储在`Department`导航属性`Course`实体。 (默认情况下`SchoolEntities`由数据模型设计器生成的类时所需时间并将已绑定到该类中，因此，设置的数据源控件检索相关的数据`Include`属性不需要。 但是，将其设置可以提高性能的页上，因为否则 Entity Framework 会使分离的数据库调用来检索数据`Course`实体和相关`Department`实体。)

之后`EntityDataSource`控制您刚创建的插入以下标记来创建`QueryExtender`绑定到的控件`EntityDataSource`控件。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression`元素指定你想要选择其标题与在文本框中输入的值匹配的课程。 仅在文本框中输入尽可能多的字符进行比较，因为`SearchType`属性指定`StartsWith`。

`OrderByExpression`元素指定结果集将按部门名称中的课程标题。 请注意，指定院系名称的方式： `Department.Name`。 因为之间的关联`Course`实体和`Department`实体是一对一，`Department`导航属性包含`Department`实体。 （如果这是一个对多关系，该属性将包含一个集合。）若要获取部门名称，必须指定`Name`属性的`Department`实体。

最后，添加`GridView`控件来显示课程列表：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

第一列是显示院系名称的模板字段。 数据绑定表达式指定`Department.Name`，就像您在中看到`QueryExtender`控件。

运行页。 初始显示按部门、 然后按课程标题，按顺序显示所有课程的列表。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

输入"m"，然后单击**搜索**若要查看其标题以"m"（搜索不是区分） 开头的所有课程。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>使用"Like"运算符来筛选数据

您可以实现类似的效果`QueryExtender`控件的`StartsWith`， `Contains`，和`EndsWith`使用搜索类型`Like`中的运算符`EntityDataSource`控件的`Where`属性。 在本教程的此部分中，您将了解如何使用`Like`运算符按名称搜索的一名学生。

打开*Students.aspx*中**源**视图。 之后`GridView`控件，添加以下标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

此标记是类似于什么前面已经看到除`Where`属性值。 第二部分`Where`表达式定义的子字符串搜索 (`LIKE %FirstMidName% or LIKE %LastName%`) 搜索在文本框中输入的内容的第一个和最后一个名称。

运行页。 最初会显示所有学生的默认值为因为`StudentName`参数是"%"。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

在文本框中输入的字母"g"，然后单击**搜索**。 请参阅中的第一个或最后一个名称有"g"的学生列表。

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

现在显示、 更新、 筛选、 排序，还对各个表中的数据分组。 在下一教程中你将开始处理相关数据 （母版-详细信息方案）。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
