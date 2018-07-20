---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 创建用于 ASP.NET MVC 应用程序 (4 个 10) 的更复杂的数据模型 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: beda9585a3050e35c250d0cb7ab1dc8a464efa3d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816238"
---
<a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>创建用于 ASP.NET MVC 应用程序 (4 个 10) 的更复杂的数据模型
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


在前面的教程中，您过了由三个实体组成的简单数据模型。 在本教程将添加更多实体和关系并将通过指定格式设置、 验证和数据库映射规则来自定义数据模型。 您将看到自定义数据模型的两个方法： 通过将属性添加到实体类并通过将代码添加到数据库上下文类。

完成本教程后，实体类将构成下图所示的完整数据模型：

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>使用特性自定义数据模型

本节介绍如何使用指定格式化、验证和数据库映射规则的特性来自定义数据模型。 然后在多个以下各节，你将创建一种完整`School`通过添加数据模型属性对类已在模型中剩余的实体类型的创建和创建新类。

### <a name="the-datatype-attribute"></a>DataType 特性

对于学生注册日期，目前所有网页都显示有时间和日期，尽管对此字段而言重要的只是日期。 使用数据注释特性，可更改一次代码，修复每个视图中数据的显示格式。 若要查看如何执行此操作，请向 `Student` 类的 `EnrollmentDate` 属性添加一个特性。

在*Models\Student.cs*，添加`using`语句`System.ComponentModel.DataAnnotations`命名空间，并添加`DataType`并`DisplayFormat`属性到`EnrollmentDate`属性，如下面的示例中所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性用于指定比数据库内部类型更具体的数据类型。 在此示例中，我们只想跟踪日期，而不是日期和时间。 [DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供了多种数据类型，如*日期、 时间、 电话号码、 货币、 电子邮件地址*和的详细信息。 应用程序还可通过 `DataType` 特性自动提供类型特定的功能。 例如，`mailto:`可以为创建链接[DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)，和日期选择器可提供用于[DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)中支持的浏览器[HTML5](http://html5.org/). [数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性发出 HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (读作*数据 dash*) 特性供 HTML 5 浏览器理解。 [数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性不提供任何验证。

`DataType.Date` 不指定显示日期的格式。 默认情况下，显示该数据字段根据基于服务器的默认格式[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)。

`DisplayFormat` 特性用于显式指定日期格式：


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


`ApplyFormatInEditMode`设置指定，指定的格式设置也应该应用时的值显示在文本框中以进行编辑。 (您可能不想为某些字段 — 例如，对于货币值，您可能不希望在文本框中的货币符号以进行编辑。)

可以使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性本身，但它通常是使用一个好办法[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性。 `DataType`特性传达*语义*的数据作为相对于屏幕上的呈现方式，提供了以下具有前所未有的优势`DisplayFormat`:

- 在浏览器可启用 HTML5 功能 （例如显示日历控件、 区域设置适用的货币符号、 电子邮件链接等。）。
- 默认情况下，在浏览器将呈现数据采用正确的格式基于你[区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)。
- [数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性使 MVC 能够选择正确的字段模板来呈现数据 ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)如果由自身使用字符串模板)。 有关详细信息，请参阅 Brad Wilson [ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。 （为 MVC 2 编写的但本文仍适用于 ASP.NET MVC 的当前版本。）

如果您使用`DataType`属性与日期字段，则必须指定`DisplayFormat`还以确保字段正确呈现在 Chrome 浏览器中的属性。 有关详细信息，请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。

再次运行学生索引页，请注意注册日期不再显示时间。 相同，则为 true 的任何视图，它使用`Student`模型。

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

此外可以指定数据验证规则和使用属性的消息。 假设要确保用户输入的名称不超过 50 个字符。 若要添加此限制，添加[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)向属性`LastName`和`FirstMidName`属性，如下面的示例中所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性不会阻止用户输入一个名称的空格。 可以使用[正则表达式](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性来限制应用于输入。 例如，下面的代码要求第一个字符为大写，其余字符按字母顺序排列：

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)属性提供了与类似的功能[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性但不提供客户端验证。

运行应用程序，然后单击**学生**选项卡。你收到以下错误：

*创建数据库后，支持 SchoolContext 上下文的模型已更改。请考虑使用 Code First 迁移来更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。*

数据库模型已更改需要在数据库架构中，更改的方式，实体框架检测到的。 将使用迁移来更新架构，而不会丢失任何数据，使用 UI 添加到数据库。 如果更改由创建的数据`Seed`方法，将更改回其原始状态由于[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法中使用`Seed`方法。 ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)等效于"upsert"操作从数据库术语中。)

在包管理器控制台 (PMC) 中输入以下命令：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration MaxLengthOnNames`命令创建名为的文件*&lt;时间戳&gt;\_MaxLengthOnNames.cs*。 此文件包含将更新数据库以匹配当前数据模型的代码。 Entity Framework 使用迁移文件名前面预置的时间戳进行排序的迁移。 如果删除数据库，创建多个迁移后，或使用迁移部署该项目，在其中创建顺序应用所有迁移。

运行**创建**页上，然后输入名称超过 50 个字符。 一旦超过 50 个字符时，客户端验证将立即显示一条错误消息。

![客户端端 val 错误](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>列属性

还可使用特性来控制类和属性映射到数据库的方式。 假设在名字字段使用了 `FirstMidName`，这是因为该字段也可能包含中间名。 但却希望将数据库列命名为 `FirstName`，因为要针对数据库编写即席查询的用户习惯使用该姓名。 若要进行此映射，可使用 `Column` 特性。

`Column` 特性指定，创建数据库时，映射到 `FirstMidName` 属性的 `Student` 表的列将被命名为 `FirstName`。 换言之，在代码引用 `Student.FirstMidName` 时，数据来源将是 `Student` 表的 `FirstName` 列或在其中进行更新。 如果未指定列名称，系统会提供名称与属性名称相同。

添加 using 语句[System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)和列名称属性为`FirstMidName`属性，如以下突出显示的代码中所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

添加了[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)更改备份 SchoolContext，因此它不会与数据库匹配的模型。 在 PMC 创建另一个迁移中输入以下命令：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

在中**服务器资源管理器**(**数据库资源管理器**如果你使用 for Web Express)，双击*学生*表。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

下图显示的原始列名称之前应用的前两个迁移。 除了从更改的列名称`FirstMidName`到`FirstName`，从已更改的两个名称列`MAX`长度为 50 个字符。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

您还可以进行数据库映射更改使用[Fluent API](https://msdn.microsoft.com/data/jj591617)，正如您将看到在本教程的后面。

> [!NOTE]
> 如果您尝试编译之前完成创建所有这些实体类，可能会收到编译器错误。


## <a name="create-the-instructor-entity"></a>创建 Instructor 实体

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

创建*Models\Instructor.cs*，模板代码替换为以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

请注意，`Student` 和 `Instructor` 实体中具有几个相同属性。 在中[实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)本系列后面的教程，您将重构使用继承来消除此冗余。

### <a name="the-required-and-display-attributes"></a>所需和显示属性

在属性`LastName`属性指定它是必填的字段，在文本框中的标题应 （而不是属性名称，它将是"LastName"没有空格），为"Last Name"和值不能超过 50 个字符。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[StringLength 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)设置数据库中的最大长度，并提供客户端和服务器端的 ASP.NET MVC 验证。 还可在此属性中指定最小字符串长度，但最小值对数据库架构没有影响。 [所需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)不需要值类型，如 DateTime、 int、 double、 和 float。 值类型无法将分配一个 null 值，因此它们是本质上是必需的。 无法删除[所需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)并将其替换的最小长度参数为`StringLength`属性：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

因此您也可以编写 instructor 类，如下所示，可以在同一行，将多个属性：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 计算属性

`FullName` 是计算属性，可返回通过串联两个其他属性创建的值。 因此只有`get`访问器，但没有`FullName`将在数据库中生成列。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>课程和 OfficeAssignment 导航属性

`Courses` 和 `OfficeAssignment` 是导航属性。 如前所述，它们通常定义为[虚拟](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，以便他们可以利用名为实体框架功能[延迟加载](https://msdn.microsoft.com/magazine/hh205756.aspx)。 此外，如果导航属性可以包含多个实体，其类型必须实现[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)接口。 (例如[IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)但不是限定[IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx)因为`IEnumerable<T>`不会实现[添加](https://msdn.microsoft.com/library/63ywd54z.aspx).

一名讲师可以教授任意数量的课程，因此`Courses`定义为一系列`Course`实体。 我们的业务规则规定一名讲师只能具有最多一个办公室，因此`OfficeAssignment`定义为单个`OfficeAssignment`实体 (这可能会`null`如果没有 office 分配)。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>创建 OfficeAssignment 实体

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

创建*Models\OfficeAssignment.cs*使用以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

生成项目时，该操作将保存所做的更改并确认没有进行任何复制并粘贴编译器可以捕获的错误。

### <a name="the-key-attribute"></a>键属性

对零或一一之间没有关系`Instructor`和`OfficeAssignment`实体。 分配到办公室的讲师相关才存在办公室分配，因此其主键也是其外的键`Instructor`实体。 但 Entity Framework 无法自动识别`InstructorID`作为主要因为其名称不符合此实体的键`ID`或*classname* `ID`命名约定。 因此，`Key` 特性用于将其识别为主键：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

此外可以使用`Key`属性如果实体具有其自己的主键，但你想要属性名称不同于`classnameID`或`ID`。 默认情况下 EF 将键视为非数据库生成因为该列面向的是识别关系。

### <a name="the-foreignkey-attribute"></a>ForeignKey 属性

当两个实体之间的一对一关系或一对零或一一种关系 (如`OfficeAssignment`和`Instructor`)，EF 不能计算出的关系的哪一端是主体，依赖哪一端。 一对一关系中与其他类的每个类具有引用导航属性。 [ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以应用于相关的类来建立此关系。 如果省略[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，当你尝试创建迁移时出现以下错误：

无法确定类型 ContosoUniversity.Models.OfficeAssignment 和 ContosoUniversity.Models.Instructor 之间的关联的主体端。 此关联的主体端必须使用的关系 fluent API 或数据批注进行显式配置。

本教程的后面，我们将介绍如何使用 fluent API 配置此关系。

### <a name="the-instructor-navigation-property"></a>Instructor 导航属性

`Instructor`实体具有一个可以为 null`OfficeAssignment`导航属性 （因为一名讲师可能没有办公室分配），并`OfficeAssignment`实体具有不可为 null`Instructor`导航属性 （因为办公室分配不能没有讲师-`InstructorID`不可为 null)。 当`Instructor`实体具有相关`OfficeAssignment`实体，每个实体都有对另一个在其导航属性的引用。

您可以将`[Required]`Instructor 导航属性来指定必须有相关的讲师，但无需这样做是因为 InstructorID 外键 （这也是此表的关键） 是不可以为 null 的属性。

## <a name="modify-the-course-entity"></a>修改 Course 实体

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在中*Models\Course.cs*，添加的代码之前替换以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Course 实体具有外键属性`DepartmentID`它指向相关`Department`实体，同时它具有`Department`导航属性。 如果拥有相关实体的导航属性，则 Entity Framework 不会要求为数据模型添加外键属性。 EF 会自动在数据库中创建外键在需要的位置。 但如果数据模型包含外键，则更新会变得更简单、更高效。 例如，当提取 course 实体进行编辑，请`Department`实体为 null 如果未加载它，因此当更新 course 实体，必须先提取`Department`实体。 当外键属性`DepartmentID`包含在数据模型中，您无需提取`Department`实体，然后才能更新。

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 特性

[DatabaseGenerated 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)与[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)参数`CourseID`属性指定主键值是由用户提供而不是由数据库生成。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

默认情况下，Entity Framework 假定主键值由数据库生成。 大多数情况下，这是理想情况。 但是，对于`Course`实体，您将使用用户指定的课程编号，例如 1000年系列的一个部门，另一个系为 2000年系列等。

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

外键属性和导航属性中的`Course`实体可反映以下关系：

- 向一个系分配课程后，出于上述原因，会出现 `DepartmentID` 外键和 `Department` 导航属性。 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 参与一门课程的学生数量不定，因此 `Enrollments` 导航属性是一个集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 一门课程可能由多位讲师讲授，因此 `Instructors` 导航属性是一个集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>创建 Department 实体

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

创建*Models\Department.cs*使用以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>列属性

之前用于[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)若要更改列名称映射。 中的代码`Department`实体，`Column`特性用于更改 SQL 数据类型映射，以便将使用 SQL Server 定义该列[资金](https://msdn.microsoft.com/library/ms179882.aspx)数据库中的类型：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

列映射通常不是必需的因为实体框架通常选择适当 SQL Server 数据类型为属性定义的 CLR 类型。 CLR `decimal` 类型会映射到 SQL Server `decimal` 类型。 但在这种情况下您知道列将包含货币金额，并[资金](https://msdn.microsoft.com/library/ms179882.aspx)数据类型是更适合。

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

外键和导航属性可反映以下关系：

- 一个系可能有也可能没有管理员，而管理员始终是讲师。 因此`InstructorID`属性是作为外键到包含`Instructor`实体，并将问号后添加`int`类型指派将标记为可为 null 的属性。导航属性名为`Administrator`但其中包含`Instructor`实体： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 一个系可以有多门课程，因此没有`Courses`导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > 按照约定，Entity Framework 能针对不可为 null 的外键和多对多关系启用级联删除。 这可能导致循环级联删除规则，初始值设定项代码运行时将导致异常。 例如，如果你未定义`Department.InstructorID`为可以为 null 的属性，你会收到以下异常消息的初始值设定项运行时:"引用关系会导致不允许的循环引用。" 如果您的业务规则需要`InstructorID`为不可为 null 的属性，必须使用以下 fluent API 来禁用此关系的级联删除： 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]


## <a name="modifying-the-student-entity"></a>修改 Student 实体

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

在中*Models\Student.cs*，添加的代码之前替换以下代码。 突出显示所作更改。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>Enrollment 实体

 在中*Models\Enrollment.cs*，添加的代码之前替换以下代码

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>外键和导航属性

外键属性和导航属性可反映以下关系：

- 注册记录面向一门课程，因此存在 `CourseID` 外键属性和 `Course` 导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 注册记录面向一名学生，因此存在 `StudentID` 外键属性和 `Student` 导航属性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>多对多关系

没有之间的多对多关系`Student`和`Course`实体，并`Enrollment`实体用作多对多联接表*有效负载为*数据库中。 这意味着`Enrollment`表包含除联接表的外键的其他数据 (在这种情况下，主键和`Grade`属性)。

下图显示这些关系在实体关系图中的外观。 (使用生成此关系图[Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); 创建此关系图不是本教程的一部分，只需使用此处为举例说明。)

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

每条关系线都为 1，另一端星号 (\*) 在另一个，指示一个对多关系。

如果`Enrollment`表不包含年级信息，它只需包含两个外键`CourseID`和`StudentID`。 在这种情况下，它将对应的多对多联接表*不带有效负载*(或*纯联接表*) 在数据库中，并且不会有根本为它创建的模型类。 `Instructor`和`Course`实体都有这种多对多关系，并且正如您所看到的它们之间没有实体类：

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

但是在数据库中，需要联接表，如以下数据库关系图中所示：

![Instructor-Course_many-to-many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

实体框架会自动创建`CourseInstructor`表，并且您读取和更新到通过读取和更新的间接`Instructor.Courses`和`Course.Instructors`导航属性。

## <a name="entity-diagram-showing-relationships"></a>显示关系的实体关系图

下图显示 Entity Framework Power Tools 针对已完成的学校模型创建的关系图。

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

除了多对多关系线 (\*到\*) 和一个对多关系线 (1 到\*)，您可以看到对零或一一的关系线 (1 到 0..1) 之间`Instructor`和`OfficeAssignment`实体和 0-或--一对多关系线 (0..1 到\*) 之间的 Instructor 和 Department 实体。

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>通过将代码添加到数据库上下文自定义数据模型

接下来将添加到新的实体`SchoolContext`类，并自定义映射使用的某些[fluent API](https://msdn.microsoft.com/data/jj591617)调用。 （该 API 是"fluent"因为通常在将一系列方法调用连接成单个语句后才能使用。）

在本教程将使用 fluent API，仅对数据库不能使用特性实现的映射。 但 Fluent API 还可用于指定大多数格式化、验证和映射规则，这可通过特性完成。 `MinimumLength` 等特性不能通过 Fluent API 应用。 如前所述，`MinimumLength`不会更改架构，它仅应用客户端和服务器端验证规则

某些开发者倾向于仅使用 Fluent API 以保持实体类的“纯净”。 如有需要，可混合使用特性和 Fluent API，且有些自定义只能通过 Fluent API 实现，但通常建议选择一种方法并尽可能坚持使用这一种。

若要添加的新实体的数据建模和执行数据库没有做通过使用特性的映射中的代码替换*DAL\SchoolContext.cs*使用以下代码：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

中的新语句[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法配置多对多联接表：

- 之间的多对多关系`Instructor`和`Course`实体，该代码指定联接表的表和列名称。 代码首先可以配置多对多关系，而无需此代码，但如果不调用它，则会默认名称如`InstructorInstructorID`为`InstructorID`列。

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

以下代码举例说明如何您可以使用 fluent API 而不是属性来指定之间的关系`Instructor`和`OfficeAssignment`实体：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

有关"fluent API"语句会在后台执行的操作的信息，请参阅[Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx)博客文章。

## <a name="seed-the-database-with-test-data"></a>使用测试数据设定数据库种子

中的代码替换*migrations\ configuration.cs*文件与以下代码，以便为已创建的新实体提供种子数据。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

如您所看到的第一个教程中，此代码的大部分只需更新或创建新实体对象并将示例数据加载到所需的测试的属性。 但请注意如何`Course`具有多对多关系的实体与`Instructor`实体，进行处理：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

当您创建`Course`对象，初始化`Instructors`导航属性为空集合使用的代码`Instructors = new List<Instructor>()`。 这样就可以添加`Instructor`与此相关的实体`Course`通过使用`Instructors.Add`方法。 如果未创建一个空列表，您将无法添加这些关系，因为`Instructors`属性将为 null，并且不会有`Add`方法。 您也可以添加到构造函数的列表初始化。

## <a name="add-a-migration-and-update-the-database"></a>添加迁移并更新数据库

在 PMC 中，输入`add-migration`命令：

`PM> add-Migration Chap4`

如果尝试在此时更新数据库，您将收到以下错误：

*ALTER TABLE 语句与 FOREIGN KEY 约束冲突"FK\_dbo。课程\_dbo。部门\_DepartmentID"。冲突发生于数据库"ContosoUniversity"表"dbo。部门"，列 DepartmentID。*

编辑&lt;*时间戳&gt;\_Chap4.cs*文件，并更改以下代码 (将添加一条 SQL 语句和修改`AddColumn`语句):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(请确保注释掉或删除现有`AddColumn`行时添加新的活动，或当你输入时，将收到错误`update-database`命令。)

有时在执行迁移的现有数据时，您需要将存根数据插入数据库，满足外键约束和这就是你要执行的操作现在。 生成的代码将添加不可为 null`DepartmentID`外键的`Course`表。 如果已经有了中的行`Course`表的代码运行时，`AddColumn`操作会失败，因为 SQL Server 不知道要放入不能为 null 的列的值。 因此，你已更改代码以便为新列默认值，并创建了名为"Temp"作为默认系的存根 （stub） 部门。 因此，如果存在现有`Course`行时此代码运行时，它们将所有与"Temp"系建立联系。

当`Seed`方法运行时，它将插入中的行`Department`表和它将与现有`Course`到这些新行`Department`行。 如果尚未在 UI 中添加任何课程，然后不再需要"Temp"系或默认值上`Course.DepartmentID`列。 若要允许，有人可能已添加课程使用应用程序的可能性，您还想要更新`Seed`方法代码，以确保所有`Course`行 (而不仅仅是由早期运行的插入`Seed`方法) 具有有效`DepartmentID`值之前删除默认列中的值并删除"Temp"系。

完成编辑后&lt;*时间戳&gt;\_Chap4.cs*文件中，输入`update-database`PMC 执行迁移命令。

> [!NOTE]
> 就可以将迁移数据，也使架构更改时遇到其他错误。 如果遇到无法解决的迁移错误，您可以更改中的连接字符串*Web.config*文件或删除的数据库。 最简单方法是在数据库重命名*Web.config*文件。 例如，将数据库名称更改为 CU\_测试在下面的示例所示：
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
>  使用新数据库没有数据迁移，和`update-database`命令是更有望完成且未出错。 有关如何删除数据库的说明，请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。


打开中的数据库**服务器资源管理器**像前面，并展开**表**节点以查看是否已创建的所有表。 (如果仍有**服务器资源管理器**从较早的时间打开，请单击**刷新**按钮。)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

未创建的模型类`CourseInstructor`表。 如前面所述，这是一个联接表之间的多对多关系`Instructor`和`Course`实体。

右键单击`CourseInstructor`表，然后选择**显示表数据**以确认它在其中为具有数据`Instructor`添加到实体`Course.Instructors`导航属性。

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>总结

现在你就得到了更复杂的数据模型和相应的数据库。 以下教程中将了解有关访问相关的数据的不同方式的详细信息。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
