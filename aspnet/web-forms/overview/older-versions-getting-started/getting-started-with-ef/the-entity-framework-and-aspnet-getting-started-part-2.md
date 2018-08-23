---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 2 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: a0b4acca93deee4fb514fa1bc3e2bd13490cf10e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832248"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 2 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="the-entitydatasource-control"></a>EntityDataSource 控件

上一教程中创建网站、 数据库和数据模型。 在本教程中使用`EntityDataSource`ASP.NET 提供了以使其更易于使用的实体框架数据模型的控件。 你将创建`GridView`控件用于显示和编辑学生数据`DetailsView`添加新学生，控件和一个`DropDownList`用于选择院系 （其中你将使用用于显示关联的课程的更高版本） 的控件。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

请注意，在此应用程序也不会输入的验证向添加更新数据库页的错误处理一些不会可靠就需要在生产应用程序中。 该保留本教程侧重于实体框架，并将其保留从获取太长。 有关如何将这些功能添加到你的应用程序的详细信息，请参阅[验证用户输入在 ASP.NET Web Pages](https://msdn.microsoft.com/library/7kh55542.aspx)并[中的 ASP.NET 网页和应用程序的错误处理](https://msdn.microsoft.com/library/w16865z6.aspx)。

## <a name="adding-and-configuring-the-entitydatasource-control"></a>添加和配置 EntityDataSource 控件

您将首先配置`EntityDataSource`控件来读取`Person`中的实体`People`实体集。

请确保已打开的 Visual Studio 并且你正在使用该项目创建第 1 部分中。 如果尚未生成项目，因为您创建数据模型或自上一次更改后对其所做，现在生成项目。 对数据模型的更改将不会提供给设计器之前生成项目。

创建新的 web 页面使用**使用母版页的 Web 窗体**模板，并将其命名*Students.aspx*。

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

指定*Site.Master*作为主页面。 所有页面创建为这些教程将使用此母版页。

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

在中**源**视图中，添加`h2`到标题`Content`控件命名为`Content2`，如以下示例所示：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

从**数据**选项卡**工具箱**，将`EntityDataSource`控制对页面、 将其放在标题下方和更改为 ID `StudentsEntityDataSource`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

切换到**设计**查看，单击数据源控件的智能标记，然后单击**配置数据源**以启动**配置数据源**向导。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

在**配置 ObjectContext**向导步骤中，选择**SchoolEntities**的值作为**名为连接**，然后选择**SchoolEntities**作为**DefaultContainerName**值。 然后，单击 **“下一步”**。

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

注意： 如果在这种情况下获取下列对话框中，你必须继续下一步前生成项目。

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

在中**配置数据选择**步骤中，选择**人**的值作为**EntitySetName**。 下**选择**，请确保**选择一个**ll 复选框处于选中状态。 然后选择要启用更新和删除的选项。 完成后，单击**完成**。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>配置数据库规则以允许删除

您将创建一个允许用户删除来自学生页面`Person`具有与其他表的三个关系的表 (`Course`， `StudentGrade`，和`OfficeAssignment`)。 默认情况下，数据库会阻止你删除中的行`Person`如果有一个其他表中的相关的行。 首先，可以手动删除相关的行，或者可以配置数据库删除时自动删除它们`Person`行。 对于本教程中的学生记录，将配置要自动删除相关的数据的数据库。 由于学生可以具有相关的行仅在`StudentGrade`表中，你需要配置三个关系之一。

如果您使用的*School.mdf*文件下载从与本教程中的项目中，可以跳过本部分中，因为这些配置更改已完成。 如果通过运行脚本创建数据库，请通过执行以下步骤配置该数据库。

在中**服务器资源管理器**，打开你在第 1 部分中创建的数据库关系图。 右键单击之间的关系`Person`并`StudentGrade`（表之间的行），然后选择**属性**。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

在中**属性**窗口中，展开**INSERT 和 UPDATE 规范**并设置**DeleteRule**属性设置为**Cascade**。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

保存并关闭关系图。 如果系统提示您是否要更新数据库，请单击**是**。

若要确保模型保留在内存中数据库的作用与同步的实体，必须在数据模型中设置相应的规则。 打开*SchoolModel.edmx*，右键单击之间的关联连线`Person`并`StudentGrade`，然后选择**属性**。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

在中**属性**窗口中，将**End1 OnDelete**到**级联**。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

保存并关闭*SchoolModel.edmx*文件，然后再重新生成项目。

一般情况下，当在数据库发生更改，必须如何同步处理模型的多个选项：

- 对于某些类型的更改 （例如添加或刷新表、 视图或存储的过程），用鼠标右键单击在设计器中，选择**从数据库更新模型**自动具有设计器使所做的更改。
- 重新生成数据模型。
- 请手动更新此类似。

在这种情况下，无法重新生成模型或刷新受关系更改的表，但然后您将不得不再次进行更改后的字段名称 (从`FirstName`到`FirstMidName`)。

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>使用 GridView 控件以读取和更新实体

在本部分将使用`GridView`控件以显示、 更新或删除学生。

打开或切换到*Students.aspx* ，并切换到**设计**视图。 从**数据**选项卡**工具箱**，拖动`GridView`右侧的控件`EntityDataSource`控件，将其`StudentsGridView`，单击智能标记，并选择**StudentsEntityDataSource**作为数据源。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

单击**刷新架构**(单击**是**如果系统提示确认)，然后单击**启用分页**，**启用排序**， **启用编辑**，并**启用删除**。

单击**编辑列**。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

在**所选字段**框中，删除**PersonID**， **LastName**，以及**HireDate**。 通常不显示给用户的记录密钥、 雇佣日期与学生，并不会将名称的两个部分放在一个字段，因此您只需要一个名称字段。）

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

选择**FirstMidName**字段，然后单击**此字段转换为 TemplateField**。

执行相同操作**EnrollmentDate**。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

单击**确定**，然后切换到**源**视图。 剩余的更改都将更轻松地在标记中直接执行。 `GridView`控制标记现在会查找将如下例所示。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

第一列后命令字段是一个模板字段的当前显示的第一个名称。 更改此模板字段以类似于以下示例的标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

在显示模式下，两个`Label`控件显示的第一个和最后一个名称。 在编辑模式，因此您可以更改的第一个和最后一个名称提供两个文本框。 如同`Label`中的控件显示模式，则使用`Bind`和`Eval`表达式可以像使用直接连接到数据库的 ASP.NET 数据源控件。 唯一的区别是指定实体属性，而不是数据库列。

最后一列是一个模板字段，显示注册日期。 更改此字段以类似于以下示例的标记：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

在这种显示和编辑模式下，"{0，d}"的格式字符串会导致显示"short date"格式的日期。 （您的计算机可能配置为显示此格式以不同的方式从本教程中所示的屏幕图像。）

请注意，在每个这些模板字段，在设计器使用`Bind`表达式中的，通过默认情况下，但您已更改为`Eval`中的表达式`ItemTemplate`元素。 `Bind`表达式使数据中可用`GridView`控制属性，以防需要访问代码中的数据。 在此页中，不需要访问在代码中，此数据，因此，可以使用`Eval`，这是更高效。 有关详细信息，请参阅[将数据从数据控件](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)。

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>修订 EntityDataSource 控件标记，以提高性能

中的标记`EntityDataSource`控件中，删除`ConnectionString`并`DefaultContainerName`属性，并将其替换为`ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`属性。 这是每次创建时应进行的更改`EntityDataSource`控制，除非您需要使用不同于对象上下文类中硬编码的连接。 使用`ContextTypeName`属性提供以下优势：

- 性能更好。 当`EntityDataSource`控件初始化数据模型使用`ConnectionString`和`DefaultContainerName`属性，它执行其他工作要加载的每个请求中的元数据。 这不是必需的如果指定`ContextTypeName`属性。
- 默认情况下，生成的对象上下文类中启用延迟加载 (如`SchoolEntities`在本教程中) 中 Entity Framework 4.0。 这意味着，导航属性与相关数据时自动加载右需要它。 延迟加载是在本教程后面所述更多详细信息。
- 已应用于对象上下文类的任何自定义 (在这种情况下，`SchoolEntities`类) 将可供使用的控件`EntityDataSource`控件。 自定义对象上下文类是本系列教程中未涉及的高级的主题。 有关详细信息，请参阅[扩展实体框架生成类型](https://msdn.microsoft.com/library/dd456844.aspx)。

现在，标记将类似于下面的示例 （属性的顺序可能不同）：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening`属性是指由于外键列不公开为实体属性在早期版本的实体框架所需的功能。 当前版本可以使用*外键关联*，这意味着外键属性公开的以外的所有多对多关联。 如果你的实体具有外键属性和否[复杂类型](https://msdn.microsoft.com/library/bb738472.aspx)，可以将此属性设置为`False`。 不删除该属性从标记中，由于默认值为`True`。 有关详细信息，请参阅[平展对象 (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx)。

运行页面，您看到的学生和 （您将筛选为只是学生在下一教程中） 的员工列表。 名字和姓氏显示在一起。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

若要排序显示，请单击列名称。

单击**编辑**任意行中。 文本框将显示您可以在其中更改第一个和最后一个名称。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

**删除**按钮也起作用。 对于具有注册日期的行和行消失后，单击删除。 （没有注册日期的行表示讲师和可能会收到引用完整性错误。 在下一教程中，将筛选此列表只是学生。）

## <a name="displaying-data-from-a-navigation-property"></a>显示一个导航属性中的数据

现在假设你想要知道多少课程中注册每个学生。 实体框架提供了在该信息`StudentGrades`导航属性`Person`实体。 由于数据库设计不允许学生课程中注册，而无需分配的等级，对于本教程可以假定该中具有一行`StudentGrade`与课程相关联的表行是与正在参加该课程相同。 (`Courses`导航属性是仅为讲师。)

当你使用`ContextTypeName`属性的`EntityDataSource`控件，实体框架自动检索导航属性的信息时访问该属性。 这称为*延迟加载*。 但是，这可能效率低下，因为这会导致单独调用每个时间的其他信息所需的数据库。 如果您需要为返回的每个实体的导航属性中的数据`EntityDataSource`控件，它是效率，以检索相关的数据以及对数据库的单个调用中的实体本身。 这称为*预先加载*，并通过设置指定的导航属性的预先加载`Include`属性的`EntityDataSource`控件。

在中*Students.aspx*，你想要显示的每个学生的数量的课程，因此预先加载是最佳选择。 如果已显示的所有学生但显示数量的课程仅为几个它们 （这需要编写除了标记以外的一些代码），延迟加载可能更好的选择。

打开或切换到*Students.aspx*，切换到**设计**视图中，选择`StudentsEntityDataSource`，然后在**属性**窗口中设置**Include**属性设置为**StudentGrades**。 (如果您想要获取多个导航属性，则可以指定以逗号分隔其名称 — 例如， **StudentGrades、 课程**。)

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

切换到**源**视图。 在中`StudentsGridView`控件，在最后一个`asp:TemplateField`元素中，添加以下新的模板字段：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

在中`Eval`表达式，可以引用导航属性`StudentGrades`。 此属性包含一个集合，因为它具有`Count`可用于显示在其中注册学生的课程数量的属性。 在更高版本的教程中你将了解如何以显示包含而不是集合的单个实体的导航属性中的数据。 (请注意，不能使用`BoundField`元素来显示导航属性中的数据。)

运行页面，您现在看到多少课程学生中注册。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>使用 DetailsView 控件插入实体

下一步是创建一个页，具有`DetailsView`就可以添加新学生的控件。 关闭浏览器，然后创建新的 web 页面使用*Site.Master*母版页。 将该页命名为*StudentsAdd.aspx*，然后切换到**源**视图。

添加以下标记替换的现有标记`Content`名为控件`Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

此标记创建`EntityDataSource`类似于在你创建的控件*Students.aspx*，但它可用于插入。 如同`GridView`控制的绑定的字段`DetailsView`控件完全相同，只不过它们引用的实体属性的数据控件的直接连接到数据库中，为进行编码。 在这种情况下，`DetailsView`控件仅用于插入行，因此已将默认模式设置为`Insert`。

运行页面，并添加新学生。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

但是，如果现在运行插入新学生之后, 不会发生*Students.aspx*，你将看到新学生信息。

## <a name="displaying-data-in-a-drop-down-list"></a>在下拉列表中显示数据

在以下步骤将 databind`DropDownList`控制实体集使用到`EntityDataSource`控件。 在本教程的此部分中，不会执行很多与此列表。 不过，在后续部分将使用列表以允许用户选择院系，以显示课程与系关联。

创建一个名为的新 web 页*Courses.aspx*。 在中**源**视图中，添加到标题`Content`控件名为`Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

在中**设计**视图中，添加`EntityDataSource`到页面的控件一样，除这一次其命名为`DepartmentsEntityDataSource`。 选择**部门**作为**EntitySetName**值，并选择仅**DepartmentID**并**名称**属性。

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

从**标准**选项卡**工具箱**，将`DropDownList`控制对页面，将其命名`DepartmentsDropDownList`，单击智能标记，然后选择**选择数据源**到启动**数据源配置向导**。

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

在中**选择数据源**步骤中，选择**DepartmentsEntityDataSource**作为数据源中，单击**刷新架构**，然后选择**名称**作为要显示的数据字段和**DepartmentID**作为值数据字段。 单击 **“确定”**。

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

如与其他 ASP.NET 数据源控件，在指定的实体和实体属性，您使用数据绑定到控件使用实体框架的方法都是相同的。

切换到**源**查看和添加"选择系:"之前`DropDownList`控件。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

请注意，更改的标记`EntityDataSource`控件现在通过替换`ConnectionString`并`DefaultContainerName`属性与`ContextTypeName="ContosoUniversity.DAL.SchoolEntities"`属性。 最好是通常创建在更改之前链接到数据源控件的数据绑定控件后等待，直到`EntityDataSource`控制标记，因为进行更改后，在设计器将不会提供与您**刷新架构**数据绑定控件中的选项。

运行该页并从下拉列表中选择一个部门。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

这将完成介绍如何使用`EntityDataSource`控件。 使用此控件具有通常与使用其他 ASP.NET 数据源控件，没有什么不同，只不过你引用的实体和属性而不是表和列。 唯一的例外是当你想要访问导航属性。 在下一教程中将看到语法使用`EntityDataSource`控件可能也不同于其他数据源控件时筛选、 分组和排序数据。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-3.md)
