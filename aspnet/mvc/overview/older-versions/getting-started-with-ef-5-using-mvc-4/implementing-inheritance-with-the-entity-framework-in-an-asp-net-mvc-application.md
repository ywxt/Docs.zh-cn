---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (8 为 10) 中实现与实体框架的继承 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d3c3d19a62f601d007b0fac031ade1eef9f35771
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378931"
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>在 ASP.NET MVC 应用程序 (8 为 10) 中实现继承，使用实体框架
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


在上一教程中，你将处理并发异常。 本教程将演示如何在数据模型中实现继承。

在面向对象的编程中，可以使用继承来消除冗余代码。 在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。 不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>每个-层次结构一个表与每个类型一个表继承

在面向对象的编程中，可以使用继承以便更轻松地使用相关的类。 例如，`Instructor`并`Student`中的类`School`数据模型共享多个属性，这会导致冗余代码：

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。 您可以创建`Person`基类其中只包含这些共享属性，请`Instructor`和`Student`实体继承自该基类，如以下插图所示：

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

有多种方法可以在数据库中表示此继承结构。 您可以`Person`包括有关学生和教师单个表中的信息的表。 某些列可能仅适用于教师 (`HireDate`)，一些仅面向学生 (`EnrollmentDate`)、 一些对这两个 (`LastName`， `FirstName`)。 通常情况下，您必须*鉴别器*指示哪种类型的每一行的列表示。 例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。

![每个 hierarchy_example 表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

从单个数据库表生成实体继承结构的此模式称为*每个层次结构一个表*(TPH) 继承。

另一种方法是使数据库看起来更像继承结构。 例如，您可以仅将姓名字段`Person`表，并具有单独`Instructor`和`Student`具有日期字段的表。

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

此模式的数据库表，针对每个实体的类称为进行*每种类型的表*(TPT) 继承。

TPH 继承模式通常比 TPT 继承模式，实体框架中提供更好的性能因为 TPT 模式会导致复杂的联接查询。 本教程将演示如何实现 TPH 继承。 你将执行的操作，请执行以下步骤：

- 创建`Person`类，并更改`Instructor`并`Student`类继承`Person`。
- 将模型数据库的映射代码添加到数据库上下文类。
- 更改`InstructorID`并`StudentID`整个到项目引用`PersonID`。

## <a name="creating-the-person-class"></a>创建 Person 类

 注意： 你将无法创建下面的类，直到更新使用这些类的控制器后编译项目。 

在中*模型*文件夹中，创建*Person.cs*和模板代码替换为以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

在中*Instructor.cs*，派生`Instructor`类`Person`类，并删除键和姓名字段。 代码将如下所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

进行到类似的更改*Student.cs*。 `Student`类看起来如下例所示：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>将 Person 实体类型添加到模型

在中*SchoolContext.cs*，添加`DbSet`属性`Person`实体类型：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。 当您将看到，当数据库是重新创建，它将具有`Person`表来代替`Student`和`Instructor`表。

## <a name="changing-instructorid-and-studentid-to-personid"></a>更改为 PersonID InstructorID 和 StudentID

在中*SchoolContext.cs*，在讲师-课程映射语句中，更改`MapRightKey("InstructorID")`到`MapRightKey("PersonID")`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

此更改不是必需的;它仅更改在多对多联接表中的 InstructorID 列的名称。 如果保留 InstructorID 作为名称，该应用程序将仍正常工作。 下面是已完成*SchoolContext.cs*:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

接下来你需要更改`InstructorID`到`PersonID`并`StudentID`到`PersonID`在整个项目***除***加盖时间戳迁移文件中*迁移*文件夹。 若要执行此操作将查找和打开文件，需要进行更改，然后在打开的文件上执行全局更改。 中唯一的文件*迁移*应更改的文件夹是*migrations\ configuration.cs。*

1. > [!IMPORTANT]
   > 首先关闭 Visual Studio 中所有打开的文件。
2. 单击**查找和替换--的所有文件**中**编辑**菜单中，并在项目中包含的所有文件然后搜索`InstructorID`。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 打开每个文件中的**查找结果**窗口***除***&lt;时间戳&gt;*\_.cs* 中的迁移文件*迁移*文件夹中，通过双击每个文件的一行。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 打开**在文件中替换**对话框，并更改**查找**到**所有打开的文档**。
5. 使用**在文件中替换**对话框，可以更改所有`InstructorID`到 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 包含在项目中找到的所有文件`StudentID`。
7. 打开每个文件中的**查找结果**窗口***除***&lt;时间戳&gt;*\_\*.cs*迁移文件在中*迁移*文件夹中，通过双击每个文件的一行。  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 打开**在文件中替换**对话框，并更改**查找**到**所有打开的文档**。
9. 使用**在文件中替换**对话框，可以更改所有`StudentID`到`PersonID`。   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 生成项目。

(请注意，此示例演示*缺点*的`classnameID`命名主键的模式。 如果不前缀的类名称，命名主键 ID*没有*重命名需要现在。)

## <a name="create-and-update-a-migrations-file"></a>创建和更新的迁移文件

在包管理器控制台 (PMC) 中，输入以下命令：

`Add-Migration Inheritance`

运行`Update-Database`PMC 命令。 该命令将在这里失败，因为我们已将迁移并不知道如何处理的现有数据。 你收到以下错误：

*ALTER TABLE 语句与 FOREIGN KEY 约束冲突"FK\_dbo。部门\_dbo。人员\_PersonID"。冲突发生于数据库"ContosoUniversity"表"dbo。Person"，列 PersonID。*

打开*迁移\&l t; 时间戳&gt;\_Inheritance.cs* ，并将为`Up`方法使用以下代码：

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

运行`update-database`试命令。

> [!NOTE]
> 就可以将迁移数据，也使架构更改时遇到其他错误。 如果获取的迁移错误则不能解决，可以通过更改中的连接字符串来继续本教程*Web.config*文件或删除的数据库。 最简单方法是在数据库重命名*Web.config*文件。 例如，将数据库名称更改为 CU\_测试，如以下示例所示：
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 使用新数据库没有数据迁移，和`update-database`命令是更有望完成且未出错。 有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。 如果你接受这种方法，以继续本教程，跳过部署步骤放在结束本教程中，由于已部署的站点会产生相同的错误，它会自动运行迁移时。 如果你想要解决的迁移错误，最佳资源是 Entity Framework 论坛或 StackOverflow.com 之一。


## <a name="testing"></a>正在测试

运行站点，并尝试各种页面。 一切都和以前一样。

中**服务器资源管理器**展开**SchoolContext** ，然后**表**，并可以看到**学生**和**讲师**已替换为表**人员**表。 展开**Person**表，会看到它具有所有使用中的列**学生**并**讲师**表。

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

下图说明了新的 School 数据库的结构：

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>总结

现在为实现每个层次结构一个表继承`Person`， `Student`，和`Instructor`类。 有关此设置和其他继承结构的详细信息，请参阅[继承映射策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)Morteza Manavi 博客上。 在下一教程中，您将看到一些方法来实现存储库和工作单元模式。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
