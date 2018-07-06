---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 4 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: 5f8b1c15fbfd2d65b603013db3902b42faa40665
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836783"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 4 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data"></a>使用相关数据

在上一教程使用了`EntityDataSource`到筛选器、 排序和分组数据的控件。 在本教程中将显示和更新相关的数据。

你将创建讲师页显示的讲师列表。 当您选择一名讲师时，您会看到由该讲师讲授的课程列表。 当您选择一门课程时，你将看到课程和参加该课程的学生列表的详细信息。 你可以编辑教师姓名、 雇佣日期和办公室分配。 办公室分配是通过导航属性访问单独的实体集。

您可以链接到标记中或在代码中的详细信息数据的主数据。 在本教程的此部分中，将使用这两种方法。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>显示和更新在 GridView 控件中的相关的实体

创建一个名为的新 web 页*Instructors.aspx* ，它使用*Site.Master*母版页，并添加到以下标记`Content`控件命名为`Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

此标记创建`EntityDataSource`控件，以选择讲师和启用更新。 `div`元素配置标记呈现在左侧，以便可以稍后添加在右侧的列。

之间`EntityDataSource`标记和结束`</div>`标记中，添加以下标记创建`GridView`控件和一个`Label`控件，将使用错误消息：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

这`GridView`控件启用行选择、 突出显示所选的行与一种浅灰色背景颜色，并指定的处理程序 （其中你将创建更高版本）`SelectedIndexChanged`和`Updating`事件。 它还指定`PersonID`为`DataKeyNames`属性，以便在所选行的键值可以传递到你稍后将添加的另一个控件。

最后一列包含的导航属性中存储的讲师的办公室分配`Person`实体因为来自关联的实体。 请注意，`EditItemTemplate`元素指定`Eval`而不是`Bind`，这是因为`GridView`控件不能直接绑定到导航属性来更新它们。 将更新代码中的办公室分配。 若要执行此操作，将需要对引用`TextBox`控件中，将获取并保存，在`TextBox`控件的`Init`事件。

遵循`GridView`控件是`Label`用于错误消息的控件。 控件的`Visible`属性是`false`，和视图状态处于关闭状态，以便该标签将显示仅当代码使其可见中出现错误。

打开*Instructors.aspx.cs*文件，并添加以下`using`语句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

分部类名称声明，以保存对 office 分配文本框中的引用后立即添加私有类字段。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

添加的存根`SelectedIndexChanged`事件处理程序，将为更高版本中添加代码。 此外将添加的办公室分配的处理程序`TextBox`控件的`Init`事件，以便可以将存储到的引用`TextBox`控件。 将使用此引用来获取用户输入以更新与导航属性关联的实体的值。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

将使用`GridView`控件的`Updating`要更新的事件`Location`属性关联的`OfficeAssignment`实体。 添加以下处理程序`Updating`事件：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

此代码的运行时在用户单击**更新**中`GridView`行。 代码使用 LINQ to Entities 来检索`OfficeAssignment`与当前关联的实体`Person`实体，使用`PersonID`从事件参数所选行。

代码然后会执行以下操作，具体取决于中的值之一`InstructorOfficeTextBox`控件：

- 如果在文本框中有一个值，并且没有任何`OfficeAssignment`实体来更新，它将创建一个。
- 如果在文本框中有一个值，并且没有`OfficeAssignment`实体，它会更新`Location`属性值。
- 如果文本框为空且`OfficeAssignment`实体存在，它会删除该实体。

在此之后，它将保存所做的更改到数据库。 如果发生异常，它将显示一条错误消息。

运行页。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

单击**编辑**和所有字段都更改为文本框中。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

更改任何这些值，包括**办公室分配**。 单击**更新**，将看到反映在列表中的更改。

## <a name="displaying-related-entities-in-a-separate-control"></a>在一个单独的控件中显示相关的实体

每一名讲师可以教授一个或多个课程，因此将添加`EntityDataSource`控件和一个`GridView`控件以列出与讲师中选择任何讲师的课程`GridView`控件。 若要创建标题和`EntityDataSource`控件的课程实体中，添加以下标记之间的错误消息`Label`控件和关闭`</div>`标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where`参数包含的值`PersonID`中选择其行讲师的`InstructorsGridView`控件。 `Where`属性包含一个可获取所有关联的嵌套 select 命令`Person`中的实体`Course`实体的`People`导航属性并选择`Course`实体仅当其中一个关联`Person`实体包含所选`PersonID`值。

若要创建`GridView`控件。 添加以下标记紧跟`CoursesEntityDataSource`控件 (在关闭前`</div>`标记):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

因为如果选择没有讲师时，将会不显示任何课程`EmptyDataTemplate`元素是包含。

运行页。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

选择有一个或多个课程分配，一名讲师和课程列表中显示。 (注意： 尽管数据库架构允许多个课程，但提供与数据库的测试数据中没有讲师实际上有多个课程。 您可以课程向数据库添加您自己使用**服务器资源管理器**窗口或*CoursesAdd.aspx*页上，你将添加在下一个教程。)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView`控件显示几个课程字段。 若要显示某课程的所有详细信息，请将使用`DetailsView`控件为用户选择课程。 中*Instructors.aspx*，将以下标记添加结束后`</div>`标记 (请确保将此标记**后**右 div 标记，不在此之前它):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

此标记创建`EntityDataSource`绑定到控件`Courses`实体集。 `Where`属性选择课程使用`CourseID`课程中的选定行的值`GridView`控件。 该标记指定的处理程序`Selected`事件，你将使用用于显示学生成绩的更高版本，它是另一个层次结构中较低的级别。

在中*Instructors.aspx.cs*，创建以下存根`CourseDetailsEntityDataSource_Selected`方法。 （你将填写此存根 （stub） 本教程的后面，现在，您需要它，因此该页将编译并运行。）

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

运行页。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

最初没有课程详细信息由于任何课程不选择。 选择有课程分配，一名讲师，然后选择一门课程，请参阅详细信息。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>使用 EntityDataSource"选择"事件，以显示相关的数据

最后，你想要显示的所有已注册的学生和所选课程及其成绩。 若要执行此操作，将使用`Selected`的事件`EntityDataSource`控件绑定到该课程`DetailsView`。

在中*Instructors.aspx*，添加以下标记后的`DetailsView`控件：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

此标记创建`ListView`显示的学生和所选课程及其成绩列表的控件。 由于将数据绑定控件在代码中，未不指定任何数据源。 `EmptyDataTemplate`元素提供任何课程不选择时显示一条消息，这种情况下，没有显示任何学生。 `LayoutTemplate`元素创建一个 HTML 表以显示的列表和`ItemTemplate`指定要显示的列。 学生 ID 和学生等级取自`StudentGrade`实体，并且学生姓名摘自`Person`实体框架使中可用的实体`Person`导航属性`StudentGrade`实体。

在*Instructors.aspx.cs*，将用作存根带`CourseDetailsEntityDataSource_Selected`方法使用以下代码：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

此事件的事件参数提供了一个集合，它将具有零个项，如果未选择任何内容或一个项的窗体中的所选的数据如果`Course`选择实体。 如果`Course`选择实体后，该代码使用`First`方法将集合转换为单个对象。 然后，它获取`StudentGrade`实体的导航属性，将其转换为一个集合，并将绑定`GradesListView`到集合的控件。

这足够大，以显示成绩，但你想要确保第一次显示的页将显示空数据模板中的消息，只要未选择一门课程。 若要执行此操作，创建以下方法，你将调用从两个位置：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

调用此新方法从`Page_Load`方法来显示将显示的页的空数据模板第一个时间。 并调用它从`InstructorsGridView_SelectedIndexChanged`方法时选择讲师时引发该事件，因为这意味着新课程加载到课程`GridView`尚未选择控件和 none。 下面是两个调用：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

运行页。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

选择讲师的课程分配，并选择课程。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

您现在已经了解了多种用于处理相关数据。 在以下教程中，您将学习如何添加现有实体之间的关系如何删除关系，以及如何添加新的实体具有与现有实体的关系。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-5.md)
