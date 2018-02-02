---
title: "ASP.NET 核心 MVC 与 EF 核心-继承-9 的 10"
author: tdykstra
description: "本教程将演示如何在数据模型中，ASP.NET Core 应用程序中使用实体框架核心实现继承。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/inheritance
ms.openlocfilehash: 985cc38b10ef830b8274e40ad5f7050157fd4d86
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="inheritance---ef-core-with-aspnet-core-mvc-tutorial-9-of-10"></a>EF  Core 和 ASP.NET  Core  MVC 教程 —— 继承 (9 / 10)
作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 有关系列教程的详细信息，请参阅[第一个教程](intro.md)。

通过前面的教程，你学会了处理并发异常。 本教程将演示如何在数据模型中实现继承。

在面向对象编程中，你可以使用继承以便于代码重用。通过本教程，你将更改`Instructor`和`Student`类，使其派生自基本的`Person`类，其中包含导师和学生所共有的属性，如`LastName`。 更改这些类不会添加或更改任何 web 页面，但需要更改某些代码，这些更改将自动反映在数据库中。

## <a name="options-for-mapping-inheritance-to-database-tables"></a>将继承映射到数据库表

在学校的数据模型中`Instructor`和`Student`类具有多个相同的属性：

![学生和导师类](inheritance/_static/no-inheritance.png)

假设你想要消除`Instructor`和`Student`实体共享属性的冗余代码， 或者，想要编写一个服务用于格式化姓名而无需了解姓名来自一个导师还是学生。 你可以创建一个仅包含那些共享属性`Person`基类，然后`Instructor`和`Student`类都继承自该基类，如下面的插图中所示：

![学生和导师从人员类派生的类](inheritance/_static/inheritance.png)

有几种方法在数据库中表示此继承结构。 你可以在一个 Person 表中同时包含学生和导师的基本信息。 某些列 (如 HireDate) 可能仅适用于导师，某些列 (如 EnrollmentDate)仅适用于学生，某些列 (L如 astName、 FirstName)则两者通用。 通常情况下，你必须用一个标识列来指示每一行属于哪种类型。 例如，导师的标识列可能有"Instructor"而学生则是"Student"。

![表每个层次结构示例](inheritance/_static/tph.png)

这种通过单个数据库表来构建实体继承结构的模式称为单体系单表 (table-per-hierarchy TPH) 继承模式

一种替代方法是使数据库的结构看上去更像继承。 例如，在 Person 表中只有姓名字段，然后拥有单独的导师和学生表，各自包含其特有的日期字段。

![每种类型一个表继承](inheritance/_static/tpt.png)

这种模式使得每个实体由有其对应的数据库表，这种模式称为单类型单表 (table-per-type TPT) 继承模式。

另一种方法是将所有的非抽象类型映射到单个表。 类中包括继承的属性在内的所有属性将都映射为表中相应的列。 此模式称为单个具体类单表 (table-per-concrete-class TPC) 继承模式。 如果你像之前的教程那样对人员、 学生和导师类使用 TPC 继承，Student 与 Instructor 表在实现继承之后与之前没有什么不同。

TPC 和 TPH 继承模式通常比 TPT 继承模式有更好的性能，因为 TPT 模式可能会导致复杂的联接查询。

本教程会演示如何实现 TPH 继承。 TPH 是 Entity Framework Core 支持的唯一一中继承模式。  你将执行的操作是创建`Person`类中，使`Instructor`和`Student`类派生自`Person`，将新的类添加到`DbContext`，然后创建迁移。

> [!TIP] 
> 请再进行以下更改之前保存项目的副本。之后如果你遇到问题，需要从头开始的话，副本可以使你更轻松地从已保存的项目中重新开始，而不需要从第一个教程开始复原整个项目。

## <a name="create-the-person-class"></a>创建 Person 类

在 Models 文件夹中，创建 Person.cs 并将模板代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/Person.cs)]

## <a name="make-student-and-instructor-classes-inherit-from-person"></a>使 Student 和 Instructor 类继承自 Person 类

在*Instructor.cs*中， 从 Person 类派生出 Instructor 类并删除key和姓名字段。 代码如下所示：

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_AfterInheritance&highlight=8)]

对*Student.cs*进行相同的修改。

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_AfterInheritance&highlight=8)]

## <a name="add-the-person-entity-type-to-the-data-model"></a>将 Person 实体类型添加到数据模型

将 Person 实体类型添加到*SchoolContext.cs*。 高亮代码显示新添加的行。

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_AfterInheritance&highlight=19,30)]

这是 Entity Framework 实现单体系单表 (TPH) 继承模式所需的所有配置。 如你所见，当更新数据库时，它将使用 Person 表代替 Student 与 Instructor 表 。

## <a name="create-and-customize-migration-code"></a>创建并自定义迁移代码

保存所做的更改并生成项目。 然后在项目文件夹中打开命令窗口并输入以下命令：

```console
dotnet ef migrations add Inheritance
```

先不要运行`database update`命令。 该命令会导致数据丢失，因为它将删除 Instructor 表以及将 Student 表重命名为 Person。 你需要自定义代码来保留现有数据。

打开*迁移 /\<时间戳 > _Inheritance.cs*并将`Up`方法替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Migrations/20170216215525_Inheritance.cs?name=snippet_Up)]

此代码将负责以下数据库更新任务：

* 删除外键约束和指向 Student 表的索引。

* 将 Instructor 表重命名为 Person ，并使它可以用来存储学生数据作出所需更改：

* 为学生添加可以为 null EnrollmentDate 。

* 添加标识列来表明该行是名学生还是导师。

* 使雇用日期可以为 null，因为学生行不需要雇佣日期。

* 添加临时字段，用于更新指向学生的外键。 当将学生复制到 Person 表时他们将获得新的主键值。

* 将数据从 Person 表复制到学生表。 这将导致学生获得一个新的主键值。

* 修复指向学生的外键值。

* 重新创建外键约束和索引，将它们指向 Person 表。

（如果你在主键类型使用的是 GUID 而不是整数类型，学生主键值不需要更改，并且这些步骤可以被省略。）

运行`database update`命令：

```console
dotnet ef database update
```

(在生产系统中需要改变相应的`Down`方法以返回到以前的数据库版本。 本教程中你不会使用到`Down`方法。)

> [!NOTE] 
> 数据库在有数据的情况下进行架构更改时，很有可能会发生其他错误。 如果您不能解决迁移错误，你可以更改连接字符串中的数据库名称，或删除数据库。 在新数据库中，没有数据需要迁移，update-database命令更有可能完成且不发生错误。可以使用 SSOX 或运行`database drop`CLI 命令来删除数据库。

## <a name="test-with-inheritance-implemented"></a>测试实现继承后的应用

运行应用程序并尝试各种页面。 一切都和之前一样。

在**SQL Server 对象资源管理器**，展开**数据连接/SchoolContext**然后展开**表**，可以看到 Student 和 Instructor 表 已经被 Person 表所取代。 打开 Person 表设计器，您看到它具有用于 Student 与 Instructor 表的所有列。

![在 SSOX 中 person 表](inheritance/_static/ssox-person-table.png)

右键单击 Person 表，然后单击**显示表数据**可以看到标识列。

![在 SSOX-表数据中的 person 表](inheritance/_static/ssox-person-data.png)

## <a name="summary"></a>摘要

你已经对`Person`， `Student`，和`Instructor`类实现了单体系单表继承。 有关在 Entity Framework Core中实现继承的详细信息，请参阅[继承](https://docs.microsoft.com/ef/core/modeling/inheritance)。 在下一个教程中，你将看到对各种相对较高级的 Entity Framework 场景中处理问题。

>[!div class="step-by-step"]
[上一页](concurrency.md)
[下一页](advanced.md)  
