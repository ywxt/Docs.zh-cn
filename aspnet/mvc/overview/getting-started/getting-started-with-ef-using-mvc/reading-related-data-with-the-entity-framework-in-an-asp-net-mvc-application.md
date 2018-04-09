---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 读取与实体框架中的 ASP.NET MVC 应用程序的相关的数据 |Microsoft 文档
author: tdykstra
description: /ajax/tutorials/using-ajax-control-toolkit-controls-and-control-extenders-vb
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 06784d8b610856e71eae78b0db2d0253faedb955
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="57534-103">读取与相关的数据与实体框架中的 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="57534-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="57534-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="57534-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="57534-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="57534-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="57534-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="57534-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="57534-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="57534-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="57534-108">在前面的教程中，你将完成 School 数据模型。</span><span class="sxs-lookup"><span data-stu-id="57534-108">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="57534-109">在本教程中，你将读取并显示相关的数据-即，实体框架将加载到导航属性的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-109">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="57534-110">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="57534-110">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="57534-112">延迟、 Eager，和显式加载相关的数据</span><span class="sxs-lookup"><span data-stu-id="57534-112">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="57534-113">有多种实体框架可以加载到实体的导航属性的相关的数据：</span><span class="sxs-lookup"><span data-stu-id="57534-113">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="57534-114">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="57534-114">*Lazy loading*.</span></span> <span data-ttu-id="57534-115">第一次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="57534-115">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="57534-116">但是，第一次尝试访问导航属性时，将自动检索该导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-116">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="57534-117">这会导致发送到数据库的多个查询 — 一个用于在实体自身，一个必须检索每个相关实体的数据的时间。</span><span class="sxs-lookup"><span data-stu-id="57534-117">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> <span data-ttu-id="57534-118">`DbContext`类启用默认延迟加载。</span><span class="sxs-lookup"><span data-stu-id="57534-118">The `DbContext` class enables lazy loading by default.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="57534-120">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="57534-120">*Eager loading*.</span></span> <span data-ttu-id="57534-121">读取实体时，会检索与之相关的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-121">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="57534-122">这通常会导致执行一个检索所有必需数据的联接查询。</span><span class="sxs-lookup"><span data-stu-id="57534-122">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="57534-123">使用指定预先加载`Include`方法。</span><span class="sxs-lookup"><span data-stu-id="57534-123">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="57534-125">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="57534-125">*Explicit loading*.</span></span> <span data-ttu-id="57534-126">这是类似于延迟加载的只不过显式检索代码; 中的相关的数据它不会发生自动访问导航属性时。</span><span class="sxs-lookup"><span data-stu-id="57534-126">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="57534-127">你相关手动加载数据通过有关实体，以及调用中获取的对象状态管理器项[Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)集合的方法或[Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)包含属性的方法单个实体。</span><span class="sxs-lookup"><span data-stu-id="57534-127">You load related data manually by getting the object state manager entry for an entity and calling the [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) method for collections or the [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) method for properties that hold a single entity.</span></span> <span data-ttu-id="57534-128">(在下面的示例中，如果你想要加载管理员导航属性，则将替换`Collection(x => x.Courses)`与`Reference(x => x.Administrator)`。)通常，你将使用显式加载，仅当你已启用延迟加载关闭时。</span><span class="sxs-lookup"><span data-stu-id="57534-128">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.) Typically you'd use explicit loading only when you've turned lazy loading off.</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="57534-130">因为它们不立即检索的属性值，延迟加载和显式加载也同时称为*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="57534-130">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="57534-131">性能注意事项</span><span class="sxs-lookup"><span data-stu-id="57534-131">Performance considerations</span></span>

<span data-ttu-id="57534-132">如果你知道你需要每个已检索实体的相关数据，则预先加载通常性能最佳，因为数据库执行单个查询通常比执行用于检索每个实体的多个独立查询效率更高。</span><span class="sxs-lookup"><span data-stu-id="57534-132">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="57534-133">例如，在上面的示例中，假设每个部门都有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="57534-133">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="57534-134">预先加载示例将导致仅单 （联接） 查询和单个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="57534-134">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="57534-135">延迟加载和显式加载示例将都导致十一种查询和十一个往返行程到数据库。</span><span class="sxs-lookup"><span data-stu-id="57534-135">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="57534-136">当延迟较高时，额外的数据库通信会对性能造成不利影响。</span><span class="sxs-lookup"><span data-stu-id="57534-136">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="57534-137">另一方面，在某些情况下延迟加载会更加高效。</span><span class="sxs-lookup"><span data-stu-id="57534-137">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="57534-138">预先加载可能会导致非常复杂的联接为其生成 SQL Server 无法有效地处理它。</span><span class="sxs-lookup"><span data-stu-id="57534-138">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="57534-139">或如果你需要访问仅针对实体集的子集的实体的导航属性要处理，延迟加载可能更好地执行，因为预先加载将检索比你需要更多的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-139">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="57534-140">如果性能非常重要，最好测试这两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="57534-140">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="57534-141">延迟加载可以屏蔽导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="57534-141">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="57534-142">例如，未指定 eager 或显式加载但处理大量的实体并在每次迭代中使用多个导航属性的代码可能非常低效，（由于到数据库的许多往返过程）。</span><span class="sxs-lookup"><span data-stu-id="57534-142">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="57534-143">执行在开发使用在本地 SQL server 中良好运行的应用程序可能具有性能问题时由于的延迟时间增加和延迟加载移到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="57534-143">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="57534-144">分析的实际的测试加载的数据库的查询将帮助你确定延迟加载是否适用。</span><span class="sxs-lookup"><span data-stu-id="57534-144">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="57534-145">有关详细信息请参阅[Demystifying 实体框架策略： 加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)和[使用实体框架与 SQL Azure 到减少网络延迟](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57534-145">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

### <a name="disable-lazy-loading-before-serialization"></a><span data-ttu-id="57534-146">禁用序列化之前的延迟加载</span><span class="sxs-lookup"><span data-stu-id="57534-146">Disable lazy loading before serialization</span></span>

<span data-ttu-id="57534-147">如果你离开延迟加载启用序列化期间，你可以得到查询不按你预期的更多数据。</span><span class="sxs-lookup"><span data-stu-id="57534-147">If you leave lazy loading enabled during serialization, you can end up querying significantly more data than you intended.</span></span> <span data-ttu-id="57534-148">序列化通常可通过访问类型的实例上每个属性。</span><span class="sxs-lookup"><span data-stu-id="57534-148">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="57534-149">属性访问触发延迟加载，并为这些延迟加载的实体的序列化。</span><span class="sxs-lookup"><span data-stu-id="57534-149">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="57534-150">然后，序列化过程访问的延迟加载的实体，可能会导致更多延迟加载和序列化的每个属性。</span><span class="sxs-lookup"><span data-stu-id="57534-150">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="57534-151">若要防止此逐种链式反应，打开延迟加载关闭之前序列化实体。</span><span class="sxs-lookup"><span data-stu-id="57534-151">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="57534-152">也可序列化复杂，实体框架使用的代理类，如中所述[高级方案教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)。</span><span class="sxs-lookup"><span data-stu-id="57534-152">Serialization can also be complicated by the proxy classes that the Entity Framework uses, as explained in the [Advanced Scenarios tutorial](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).</span></span>

<span data-ttu-id="57534-153">若要避免序列化问题的一种方法是序列化而不是实体对象的数据传输对象 (Dto) 中所示[使用实体框架使用 Web API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教程。</span><span class="sxs-lookup"><span data-stu-id="57534-153">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) tutorial.</span></span>

<span data-ttu-id="57534-154">如果不使用 Dto，你可以禁用延迟加载，并避免由代理问题[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57534-154">If you don't use DTOs, you can disable lazy loading and avoid proxy issues by [disabling proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>

<span data-ttu-id="57534-155">以下是一些其他[如何禁用延迟加载](https://msdn.microsoft.com/data/jj574232):</span><span class="sxs-lookup"><span data-stu-id="57534-155">Here are some other [ways to disable lazy loading](https://msdn.microsoft.com/data/jj574232):</span></span>

- <span data-ttu-id="57534-156">对于特定的导航属性，省略`virtual`关键字声明的属性时。</span><span class="sxs-lookup"><span data-stu-id="57534-156">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="57534-157">对于所有导航属性，设置`LazyLoadingEnabled`到`false`，将以下代码放入上下文类的构造函数：</span><span class="sxs-lookup"><span data-stu-id="57534-157">For all navigation properties, set `LazyLoadingEnabled` to `false`, put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page-that-displays-department-name"></a><span data-ttu-id="57534-158">创建该显示部门名称的课程页</span><span class="sxs-lookup"><span data-stu-id="57534-158">Create a Courses Page That Displays Department Name</span></span>

<span data-ttu-id="57534-159">`Course`实体包括一个导航属性，包含`Department`过程分配给的部门实体。</span><span class="sxs-lookup"><span data-stu-id="57534-159">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="57534-160">若要显示分配的部门的名称列表中的课程，你需要获取`Name`属性从`Department`实体`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-160">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="57534-161">创建名为的控制器`CourseController`(不 CoursesController) 为`Course`实体类型，使用的相同选项**数据与视图，MVC 5 控制器使用 Entity Framework**你此前对的基架`Student`控制器，如下面的插图中所示：</span><span class="sxs-lookup"><span data-stu-id="57534-161">Create a controller named `CourseController` (not CoursesController) for the `Course` entity type, using the same options for the **MVC 5 Controller with views, using Entity Framework** scaffolder that you did earlier for the `Student` controller, as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Course_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="57534-163">打开*Controllers\CourseController.cs*并查看`Index`方法：</span><span class="sxs-lookup"><span data-stu-id="57534-163">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="57534-164">自动支架使用`Include`方法将`Department`导航属性指定为预先加载。</span><span class="sxs-lookup"><span data-stu-id="57534-164">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="57534-165">打开*Views\Course\Index.cshtml*和模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="57534-165">Open *Views\Course\Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="57534-166">突出显示了所做的更改：</span><span class="sxs-lookup"><span data-stu-id="57534-166">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

<span data-ttu-id="57534-167">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="57534-167">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="57534-168">更改标题从**索引**到**课程**。</span><span class="sxs-lookup"><span data-stu-id="57534-168">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="57534-169">添加了**Number**列以显示`CourseID`属性值。</span><span class="sxs-lookup"><span data-stu-id="57534-169">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="57534-170">默认情况下，支架代码不会显示主键，因为通常主键对最终用户来说是无意义的。</span><span class="sxs-lookup"><span data-stu-id="57534-170">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="57534-171">而在此示例中，主键是有意义的，因此需要显示。</span><span class="sxs-lookup"><span data-stu-id="57534-171">However, in this case the primary key is meaningful and you want to show it.</span></span>
- <span data-ttu-id="57534-172">移动**部门**右侧的列和更改其标题。</span><span class="sxs-lookup"><span data-stu-id="57534-172">Moved the **Department** column to the right side and changed its heading.</span></span> <span data-ttu-id="57534-173">基架正确选择要显示`Name`属性从`Department`实体，但应为列标题的课程页面中的此处**部门**而非**名称**。</span><span class="sxs-lookup"><span data-stu-id="57534-173">The scaffolder correctly chose to display the `Name` property from the `Department` entity, but here in the Course page the column heading should be **Department** rather than **Name**.</span></span>

<span data-ttu-id="57534-174">请注意，部门列的基架的代码显示`Name`属性`Department`实体加载到`Department`导航属性：</span><span class="sxs-lookup"><span data-stu-id="57534-174">Notice that for the Department column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="57534-175">运行页面 (选择**课程**Contoso 大学主页上的选项卡) 若要查看使用部门名称列表。</span><span class="sxs-lookup"><span data-stu-id="57534-175">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="57534-177">创建显示 Courses，并将注册一个教师页面</span><span class="sxs-lookup"><span data-stu-id="57534-177">Create an Instructors Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="57534-178">在本节中你将创建一个控制器，以及查看`Instructor`为了显示教师页的实体：</span><span class="sxs-lookup"><span data-stu-id="57534-178">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="57534-180">此页通过以下方式读取和显示相关的数据：</span><span class="sxs-lookup"><span data-stu-id="57534-180">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="57534-181">教师的列表显示来自的相关的数据`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="57534-181">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="57534-182">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="57534-182">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="57534-183">你将使用的预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="57534-183">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="57534-184">如前所述，在需要主表的所有已检索行的相关数据时，预先加载通常更高效。</span><span class="sxs-lookup"><span data-stu-id="57534-184">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="57534-185">在此示例中，需要显示所有已显示教师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="57534-185">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="57534-186">当用户选择一个教师，相关`Course`显示实体。</span><span class="sxs-lookup"><span data-stu-id="57534-186">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="57534-187">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="57534-187">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="57534-188">你将使用的预先加载`Course`实体和其相关`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="57534-188">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="57534-189">在这种情况下，因为你只为所选教师需要课程，延迟加载可能会更有效。</span><span class="sxs-lookup"><span data-stu-id="57534-189">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="57534-190">但是，此示例演示了如何使用预先加载方式来加载本身是导航属性中的实体内的导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-190">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="57534-191">当用户选择某一课程时，与相关的数据从`Enrollments`显示实体集。</span><span class="sxs-lookup"><span data-stu-id="57534-191">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="57534-192">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="57534-192">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="57534-193">你将添加显式加载`Enrollment`实体和其相关`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="57534-193">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="57534-194">（显式加载则无需因为启用了延迟加载，但下面的示例演示如何显式加载。）</span><span class="sxs-lookup"><span data-stu-id="57534-194">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="57534-195">为教师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="57534-195">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="57534-196">教师页显示三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="57534-196">The Instructors page shows three different tables.</span></span> <span data-ttu-id="57534-197">因此，你将创建包含三个属性的视图模型，每个属性保存一个表中的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-197">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="57534-198">在*Viewmodel*文件夹中，创建*InstructorIndexData.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="57534-198">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="57534-199">创建教师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="57534-199">Create the Instructor Controller and Views</span></span>

<span data-ttu-id="57534-200">创建`InstructorController`(不 InstructorsController) 控制器与 EF 读/写操作，如下面的插图中所示：</span><span class="sxs-lookup"><span data-stu-id="57534-200">Create an `InstructorController` (not InstructorsController) controller with EF read/write actions as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="57534-202">打开*Controllers\InstructorController.cs*并添加`using`语句`ViewModels`命名空间：</span><span class="sxs-lookup"><span data-stu-id="57534-202">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="57534-203">中的基架的代码`Index`方法指定仅对预先加载`OfficeAssignment`导航属性：</span><span class="sxs-lookup"><span data-stu-id="57534-203">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="57534-204">替换`Index`方法替换为以下代码以加载其他相关数据，并将其置于视图模型：</span><span class="sxs-lookup"><span data-stu-id="57534-204">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="57534-205">该方法将接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)，提供所选的教师和所选的过程的 ID 值并将所有所需的数据传递到该视图。</span><span class="sxs-lookup"><span data-stu-id="57534-205">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="57534-206">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="57534-206">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="57534-207">代码首先创建视图模型的实例并向其中放置教师列表。</span><span class="sxs-lookup"><span data-stu-id="57534-207">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="57534-208">该代码指定为预先加载`Instructor.OfficeAssignment`和`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-208">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="57534-209">第二个`Include`方法加载的课程，并为每个课程加载完成了预先加载`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-209">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="57534-210">如前所述，预先加载不是必需的但做是为了提高性能。</span><span class="sxs-lookup"><span data-stu-id="57534-210">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="57534-211">因为视图始终需要`OfficeAssignment`实体，它会在同一查询中提取的更加高效。</span><span class="sxs-lookup"><span data-stu-id="57534-211">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="57534-212">`Course` 中网页上，选择一个教师，以便预先加载优于延迟加载，仅当与比而无需选择某一课程更通常显示的页面时，实体所需。</span><span class="sxs-lookup"><span data-stu-id="57534-212">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="57534-213">如果选择 instructor ID，则会将所选的教师检索从教师视图模型中的列表。</span><span class="sxs-lookup"><span data-stu-id="57534-213">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="57534-214">视图模型`Courses`属性然后加载`Course`从该 instructor 实体`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-214">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="57534-215">`Where`方法将返回一个集合，但条件在此情况下传递到方法导致只有一个`Instructor`所返回的实体。</span><span class="sxs-lookup"><span data-stu-id="57534-215">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="57534-216">`Single`方法将集合转换为单个`Instructor`实体，使你可以访问该实体的`Courses`属性。</span><span class="sxs-lookup"><span data-stu-id="57534-216">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="57534-217">你使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)时你知道该集合的集合上的方法将有只有一项。</span><span class="sxs-lookup"><span data-stu-id="57534-217">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="57534-218">`Single`方法引发异常时传递给它的集合是否为空或没有多个项。</span><span class="sxs-lookup"><span data-stu-id="57534-218">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="57534-219">替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它返回默认值 (`null`在这种情况下) 如果该集合为空。</span><span class="sxs-lookup"><span data-stu-id="57534-219">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="57534-220">但是，在这种情况下，仍会生成异常 (从尝试查找`Courses`属性`null`引用)，和异常消息将不太清楚地指示问题的原因。</span><span class="sxs-lookup"><span data-stu-id="57534-220">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="57534-221">当调用`Single`方法，你还可以通过`Where`条件而不是调用`Where`方法单独：</span><span class="sxs-lookup"><span data-stu-id="57534-221">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="57534-222">而不是：</span><span class="sxs-lookup"><span data-stu-id="57534-222">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="57534-223">接下来，如果选择一门课程，则会从视图模型中的课程列表检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="57534-223">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="57534-224">然后视图模型的`Enrollments`属性加载与`Enrollment`从该过程的实体`Enrollments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-224">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="57534-225">修改教师索引视图</span><span class="sxs-lookup"><span data-stu-id="57534-225">Modify the Instructor Index View</span></span>

<span data-ttu-id="57534-226">在*Views\Instructor\Index.cshtml*，模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="57534-226">In *Views\Instructor\Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="57534-227">突出显示了所做的更改：</span><span class="sxs-lookup"><span data-stu-id="57534-227">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

<span data-ttu-id="57534-228">你对现有代码做出以下更改：</span><span class="sxs-lookup"><span data-stu-id="57534-228">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="57534-229">将模型类改为`InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="57534-229">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="57534-230">将页标题从“索引”改为“教师”。</span><span class="sxs-lookup"><span data-stu-id="57534-230">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="57534-231">添加**Office**显示的列`item.OfficeAssignment.Location`才`item.OfficeAssignment`不为 null。</span><span class="sxs-lookup"><span data-stu-id="57534-231">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="57534-232">(由于这是一个对零或一一个关系，因此可能不具备相关`OfficeAssignment`实体。)</span><span class="sxs-lookup"><span data-stu-id="57534-232">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- <span data-ttu-id="57534-233">添加将动态添加的代码`class="success"`到`tr`的所选教师的元素。</span><span class="sxs-lookup"><span data-stu-id="57534-233">Added code that will dynamically add `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="57534-234">这将设置为所选的行使用背景色[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)类。</span><span class="sxs-lookup"><span data-stu-id="57534-234">This sets a background color for the selected row using a [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) class.</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- <span data-ttu-id="57534-235">添加一个新`ActionLink`标记为**选择**立即之前每个行中的其他链接，这将导致所选的教师 ID 发送到`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="57534-235">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="57534-236">运行应用程序并选择**教师**选项卡。该页面将显示`Location`的相关属性`OfficeAssignment`实体和一个空表单元时没有相关的否`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="57534-236">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="57534-238">在*Views\Instructor\Index.cshtml*结束后的文件，`table`元素 （在文件末尾），添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="57534-238">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following code.</span></span> <span data-ttu-id="57534-239">此代码用于显示与所选教师相关的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="57534-239">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="57534-240">此代码读取视图模型的`Courses`属性，以便显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="57534-240">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="57534-241">它还提供了`Select`超链接，以便将发送到所选课程 ID`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="57534-241">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="57534-242">运行页面，然后选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="57534-242">Run the page and select an instructor.</span></span> <span data-ttu-id="57534-243">此时会看到一个网格，其中显示分配给所选教师的课程。每个课程都会看到相应系的名称。</span><span class="sxs-lookup"><span data-stu-id="57534-243">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="57534-245">在刚添加的代码块之后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="57534-245">After the code block you just added, add the following code.</span></span> <span data-ttu-id="57534-246">这样就会显示一个注册了所选课程的学生的列表。</span><span class="sxs-lookup"><span data-stu-id="57534-246">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="57534-247">此代码读取`Enrollments`为了显示学生的列表视图模型的属性在本课程中注册。</span><span class="sxs-lookup"><span data-stu-id="57534-247">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="57534-248">运行页面，然后选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="57534-248">Run the page and select an instructor.</span></span> <span data-ttu-id="57534-249">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="57534-249">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="57534-251">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="57534-251">Adding Explicit Loading</span></span>

<span data-ttu-id="57534-252">打开*InstructorController.cs*并查看如何`Index`方法获取有关所选过程的注册的列表：</span><span class="sxs-lookup"><span data-stu-id="57534-252">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="57534-253">时检索教师的列表，您已指定为预先加载`Courses`导航属性和`Department`当然，每个属性。</span><span class="sxs-lookup"><span data-stu-id="57534-253">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="57534-254">则你将放`Courses`集合在视图模型中，并且现在正在访问`Enrollments`从该集合中的一个实体导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-254">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="57534-255">因为你未指定为预先加载`Course.Enrollments`导航属性，该属性中的数据显示在由于延迟加载的页中。</span><span class="sxs-lookup"><span data-stu-id="57534-255">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="57534-256">如果不更改任何其他方式中的代码的情况下禁用延迟加载`Enrollments`属性将为 null 而不考虑过程实际上有多少注册。</span><span class="sxs-lookup"><span data-stu-id="57534-256">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="57534-257">在此情况下，加载`Enrollments`属性，你将需要指定预先加载或显式加载。</span><span class="sxs-lookup"><span data-stu-id="57534-257">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="57534-258">你已经了解如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="57534-258">You've already seen how to do eager loading.</span></span> <span data-ttu-id="57534-259">若要查看的显式加载示例，替换`Index`方法替换为以下代码，此操作将显式加载`Enrollments`属性。</span><span class="sxs-lookup"><span data-stu-id="57534-259">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="57534-260">更改的代码将突出显示。</span><span class="sxs-lookup"><span data-stu-id="57534-260">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

<span data-ttu-id="57534-261">获取所选后`Course`实体，新的代码显式加载该课程`Enrollments`导航属性：</span><span class="sxs-lookup"><span data-stu-id="57534-261">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="57534-262">然后它显式加载每个`Enrollment`实体的相关`Student`实体：</span><span class="sxs-lookup"><span data-stu-id="57534-262">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="57534-263">请注意，你使用`Collection`方法以加载集合属性，但对于一个属性，保存一个实体，你使用`Reference`方法。</span><span class="sxs-lookup"><span data-stu-id="57534-263">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span>

<span data-ttu-id="57534-264">立即运行教师索引页，你将看到在页上，显示的内容不会改变，虽然已经更改了如何检索的数据。</span><span class="sxs-lookup"><span data-stu-id="57534-264">Run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="57534-265">总结</span><span class="sxs-lookup"><span data-stu-id="57534-265">Summary</span></span>

<span data-ttu-id="57534-266">你现在使用所有三种方法 （延迟、 eager，和显式） 相关的数据加载到导航属性。</span><span class="sxs-lookup"><span data-stu-id="57534-266">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="57534-267">下一教程介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="57534-267">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="57534-268">请在如何喜欢本教程的方式，我们可以提高上，留下反馈。</span><span class="sxs-lookup"><span data-stu-id="57534-268">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="57534-269">你还可以请求新主题[教我编写代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="57534-269">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="57534-270">在找不到其他实体框架资源的链接[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="57534-270">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="57534-271">[上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="57534-271">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
