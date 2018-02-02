---
title: "ASP.NET 核心 MVC 与 EF 核心-数据模型的 10 5"
author: tdykstra
description: "在本教程中添加更多实体和关系，并通过指定格式设置、 验证和数据库的映射规则自定义数据模型。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/complex-data-model
ms.openlocfilehash: ac30d9ae5531934ba5163a8d9114b11ac54af8d2
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="creating-a-complex-data-model---ef-core-with-aspnet-core-mvc-tutorial-5-of-10"></a>EF Core 和 ASP.NET Core MVC 教程 —— 创建复杂的数据模型

作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 想要获取有关系列教程的信息，请参阅[第一个教程](intro.md)。

在前面的教程中，你使用的数据模型是由三个简单的实体组成。 在本教程中，你会添加更多的实体和关系并将根据指定的格式、 有效性验证规则和数据库映射规则自定义数据模型。

当完成这个教程的时候，实体类将组成以下图所示的数据模型：

![实体关系图](complex-data-model/_static/diagram.png)

## <a name="customize-the-data-model-by-using-attributes"></a>使用属性来自定义数据模型

在本部分中，你将了解如何通过使用属性来指定格式，有效性验证和数据库映射规则，然后通过特性来自定义数据模型。 在接下来的几节内容，你将通过向原来的类添加属性来创建完整的 School 数据模型，并为模型中未创建的实体类型创建新类。

### <a name="the-datatype-attribute"></a> DataType 特性

当前网页将学生修读课程的时间显示为日期 + 时间，然而对于此字段人们往往只关注日期。 通过数据注解的特性，你只需要修改一处代码就可以将每个视图中的数据显示为固定的格式。 可以通过一个例子来展示如何使用这个特性，将特性添加到`Student`类的`EnrollmentDate`中。

在*Models/Student.cs*，添加`using`语句，映入`System.ComponentModel.DataAnnotations`命名空间并向`EnrollmentDate`属性添加`DataType`和`DisplayFormat`特性，如下所示：

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

`DataType` 特性指定的数据类型比数据库内部类型更具体。 在这种情况下，我们只想关注日期，而不是日期+时间。 `DataType`枚举类提供了许多数据类型，包括日期、 时间、 电话号码、 货币、 电子邮件地址等。 应用程序还可以提供 `DataType` 特性自动提供与特性对应的特定功能。 例如，为 `DataType.EmailAddress` 自动创建 `mailto:` 链接，支持 HTML5 的浏览器自动为 `DataType.Date` 提供日期选择器。 `DataType`特性会编写 HTML 5 浏览器可以理解 `data-` 的属性。 `DataType`属性不提供任何有效性验证。

`DataType.Date` 不指定显示日期的格式。 默认情况下，根据服务器的 CultureInfo 的默认格式显示数据字段。

`DisplayFormat` 特性用于显式指定日期格式：

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

`ApplyFormatInEditMode` 表示在文本框编辑时数据也要按照对应的格式显示。 （对于某些域你可能不想对编辑值格式化-例如，你可能不想在文本编辑框中出现货币符号。）

你可以只使用`DisplayFormat`属性，但推荐同时使用`DataType`特性。 `DataType`特性传达的是数据的语义而不是如何在屏幕上显示，而且`DisplayFormat`并不能提供下面的功能:

* 浏览器会根据`DataType`可以启用 HTML5 功能 （例如以显示一个日历控件、 区域设置相对应的货币符号、 电子邮件链接，某些客户端输入验证，等等。）。

* 默认情况下，浏览器将根据区域设置采用正确的格式呈现数据。

有关详细信息，请参阅[<input>标签帮助器文档](../../mvc/views/working-with-forms.md#the-input-tag-helper)。

运行应用程序，转到学生索引页，请注意，注册日期不再显示时间。 相同将为真，使用学生模型的任何视图。

![显示日期而无需时间的学生索引页](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a>StringLength 特性

你还可以使用特性指定数据有效性验证规则和错误消息。 `StringLength`特性设置数据库最大字符串长度，并为 ASP.NET MVC 提供客户端和服务器端的有效性验证。 你还可以通过此特性指定最小字符串长度，但最小值对数据库模式没有任何影响。

假设你想要保证用户输入的名称不超过 50 个字符。可以向`LastName`和`FirstMidName`属性添加`StringLength`特性来保证最大字符串长度的限制，如下所示：

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

`StringLength`特性不会阻止用户输入空格作为名字。 要限制输入的内容可以使用`RegularExpression`特性。 例如，下面的代码就是要保证输入的第一个字符是大写且其余的字符是字母：

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z''-'\s]*$")]
```

`MaxLength`特性提供的功能类似于`StringLength`属性区别在于`MaxLength`特性不提供客户端验证。

现在，数据库模型已经改变，数据库模式需要作出适当的改变。 你将使用迁移从而在更新数据库模式的同时不丢失应用程序使用过程中添加的任何数据。

保存所做的更改并生成项目。 然后在项目文件夹中打开命令窗口并输入以下命令：

```console
dotnet ef migrations add MaxLengthOnNames
```

```console
dotnet ef database update
```

`migrations add`命令会发出警告，提示可能会发生数据丢失，因为这项更改使两个列的最大长度变短。迁移创建了一个名为*\<时间戳 > _MaxLengthOnNames.cs*的文件。 此文件`Up`方法的代码会更新数据库，以匹配当前数据模型。 `database update`命令会执行`up`中的代码。

迁移文件名称的前缀时间戳使得 Entity Framework 可以按顺序执行迁移。 你可以在运行 update-database 命令中之前, 创建多个迁移，然后迁移会按照创建的顺序执行。

运行应用程序中，选择**Students**选项卡上，单击**Create New**，并输入一个超过 50 个字符的名称。 当你单击**Create**时，客户端验证显示一条错误消息。

![学生索引页显示的字符串长度错误](complex-data-model/_static/string-length-errors.png)

### <a name="the-column-attribute"></a>Column 特性

特性还可用于控制定义的类、属性跟数据库的映射关系。 假设你已经在名字（first-name）字段使用了`FirstMidName`。 但由于编写数据库查询语句的习惯你想要将数据库对应的这一列命名为`FirstName`。 为了实现这个映射规则，可以使用`Column`特性。

`Column`特性的作用时在创建数据库时，`Student`表中对应`FirstMidName`属性的列将被命名为`FirstName`。 换而言之，在代码引用`Student.FirstMidName`，会获取`Student`表`FirstName`列的数据。 如果未指定列名，系统会使用属性名来命名列 。

在*Student.cs*文件中，添加`using`语句，引入`System.ComponentModel.DataAnnotations.Schema`，并将 `Column` 特性添加给 `FirstMidName`属性，如高亮代码所示：

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

添加`Column`属性将更改`SchoolContext`中的数据模型，使得数据模型与数据库不相匹配。

保存所做的更改并生成项目。 然后在项目文件夹中打开命令窗口并输入以下命令以创建另一个迁移：

```console
dotnet ef migrations add ColumnFirstName
```

```console
dotnet ef database update
```

在**SQL Server 对象资源管理器**，通过双击打开学生表设计器**Student**表。

![在 SSOX 中后迁移的学生表](complex-data-model/_static/ssox-after-migration.png)

在应用前两个迁移之前，名字列为 `nvarchar(MAX)` 类型，而现在是 `nvarchar(50)` 类型。列名称已从 `FirstMidName` 更改为 `FirstName`。

> [!Note]
> 如果在按照下面部分创建所有实体类之前尝试编译，编译器可能会报错。

## <a name="final-changes-to-the-student-entity"></a>对学生实体的最终更改
![学生实体](complex-data-model/_static/student-entity.png)

将*Models/Student.cs*中原有的代码改为下列代码。 高亮代码表示已更改的代码。

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a>Required 特性

`Required`特性表示对应的属性为必填的字段。 不可为 null 的类型如(DateTime、 int、 double、 float 等)不需要赋予`Required`特性。 因为不可为 null 的类型被默认视为必填字段。

可以通过使用`StringLength`特性指定最小长度类从而替换`Required`特性：

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a>Displey 特性

`Display`特性指定对应文本框的标题为“First Name”，“Last Name”，“Full Name”，“Enrollment Date”，不通过`Display`特性指定的话标题就是属性名。

### <a name="the-fullname-calculated-property"></a>FullName 计算属性

`FullName`是一个计算的属性，返回值由其他两个属性合成。 因此它具有仅一个 get 访问器，而且数据库中没有对应的`FullName`列。

## <a name="create-the-instructor-entity"></a>创建 Instructor 实体

![Instructor 实体](complex-data-model/_static/instructor-entity.png)

创建*Models/Instructor.cs*文件，将模板代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

可以注意到导师实体类中几个属性和学生实体类相同。 在之后的[实现继承](inheritance.md)教程中，你将重构此代码以消除冗余。

可以将多个特性放在一行上，这样你就可以跟下面的示例一样编写`HireDate`的特性：

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a>CourseAssignments 和 OfficeAssignment 导航属性

`CourseAssignments`和`OfficeAssignment`属性是导航属性。

一个导师可以教授任意数量的课程，因此`CourseAssignments`定义为集合。

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

如果导航属性可以具有多个实体，其类型必须是可以添加、 删除和更新条目的列表。  你可以指定`ICollection<T>`或类型，如`List<T>`或`HashSet<T>`。 如果指定的是`ICollection<T>`，EF 默认情况下会创建`HashSet<T>`集合。

至于为什么使用`CourseAssignment`实体，下面有关多对多关系的部分会由解释。

Contoso 大学业务规定一个教师最多只能有一个办公室，因此`OfficeAssignment`属性只包含单个 OfficeAssignment 实体 （当不分配任何办公室的情况下可以为 null）。

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a>创建 OfficeAssignment 实体

![OfficeAssignment 实体](complex-data-model/_static/officeassignment-entity.png)

创建*Models/OfficeAssignment.cs*文件，并将原有代码替换以下代码：

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a>Key 特性

导师实体和办公室分配实体的对应关系为一对一或者一对零，办公室分配实体只在有被分配的导师时才存在，因此其主键是对应 Instructor 实体的外键。 但是， Entity Framework 无法自动将 InstructorID 识别为此实体的主键，因为其名称未遵循 ID 或 classnameID 的命名约定。 因此，需要使用`Key`特性将该属性标识为主键：

```csharp
[Key]
public int InstructorID { get; set; }
```

即使属性的名称不为 classnameID 或 id，只要为属性添加`Key`特性就可以将其指定为实体的主键。

默认情况下，EF 将 Key 视为非数据库生成的，因为对应的列通常用来标识关系。

### <a name="the-instructor-navigation-property"></a>Instructor 导航属性

Instructor 实体具有可为 null 的`OfficeAssignment`导航属性 （因为可能有教师没有分配办公室），除此之外 OfficeAssignment 实体还具有不可为 null 的`Instructor`导航属性（因为没有教师时就不会有办公室分配-`InstructorID`不可为 null）。 当 Instructor 实体具有相关的 OfficeAssignment 实体时，两者的导航属性中都有对方的引用。

您可以将`[Required]`特性赋予`Instructor`导航属性,这样就要求必须有相关的教师。但实际上并不需要这样做，因为`InstructorID`是外键 （它也是此表的主键） 是不可为 null 的。

## <a name="modify-the-course-entity"></a>修改 Course 实体

![课程实体](complex-data-model/_static/course-entity.png)

在*Models/Course.cs*，更早版本将你添加的代码替换为下面的代码。 突出显示所做的更改。

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

课程实体具有外键属性`DepartmentID`它指向相关的部门实体，它还具有`Department`导航属性。

当你具有相关实体的导航属性时，Entity Framework 不要求你将外键属性添加到你的数据模型。EF 会自动在对应的数据库中创建外键以及[影子属性](https://docs.microsoft.com/ef/core/modeling/shadow-properties。 但是，在数据模型中包含外键可以使更新数据更简单、 更高效。 例如，当你提取要编辑的课程实体，不加载部门实体的时对应的导航属性为 null 时，所以当你更新课程实体，你将需要读取部门实体。 当外键属性`DepartmentID`包含在数据模型中，在更新之前无需提取部门实体。

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 特性

`CourseID`属性添加了`DatabaseGenerated`特性而且参数为`None`，表示主键值是由用户指定而不是由数据库自动生成。

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

默认情况下， Entity Framework 将假定主键值都由数据库生成。在大多数情况下这样的设定是可行的。 但是，对于课程实体来说需要用到用户指定的课程编号，例如一个部门使用1000系列的编号，而另一个部门使用2000系列的编号等。

`DatabaseGenerated`属性还可以用于生成默认值，如在某个数据库列用于记录创建或更新行的日期。相关详细信息，请参阅[ Generated 属性](https://docs.microsoft.com/ef/core/modeling/generated-properties)。

### <a name="foreign-key-and-navigation-properties"></a>外键属性和导航属性

外键属性和课程实体中的导航属性反映了以下关系：

课程都将被分配到一个部门，因此有`DepartmentID`外键和一个`Department`导航属性。

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

课程可以被任意数量的学生修读，因此`Enrollments`导航属性是一个集合：

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

也可能有多个教师讲授一个课程，因此`CourseAssignments`导航属性也是一个集合 ([之后的教程](#many-to-many-relationships)会解释`CourseAssignment`类型):

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

## <a name="create-the-department-entity"></a>创建 Department 实体

![部门实体](complex-data-model/_static/department-entity.png)


创建*Models/Department.cs*文件，并将原有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a>Column 特性

前面使用`Column`特性更改列名称。 在部门实体的代码中，`Column`属性用于更改 SQL 数据类型，以便在数据库中使用 SQL Server 的 money 类型定义该列：

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

列类型映射通常不是必需的，因为 Entity Framework 会基于定义属性的 CLR 类型选择相应的 SQL Server 数据类型。 CLR`decimal`类型一般映射到 SQL Server 的`decimal`类型。 但上述情况下保存在列中的是货币金额使用 money 数据类型明显更适合。

### <a name="foreign-key-and-navigation-properties"></a>外键属性和导航属性

外键和导航属性反映了以下关系：

部门可能或可能没有管理员，管理员就是一个教师。 因此`InstructorID`在 Instructor 实体中作为外键，在`int`类型后添加`?`表示属性值可以为 null。 导航属性虽然名为`Administrator`但依然是一个 Instructor 实体：

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

部门可能要管理许多课程，因此有课程导航属性：

```csharp
public ICollection<Course> Courses { get; set; }
```

> [!NOTE]
> 按照约定， Entity Framework 会对不可为 null 的外键以及多对多关系进行级联删除。 这可能会导致循环的级联删除，当你尝试添加迁移时，将导致异常。 例如，如果你未定义 Department，而且InstructorID 属性可为 null，EF 会配置一个级联删除规则，在删除部门的同时会删除导师，这是你不希望发生的。 如果您的业务规则要求`InstructorID`属性不可为 null，你必须使用以下链式 API 语句来禁用此关系上的级联删除：
> ```csharp
> modelBuilder.Entity<Department>()
>    .HasOne(d => d.Administrator)
>    .WithMany()
>    .OnDelete(DeleteBehavior.Restrict)
> ```

## <a name="modify-the-enrollment-entity"></a>修改 Enrollment 实体

![注册实体](complex-data-model/_static/enrollment-entity.png)

在*Models/Enrollment.cs*文件中，将早期的代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a>外键属性和导航属性

外键属性和导航属性反映了以下关系：

修读记录是对于单个课程来说的的，因此修读实体中包含`CourseID`外键属性和`Course`导航属性：

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

修读记录值适用于单个学生，因此修读实体中包含`StudentID`外键属性和`Student`导航属性：

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a>多对多关系

学生和课程实体之间的关系为多对多关系，修读实体在*具有负载*的数据库中作为为多对多联接表。 "具有负载"意味着包含修读信息的数据表除了联接的表的外键以外的还有其他数据 （在这里为主键和年级属性）。

下图显示这些实体的关系。 (此关系图使用 Entity Framework  Power Tools for EF 6.x生成; 创建关系图不在本教程的范围之内，在此处只作说明。)

![学生课程多对多关系](complex-data-model/_static/student-course.png)

每条关系连线一端为1，另一端为星号 （*），这种连线表示的是一对多的关系。

如果修读表没有包括年级信息，它只需包含两个的外键 CourseID 和 StudentID。 在这种情况下，它在数据库中就是是没有负载的多对多联接表 （或纯联接表）。 教师和课程实体就具有这种多对多关系，下一步就会创建一个作为纯连接表的实体类。

（EF 6.x 支持多对多关系的隐式联接表，但 EF Core 不支持。 有关详细信息，请参阅[在 GitHub EF Core 库中的讨论](https://github.com/aspnet/EntityFramework/issues/1368)。) 

## <a name="the-courseassignment-entity"></a>CourseAssignment 实体

![CourseAssignment 实体](complex-data-model/_static/courseassignment-entity.png)

创建*Models/CourseAssignment.cs*，将原有代码替换为以下代码：

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="join-entity-names"></a>为联结实体命名

在数据库中需要联接表来描述教师与课程之间的多对多关系，而且需要由一个实体集来描述。 一般将联接实体命名为`EntityName1EntityName2`，按照这个规则可以将这个实体集命名为`CourseInstructor`。但是，我们建议你选择一个能够准确描述关系的名称。数据模型一开始都是简单的而之后会被扩展，通常都会由无负载联接变为有负载联接。 如果一开始就有一个描述性的实体名称时，之后就不需要更改它的名称。 理想情况下，联接实体代表业务域中的某项特定操作，而这项操作会有特定的名称（可能是单个单词）。 例如，Books实体和Consumers实体的关系可以是 Consumers 对 Books 的评分，这个关系可以通过名为 Rating 的实体联接。 因此，`CourseAssignment`是比`CourseInstructor`更好的选择。

### <a name="composite-key"></a>复合主键

如果外键不可为 null 的而且唯一标识表的每一行，则无需单独的主键。 *InstructorID*和*CourseID*属性应充当复合主键。 EF 标识复合主键的唯一方法是使用*fluent API* （不能通过使用特性来标识复合主键）。 你在下一节中将看到如何配置复合主键。 

复合主键可确保该虽然同一个课程有多个数据行，同一个导师也有多个数据行，但一个导师的同一个课程只有一个数据行。 `Enrollment`联接实体定义了自己的主键，因此可能会出现上述类型的重复项。 若要防止此类重复项，你可以向外键字段添加唯一索引，或类似于`CourseAssignment`一样为`Enrollment`配置复合主键。 有关详细信息，请参阅[索引](https://docs.microsoft.com/ef/core/modeling/indexes)。

## <a name="update-the-database-context"></a>更新数据库上下文

向*Data/SchoolContext.cs*文件添加下面的高亮代码：

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

代码添加新的实体，并向 CourseAssignment 实体配置复合主键。

## <a name="fluent-api-alternative-to-attributes"></a>使用 Fluent API 替代特性

上面代码`DbContext`类中的`OnModelCreating`方法使用了*fluent API*配置 EF 行为。 API 称为"fluent"，因为它通常在一个语句中调用一连串的几个方法，[EF  Core 文档]中关于 Fluent API 的示例(https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration):

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

在本教程中，仅在不能使用特性来映射数据库配置时使用 fluent API。事实上你可以使用 fluent API 来指定格式、 验证和映射规则，同时也可以给通过使用特性来实现这几种功能。 某些特性，如`MinimumLength`不能使用 fluent API 实现。 之前曾经说过，`MinimumLength`不会更改数据库模式，它仅用于客户端和服务器端有效性验证。

一些开发人员只使用 fluent API ，以保持实体类"整洁"。 只要你愿意，可以混合使用特性和 fluent API，有少量的自定义项仅可通过 fluent API 配置，建议在允许的情况下只选择其中的一种方法。当同时使用两者的时候，当存在两者要进行同一个配置的时候，则 Fluent API 的配置会覆盖特性的配置。

有关与 fluent API vs 特性的详细信息，请参阅[配置的方法](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)。

## <a name="entity-diagram-showing-relationships"></a>显示实体的关系图

下图显示的是由 Entity Framework  Power Tools 创建的完整的 School 模型关系图。

![实体关系图](complex-data-model/_static/diagram.png)

除了一对多关系的连线 (1 - *)，你可以看到导师和办公室分配实体之间是一对零或一对一连线(1 - 0..1)而导师和部门实体之间时一对多或者零对多连线(0..1 - *)。

## <a name="seed-the-database-with-test-data"></a>为数据库添加种子测试数据

将*Data/DbInitializer.cs*文件中的代码替换为以下代码，用于为新创建的实体提供种子测试数据。

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

正如你在第一个教程中看到的，大多数的代码都是用来创建新的实体对象，并加载所需的示例数据。 请注意代码如何处理多对多关系： 该代码通过创建`Enrollments`和`CourseAssignment`联接实体集创建关系。

## <a name="add-a-migration"></a>添加迁移

保存所做的更改并生成项目。 然后在项目文件夹中打开命令窗口并输入`migrations add`命令 （先不用执行 `database update` 命令）：

```console
dotnet ef migrations add ComplexDataModel
```

输出可能造成数据丢失的警告。

```text
An operation was scaffolded that may result in the loss of data. Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

此时如果你尝试运行`database update`命令 （尚未执行此操作），则会遇到以下错误：

> The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.

如果执行迁移时数据库存在数据，你需要将桩 （stub） 数据插入数据库以满足外键约束。`Up`方法将不可为 null 的 DepartmentID 外键添加到 Course 表。 如果在代码运行时 Coure 表中已经有数据，`AddColumn`操作会失败，因为 SQL Server 并不知道要向不可为 null 的列插入什么值。本教程会在新的数据库上运行迁移，但生产应环境的用程序需要在迁移时处理现有数据，因此下面的示例展示了如何处理现有数据。

若要在有历史数据的情况下运行迁移，你需要你需要更改代码，用于向指定新列的默认值。创建一个名为“Temp”的桩（stub）部门作为默认部门。执行`up`方法之后，现有的 Course 行就会全部关联到“Temp”部门。

* 打开*{timestamp}_ComplexDataModel.cs*文件。 

* 注释掉的向 Course 表添加 DepartmentID 列的代码行。

  [!code-csharp[Main](intro/samples/cu/Migrations/20170215234014_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

* 添加以下高亮代码到创建 Department 表的代码后：

  [!code-csharp[Main](intro/samples/cu/Migrations/20170215234014_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]

在生产环境的应用程序，你将编写代码或脚本添加部门行和与新添加的部门相关的课程行。 之后不再需要"Temp"部门或 Course.DepartmentID 列上的默认值。

保存所做的更改并生成项目。

## <a name="change-the-connection-string-and-update-the-database"></a>更改连接字符串，并更新数据库

在`DbInitializer`类中编写了新的代码将新创建实体的种子数据添加到空数据库。若要使 EF 创建全新的数据库，将*appsettings.json*中连接字符串的数据库名称改为 ContosoUniversity3 或尚未在计算机使用的其他名称。

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
  },
```

保存更改。

> [!NOTE]
> 在测试中不一定要改变数据库的名称，可以直接删除原有的数据库。 使用**SQL Server 对象资源管理器**(SSOX) 或`database drop`CLI 命令删除数据库：
> ```console
> dotnet ef database drop
> ```

在更改的数据库名称或删除数据库之后，命令窗口中运行`database update`命令以执行迁移。

```console
dotnet ef database update
```

运行应用，`DbInitializer.Initialize`方法会运行并填充新数据库。

在 SSOX 中打开早期版本的数据库并展开**Tables**节点以查看是否已经创建的所有表。 (如果之前已经打开了 SSOX ，请单击**刷新**按钮。)

![在 SSOX 中的表](complex-data-model/_static/ssox-tables.png)

运行应用，以触发初始化种子数据库的代码。

右键单击**CourseAssignment**表，然后选择**查看数据**以验证表中存在数据。

![在 SSOX 中 CourseAssignment 数据](complex-data-model/_static/ssox-ci-data.png)

## <a name="summary"></a>总结

现在相应的数据库有了更复杂的数据模型。 在之后的教程中，你将了解有关如何访问相关的数据。

>[!div class="step-by-step"]
[上一页](migrations.md)
[下一页](read-related-data.md)  
