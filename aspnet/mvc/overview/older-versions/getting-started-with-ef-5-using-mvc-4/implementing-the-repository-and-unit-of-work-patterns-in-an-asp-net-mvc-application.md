---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (9 的 10) 中实现的存储库和单元的工作模式 |Microsoft 文档
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 1f870b61658686769304a7809bde62e66da3bd0c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875864"
---
<a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="8b48a-103">在 ASP.NET MVC 应用程序 (9 的 10) 中实现的存储库和单元的工作模式</span><span class="sxs-lookup"><span data-stu-id="8b48a-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>
====================
<span data-ttu-id="8b48a-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8b48a-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8b48a-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="8b48a-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="8b48a-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8b48a-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="8b48a-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8b48a-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="8b48a-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="8b48a-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="8b48a-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="8b48a-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="8b48a-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8b48a-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="8b48a-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="8b48a-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="8b48a-112">在以前的教程，你用于继承减少冗余代码中的`Student`和`Instructor`实体类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-112">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="8b48a-113">在本教程中，你将看到的 CRUD 操作中使用的存储库和单元的工作模式的一些方法。</span><span class="sxs-lookup"><span data-stu-id="8b48a-113">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="8b48a-114">如前面的教程，在此将更改你的代码适用于页你已创建而不是创建新的页的方式。</span><span class="sxs-lookup"><span data-stu-id="8b48a-114">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="8b48a-115">存储库和单元的工作模式</span><span class="sxs-lookup"><span data-stu-id="8b48a-115">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="8b48a-116">存储库和单元的工作模式旨在创建数据访问层和应用程序的业务逻辑层之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="8b48a-116">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="8b48a-117">实现这些模式有助于使应用程序免受数据存储中所作更改的影响，而且有助于进行自动单元测试或测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="8b48a-117">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="8b48a-118">在本教程中，你将实施每个实体类型的存储库类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-118">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="8b48a-119">有关`Student`你将创建存储库接口和存储库类的实体类型。</span><span class="sxs-lookup"><span data-stu-id="8b48a-119">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="8b48a-120">当你的控制器中实例化存储库时，你将使用该接口，以便控制器将接受对任何实现存储库接口的对象的引用。</span><span class="sxs-lookup"><span data-stu-id="8b48a-120">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="8b48a-121">当控制器运行在 web 服务器下时，它将接收适用于实体框架的存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-121">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="8b48a-122">当控制器运行下一个单元测试类时，它将接收适用于你可以轻松地操作进行测试，例如，内存中集合的方式存储数据的存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-122">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="8b48a-123">将稍后在本教程中使用多个存储库和单元的工作类`Course`和`Department`中的实体类型`Course`控制器。</span><span class="sxs-lookup"><span data-stu-id="8b48a-123">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="8b48a-124">工作类的单元通过创建单个数据库上下文类由所有这些共享协调多个存储库的工作。</span><span class="sxs-lookup"><span data-stu-id="8b48a-124">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="8b48a-125">如果你想要能够执行自动的单元测试，您可以创建并使用这些类的接口，与用于相同的方式`Student`存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-125">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="8b48a-126">但是，为了简化本教程，将创建并没有接口的情况下使用这些类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-126">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="8b48a-127">下图显示了一种方法有助于概念化控制器和上下文类相比于不在任何使用的存储库或单元的工作模式之间的关系。</span><span class="sxs-lookup"><span data-stu-id="8b48a-127">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="8b48a-129">在本系列教程中，不会创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="8b48a-129">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="8b48a-130">MVC 应用程序使用的存储库模式 TDD 的介绍，请参阅[演练： 使用 ASP.NET MVC 使用 TDD](https://msdn.microsoft.com/library/ff847525.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8b48a-130">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="8b48a-131">有关存储库模式的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="8b48a-131">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="8b48a-132">[存储库模式](https://msdn.microsoft.com/library/ff649690.aspx)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="8b48a-132">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="8b48a-133">[使用实体框架 4.0 中使用存储库和单元的工作模式](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)实体框架团队博客上。</span><span class="sxs-lookup"><span data-stu-id="8b48a-133">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="8b48a-134">[敏捷的实体框架 4 存储库](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)系列 Julie Lerman 博客上的文章。</span><span class="sxs-lookup"><span data-stu-id="8b48a-134">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="8b48a-135">[生成快速 HTML5/jQuery 应用程序的帐户](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)Dan Wahlin 博客上。</span><span class="sxs-lookup"><span data-stu-id="8b48a-135">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="8b48a-136">有多种方法来实现的存储库和单元的工作模式。</span><span class="sxs-lookup"><span data-stu-id="8b48a-136">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="8b48a-137">你可以使用存储库类，具有或不工作类的一个单元。</span><span class="sxs-lookup"><span data-stu-id="8b48a-137">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="8b48a-138">你可以实现所有实体类型，或另一个用于每种类型的单个存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-138">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="8b48a-139">如果你实现一个用于每种类型，你可以使用单独的类、 泛型基类和派生的类中，或一个抽象基类和派生的类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-139">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="8b48a-140">你可以在你的存储库中包含业务逻辑或限制对数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="8b48a-140">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="8b48a-141">你也可以生成一个抽象层入数据库上下文类通过[IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)存在接口而不是[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)实体集的类型。</span><span class="sxs-lookup"><span data-stu-id="8b48a-141">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="8b48a-142">实现在本教程中所示的抽象层的方法是你需要考虑，不建议所有方案和环境的一个选项。</span><span class="sxs-lookup"><span data-stu-id="8b48a-142">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>


## <a name="creating-the-student-repository-class"></a><span data-ttu-id="8b48a-143">创建学生存储库类</span><span class="sxs-lookup"><span data-stu-id="8b48a-143">Creating the Student Repository Class</span></span>

<span data-ttu-id="8b48a-144">在*DAL*文件夹中，创建一个名为的类文件*IStudentRepository.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-144">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="8b48a-145">此代码声明了一组典型的 CRUD 方法，包括两个读取的方法-一个返回所有`Student`实体和查找单个的一个`Student`实体的 id。</span><span class="sxs-lookup"><span data-stu-id="8b48a-145">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="8b48a-146">在*DAL*文件夹中，创建一个名为的类文件*StudentRepository.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8b48a-146">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="8b48a-147">将现有代码替换为以下代码，实现`IStudentRepository`接口：</span><span class="sxs-lookup"><span data-stu-id="8b48a-147">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="8b48a-148">在类变量中，定义的数据库上下文和构造函数需要调用对象上下文的实例中传递：</span><span class="sxs-lookup"><span data-stu-id="8b48a-148">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="8b48a-149">无法实例化新的上下文中存储库，但如果你使用一个控制器中的多个存储库，每个将最终会与单独的上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-149">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="8b48a-150">稍后你将使用中的多个存储库`Course`控制器，你将看到一套工作类可以确保所有存储库使用相同的上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-150">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="8b48a-151">存储库实现[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)并释放数据库上下文，你在前面看到控制器上，以及其 CRUD 方法前面所看到的相同方式进行调用的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-151">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="8b48a-152">更改为使用存储库的学生控制器</span><span class="sxs-lookup"><span data-stu-id="8b48a-152">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="8b48a-153">在*StudentController.cs*，当前类中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="8b48a-153">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="8b48a-154">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8b48a-154">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="8b48a-155">控制器现在声明实现的对象的类变量`IStudentRepository`而不是上下文类的接口：</span><span class="sxs-lookup"><span data-stu-id="8b48a-155">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="8b48a-156">默认 （无参数） 构造函数创建新的上下文实例，和一个可选的构造函数允许调用方传入的上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-156">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="8b48a-157">(如果你使用*依赖关系注入*，或 DI，你不需要默认构造函数因为 DI 软件将确保始终将提供正确的存储库对象。)</span><span class="sxs-lookup"><span data-stu-id="8b48a-157">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="8b48a-158">在 CRUD 方法中，而非上下文现在称为存储库：</span><span class="sxs-lookup"><span data-stu-id="8b48a-158">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="8b48a-159">与`Dispose`方法立即释放而非上下文存储库：</span><span class="sxs-lookup"><span data-stu-id="8b48a-159">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="8b48a-160">运行站点，然后单击**学生**选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b48a-160">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="8b48a-162">页查找，并像之前更改代码以使用存储库，并且其他学生页也适用相同的操作方式相同。</span><span class="sxs-lookup"><span data-stu-id="8b48a-162">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="8b48a-163">但是，没有方式的一项重大差异`Index`控制器方法执行筛选和排序。</span><span class="sxs-lookup"><span data-stu-id="8b48a-163">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="8b48a-164">此方法的原始版本包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-164">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="8b48a-165">已更新`Index`方法包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-165">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="8b48a-166">仅突出显示的代码已更改。</span><span class="sxs-lookup"><span data-stu-id="8b48a-166">Only the highlighted code has changed.</span></span>

<span data-ttu-id="8b48a-167">该代码的原始版本中`students`被类型化为`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="8b48a-167">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="8b48a-168">查询不发送到数据库中，直到它被转换为使用一种方法，如集合`ToList`，这不会出现在之前的索引视图访问学生模型。</span><span class="sxs-lookup"><span data-stu-id="8b48a-168">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="8b48a-169">`Where`在上面的原始代码的方法将成为`WHERE`发送到数据库的 SQL 查询中的子句。</span><span class="sxs-lookup"><span data-stu-id="8b48a-169">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="8b48a-170">这反过来意味着仅所选的实体由数据库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-170">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="8b48a-171">但是，由于更改`context.Students`到`studentRepository.GetStudents()`、`students`变量后此语句是`IEnumerable`包含所有学生在数据库中的集合。</span><span class="sxs-lookup"><span data-stu-id="8b48a-171">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="8b48a-172">应用的最终结果`Where`方法相同，但现在在 web 服务器上而不是数据库的内存中完成工作。</span><span class="sxs-lookup"><span data-stu-id="8b48a-172">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="8b48a-173">对于返回大量数据的查询，这可能效率低下。</span><span class="sxs-lookup"><span data-stu-id="8b48a-173">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="8b48a-174">**IQueryable vs。IEnumerable**</span><span class="sxs-lookup"><span data-stu-id="8b48a-174">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="8b48a-175">实现存储库如下所示，即使输入中的一些东西后**搜索**框发送给 SQL Server 的查询返回所有学生行，因为它不包括您的搜索条件：</span><span class="sxs-lookup"><span data-stu-id="8b48a-175">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="8b48a-176">因为存储库中执行查询，而不必知道有关搜索条件，此查询将返回所有学生数据。</span><span class="sxs-lookup"><span data-stu-id="8b48a-176">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="8b48a-177">排序、 应用搜索条件，以及选择对应的数据子集 （在这种情况下显示只需 3 行） 的分页在内存中完成的过程更高版本在`ToPagedList`方法调用`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="8b48a-177">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="8b48a-178">在以前版本的代码 （之前实现存储库中），查询不发送到数据库之前应用搜索条件之后, 时`ToPagedList`上调用`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="8b48a-178">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="8b48a-179">当上调用 ToPagedList`IQueryable`对象，查询发送到 SQL Server 指定搜索字符串中，和作为结果返回满足搜索条件的行，并且没有筛选需要在内存中完成。</span><span class="sxs-lookup"><span data-stu-id="8b48a-179">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="8b48a-180">（以下教程说明如何检查查询发送到 SQL Server）。</span><span class="sxs-lookup"><span data-stu-id="8b48a-180">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>


<span data-ttu-id="8b48a-181">以下部分演示如何实现存储库，可以指定由数据库应进行这项工作的方法。</span><span class="sxs-lookup"><span data-stu-id="8b48a-181">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="8b48a-182">你现在已创建控制器和实体框架数据库上下文之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="8b48a-182">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="8b48a-183">如果你已会执行自动的单元测试与此应用程序，你可以实现的单元测试项目中创建一个备用的存储库类`IStudentRepository` *。*</span><span class="sxs-lookup"><span data-stu-id="8b48a-183">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="8b48a-184">而不是调用的上下文以读取和写入数据，此模拟的存储库类可能会为了测试控制器函数操作内存中的集合。</span><span class="sxs-lookup"><span data-stu-id="8b48a-184">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="8b48a-185">实现泛型的存储库和单元的工作类</span><span class="sxs-lookup"><span data-stu-id="8b48a-185">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="8b48a-186">创建每个实体类型的存储库类可能会导致大量的冗余代码，并且它可能导致部分更新。</span><span class="sxs-lookup"><span data-stu-id="8b48a-186">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="8b48a-187">例如，假设你需要更新作为同一事务的一部分的两个不同的实体类型。</span><span class="sxs-lookup"><span data-stu-id="8b48a-187">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="8b48a-188">如果每个使用单独的数据库上下文实例，一个可能成功，并且其他可能会失败。</span><span class="sxs-lookup"><span data-stu-id="8b48a-188">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="8b48a-189">最大程度减少冗余代码的一种方法是使用泛型的存储库，并确保一种方法，所有存储库使用相同的数据库上下文 （并因此协调所有更新） 是使用一套工作类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-189">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="8b48a-190">在本教程的本部分中，你将创建`GenericRepository`类和一个`UnitOfWork`类，并使用它们在`Course`控制器同时访问`Department`和`Course`实体集。</span><span class="sxs-lookup"><span data-stu-id="8b48a-190">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="8b48a-191">如前面所述，为了简化本教程的此部分，你不创建这些类的接口。</span><span class="sxs-lookup"><span data-stu-id="8b48a-191">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="8b48a-192">但如果你已将使用它们来促进 TDD，你将通常实现它们与接口相同的方式`Student`存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-192">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="8b48a-193">创建泛型的存储库</span><span class="sxs-lookup"><span data-stu-id="8b48a-193">Create a Generic Repository</span></span>

<span data-ttu-id="8b48a-194">在*DAL*文件夹中，创建*GenericRepository.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-194">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="8b48a-195">数据库上下文和存储库为实例化的实体集，声明类变量：</span><span class="sxs-lookup"><span data-stu-id="8b48a-195">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="8b48a-196">构造函数接受的数据库上下文实例并初始化实体设置变量：</span><span class="sxs-lookup"><span data-stu-id="8b48a-196">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="8b48a-197">`Get`方法使用 lambda 表达式来允许调用的代码指定的筛选器条件和通过，对结果进行排序的列和字符串参数允许调用方为预先加载提供以逗号分隔的导航属性的列表：</span><span class="sxs-lookup"><span data-stu-id="8b48a-197">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="8b48a-198">代码`Expression<Func<TEntity, bool>> filter`意味着调用方将提供 lambda 表达式基于`TEntity`类型和此表达式将返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="8b48a-198">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="8b48a-199">例如，如果存储库为实例化`Student`实体类型调用方法中的代码可能会指定`student => student.LastName == "Smith`&quot;为`filter`参数。</span><span class="sxs-lookup"><span data-stu-id="8b48a-199">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="8b48a-200">代码`Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy`也意味着调用方将提供 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="8b48a-200">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="8b48a-201">但在这种情况下，该表达式的输入是`IQueryable`对象`TEntity`类型。</span><span class="sxs-lookup"><span data-stu-id="8b48a-201">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="8b48a-202">该表达式将返回的有序的版本`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="8b48a-202">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="8b48a-203">例如，如果存储库为实例化`Student`实体类型调用方法中的代码可能会指定`q => q.OrderBy(s => s.LastName)`为`orderBy`参数。</span><span class="sxs-lookup"><span data-stu-id="8b48a-203">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="8b48a-204">中的代码`Get`方法创建`IQueryable`对象，然后将应用筛选器表达式，如果有一个：</span><span class="sxs-lookup"><span data-stu-id="8b48a-204">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="8b48a-205">接下来，它分析的逗号分隔列表后应用 eager 加载表达式：</span><span class="sxs-lookup"><span data-stu-id="8b48a-205">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="8b48a-206">最后，它采用`orderBy`如果有一个表达式并返回结果; 否则它将返回结果从无序的查询：</span><span class="sxs-lookup"><span data-stu-id="8b48a-206">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="8b48a-207">当调用`Get`方法，你可以执行操作筛选和排序`IEnumerable`由而不是提供这些函数的参数的方法返回的集合。</span><span class="sxs-lookup"><span data-stu-id="8b48a-207">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="8b48a-208">但排序和筛选工作然后应该在 web 服务器上的内存中。</span><span class="sxs-lookup"><span data-stu-id="8b48a-208">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="8b48a-209">通过使用这些参数，可以确保工作由数据库而不是 web 服务器完成。</span><span class="sxs-lookup"><span data-stu-id="8b48a-209">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="8b48a-210">一种替代方法是创建针对特定实体类型的派生的类并添加专用`Get`方法，如`GetStudentsInNameOrder`或`GetStudentsByName`。</span><span class="sxs-lookup"><span data-stu-id="8b48a-210">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="8b48a-211">但是，在复杂应用程序，这可以导致大量的此类派生的类和专业化的方法，这可能是多工作以维护。</span><span class="sxs-lookup"><span data-stu-id="8b48a-211">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="8b48a-212">中的代码`GetByID`， `Insert`，和`Update`methods 是类似于你在非泛型存储库中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="8b48a-212">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="8b48a-213">(不提供中的预先加载参数`GetByID`签名，因为不能使用的预先加载`Find`方法。)</span><span class="sxs-lookup"><span data-stu-id="8b48a-213">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="8b48a-214">两个重载为提供`Delete`方法：</span><span class="sxs-lookup"><span data-stu-id="8b48a-214">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="8b48a-215">只需在 ID 中的实体要删除、 传递这些允许之一，且其中一个使用实体实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-215">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="8b48a-216">正如你在看到[处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程，并发处理你需要的`Delete`采用实体实例的方法包括跟踪属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="8b48a-216">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="8b48a-217">此泛型的存储库将处理典型 CRUD 要求。</span><span class="sxs-lookup"><span data-stu-id="8b48a-217">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="8b48a-218">当特定实体类型具有特殊要求，如更复杂的筛选或排序，你可以创建具有该类型的其他方法的派生的类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-218">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="8b48a-219">创建工作类的单元</span><span class="sxs-lookup"><span data-stu-id="8b48a-219">Creating the Unit of Work Class</span></span>

<span data-ttu-id="8b48a-220">单元工作类的一个用途： 若要确保当你使用多个存储库，它们共享单个数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-220">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="8b48a-221">这样一来，完成的工作单元时可以调用`SaveChanges`上下文的该实例上的方法并确保所有相关的更改都将协调。</span><span class="sxs-lookup"><span data-stu-id="8b48a-221">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="8b48a-222">所有这些类需求是`Save`方法和每个存储库的属性。</span><span class="sxs-lookup"><span data-stu-id="8b48a-222">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="8b48a-223">每个存储库属性返回已与其他存储库实例使用相同的数据库上下文实例实例化的存储库实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-223">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="8b48a-224">在*DAL*文件夹中，创建一个名为的类文件*UnitOfWork.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-224">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="8b48a-225">该代码创建的数据库上下文和每个存储库的类变量。</span><span class="sxs-lookup"><span data-stu-id="8b48a-225">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="8b48a-226">有关`context`实例化的变量，新的上下文是：</span><span class="sxs-lookup"><span data-stu-id="8b48a-226">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="8b48a-227">每个存储库属性检查是否已存在存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-227">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="8b48a-228">否则，它实例化的存储库，并传入上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-228">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="8b48a-229">因此，所有存储库共享同一上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-229">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="8b48a-230">`Save`方法调用`SaveChanges`上的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-230">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="8b48a-231">与实例化数据库上下文在类变量中，任何类一样`UnitOfWork`类实现`IDisposable`并释放上下文。</span><span class="sxs-lookup"><span data-stu-id="8b48a-231">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="8b48a-232">更改用于 UnitOfWork 类和存储库的课程控制器</span><span class="sxs-lookup"><span data-stu-id="8b48a-232">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="8b48a-233">你目前在设置的代码替换*CourseController.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8b48a-233">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="8b48a-234">此代码将添加的类变量`UnitOfWork`类。</span><span class="sxs-lookup"><span data-stu-id="8b48a-234">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="8b48a-235">(如果已使用接口，此处所示，不会初始化这里的变量; 相反，你会实施两个构造函数的模式，就像未`Student`存储库。)</span><span class="sxs-lookup"><span data-stu-id="8b48a-235">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="8b48a-236">类的其余部分，对数据库上下文的所有引用替换都为相应的存储库，对引用使用`UnitOfWork`属性访问存储库。</span><span class="sxs-lookup"><span data-stu-id="8b48a-236">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="8b48a-237">`Dispose`方法会释放`UnitOfWork`实例。</span><span class="sxs-lookup"><span data-stu-id="8b48a-237">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="8b48a-238">运行站点，然后单击**课程**选项卡。</span><span class="sxs-lookup"><span data-stu-id="8b48a-238">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="8b48a-240">页查找并确实执行此操作之前所做的更改，以及其他课程页也适用相同的操作方式相同。</span><span class="sxs-lookup"><span data-stu-id="8b48a-240">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="8b48a-241">总结</span><span class="sxs-lookup"><span data-stu-id="8b48a-241">Summary</span></span>

<span data-ttu-id="8b48a-242">你现在已实现的存储库和单元的工作模式。</span><span class="sxs-lookup"><span data-stu-id="8b48a-242">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="8b48a-243">你为泛型存储库中的方法参数中使用 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="8b48a-243">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="8b48a-244">有关如何使用与这些表达式的详细信息`IQueryable`对象，请参阅[IQueryable(T) 接口 (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="8b48a-244">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="8b48a-245">在下一个教程中，你将了解如何处理某些高级方案中。</span><span class="sxs-lookup"><span data-stu-id="8b48a-245">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="8b48a-246">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="8b48a-246">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8b48a-247">[上一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="8b48a-247">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
