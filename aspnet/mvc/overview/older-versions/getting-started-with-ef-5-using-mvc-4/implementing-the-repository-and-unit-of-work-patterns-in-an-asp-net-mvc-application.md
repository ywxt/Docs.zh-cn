---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (共 10 个 9) 中实现存储库和工作单元模式 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9de8b33e4c533b90b7653544a6814d1ee756cf50
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814564"
---
<a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>在 ASP.NET MVC 应用程序 (共 10 个 9) 中实现存储库和工作单元模式
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。 一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


在上一教程中使用继承来减少冗余代码中的`Student`和`Instructor`实体类。 在本教程中，您将看到的 CRUD 操作使用的存储库和工作单元模式的一些方法。 如前面的教程中所示在此将更改你的代码适用于页你已创建而不是创建新的页的方式。

## <a name="the-repository-and-unit-of-work-patterns"></a>存储库和工作单元模式

存储库和工作单元模式旨在创建数据访问层和应用程序的业务逻辑层之间的抽象层。 实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。

在本教程中将实现每个实体类型的存储库类。 有关`Student`您将创建一个存储库接口和存储库类的实体类型。 当你在控制器中实例化存储库时，您将使用接口，以便在控制器将接受任何实现存储库接口的对象的引用。 当控制器在 web 服务器下运行时，它将接收适用于实体框架的存储库。 当控制器在单元测试类下运行时，它将接收适用于您可以轻松地操作进行测试，例如内存中集合的方式存储的数据的存储库。

本教程的后面将使用多个存储库和工作类的一个单元`Course`并`Department`中的实体类型`Course`控制器。 单位工作类通过创建由所有这些共享的单个数据库上下文类协调多个存储库的工作。 如果你想要能够执行自动化的单元测试，您可以创建并与你对相同的方式使用这些类的接口`Student`存储库。 但是，为了简化本教程，将创建和使用这些类没有接口。

下图显示了概念化控制器和到不在所有使用的存储库或工作单元模式进行比较的上下文类之间的关系的一种方法。

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

在本系列教程中，不会创建单元测试。 有关使用存储库模式的 MVC 应用程序使用 TDD 的介绍，请参阅[演练： 使用 ASP.NET MVC 使用 TDD](https://msdn.microsoft.com/library/ff847525.aspx)。 有关存储库模式的详细信息，请参阅以下资源：

- [存储库模式](https://msdn.microsoft.com/library/ff649690.aspx)MSDN 上。
- [存储库和工作单元模式中使用 Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) Entity Framework 团队博客上。
- [敏捷的实体框架 4 存储库](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)系列 Julie Lerman 的博客上的文章。
- [构建一个快速的 jQuery HTML5/应用程序的帐户](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)Dan Wahlin 的博客上。

> [!NOTE]
> 有许多方法来实现存储库和工作单元模式。 使用或不工作类的一个单元，可以使用存储库类。 您可以实现所有实体类型，或另一个用于每种类型的单个存储库。 如果你实现一个用于每种类型，可以使用单独的类、 泛型基类和派生的类中，或一个抽象基类和派生的类。 可以在存储库中包括的业务逻辑，也可以限制对数据访问逻辑。 您可以生成一个抽象层到您的数据库上下文类使用[IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)而不是那里接口[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)的实体集的类型。 实现一个抽象层，在本教程中所示的方法是为您要考虑，不推荐用于所有方案和环境的一个选项。


## <a name="creating-the-student-repository-class"></a>创建 Student 存储库类

在中*DAL*文件夹中，创建名为的类文件*IStudentRepository.cs*和现有代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

此代码声明了一组典型的 CRUD 方法，包括两种读取的方法 — 一个用于返回所有`Student`实体和一个查找单个`Student`实体的 id。

在中*DAL*文件夹中，创建名为的类文件*StudentRepository.cs*文件。 现有代码替换为以下代码，实现`IStudentRepository`接口：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

在类变量中，定义数据库上下文和构造函数需要调用对象上下文的实例中传递：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

无法实例化新的上下文中存储库，但如果您使用一个控制器中的多个存储库，每个将最终会有单独的上下文。 稍后将使用多个存储库中的`Course`控制器，并且您将看到工作类的一个单元可以确保所有存储库使用相同的上下文。

存储库中实现[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)并释放数据库上下文，如前面在控制器中看到以及其 CRUD 方法调用数据库上下文中是您在前面看到的相同。

## <a name="change-the-student-controller-to-use-the-repository"></a>更改学生控制器，若要使用的存储库

在中*StudentController.cs*，当前类中的代码替换为以下代码。 突出显示所作更改。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

控制器现在声明实现的对象的类变量`IStudentRepository`接口而不是上下文类：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

默认 （无参数） 构造函数创建一个新的上下文实例，并可选的构造函数允许调用方将上下文实例中传递。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

(如果已使用*依赖关系注入*，或 DI，无需使用默认构造函数因为 DI 软件可确保始终将提供正确的存储库对象。)

在 CRUD 方法中，而不是上下文现在称为存储库：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

和`Dispose`方法立即释放而不是上下文的存储库：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

运行站点，并单击**学生**选项卡。

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

该页面看起来，并像以前那样之前更改代码以使用存储库，因此其他学生页面还运行相同工作方式相同。 但是，没有方法中的一个重要区别`Index`控制器方法的执行筛选和排序。 此方法的原始版本包含以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

已更新`Index`方法包含以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

突出显示的代码已更改。

该代码中，在原始版本中`students`被类型化为`IQueryable`对象。 查询不会发送到数据库中，直到它被转换为使用一种方法，如集合`ToList`，直到索引视图访问学生模型，这就不会出现。 `Where`上面的原始代码中的方法将成为`WHERE`发送到数据库的 SQL 查询中的子句。 这反过来意味着只有所选的实体由数据库返回。 但是，由于更改而`context.Students`到`studentRepository.GetStudents()`，则`students`变量后此语句是`IEnumerable`集合，其中包括在数据库中的所有学生。 应用的最终结果`Where`方法相同，但现在在 web 服务器上而不是由数据库的内存中完成工作。 对于返回大量数据的查询，这可能效率很低。

> [!TIP]
> 
> **IQueryable vs。IEnumerable**
> 
> 在实现存储库如下所示，即使输入中的某些内容后**搜索**框查询发送到 SQL Server 返回学生的所有行，因为它不包括您的搜索条件：
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 因为存储库无需知道有关搜索条件执行查询，此查询返回的所有学生数据。 排序、 应用搜索条件，并选择数据的子集，用于在内存中完成分页 （在这种情况下显示仅 3 行） 的过程更高版本时，`ToPagedList`上调用方法`IEnumerable`集合。
> 
> 在上一版本中的代码 （在之前实现存储库），该查询不会发送到之前的数据库后应用的搜索条件，当`ToPagedList`上调用`IQueryable`对象。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> 当调用 ToPagedList 时`IQueryable`对象，发送到 SQL Server 的查询指定的搜索字符串，而作为结果返回符合搜索条件的行，并且没有筛选需要在内存中完成。
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> （以下教程介绍如何检查查询发送到 SQL Server。）


以下部分介绍如何实现存储库方法，您可以指定应由数据库完成此工作。

你现在已创建的控制器和实体框架数据库上下文之间的抽象层。 如果您将执行自动的单元测试与此应用程序，则可以创建备用存储库类中实现的单元测试项目`IStudentRepository` *。* 而不是调用要读取和写入数据的上下文，此 mock 存储库类可能会为了测试控制器函数操作内存中集合。

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>实现泛型存储库和单元的工作类

创建每个实体类型的存储库类可能会导致大量的冗余代码，并且它可能导致部分更新。 例如，假设您需要更新在同一事务中的两个不同的实体类型。 如果每个使用单独的数据库上下文实例，其中一个操作可能会成功和其他可能会失败。 最大程度减少冗余代码的一种方法是使用泛型存储库，并确保一种方法，所有存储库可以使用相同的数据库上下文 （并因此协调所有更新） 是使用工作类的一个单元。

在本教程的本部分中，将创建`GenericRepository`类和一个`UnitOfWork`类，并使用它们在`Course`控制器同时访问`Department`和`Course`实体集。 如前面所述，为了简化本教程的此部分未创建这些类的接口。 但如果要使用它们来促进 TDD，你将通常实现这些接口使用相同的方式`Student`存储库。

### <a name="create-a-generic-repository"></a>创建泛型存储库

在中*DAL*文件夹中，创建*GenericRepository.cs*和现有代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

为数据库上下文和存储库为实例化的实体集声明类变量：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

构造函数接受数据库上下文实例并初始化实体集变量：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get`方法使用 lambda 表达式来允许调用代码指定筛选条件和一个列，通过对结果进行排序和字符串参数允许调用方提供的预先加载导航属性的逗号分隔列表：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

代码`Expression<Func<TEntity, bool>> filter`意味着调用方将提供 lambda 表达式基于`TEntity`类型和此表达式将返回一个布尔值。 例如，如果存储库为实例化`Student`实体类型，指定调用方法中的代码可能`student => student.LastName == "Smith`&quot;为`filter`参数。

代码`Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy`也意味着调用方将提供 lambda 表达式。 但在这种情况下，该表达式的输入`IQueryable`对象`TEntity`类型。 该表达式将返回是有序的新版`IQueryable`对象。 例如，如果存储库为实例化`Student`实体类型，指定调用方法中的代码可能`q => q.OrderBy(s => s.LastName)`为`orderBy`参数。

中的代码`Get`方法创建`IQueryable`对象，然后应用筛选器表达式，如果有一个：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

接下来，它分析的以逗号分隔列表之后适用的预先加载表达式：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

最后，它采用`orderBy`如果有一个表达式，并返回结果; 否则它返回从无序查询结果：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

当您调用`Get`方法，可以进行筛选和排序上`IEnumerable`而不是提供这些函数的参数的方法返回的集合。 但排序和筛选工作然后将完成 web 服务器上的内存中。 通过使用这些参数可确保工作都由数据库而不是 web 服务器完成。 一种替代方法是创建特定实体类型的派生的类并添加专用`Get`方法，如`GetStudentsInNameOrder`或`GetStudentsByName`。 但是，在复杂的应用程序，这可能导致大量此类派生的类和专用的方法，这可能是更多的工作来维护。

中的代码`GetByID`， `Insert`，和`Update`方法是类似于在非泛型存储库中看到。 (不提供中的预先加载参数`GetByID`签名，因为不能与预先加载`Find`方法。)

为提供了两个重载`Delete`方法：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

只需 ID 中的实体的要删除传递这些允许之一和一个采用实体实例。 中所示[处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中，并发处理，您需要`Delete`采用实体实例的方法包括跟踪属性的原始值。

此泛型存储库将处理典型 CRUD 要求。 当特定实体类型具有特殊要求，如更复杂的筛选或排序，可以创建具有该类型的其他方法的派生的类。

## <a name="creating-the-unit-of-work-class"></a>创建工作类的单元

单位工作类提供一种用途： 若要确保使用多个存储库时，它们共享单一数据库上下文。 这样一来，完成的工作单元时可以调用`SaveChanges`上下文的该实例上的方法并确保所有相关的更改都将协调。 类需要做的一切是`Save`方法和属性的每个存储库。 每个存储库属性将返回已作为其他存储库实例使用相同的数据库上下文实例实例化的存储库实例。

在中*DAL*文件夹中，创建名为的类文件*UnitOfWork.cs*和模板代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

该代码创建数据库上下文和每个存储库的类变量。 有关`context`实例化的变量时，新的上下文是：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

每个存储库属性检查是否已存在存储库。 如果没有，它实例化的存储库，在上下文实例中传递。 因此，所有存储库共享相同的上下文实例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save`方法调用`SaveChanges`上的数据库上下文。

与实例化类变量中的数据库上下文的任何类一样`UnitOfWork`类实现`IDisposable`和释放上下文。

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>更改为使用 UnitOfWork 类和存储库的课程控制器

当前包含的代码替换为*CourseController.cs*使用以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

此代码将添加一个类变量`UnitOfWork`类。 (如果在此处使用接口，则不会初始化变量此处; 相反，你会实施一种模式的两个构造函数，就像你对`Student`存储库。)

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

在类的其余部分，对数据库上下文的所有引用都替换为对相应的存储库的引用使用`UnitOfWork`属性来访问存储库。 `Dispose`方法会释放`UnitOfWork`实例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

运行站点，并单击**课程**选项卡。

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

该页面看起来，并像之前所做的更改，以及其他课程页也适用相同工作方式相同。

## <a name="summary"></a>总结

您现在已实现的存储库和工作单元模式。 您已经使用 lambda 表达式作为泛型存储库中的方法参数。 有关如何使用这些表达式的详细信息`IQueryable`对象，请参阅[IQueryable(T) 接口 (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) MSDN 库中。 在下一个教程中，您将了解如何处理一些高级的方案。

其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

> [!div class="step-by-step"]
> [上一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
