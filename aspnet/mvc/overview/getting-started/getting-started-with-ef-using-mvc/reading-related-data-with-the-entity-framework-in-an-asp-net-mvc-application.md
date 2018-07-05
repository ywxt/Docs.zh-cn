---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 读取相关的数据使用实体框架中的 ASP.NET MVC 应用程序 |Microsoft Docs
author: tdykstra
description: /ajax/tutorials/using-ajax-control-toolkit-controls-and-control-extenders-vb
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 24ee4cd1de4b2868af15513439a88e5363ee11e9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401271"
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="0ad3e-103">读取相关数据与 ASP.NET MVC 应用程序中的实体框架</span><span class="sxs-lookup"><span data-stu-id="0ad3e-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="0ad3e-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0ad3e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0ad3e-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="0ad3e-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="0ad3e-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="0ad3e-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="0ad3e-108">在上一教程中，您将完成学校数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-108">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="0ad3e-109">在本教程将读取并显示相关的数据-即 Entity Framework 加载到导航属性的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-109">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="0ad3e-110">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-110">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="0ad3e-112">延迟、 及早计算，和显式加载相关数据</span><span class="sxs-lookup"><span data-stu-id="0ad3e-112">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="0ad3e-113">有几种方法，实体框架可以相关的数据加载到实体的导航属性：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-113">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="0ad3e-114">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-114">*Lazy loading*.</span></span> <span data-ttu-id="0ad3e-115">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-115">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="0ad3e-116">然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-116">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="0ad3e-117">这会导致发送到数据库的多个查询 — 一个用于实体本身，一个必须检索每个相关实体数据的时间。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-117">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> <span data-ttu-id="0ad3e-118">`DbContext`类默认情况下启用延迟加载。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-118">The `DbContext` class enables lazy loading by default.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="0ad3e-120">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-120">*Eager loading*.</span></span> <span data-ttu-id="0ad3e-121">读取该实体时，会同时检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-121">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="0ad3e-122">此时通常会出现单一联接查询，检索所有必需数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-122">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="0ad3e-123">使用指定预先加载`Include`方法。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-123">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="0ad3e-125">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-125">*Explicit loading*.</span></span> <span data-ttu-id="0ad3e-126">这是类似于延迟加载的只不过显式检索相关的数据中的代码;它不会自动发生时您访问导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-126">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="0ad3e-127">加载相关的数据手动通过实体和调用获取对象状态管理器入口[Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)集合的方法或[Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)方法保存的属性单个实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-127">You load related data manually by getting the object state manager entry for an entity and calling the [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) method for collections or the [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) method for properties that hold a single entity.</span></span> <span data-ttu-id="0ad3e-128">(在以下示例中，如果你想要加载管理员导航属性，您会取代`Collection(x => x.Courses)`与`Reference(x => x.Administrator)`。)通常会使用显式加载，仅当你已启用延迟加载关闭时。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-128">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.) Typically you'd use explicit loading only when you've turned lazy loading off.</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="0ad3e-130">因为它们不立即检索属性值，延迟加载和显式加载也都称为*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-130">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="0ad3e-131">性能注意事项</span><span class="sxs-lookup"><span data-stu-id="0ad3e-131">Performance considerations</span></span>

<span data-ttu-id="0ad3e-132">如果知道自己需要每个检索的实体的相关数据，选择预先加载可获得最佳性能，因为相比每个检索的实体的单独查询，发送到数据库的单个查询更加有效。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-132">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="0ad3e-133">例如，在上面的示例中，假设每个系有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-133">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="0ad3e-134">预先加载示例会导致只需单一 （联接） 查询，将单个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-134">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="0ad3e-135">延迟加载和显式加载示例将同时导致 11 个查询和 11 个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-135">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="0ad3e-136">延迟较高时，额外往返数据库对性能尤为不利。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-136">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="0ad3e-137">但是，在某些情况下延迟加载是更高效。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-137">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="0ad3e-138">预先加载可能会导致非常复杂的联接为其生成 SQL Server 无法有效地处理它。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-138">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="0ad3e-139">或者，如果您需要访问实体的导航属性仅对一组实体的子集进行处理，延迟加载可能会更好地执行，因为预先加载将检索数据超过所需的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-139">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="0ad3e-140">如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-140">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="0ad3e-141">延迟加载可以屏蔽会导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-141">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="0ad3e-142">例如，（由于与数据库的多个往返） 未指定预先或显式加载，但处理大量的实体并在每次迭代中使用多个导航属性的代码可能是非常低效。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-142">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="0ad3e-143">在开发使用本地 SQL 服务器中执行的应用程序可能具有性能问题时增加延迟时间和延迟加载由于移到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-143">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="0ad3e-144">分析数据库查询的实际测试负载将有助于确定延迟加载是否适当。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-144">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="0ad3e-145">有关详细信息请参阅[揭开面纱实体框架策略： 加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)并[使用 Entity Framework 减少 SQL Azure 的网络延迟到](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-145">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

### <a name="disable-lazy-loading-before-serialization"></a><span data-ttu-id="0ad3e-146">禁用延迟加载序列化之前</span><span class="sxs-lookup"><span data-stu-id="0ad3e-146">Disable lazy loading before serialization</span></span>

<span data-ttu-id="0ad3e-147">如果将延迟加载已启用序列化期间，您可以得到查询比你预期更多的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-147">If you leave lazy loading enabled during serialization, you can end up querying significantly more data than you intended.</span></span> <span data-ttu-id="0ad3e-148">序列化通常可通过访问类型的实例上每个属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-148">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="0ad3e-149">属性访问触发延迟加载，并为这些延迟加载的实体进行序列化。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-149">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="0ad3e-150">然后，序列化过程访问的延迟加载的实体，可能会导致更多的延迟加载和序列化的每个属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-150">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="0ad3e-151">若要防止此用尽链式反应，启用延迟加载关闭之前序列化实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-151">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="0ad3e-152">此外将序列化复杂由实体框架使用，代理类，如中所述[高级方案教程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-152">Serialization can also be complicated by the proxy classes that the Entity Framework uses, as explained in the [Advanced Scenarios tutorial](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).</span></span>

<span data-ttu-id="0ad3e-153">若要避免序列化问题的一种方法是要序列化数据传输对象 (Dto)，而不是实体对象，如中所示[使用实体框架使用 Web API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-153">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) tutorial.</span></span>

<span data-ttu-id="0ad3e-154">如果不使用 Dto，可以禁用延迟加载，从而避免由代理问题[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-154">If you don't use DTOs, you can disable lazy loading and avoid proxy issues by [disabling proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>

<span data-ttu-id="0ad3e-155">以下是一些其他[方式禁用延迟加载](https://msdn.microsoft.com/data/jj574232):</span><span class="sxs-lookup"><span data-stu-id="0ad3e-155">Here are some other [ways to disable lazy loading](https://msdn.microsoft.com/data/jj574232):</span></span>

- <span data-ttu-id="0ad3e-156">对于特定的导航属性，省略`virtual`关键字声明的属性时。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-156">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="0ad3e-157">对于所有导航属性，设置`LazyLoadingEnabled`到`false`，上下文类的构造函数中添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-157">For all navigation properties, set `LazyLoadingEnabled` to `false`, put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page-that-displays-department-name"></a><span data-ttu-id="0ad3e-158">创建该显示院系名称的课程页</span><span class="sxs-lookup"><span data-stu-id="0ad3e-158">Create a Courses Page That Displays Department Name</span></span>

<span data-ttu-id="0ad3e-159">`Course`实体包括导航属性包含`Department`院系的课程将分配到的实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-159">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="0ad3e-160">若要在课程列表中显示的分配系的名称，您需要获取`Name`属性从`Department`中的实体`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-160">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="0ad3e-161">创建名为的控制器`CourseController`(不 CoursesController) 用于`Course`实体类型，使用相同的选项**包含的 MVC 5 控制器视图，使用实体框架**用于之前所做的基架`Student`控制器，如下图中所示：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-161">Create a controller named `CourseController` (not CoursesController) for the `Course` entity type, using the same options for the **MVC 5 Controller with views, using Entity Framework** scaffolder that you did earlier for the `Student` controller, as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Course_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="0ad3e-163">打开*Controllers\CourseController.cs*并查看`Index`方法：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-163">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="0ad3e-164">自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-164">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="0ad3e-165">打开*Views\Course\Index.cshtml*和模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-165">Open *Views\Course\Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="0ad3e-166">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-166">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

<span data-ttu-id="0ad3e-167">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-167">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="0ad3e-168">更改将标题从**索引**到**课程**。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-168">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="0ad3e-169">添加了显示 `CourseID` 属性值的“数字”列。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-169">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="0ad3e-170">默认情况下，主键不是基架，因为它们通常是向最终用户无意义。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-170">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="0ad3e-171">但在这种情况下主键是有意义的，而你需要将其呈现出来。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-171">However, in this case the primary key is meaningful and you want to show it.</span></span>
- <span data-ttu-id="0ad3e-172">移动**部门**列的右侧，更改其标题。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-172">Moved the **Department** column to the right side and changed its heading.</span></span> <span data-ttu-id="0ad3e-173">基架正确选择显示`Name`属性从`Department`实体，但应为列标题的课程页中的此处**部门**而非**名称**。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-173">The scaffolder correctly chose to display the `Name` property from the `Department` entity, but here in the Course page the column heading should be **Department** rather than **Name**.</span></span>

<span data-ttu-id="0ad3e-174">请注意，对于部门列中，基架的代码将显示`Name`的属性`Department`实体加载到`Department`导航属性：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-174">Notice that for the Department column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="0ad3e-175">运行页 (选择**课程**Contoso University 主页上的选项卡) 若要查看包含系名称列表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-175">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="0ad3e-177">创建显示课程和注册的讲师页</span><span class="sxs-lookup"><span data-stu-id="0ad3e-177">Create an Instructors Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="0ad3e-178">将在本部分中创建一个控制器并查看`Instructor`实体以显示讲师页：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-178">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="0ad3e-180">该页面通过以下方式读取和显示相关数据：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-180">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="0ad3e-181">讲师列表显示的相关的数据`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-181">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="0ad3e-182">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-182">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="0ad3e-183">你将使用预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-183">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="0ad3e-184">如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-184">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="0ad3e-185">在这种情况下，你希望显示所有显示的讲师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-185">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="0ad3e-186">当用户选择一名讲师，相关`Course`实体的显示。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-186">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="0ad3e-187">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-187">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="0ad3e-188">你将使用预先加载`Course`实体和其相关`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-188">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="0ad3e-189">在这种情况下，可能延迟加载是更高效，因为你需要仅对所选讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-189">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="0ad3e-190">但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-190">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="0ad3e-191">当用户选择一门课程时，与相关的数据从`Enrollments`显示实体集。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-191">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="0ad3e-192">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-192">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="0ad3e-193">你将添加用于显式加载`Enrollment`实体和其相关`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-193">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="0ad3e-194">（显式加载无需因为启用了延迟加载，但这将显示如何执行显式加载。）</span><span class="sxs-lookup"><span data-stu-id="0ad3e-194">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="0ad3e-195">为讲师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="0ad3e-195">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="0ad3e-196">讲师页显示了三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-196">The Instructors page shows three different tables.</span></span> <span data-ttu-id="0ad3e-197">因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-197">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="0ad3e-198">在中*Viewmodel*文件夹中，创建*InstructorIndexData.cs*和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-198">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="0ad3e-199">创建讲师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="0ad3e-199">Create the Instructor Controller and Views</span></span>

<span data-ttu-id="0ad3e-200">创建`InstructorController`(不 InstructorsController) 控制器使用 EF 读/写操作，如下图中所示：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-200">Create an `InstructorController` (not InstructorsController) controller with EF read/write actions as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="0ad3e-202">打开*Controllers\InstructorController.cs*并添加`using`语句`ViewModels`命名空间：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-202">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="0ad3e-203">中的基架的代码`Index`方法指定预先加载仅`OfficeAssignment`导航属性：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-203">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="0ad3e-204">替换为`Index`方法与以下代码以加载其他相关数据并将其放在视图模型中：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-204">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="0ad3e-205">该方法接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)，提供 ID 值的所选的讲师和课程，并将所有所需的数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-205">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="0ad3e-206">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-206">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="0ad3e-207">代码先创建一个视图模型实例，并在其中放入讲师列表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-207">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="0ad3e-208">该代码指定预先加载`Instructor.OfficeAssignment`和`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-208">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="0ad3e-209">第二个`Include`方法加载课程，并为每个课程加载完成了预先加载`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-209">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="0ad3e-210">正如前面提到，预先加载不是必需的但做是为了提高性能。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-210">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="0ad3e-211">由于视图始终需要`OfficeAssignment`实体，它是更有效地在同一查询中提取的。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-211">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="0ad3e-212">`Course` 实体是必需的因此预先加载是优于延迟加载，仅当与选中课程更频繁地显示的页中 web 页上，选择一名讲师时。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-212">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="0ad3e-213">如果选择了讲师 ID，则从视图模型中的讲师列表检索所选的讲师。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-213">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="0ad3e-214">视图模型`Courses`属性然后加载`Course`讲师实体`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-214">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="0ad3e-215">`Where`方法将返回一个集合，但在这种情况下只有一个在向该方法传入条件`Instructor`所返回的实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-215">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="0ad3e-216">`Single`方法将集合转换为一个`Instructor`实体，这将使您可以访问该实体的`Courses`属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-216">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="0ad3e-217">您使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)集合时知道集合上的方法将具有只有一个项。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-217">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="0ad3e-218">`Single`方法将引发异常，如果传递给它的集合为空或多个项。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-218">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="0ad3e-219">一种替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它返回默认值 (`null`这种情况下) 是否为空集合。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-219">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="0ad3e-220">但是，在这种情况下，仍会引发异常 (尝试查找`Courses`属性上的`null`引用)，和异常消息会清楚指出问题的原因。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-220">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="0ad3e-221">当您调用`Single`方法，您还可以传入`Where`条件而不是调用`Where`方法分开：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-221">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="0ad3e-222">而不是：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-222">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="0ad3e-223">接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-223">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="0ad3e-224">然后，视图模型的`Enrollments`属性加载`Enrollment`从该课程实体`Enrollments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-224">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="0ad3e-225">修改讲师索引视图</span><span class="sxs-lookup"><span data-stu-id="0ad3e-225">Modify the Instructor Index View</span></span>

<span data-ttu-id="0ad3e-226">在中*Views\Instructor\Index.cshtml*，模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-226">In *Views\Instructor\Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="0ad3e-227">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-227">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

<span data-ttu-id="0ad3e-228">已对现有代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-228">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="0ad3e-229">将模型类更改为了 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-229">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="0ad3e-230">将页标题从“索引”更改为了“讲师”。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-230">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="0ad3e-231">添加**Office**显示的列`item.OfficeAssignment.Location`仅当`item.OfficeAssignment`不为 null。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-231">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="0ad3e-232">(这是一对零或一一关系，因为可能不会有相关`OfficeAssignment`实体。)</span><span class="sxs-lookup"><span data-stu-id="0ad3e-232">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- <span data-ttu-id="0ad3e-233">添加了的代码，将动态添加`class="success"`到`tr`的所选讲师的元素。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-233">Added code that will dynamically add `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="0ad3e-234">这将设置为所选的行使用背景色[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)类。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-234">This sets a background color for the selected row using a [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) class.</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- <span data-ttu-id="0ad3e-235">添加了新`ActionLink`标记为**选择**之前每个行中的其他链接，这将导致所选的讲师 ID 发送到`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-235">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="0ad3e-236">运行应用程序，并选择**讲师**选项卡。页将显示`Location`属性的相关`OfficeAssignment`实体和一个空表单元时有无相关`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-236">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="0ad3e-238">在中*Views\Instructor\Index.cshtml*文件之后，结束`table`元素 （在文件末尾），添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-238">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following code.</span></span> <span data-ttu-id="0ad3e-239">选择讲师时，此代码显示与讲师相关的课程列表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-239">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="0ad3e-240">此代码读取视图模型的 `Courses` 属性以显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-240">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="0ad3e-241">它还提供了`Select`发送到所选课程的 ID 的超链接`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-241">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="0ad3e-242">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-242">Run the page and select an instructor.</span></span> <span data-ttu-id="0ad3e-243">此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-243">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="0ad3e-245">在刚刚添加的代码块后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-245">After the code block you just added, add the following code.</span></span> <span data-ttu-id="0ad3e-246">选择课程后，代码将显示参与课程的学生列表。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-246">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="0ad3e-247">此代码读取`Enrollments`以便显示学生列表视图模型属性参加该课程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-247">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="0ad3e-248">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-248">Run the page and select an instructor.</span></span> <span data-ttu-id="0ad3e-249">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-249">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="0ad3e-251">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="0ad3e-251">Adding Explicit Loading</span></span>

<span data-ttu-id="0ad3e-252">打开*InstructorController.cs* ，并查看如何`Index`方法获取所选课程的注册列表：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-252">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="0ad3e-253">当检索讲师列表时，您指定了预先加载`Courses`导航属性和`Department`属性的每个课程。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-253">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="0ad3e-254">然后您将放`Courses`集合视图模型中，现在正在访问`Enrollments`从该集合中的一个实体的导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-254">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="0ad3e-255">因为未指定预先加载`Course.Enrollments`导航属性，作为延迟加载结果页中显示来自该属性的数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-255">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="0ad3e-256">如果无需更改代码以任何方式禁用延迟加载`Enrollments`属性将为 null 而不考虑该课程实际上有多少注册。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-256">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="0ad3e-257">在此情况下，若要加载`Enrollments`属性，您将需要指定预先加载还是显式加载。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-257">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="0ad3e-258">您所见如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-258">You've already seen how to do eager loading.</span></span> <span data-ttu-id="0ad3e-259">若要查看的显式加载示例，请替换`Index`方法显式加载的以下代码替换`Enrollments`属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-259">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="0ad3e-260">突出显示更改的代码。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-260">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

<span data-ttu-id="0ad3e-261">获取所选后`Course`实体，新代码，显式加载该课程`Enrollments`导航属性：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-261">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="0ad3e-262">然后它显式加载每个`Enrollment`实体的相关`Student`实体：</span><span class="sxs-lookup"><span data-stu-id="0ad3e-262">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="0ad3e-263">请注意，使用`Collection`方法以加载集合属性，但对于一个属性，保存只是一个实体，你使用`Reference`方法。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-263">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span>

<span data-ttu-id="0ad3e-264">立即运行讲师索引页，尽管已经更改数据的检索方式，您将看到的页上，显示的内容没有区别。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-264">Run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="0ad3e-265">总结</span><span class="sxs-lookup"><span data-stu-id="0ad3e-265">Summary</span></span>

<span data-ttu-id="0ad3e-266">现在，你已使用所有三种方式 （延迟、 及早计算，和显式） 将相关的数据加载到导航属性。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-266">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="0ad3e-267">下一个教程将介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-267">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="0ad3e-268">请在你喜欢本教程的内容，我们可以提高上留下反馈。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-268">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="0ad3e-269">此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-269">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span>

<span data-ttu-id="0ad3e-270">其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="0ad3e-270">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0ad3e-271">[上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="0ad3e-271">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
