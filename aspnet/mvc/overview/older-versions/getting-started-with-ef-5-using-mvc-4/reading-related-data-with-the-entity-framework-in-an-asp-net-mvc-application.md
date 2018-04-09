---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 读取与实体框架中的 ASP.NET MVC 应用程序 (5 的 10) 的相关的数据 |Microsoft 文档
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 831f5e0a8b57907ea012c10c1d1f8ff166f5e88b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="34e0b-103">读取与相关的数据与实体框架中的 ASP.NET MVC 应用程序 (5 的 10)</span><span class="sxs-lookup"><span data-stu-id="34e0b-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>
====================
<span data-ttu-id="34e0b-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="34e0b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="34e0b-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="34e0b-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="34e0b-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="34e0b-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="34e0b-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="34e0b-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="34e0b-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="34e0b-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="34e0b-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="34e0b-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="34e0b-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="34e0b-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="34e0b-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="34e0b-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="34e0b-112">在前面的教程中，你将完成 School 数据模型。</span><span class="sxs-lookup"><span data-stu-id="34e0b-112">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="34e0b-113">在本教程中，你将读取并显示相关的数据-即，实体框架将加载到导航属性的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-113">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="34e0b-114">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="34e0b-114">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="34e0b-116">延迟、 Eager，和显式加载相关的数据</span><span class="sxs-lookup"><span data-stu-id="34e0b-116">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="34e0b-117">有多种实体框架可以加载到实体的导航属性的相关的数据：</span><span class="sxs-lookup"><span data-stu-id="34e0b-117">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="34e0b-118">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="34e0b-118">*Lazy loading*.</span></span> <span data-ttu-id="34e0b-119">第一次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-119">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="34e0b-120">但是，第一次尝试访问导航属性时，将自动检索该导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-120">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="34e0b-121">这会导致发送到数据库的多个查询 — 一个用于在实体自身，一个必须检索每个相关实体的数据的时间。</span><span class="sxs-lookup"><span data-stu-id="34e0b-121">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="34e0b-123">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="34e0b-123">*Eager loading*.</span></span> <span data-ttu-id="34e0b-124">读取实体时，会检索与之相关的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-124">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="34e0b-125">这通常会导致执行一个检索所有必需数据的联接查询。</span><span class="sxs-lookup"><span data-stu-id="34e0b-125">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="34e0b-126">使用指定预先加载`Include`方法。</span><span class="sxs-lookup"><span data-stu-id="34e0b-126">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="34e0b-128">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="34e0b-128">*Explicit loading*.</span></span> <span data-ttu-id="34e0b-129">这是类似于延迟加载的只不过显式检索代码; 中的相关的数据它不会发生自动访问导航属性时。</span><span class="sxs-lookup"><span data-stu-id="34e0b-129">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="34e0b-130">你相关手动加载数据通过有关实体，以及调用中获取的对象状态管理器项`Collection.Load`集合的方法或`Reference.Load`保存单个实体的属性的方法。</span><span class="sxs-lookup"><span data-stu-id="34e0b-130">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="34e0b-131">(在下面的示例中，如果你想要加载管理员导航属性，则将替换`Collection(x => x.Courses)`与`Reference(x => x.Administrator)`。)</span><span class="sxs-lookup"><span data-stu-id="34e0b-131">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="34e0b-133">因为它们不立即检索的属性值，延迟加载和显式加载也同时称为*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="34e0b-133">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="34e0b-134">一般情况下，如果你知道需要相关的数据检索，预先加载提供最佳性能，每个实体因为单个查询发送到数据库通常比用于检索每个实体的单独查询效率更高。</span><span class="sxs-lookup"><span data-stu-id="34e0b-134">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="34e0b-135">例如，在上面的示例中，假设每个部门都有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="34e0b-135">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="34e0b-136">预先加载示例将导致仅单 （联接） 查询和单个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="34e0b-136">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="34e0b-137">延迟加载和显式加载示例将都导致十一种查询和十一个往返行程到数据库。</span><span class="sxs-lookup"><span data-stu-id="34e0b-137">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="34e0b-138">当延迟较高时，额外的数据库通信会对性能造成不利影响。</span><span class="sxs-lookup"><span data-stu-id="34e0b-138">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="34e0b-139">另一方面，在某些情况下延迟加载会更加高效。</span><span class="sxs-lookup"><span data-stu-id="34e0b-139">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="34e0b-140">预先加载可能会导致非常复杂的联接为其生成 SQL Server 无法有效地处理它。</span><span class="sxs-lookup"><span data-stu-id="34e0b-140">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="34e0b-141">或如果你需要访问仅针对实体集的子集的实体的导航属性要处理，延迟加载可能更好地执行，因为预先加载将检索比你需要更多的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-141">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="34e0b-142">如果性能非常重要，最好测试这两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="34e0b-142">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="34e0b-143">通常，你将使用显式加载，仅当你已启用延迟加载关闭时。</span><span class="sxs-lookup"><span data-stu-id="34e0b-143">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="34e0b-144">你应打开延迟加载关闭时的一个方案是在序列化过程。</span><span class="sxs-lookup"><span data-stu-id="34e0b-144">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="34e0b-145">延迟加载和序列化，不要混合并且如果你不小心处理可以得到查询更多的数据不按预期时延迟加载已启用。</span><span class="sxs-lookup"><span data-stu-id="34e0b-145">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="34e0b-146">序列化通常可通过访问类型的实例上每个属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-146">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="34e0b-147">属性访问触发延迟加载，并为这些延迟加载的实体的序列化。</span><span class="sxs-lookup"><span data-stu-id="34e0b-147">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="34e0b-148">然后，序列化过程访问的延迟加载的实体，可能会导致更多延迟加载和序列化的每个属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-148">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="34e0b-149">若要防止此逐种链式反应，打开延迟加载关闭之前序列化实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-149">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="34e0b-150">数据库上下文类默认情况下执行延迟加载。</span><span class="sxs-lookup"><span data-stu-id="34e0b-150">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="34e0b-151">有两种方法，若要禁用延迟加载：</span><span class="sxs-lookup"><span data-stu-id="34e0b-151">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="34e0b-152">对于特定的导航属性，省略`virtual`关键字声明的属性时。</span><span class="sxs-lookup"><span data-stu-id="34e0b-152">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="34e0b-153">对于所有导航属性，设置`LazyLoadingEnabled`到`false`。</span><span class="sxs-lookup"><span data-stu-id="34e0b-153">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="34e0b-154">例如，你可以将下面的代码置于上下文类的构造函数：</span><span class="sxs-lookup"><span data-stu-id="34e0b-154">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="34e0b-155">延迟加载可以屏蔽导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="34e0b-155">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="34e0b-156">例如，未指定 eager 或显式加载但处理大量的实体并在每次迭代中使用多个导航属性的代码可能非常低效，（由于到数据库的许多往返过程）。</span><span class="sxs-lookup"><span data-stu-id="34e0b-156">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="34e0b-157">执行在开发使用在本地 SQL server 中良好运行的应用程序可能具有性能问题时由于的延迟时间增加和延迟加载移到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="34e0b-157">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="34e0b-158">分析的实际的测试加载的数据库的查询将帮助你确定延迟加载是否适用。</span><span class="sxs-lookup"><span data-stu-id="34e0b-158">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="34e0b-159">有关详细信息请参阅[Demystifying 实体框架策略： 加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用实体框架与 SQL Azure 到减少网络延迟](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34e0b-159">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="34e0b-160">创建该显示部门名称的课程索引页</span><span class="sxs-lookup"><span data-stu-id="34e0b-160">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="34e0b-161">`Course`实体包括一个导航属性，包含`Department`过程分配给的部门实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-161">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="34e0b-162">若要显示分配的部门的名称列表中的课程，你需要获取`Name`属性从`Department`实体`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-162">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="34e0b-163">创建名为的控制器`CourseController`为`Course`实体类型，使用相同的选项，你此前对`Student`控制器，如下面的插图中所示 （上下文类 DAL 的命名空间与图中，不同的是除外不是模型命名空间）：</span><span class="sxs-lookup"><span data-stu-id="34e0b-163">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="34e0b-165">打开*Controllers\CourseController.cs*并查看`Index`方法：</span><span class="sxs-lookup"><span data-stu-id="34e0b-165">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="34e0b-166">自动支架使用`Include`方法将`Department`导航属性指定为预先加载。</span><span class="sxs-lookup"><span data-stu-id="34e0b-166">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="34e0b-167">打开*Views\Course\Index.cshtml*和替换为以下代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="34e0b-167">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="34e0b-168">突出显示了所做的更改：</span><span class="sxs-lookup"><span data-stu-id="34e0b-168">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="34e0b-169">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="34e0b-169">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="34e0b-170">更改标题从**索引**到**课程**。</span><span class="sxs-lookup"><span data-stu-id="34e0b-170">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="34e0b-171">向左移动行链接。</span><span class="sxs-lookup"><span data-stu-id="34e0b-171">Moved the row links to the left.</span></span>
- <span data-ttu-id="34e0b-172">添加的列标题下**数**显示`CourseID`属性值。</span><span class="sxs-lookup"><span data-stu-id="34e0b-172">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="34e0b-173">（默认情况下，主键不基架因为它们通常是向最终用户无意义。</span><span class="sxs-lookup"><span data-stu-id="34e0b-173">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="34e0b-174">但是，在这种情况下的主键有意义，以及你想要对其进行说明。）</span><span class="sxs-lookup"><span data-stu-id="34e0b-174">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="34e0b-175">更改从最后一个列标题**DepartmentID** (外键与名称`Department`实体) 到**部门**。</span><span class="sxs-lookup"><span data-stu-id="34e0b-175">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="34e0b-176">请注意，最后一列，则基架的代码显示`Name`属性`Department`实体加载到`Department`导航属性：</span><span class="sxs-lookup"><span data-stu-id="34e0b-176">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="34e0b-177">运行页面 (选择**课程**Contoso 大学主页上的选项卡) 若要查看使用部门名称列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-177">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="34e0b-179">创建显示 Courses，并将注册一个教师索引页面</span><span class="sxs-lookup"><span data-stu-id="34e0b-179">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="34e0b-180">在本节中你将创建一个控制器，以及查看`Instructor`为了显示教师索引页的实体：</span><span class="sxs-lookup"><span data-stu-id="34e0b-180">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="34e0b-182">此页通过以下方式读取和显示相关的数据：</span><span class="sxs-lookup"><span data-stu-id="34e0b-182">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="34e0b-183">教师的列表显示来自的相关的数据`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-183">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="34e0b-184">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="34e0b-184">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="34e0b-185">你将使用的预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-185">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="34e0b-186">如前所述，在需要主表的所有已检索行的相关数据时，预先加载通常更高效。</span><span class="sxs-lookup"><span data-stu-id="34e0b-186">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="34e0b-187">在此示例中，需要显示所有已显示教师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="34e0b-187">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="34e0b-188">当用户选择一个教师，相关`Course`显示实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-188">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="34e0b-189">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="34e0b-189">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="34e0b-190">你将使用的预先加载`Course`实体和其相关`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-190">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="34e0b-191">在这种情况下，因为你只为所选教师需要课程，延迟加载可能会更有效。</span><span class="sxs-lookup"><span data-stu-id="34e0b-191">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="34e0b-192">但是，此示例演示了如何使用预先加载方式来加载本身是导航属性中的实体内的导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-192">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="34e0b-193">当用户选择某一课程时，与相关的数据从`Enrollments`显示实体集。</span><span class="sxs-lookup"><span data-stu-id="34e0b-193">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="34e0b-194">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="34e0b-194">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="34e0b-195">你将添加显式加载`Enrollment`实体和其相关`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-195">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="34e0b-196">（显式加载则无需因为启用了延迟加载，但下面的示例演示如何显式加载。）</span><span class="sxs-lookup"><span data-stu-id="34e0b-196">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="34e0b-197">为教师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="34e0b-197">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="34e0b-198">教师索引页显示三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-198">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="34e0b-199">因此，你将创建包含三个属性的视图模型，每个属性保存一个表中的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-199">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="34e0b-200">在*Viewmodel*文件夹中，创建*InstructorIndexData.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="34e0b-200">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="34e0b-201">为选定的行添加样式</span><span class="sxs-lookup"><span data-stu-id="34e0b-201">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="34e0b-202">若要将选定的行的标记，你需要不同的背景色。</span><span class="sxs-lookup"><span data-stu-id="34e0b-202">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="34e0b-203">若要为此 UI 提供样式，请将以下突出显示的代码添加到部分`/* info and errors */`中*Content\Site.css*，如下所示：</span><span class="sxs-lookup"><span data-stu-id="34e0b-203">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="34e0b-204">正在创建教师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="34e0b-204">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="34e0b-205">创建`InstructorController`控制器下图中所示：</span><span class="sxs-lookup"><span data-stu-id="34e0b-205">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="34e0b-207">打开*Controllers\InstructorController.cs*并添加`using`语句`ViewModels`命名空间：</span><span class="sxs-lookup"><span data-stu-id="34e0b-207">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="34e0b-208">中的基架的代码`Index`方法指定仅对预先加载`OfficeAssignment`导航属性：</span><span class="sxs-lookup"><span data-stu-id="34e0b-208">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="34e0b-209">替换`Index`方法替换为以下代码以加载其他相关数据，并将其置于视图模型：</span><span class="sxs-lookup"><span data-stu-id="34e0b-209">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="34e0b-210">该方法将接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)，提供所选的教师和所选的过程的 ID 值并将所有所需的数据传递到该视图。</span><span class="sxs-lookup"><span data-stu-id="34e0b-210">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="34e0b-211">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="34e0b-211">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP]
> 
> <span data-ttu-id="34e0b-212">**路线数据**</span><span class="sxs-lookup"><span data-stu-id="34e0b-212">**Route data**</span></span>
> 
> <span data-ttu-id="34e0b-213">路由数据是在路由表中指定的 URL 段中找到模型联编程序的数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-213">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="34e0b-214">例如，默认路由指定`controller`， `action`，和`id`段：</span><span class="sxs-lookup"><span data-stu-id="34e0b-214">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> <span data-ttu-id="34e0b-215">routes.MapRoute(</span><span class="sxs-lookup"><span data-stu-id="34e0b-215">routes.MapRoute(</span></span>  
>  <span data-ttu-id="34e0b-216">名称:"默认情况下，"</span><span class="sxs-lookup"><span data-stu-id="34e0b-216">name: "Default",</span></span>  
>  <span data-ttu-id="34e0b-217">url:"{controller} / {action} / {id}"，</span><span class="sxs-lookup"><span data-stu-id="34e0b-217">url: "{controller}/{action}/{id}",</span></span>  
>  <span data-ttu-id="34e0b-218">默认值： new {控制器 ="主页"，操作 ="Index"，id = UrlParameter.Optional}</span><span class="sxs-lookup"><span data-stu-id="34e0b-218">defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }</span></span>  
> <span data-ttu-id="34e0b-219">);</span><span class="sxs-lookup"><span data-stu-id="34e0b-219">);</span></span>
> 
> <span data-ttu-id="34e0b-220">在下面的 URL，将默认路由映射`Instructor`作为`controller`，`Index`作为`action`并将它作为 1 `id`; 这些是路由数据值。</span><span class="sxs-lookup"><span data-stu-id="34e0b-220">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="34e0b-221">"？ courseID = 2021年"是一个查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="34e0b-221">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="34e0b-222">模型联编程序还将起作用，如果你通过`id`作为查询字符串值：</span><span class="sxs-lookup"><span data-stu-id="34e0b-222">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="34e0b-223">通过创建 Url `ActionLink` Razor 视图中的语句。</span><span class="sxs-lookup"><span data-stu-id="34e0b-223">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="34e0b-224">在下面的代码中，`id`参数和默认路由匹配，因此`id`将添加到路由数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-224">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="34e0b-225">在下面的代码中，`courseID`不匹配默认路由中的参数，因此，它将添加作为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="34e0b-225">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]


<span data-ttu-id="34e0b-226">代码首先创建视图模型的实例并向其中放置教师列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-226">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="34e0b-227">该代码指定为预先加载`Instructor.OfficeAssignment`和`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-227">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="34e0b-228">第二个`Include`方法加载的课程，并为每个课程加载完成了预先加载`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-228">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="34e0b-229">如前所述，预先加载不是必需的但做是为了提高性能。</span><span class="sxs-lookup"><span data-stu-id="34e0b-229">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="34e0b-230">因为视图始终需要`OfficeAssignment`实体，它会在同一查询中提取的更加高效。</span><span class="sxs-lookup"><span data-stu-id="34e0b-230">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="34e0b-231">`Course` 中网页上，选择一个教师，以便预先加载优于延迟加载，仅当与比而无需选择某一课程更通常显示的页面时，实体所需。</span><span class="sxs-lookup"><span data-stu-id="34e0b-231">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="34e0b-232">如果选择 instructor ID，则会将所选的教师检索从教师视图模型中的列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-232">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="34e0b-233">视图模型`Courses`属性然后加载`Course`从该 instructor 实体`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-233">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="34e0b-234">`Where`方法将返回一个集合，但条件在此情况下传递到方法导致只有一个`Instructor`所返回的实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-234">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="34e0b-235">`Single`方法将集合转换为单个`Instructor`实体，使你可以访问该实体的`Courses`属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-235">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="34e0b-236">你使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)时你知道该集合的集合上的方法将有只有一项。</span><span class="sxs-lookup"><span data-stu-id="34e0b-236">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="34e0b-237">`Single`方法引发异常时传递给它的集合是否为空或没有多个项。</span><span class="sxs-lookup"><span data-stu-id="34e0b-237">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="34e0b-238">替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它返回默认值 (`null`在这种情况下) 如果该集合为空。</span><span class="sxs-lookup"><span data-stu-id="34e0b-238">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="34e0b-239">但是，在这种情况下，仍会生成异常 (从尝试查找`Courses`属性`null`引用)，和异常消息将不太清楚地指示问题的原因。</span><span class="sxs-lookup"><span data-stu-id="34e0b-239">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="34e0b-240">当调用`Single`方法，你还可以通过`Where`条件而不是调用`Where`方法单独：</span><span class="sxs-lookup"><span data-stu-id="34e0b-240">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="34e0b-241">而不是：</span><span class="sxs-lookup"><span data-stu-id="34e0b-241">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="34e0b-242">接下来，如果选择一门课程，则会从视图模型中的课程列表检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="34e0b-242">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="34e0b-243">然后视图模型的`Enrollments`属性加载与`Enrollment`从该过程的实体`Enrollments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-243">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="34e0b-244">修改教师索引视图</span><span class="sxs-lookup"><span data-stu-id="34e0b-244">Modifying the Instructor Index View</span></span>

<span data-ttu-id="34e0b-245">在*Views\Instructor\Index.cshtml*，替换为以下代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="34e0b-245">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="34e0b-246">突出显示了所做的更改：</span><span class="sxs-lookup"><span data-stu-id="34e0b-246">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="34e0b-247">你对现有代码做出以下更改：</span><span class="sxs-lookup"><span data-stu-id="34e0b-247">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="34e0b-248">将模型类改为`InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="34e0b-248">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="34e0b-249">将页标题从“索引”改为“教师”。</span><span class="sxs-lookup"><span data-stu-id="34e0b-249">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="34e0b-250">向左移动行列链接。</span><span class="sxs-lookup"><span data-stu-id="34e0b-250">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="34e0b-251">删除**FullName**列。</span><span class="sxs-lookup"><span data-stu-id="34e0b-251">Removed the **FullName** column.</span></span>
- <span data-ttu-id="34e0b-252">添加**Office**显示的列`item.OfficeAssignment.Location`才`item.OfficeAssignment`不为 null。</span><span class="sxs-lookup"><span data-stu-id="34e0b-252">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="34e0b-253">(由于这是一个对零或一一个关系，因此可能不具备相关`OfficeAssignment`实体。)</span><span class="sxs-lookup"><span data-stu-id="34e0b-253">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="34e0b-254">添加将动态添加的代码`class="selectedrow"`到`tr`的所选教师的元素。</span><span class="sxs-lookup"><span data-stu-id="34e0b-254">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="34e0b-255">此设置使用 CSS 类之前创建所选行的背景色。</span><span class="sxs-lookup"><span data-stu-id="34e0b-255">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="34e0b-256">(`valign`属性将在以下教程中有用，当你将多行的列添加到表。)</span><span class="sxs-lookup"><span data-stu-id="34e0b-256">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="34e0b-257">添加一个新`ActionLink`标记为**选择**立即之前每个行中的其他链接，这将导致所选的教师 ID 发送到`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="34e0b-257">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="34e0b-258">运行应用程序并选择**教师**选项卡。该页面将显示`Location`的相关属性`OfficeAssignment`实体和一个空表单元时没有相关的否`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="34e0b-258">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="34e0b-260">在*Views\Instructor\Index.cshtml*结束后的文件，`table`元素 （在文件末尾），添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="34e0b-260">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="34e0b-261">此时将显示一个教师选中与一个教师相关的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-261">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="34e0b-262">此代码读取视图模型的`Courses`属性，以便显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-262">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="34e0b-263">它还提供了`Select`超链接，以便将发送到所选课程 ID`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="34e0b-263">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="34e0b-264">*.Css*由浏览器缓存文件。</span><span class="sxs-lookup"><span data-stu-id="34e0b-264">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="34e0b-265">如果你运行应用程序时，你看不到所做的更改，请执行硬刷新 (请按住 CTRL 键同时单击**刷新**按钮，或按 CTRL + F5)。</span><span class="sxs-lookup"><span data-stu-id="34e0b-265">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>


<span data-ttu-id="34e0b-266">运行页面，然后选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="34e0b-266">Run the page and select an instructor.</span></span> <span data-ttu-id="34e0b-267">此时会看到一个网格，其中显示分配给所选教师的课程。每个课程都会看到相应系的名称。</span><span class="sxs-lookup"><span data-stu-id="34e0b-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="34e0b-269">在刚添加的代码块之后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="34e0b-269">After the code block you just added, add the following code.</span></span> <span data-ttu-id="34e0b-270">这样就会显示一个注册了所选课程的学生的列表。</span><span class="sxs-lookup"><span data-stu-id="34e0b-270">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="34e0b-271">此代码读取`Enrollments`为了显示学生的列表视图模型的属性在本课程中注册。</span><span class="sxs-lookup"><span data-stu-id="34e0b-271">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="34e0b-272">运行页面，然后选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="34e0b-272">Run the page and select an instructor.</span></span> <span data-ttu-id="34e0b-273">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="34e0b-273">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="34e0b-275">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="34e0b-275">Adding Explicit Loading</span></span>

<span data-ttu-id="34e0b-276">打开*InstructorController.cs*并查看如何`Index`方法获取有关所选过程的注册的列表：</span><span class="sxs-lookup"><span data-stu-id="34e0b-276">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="34e0b-277">时检索教师的列表，您已指定为预先加载`Courses`导航属性和`Department`当然，每个属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-277">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="34e0b-278">则你将放`Courses`集合在视图模型中，并且现在正在访问`Enrollments`从该集合中的一个实体导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-278">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="34e0b-279">因为你未指定为预先加载`Course.Enrollments`导航属性，该属性中的数据显示在由于延迟加载的页中。</span><span class="sxs-lookup"><span data-stu-id="34e0b-279">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="34e0b-280">如果不更改任何其他方式中的代码的情况下禁用延迟加载`Enrollments`属性将为 null 而不考虑过程实际上有多少注册。</span><span class="sxs-lookup"><span data-stu-id="34e0b-280">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="34e0b-281">在此情况下，加载`Enrollments`属性，你将需要指定预先加载或显式加载。</span><span class="sxs-lookup"><span data-stu-id="34e0b-281">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="34e0b-282">你已经了解如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="34e0b-282">You've already seen how to do eager loading.</span></span> <span data-ttu-id="34e0b-283">若要查看的显式加载示例，替换`Index`方法替换为以下代码，此操作将显式加载`Enrollments`属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-283">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="34e0b-284">更改的代码将突出显示。</span><span class="sxs-lookup"><span data-stu-id="34e0b-284">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="34e0b-285">获取所选后`Course`实体，新的代码显式加载该课程`Enrollments`导航属性：</span><span class="sxs-lookup"><span data-stu-id="34e0b-285">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="34e0b-286">然后它显式加载每个`Enrollment`实体的相关`Student`实体：</span><span class="sxs-lookup"><span data-stu-id="34e0b-286">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="34e0b-287">请注意，你使用`Collection`方法以加载集合属性，但对于一个属性，保存一个实体，你使用`Reference`方法。</span><span class="sxs-lookup"><span data-stu-id="34e0b-287">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="34e0b-288">你可以立即运行教师索引页和虽然已经更改了如何检索的数据，你会看到在页上，显示的显示没有区别。</span><span class="sxs-lookup"><span data-stu-id="34e0b-288">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="34e0b-289">总结</span><span class="sxs-lookup"><span data-stu-id="34e0b-289">Summary</span></span>

<span data-ttu-id="34e0b-290">你现在使用所有三种方法 （延迟、 eager，和显式） 相关的数据加载到导航属性。</span><span class="sxs-lookup"><span data-stu-id="34e0b-290">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="34e0b-291">下一教程介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="34e0b-291">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="34e0b-292">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="34e0b-292">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34e0b-293">[上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="34e0b-293">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
