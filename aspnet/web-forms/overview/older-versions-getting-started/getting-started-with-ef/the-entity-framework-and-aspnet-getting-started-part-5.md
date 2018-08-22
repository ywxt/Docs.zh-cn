---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 5 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 3209ab3bca58e0dde90cf279732d177418b034e4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825991"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 5 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data-continued"></a>使用相关数据，继续执行

开始使用上一教程中`EntityDataSource`控件能够使用相关数据。 显示多个级别的层次结构和编辑导航属性中的数据。 在本教程中将继续使用相关数据，通过添加和删除关系以及添加新实体具有与现有实体的关系。

你将创建页添加课程分配给部门。 部门已经存在，并且在创建新的课程，同时你将建立它与现有院系之间的关系。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

你还将创建适用于多对多关系通过将一名讲师分配给一门课程 （添加您选择的两个实体之间的关系） 的页面或从一门课程中删除一名讲师 (删除两个实体之间的关系，您选择）。 在数据库中，添加一名讲师和课程之间的关系会导致新行添加到`CourseInstructor`关联表; 中删除关系涉及删除行从`CourseInstructor`关联表。 但是，您执行此操作在实体框架中通过参考的情况下设置导航属性`CourseInstructor`显式表。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>将具有关系的实体添加到现有实体

创建一个名为的新 web 页*CoursesAdd.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

此标记创建`EntityDataSource`选择课程，这样的插入，并且指定的的控件的处理程序`Inserting`事件。 将使用该处理程序来更新`Department`导航属性时的新`Course`创建实体。

标记还会创建`DetailsView`用于添加新控件`Course`实体。 此标记使用的绑定的字段`Course`实体属性。 你必须输入`CourseID`值，因为这不是系统生成的 ID 字段。 相反，它是创建过程时必须手动指定课程编号。

使用的模板字段`Department`导航属性因为导航属性不能用于`BoundField`控件。 模板字段提供用于选择院系的下拉列表。 下拉列表绑定到`Departments`实体集通过使用`Eval`而非`Bind`、 再次因为不能直接将导航属性绑定来更新它们。 指定的处理程序`DropDownList`控件的`Init`事件，以便你可以通过更新的代码中存储对用于控件的引用`DepartmentID`外键。

在中*CoursesAdd.aspx.cs*只是分部类声明后，添加一个类字段以保存对引用`DepartmentsDropDownList`控件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

添加的处理程序`DepartmentsDropDownList`控件的`Init`事件，以便可以将存储到控件的引用。 这样就可以获取用户输入的值，并使用它来更新`DepartmentID`的值`Course`实体。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

添加的处理程序`DetailsView`控件的`Inserting`事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

当用户单击`Insert`，则`Inserting`插入新记录之前引发事件。 在处理程序中的代码获取`DepartmentID`从`DropDownList`控制，并使用它来设置值将用于`DepartmentID`属性的`Course`实体。

实体框架将会负责处理添加到此课程`Courses`导航属性关联的`Department`实体。 它还会添加到部门`Department`导航属性`Course`实体。

运行页。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

输入 ID、 title、 数信用额度，并选择一个部门，然后单击**插入**。

运行*Courses.aspx*页，然后选择同一个部门，以确定新课程。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>使用多对多关系

之间的关系`Courses`实体集和`People`实体集是多对多关系。 一个`Course`实体具有名为的导航属性`People`，可以包含零、 一个或多个相关`Person`实体 （表示讲师分配该课程的教授）。 和一个`Person`实体具有名为的导航属性`Courses`，可以包含零、 一个或多个相关`Course`实体 (表示课程分配该讲师教授)。 一个讲师可能教授多个课程和一门课程可能由多位讲师讲授。 在本演练的此部分中，您将添加和删除之间的关系`Person`和`Course`通过更新相关的实体的导航属性的实体。

创建一个名为的新 web 页*InstructorsCourses.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

此标记创建`EntityDataSource`检索的名称的控件和`PersonID`的`Person`讲师的实体。 一个`DropDrownList`控件绑定到`EntityDataSource`控件。 `DropDownList`控制指定的处理程序`DataBound`事件。 你将使用此处理程序到 databind 这两个下拉列表中，显示课程。

标记还会创建将课程分配到所选讲师的使用的控件的以下组：

- 一个`DropDownList`用于选择一门课程，分配的控件。 使用当前未指派给所选讲师的课程，将填充此控件。
- 一个`Button`控件以启动分配。
- 一个`Label`控件来显示一条错误消息，如果分配将失败。

最后，标记还创建一组控件用于移除所选讲师的课程。

在中*InstructorsCourses.aspx.cs*，添加 using 语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

添加用于填充两个下拉列表显示课程的一个方法：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

此代码获取中的所有课程`Courses`实体集，并都获取从课程`Courses`导航属性`Person`显示所选讲师的实体。 然后，确定将哪些课程分配给该讲师，并相应地填充下拉列表。

添加的处理程序`Assign`按钮的`Click`事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

此代码获取`Person`显示所选讲师的实体获取`Course`选定课程的实体，并将添加到所选的课程`Courses`讲师的导航属性`Person`实体。 然后，将所做的更改保存到数据库并重新填充下拉列表，因此可以立即看到结果。

添加的处理程序`Remove`按钮的`Click`事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

此代码获取`Person`显示所选讲师的实体获取`Course`选定课程的实体，并删除从所选的课程`Person`实体的`Courses`导航属性。 然后，将所做的更改保存到数据库并重新填充下拉列表，因此可以立即看到结果。

将代码添加到`Page_Load`时没有错误报告，并为添加处理程序，可确保错误消息的方法不可见`DataBound`和`SelectedIndexChanged`讲师下拉列表来填充课程下拉列表的事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

运行页。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

选择讲师。 <strong>分配一门课程</strong>下拉列表显示的课程的教师不讲解，并<strong>删除一门课程</strong>下拉列表显示已分配给讲师的课程。 在中<strong>分配一门课程</strong>部分，选择一门课程，然后单击<strong>分配</strong>。 本课程将移到<strong>删除一门课程</strong>下拉列表。 选择在一门课程<strong>删除一门课程</strong>部分，然后单击<strong>删除</strong><em>。</em> 本课程将移到<strong>分配一门课程</strong>下拉列表。

现已了解其他一些方法，使用相关数据。 在以下教程中，您将了解如何在数据模型中使用继承来提高您的应用程序的可维护性。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
