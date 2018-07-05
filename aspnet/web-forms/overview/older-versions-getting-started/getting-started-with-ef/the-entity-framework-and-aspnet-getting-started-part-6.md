---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 6 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 99861197e00a3f2f6811ef13136fac63b993ef32
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372101"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 6 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="implementing-table-per-hierarchy-inheritance"></a>实现“每个层次结构一个表”继承

上一教程中你的相关数据处理，通过添加和删除关系以及添加新的实体具有与现有实体的关系。 本教程将演示如何在数据模型中实现继承。

在面向对象的编程中，可以使用继承以便更轻松地使用相关的类。 例如，可以创建`Instructor`并`Student`派生的类`Person`基类。 可以在实体框架中创建相同类型的实体之间的继承结构。

在本教程的此部分中，不会创建任何新的 web 页面。 相反，您将添加到数据模型派生实体和修改现有页面以使用新的实体。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每个-层次结构一个表与每个类型一个表继承

在一个表或多个表中，数据库可以存储相关对象的信息。 例如，在`School`数据库，`Person`表包含有关学生和教师单个表中的信息。 某些列仅适用于教师 (`HireDate`)，一些仅面向学生 (`EnrollmentDate`)，还有一些对两者 (`LastName`， `FirstName`)。

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

你可以配置 Entity Framework 以创建`Instructor`并`Student`继承的实体`Person`实体。 从单个数据库表生成实体继承结构的此模式称为*每个层次结构一个表*(TPH) 继承。

课程，`School`数据库使用了不同的模式。 在线课程和现场课程都存储在单独的表，其中每个外键指向`Course`表。 仅在存储信息普遍适用于这两种课程类型`Course`表。

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

可以配置实体框架数据模型，以便`OnlineCourse`并`OnsiteCourse`实体继承`Course`实体。 从单独为每种类型，与每个单独的表返回引用表，用于存储所有类型通用的数据的表生成实体继承结构的此模式称为*每种类型的表*(TPT) 继承。

TPH 继承模式通常比 TPT 继承模式，实体框架中提供更好的性能因为 TPT 模式会导致复杂的联接查询。 本演练演示如何实现 TPH 继承。 你将执行的操作，请执行以下步骤：

- 创建`Instructor`并`Student`派生的实体类型`Person`。
- 移动属性中的派生实体与相关`Person`到派生实体的实体。
- 在派生类型中设置属性的约束。
- 使`Person`实体抽象实体。
- 映射每个派生实体与`Person`具有一个条件以指定如何确定表是否`Person`行表示派生类型。

## <a name="adding-instructor-and-student-entities"></a>添加 Instructor 和 Student 实体

打开<em>SchoolModel.edmx</em>文件中，右键单击设计器中，选择中的未占用的区域<strong>添加</strong>，然后选择<strong>实体</strong><em>。</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

在中**添加实体**对话框中，实体名称`Instructor`并设置其**基类型**选项设为`Person`。

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

单击 **“确定”**。 在设计器创建`Instructor`派生的实体`Person`实体。 新的实体尚没有任何属性。

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

重复此过程来创建`Student`也派生的实体`Person`。

只有讲师有雇佣日期，因此您需要将该属性从移动`Person`实体与`Instructor`实体。 在中`Person`实体，右击`HireDate`属性，单击**剪切**。 然后右键单击**属性**中`Instructor`实体，然后单击**粘贴**。

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

雇佣日期`Instructor`实体不能为 null。 右键单击`HireDate`属性中，单击**属性**，然后在**属性**窗口中更改`Nullable`到`False`。

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

重复此过程来移动`EnrollmentDate`属性从`Person`实体与`Student`实体。 请确保还设置`Nullable`到`False`为`EnrollmentDate`属性。

既然`Person`实体包含所共有的属性`Instructor`和`Student`实体 （除了导航属性，它不移动），实体仅可作为中的继承结构的基实体。 因此，您需要确保永远不会视为一个独立的实体。 右键单击`Person`实体中，选择**属性**，然后在**属性**窗口中的值更改**抽象**属性设置为**True**。

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Instructor 和 Student 实体映射到 Person 表

现在，您需要告诉实体框架如何区分`Instructor`和`Student`数据库中的实体。

右键单击`Instructor`实体，然后选择**表映射**。 在中**映射详细信息**窗口中，单击**添加表或视图**，然后选择**人员**。

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

单击**添加一个条件**，然后选择**HireDate**。

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

更改**运算符**到**是**并**值 / 属性**到**Not Null**。

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

重复的过程`Students`实体，指定此实体将映射到`Person`表`EnrollmentDate`列不为 null。 然后保存并关闭数据模型。

生成项目中，以创建为类的新实体并使其可在设计器中。

## <a name="using-the-instructor-and-student-entities"></a>使用 Instructor 和 Student 实体

创建适用于学生和教师数据，则数据绑定到的网页时`Person`实体集，并筛选依据`HireDate`或`EnrollmentDate`属性将返回的数据限制为学生或教师。 但是，现在当您将绑定到每个数据源控件`Person`实体集，可以仅指定`Student`或`Instructor`应选择实体类型。 因为实体框架知道如何区分学生和教师中的`Person`实体集，可以删除`Where`你手动输入要执行此操作的属性设置。

在 Visual Studio 设计器中，您可以指定的实体类型`EntityDataSource`中选择控件应**EntityTypeFilter**下拉列表框中的`Configure Data Source`向导，如下面的示例中所示。

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

然后在**属性**窗口，可移除`Where`子句不再需要如下面的示例中所示的值。

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

但是，因为你已更改的标记`EntityDataSource`使用的控件`ContextTypeName`属性，则不能运行**配置数据源**向导上`EntityDataSource`已创建的控件。 因此，您将通过更改标记改为使所需的更改。

打开*Students.aspx*页。 在中`StudentsEntityDataSource`控件中，删除`Where`属性，并添加`EntityTypeFilter="Student"`属性。 现在，标记将类似于下面的示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

设置`EntityTypeFilter`属性可确保`EntityDataSource`控件将自动选择仅指定的实体类型。 如果你想要同时检索`Student`和`Instructor`实体类型，则不要设置此属性。 (您可以检索多个实体类型与一个`EntityDataSource`控制仅当您使用的只读数据访问的控件。 如果您使用的`EntityDataSource`控件插入、 更新或删除实体，并绑定到的实体集可以包含多个类型，如果仅使用一个实体类型，您必须将此属性设置。)

重复的过程`SearchEntityDataSource`控件，但只有的部分中删除`Where`属性选择`Student`而不是完全删除该属性的实体。 控件的开始标记现在将类似于下面的示例：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

运行页以验证它仍然可以像以前一样。

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

更新你在之前的教程中，以便他们使用新创建的以下页面`Student`并`Instructor`而不是实体`Person`实体，然后运行它们来验证它们按以前一样工作：

- 在中*StudentsAdd.aspx*，添加`EntityTypeFilter="Student"`到`StudentsEntityDataSource`控件。 现在，标记将类似于下面的示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- 在中*About.aspx*，添加`EntityTypeFilter="Student"`到`StudentStatisticsEntityDataSource`控制并删除`Where="it.EnrollmentDate is not null"`。 现在，标记将类似于下面的示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- 在*Instructors.aspx*并*InstructorsCourses.aspx*，将添加`EntityTypeFilter="Instructor"`到`InstructorsEntityDataSource`控制并删除`Where="it.HireDate is not null"`。 中的标记*Instructors.aspx*现在类似于下面的示例： 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    中的标记*InstructorsCourses.aspx*现在将类似于下面的示例：

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

这些更改会导致您改进了几种方式的 Contoso 大学应用程序的可维护性。 已移动从 UI 层的选择和验证逻辑 (*.aspx*标记) 并使其数据访问层的重要组成部分。 这有助于隔离可能会对数据库架构或数据模型进行在将来的更改从应用程序代码。 例如，可以决定学生可能雇佣教师的辅助工具为并会因此雇佣日期。 然后可以添加要将学生与教师区分开来，并更新数据模型的新属性。 Web 应用程序中的没有代码将需要更改除非你想要显示面向学生的雇佣日期。 添加的另一个好处`Instructor`和`Student`实体是你的代码是比时它称为可更轻松地理解`Person`都实际学生的对象或讲师。

现在已了解在实体框架中实现的继承模式的一种方法。 在以下教程中，将了解如何使用存储的过程，以便更好地控制实体框架访问数据库的方式。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-7.md)
