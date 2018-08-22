---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体的第 7 部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用实体框架的 ASP.NET Web 窗体应用程序。 示例应用程序是...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 48092838ac0b00137ae0a4e37391c31883afcd09
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824888"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Getting Started with Entity Framework 4.0 数据库和 ASP.NET 4 Web 窗体-第 7 部分
====================
通过[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 4.0 和 Visual Studio 2010 的 ASP.NET Web 窗体应用程序。 有关教程系列的信息，请参阅[系列中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="using-stored-procedures"></a>使用存储过程

在上一教程中，您将实现的每个层次结构一个表继承模式。 本教程将演示如何使用存储的过程来获得更好地控制数据库访问权限。

实体框架允许你指定它应将存储的过程用于数据库访问权限。 对于任何实体类型，可以指定要用于创建、 更新或删除该类型的实体的存储的过程。 然后在数据模型中可以添加到存储过程可用于执行任务，例如检索实体集的引用。

使用存储的过程是数据库访问权限的一个常见要求。 在某些情况下的数据库管理员可能需要的所有数据库访问都经历出于安全原因的存储过程。 在其他情况下您可能想要构建到实体框架在更新数据库时使用的进程的一些业务逻辑。 例如，删除某个实体时您可能想要将其复制到存档数据库。 或者，每次更新行时您可能想要一次更改该记录到日志记录表中写入行。 每当 Entity Framework 删除的实体或实体来更新实体时调用的存储过程中，可以执行这些类型的任务。

如前面的教程，你将不创建任何新页面。 相反，你将更改实体框架访问数据库，对于某些已创建的页面的方式。

在本教程中，你将创建用于插入数据库中的存储的过程`Student`和`Instructor`实体。 会将它们添加到数据模型中，并且你将指定实体框架应使用它们将添加`Student`和`Instructor`到数据库的实体。 此外将创建的存储的过程，可用于检索`Course`实体。

## <a name="creating-stored-procedures-in-the-database"></a>在数据库中创建存储的过程

(如果您使用的*School.mdf*文件从下载本教程项目中，则可以跳过本部分因为已存在存储的过程。)

在**服务器资源管理器**，展开*School.mdf*，右键单击**Stored Procedures**，然后选择**添加新存储过程**。

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

复制以下 SQL 语句并将其粘贴到存储的过程窗口中，替换主干存储的过程。

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 实体具有四个属性： `PersonID`， `LastName`， `FirstName`，和`EnrollmentDate`。 该数据库会自动生成的 ID 值和存储的过程接受其他三个参数。 存储的过程返回的新行的记录键的值，以便实体框架可以跟踪的它在内存中保留的实体的版本中。

保存并关闭存储的过程窗口中。

创建`InsertInstructor`中相同的方式，使用以下 SQL 语句的存储过程：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

创建`Update`存储过程`Student`和`Instructor`实体还。 (数据库中已经有`DeletePerson`存储过程，这将适用于两者`Instructor`和`Student`实体。)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

在本教程中，您将映射所有三个函数-insert、 update 和 delete-每个实体类型。 Entity Framework 版本 4，您可以将映射只是一个或两个函数到存储过程，而无需映射其他用户，有一个例外： 如果映射 update 函数，但不是删除函数，实体框架将引发异常时，尝试删除实体。 在 Entity Framework 版本 3.5 中，您没有映射的存储的过程中如此大的灵活性： 如果您已映射到一个函数都需要映射所有三个。

若要创建读取而不更新数据的存储的过程，创建一个选择所有`Course`实体，使用以下 SQL 语句：

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>将存储的过程添加到数据模型

在数据库中，现在定义的存储的过程，但必须将它们添加到要向实体框架提供的数据模型。 打开*SchoolModel.edmx*，右键单击设计图面上，然后选择**从数据库更新模型**。 在**添加**选项卡**选择数据库对象**对话框中，展开**Stored Procedures**，选择新创建的存储的过程和`DeletePerson`存储过程，然后依次**完成**。

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>映射存储的过程

在数据模型设计器中，右键单击`Student`实体，然后选择**存储过程映射**。

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

**映射详细信息**窗口随即出现，可以在其中指定实体框架应使用的插入、 更新和删除此类型的实体的存储的过程。

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

设置**插入**函数来**InsertStudent**。 窗口显示的存储的过程参数，其中每个必须映射到实体属性的列表。 原因是名称相同，两个都自动映射。 不存在名为实体属性`FirstName`，因此必须手动选择`FirstMidName`从下拉列表，显示可用的实体属性。 (这是因为更改的名称`FirstName`属性设置为`FirstMidName`中的第一个教程。)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

在同一**映射详细信息**窗口中，映射`Update`函数来`UpdateStudent`存储过程 (请确保指定`FirstMidName`的参数值作为`FirstName`，如你对`Insert`存储过程） 和`Delete`函数来`DeletePerson`存储过程。

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

请遵循相同的过程来映射 insert、 update 和 delete 存储过程用于为讲师`Instructor`实体。

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

对于读取而不是更新数据的存储过程，您使用**模型浏览器**窗口，以将存储的过程映射到实体类型将其返回。 在数据模型设计器中，右键单击设计图面并选择**模型浏览器**。 打开**SchoolModel.Store**节点，然后打开**存储过程**节点。 然后右键单击`GetCourses`存储过程，然后选择**添加函数导入**。

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

在中**添加函数导入**对话框中的**返回集合的**选择**实体**，然后选择`Course`作为实体类型返回。 完成后，单击**确定**。 保存并关闭 *.edmx*文件。

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>使用 Insert、 Update 和 Delete 存储的过程

存储的过程以插入、 更新和删除数据后已添加到数据模型和映射到相应的实体会自动由实体框架使用。 现在可以运行*StudentsAdd.aspx*页上，并每次创建新的学生，将使用实体框架`InsertStudent`存储过程来添加新行`Student`表。

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

运行*Students.aspx*页和新的学生将显示在列表中。

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

更改名称，以验证更新函数工作，然后再删除该学生验证的删除函数正常工作。

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>使用选择的存储的过程

实体框架不会自动运行存储的过程如`GetCourses`，并不能将其用于`EntityDataSource`控件。 若要使用它们，它们从代码调用。

打开*InstructorsCourses.aspx.cs*文件。 `PopulateDropDownLists`方法使用 LINQ 到 Entities 查询来检索所有 course 实体，以便它可以循环访问列表并确定的哪些分配给讲师，哪些是未分配：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

将此替换为以下代码：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

页面现在使用`GetCourses`存储过程来检索所有课程的列表。 运行页以验证它像以前一样工作。

(使用与这些实体，具体取决于相关的数据，存储过程来检索的实体的导航属性可能不自动填充`ObjectContext`默认设置。 有关详细信息，请参阅[加载相关对象](https://msdn.microsoft.com/library/bb896272.aspx)MSDN 库中。)

在下一步的教程中，您将了解如何使用动态数据功能来轻松地计划和测试数据格式设置和验证规则。 而不是指定每个网页规则，如数据格式字符串和字段是必填上，可以在数据模型元数据中指定此类规则，这些自动应用在每一页上。

> [!div class="step-by-step"]
> [上一页](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [下一页](the-entity-framework-and-aspnet-getting-started-part-8.md)
