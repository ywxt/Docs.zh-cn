---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 读取相关的数据使用实体框架在 ASP.NET MVC 应用程序 (共 10 个 5) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4767b015db0bad09942802827ce54162687fcabc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833110"
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="473c3-103">读取相关数据使用实体框架在 ASP.NET MVC 应用程序 (5 10 个)</span><span class="sxs-lookup"><span data-stu-id="473c3-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>
====================
<span data-ttu-id="473c3-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="473c3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="473c3-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="473c3-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="473c3-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="473c3-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="473c3-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="473c3-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="473c3-108">您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。</span><span class="sxs-lookup"><span data-stu-id="473c3-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="473c3-109">如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="473c3-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="473c3-110">通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="473c3-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="473c3-111">一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="473c3-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="473c3-112">在上一教程中，您将完成学校数据模型。</span><span class="sxs-lookup"><span data-stu-id="473c3-112">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="473c3-113">在本教程将读取并显示相关的数据-即 Entity Framework 加载到导航属性的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-113">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="473c3-114">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="473c3-114">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="473c3-116">延迟、 及早计算，和显式加载相关数据</span><span class="sxs-lookup"><span data-stu-id="473c3-116">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="473c3-117">有几种方法，实体框架可以相关的数据加载到实体的导航属性：</span><span class="sxs-lookup"><span data-stu-id="473c3-117">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="473c3-118">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="473c3-118">*Lazy loading*.</span></span> <span data-ttu-id="473c3-119">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-119">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="473c3-120">然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-120">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="473c3-121">这会导致发送到数据库的多个查询 — 一个用于实体本身，一个必须检索每个相关实体数据的时间。</span><span class="sxs-lookup"><span data-stu-id="473c3-121">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="473c3-123">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="473c3-123">*Eager loading*.</span></span> <span data-ttu-id="473c3-124">读取该实体时，会同时检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-124">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="473c3-125">此时通常会出现单一联接查询，检索所有必需数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-125">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="473c3-126">使用指定预先加载`Include`方法。</span><span class="sxs-lookup"><span data-stu-id="473c3-126">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="473c3-128">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="473c3-128">*Explicit loading*.</span></span> <span data-ttu-id="473c3-129">这是类似于延迟加载的只不过显式检索相关的数据中的代码;它不会自动发生时您访问导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-129">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="473c3-130">加载相关的数据手动通过实体和调用获取对象状态管理器入口`Collection.Load`集合的方法或`Reference.Load`保存单个实体的属性的方法。</span><span class="sxs-lookup"><span data-stu-id="473c3-130">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="473c3-131">(在以下示例中，如果你想要加载管理员导航属性，您会取代`Collection(x => x.Courses)`与`Reference(x => x.Administrator)`。)</span><span class="sxs-lookup"><span data-stu-id="473c3-131">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="473c3-133">因为它们不立即检索属性值，延迟加载和显式加载也都称为*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="473c3-133">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="473c3-134">一般情况下，如果您知道你需要相关的数据对于每个实体检索到的预先加载提供最佳性能，因为发送到数据库的单个查询通常比个检索每个实体的单独查询更有效。</span><span class="sxs-lookup"><span data-stu-id="473c3-134">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="473c3-135">例如，在上面的示例中，假设每个系有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="473c3-135">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="473c3-136">预先加载示例会导致只需单一 （联接） 查询，将单个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="473c3-136">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="473c3-137">延迟加载和显式加载示例将同时导致 11 个查询和 11 个往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="473c3-137">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="473c3-138">延迟较高时，额外往返数据库对性能尤为不利。</span><span class="sxs-lookup"><span data-stu-id="473c3-138">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="473c3-139">但是，在某些情况下延迟加载是更高效。</span><span class="sxs-lookup"><span data-stu-id="473c3-139">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="473c3-140">预先加载可能会导致非常复杂的联接为其生成 SQL Server 无法有效地处理它。</span><span class="sxs-lookup"><span data-stu-id="473c3-140">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="473c3-141">或者，如果您需要访问实体的导航属性仅对一组实体的子集进行处理，延迟加载可能会更好地执行，因为预先加载将检索数据超过所需的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-141">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="473c3-142">如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="473c3-142">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="473c3-143">通常会使用显式加载，仅当你已启用延迟加载关闭时。</span><span class="sxs-lookup"><span data-stu-id="473c3-143">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="473c3-144">你应打开延迟加载关闭时的一个方案是在序列化过程。</span><span class="sxs-lookup"><span data-stu-id="473c3-144">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="473c3-145">延迟加载和序列化，不要混合，如果您不小心最终查询更多的数据比预期时延迟加载处于启用状态。</span><span class="sxs-lookup"><span data-stu-id="473c3-145">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="473c3-146">序列化通常可通过访问类型的实例上每个属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-146">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="473c3-147">属性访问触发延迟加载，并为这些延迟加载的实体进行序列化。</span><span class="sxs-lookup"><span data-stu-id="473c3-147">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="473c3-148">然后，序列化过程访问的延迟加载的实体，可能会导致更多的延迟加载和序列化的每个属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-148">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="473c3-149">若要防止此用尽链式反应，启用延迟加载关闭之前序列化实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-149">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="473c3-150">默认情况下，数据库上下文类执行延迟加载。</span><span class="sxs-lookup"><span data-stu-id="473c3-150">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="473c3-151">有两种禁用延迟加载的方法：</span><span class="sxs-lookup"><span data-stu-id="473c3-151">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="473c3-152">对于特定的导航属性，省略`virtual`关键字声明的属性时。</span><span class="sxs-lookup"><span data-stu-id="473c3-152">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="473c3-153">对于所有导航属性，设置`LazyLoadingEnabled`到`false`。</span><span class="sxs-lookup"><span data-stu-id="473c3-153">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="473c3-154">例如，可以将以下代码放在您的上下文类的构造函数中：</span><span class="sxs-lookup"><span data-stu-id="473c3-154">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="473c3-155">延迟加载可以屏蔽会导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-155">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="473c3-156">例如，（由于与数据库的多个往返） 未指定预先或显式加载，但处理大量的实体并在每次迭代中使用多个导航属性的代码可能是非常低效。</span><span class="sxs-lookup"><span data-stu-id="473c3-156">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="473c3-157">在开发使用本地 SQL 服务器中执行的应用程序可能具有性能问题时增加延迟时间和延迟加载由于移到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="473c3-157">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="473c3-158">分析数据库查询的实际测试负载将有助于确定延迟加载是否适当。</span><span class="sxs-lookup"><span data-stu-id="473c3-158">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="473c3-159">有关详细信息请参阅[揭开面纱实体框架策略： 加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx)并[使用 Entity Framework 减少 SQL Azure 的网络延迟到](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="473c3-159">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="473c3-160">创建该显示院系名称的课程索引页</span><span class="sxs-lookup"><span data-stu-id="473c3-160">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="473c3-161">`Course`实体包括导航属性包含`Department`院系的课程将分配到的实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-161">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="473c3-162">若要在课程列表中显示的分配系的名称，您需要获取`Name`属性从`Department`中的实体`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-162">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="473c3-163">创建名为的控制器`CourseController`有关`Course`实体类型，使用之前的相同选项`Student`控制器，如下图中所示 （但与不同的映像，您的上下文类位于 DAL 的命名空间，不是模型命名空间）：</span><span class="sxs-lookup"><span data-stu-id="473c3-163">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="473c3-165">打开*Controllers\CourseController.cs*并查看`Index`方法：</span><span class="sxs-lookup"><span data-stu-id="473c3-165">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="473c3-166">自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="473c3-166">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="473c3-167">打开*Views\Course\Index.cshtml*和现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-167">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="473c3-168">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="473c3-168">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="473c3-169">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="473c3-169">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="473c3-170">更改将标题从**索引**到**课程**。</span><span class="sxs-lookup"><span data-stu-id="473c3-170">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="473c3-171">向左移动行链接。</span><span class="sxs-lookup"><span data-stu-id="473c3-171">Moved the row links to the left.</span></span>
- <span data-ttu-id="473c3-172">添加列标题下的**数量**显示`CourseID`属性值。</span><span class="sxs-lookup"><span data-stu-id="473c3-172">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="473c3-173">（默认情况下，主键不是已搭建基架因为它们通常是向最终用户无意义。</span><span class="sxs-lookup"><span data-stu-id="473c3-173">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="473c3-174">但是，在这种情况下主键是有意义并且你想要显示它。）</span><span class="sxs-lookup"><span data-stu-id="473c3-174">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="473c3-175">更改从最后一个列标题**DepartmentID** (到外键的名称`Department`实体) 对**部门**。</span><span class="sxs-lookup"><span data-stu-id="473c3-175">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="473c3-176">请注意，对于最后一列中，基架的代码将显示`Name`的属性`Department`实体加载到`Department`导航属性：</span><span class="sxs-lookup"><span data-stu-id="473c3-176">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="473c3-177">运行页 (选择**课程**Contoso University 主页上的选项卡) 若要查看包含系名称列表。</span><span class="sxs-lookup"><span data-stu-id="473c3-177">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="473c3-179">创建显示课程和注册的讲师索引页</span><span class="sxs-lookup"><span data-stu-id="473c3-179">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="473c3-180">将在本部分中创建一个控制器并查看`Instructor`实体以显示讲师索引页：</span><span class="sxs-lookup"><span data-stu-id="473c3-180">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="473c3-182">该页面通过以下方式读取和显示相关数据：</span><span class="sxs-lookup"><span data-stu-id="473c3-182">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="473c3-183">讲师列表显示的相关的数据`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-183">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="473c3-184">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="473c3-184">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="473c3-185">你将使用预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-185">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="473c3-186">如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。</span><span class="sxs-lookup"><span data-stu-id="473c3-186">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="473c3-187">在这种情况下，你希望显示所有显示的讲师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="473c3-187">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="473c3-188">当用户选择一名讲师，相关`Course`实体的显示。</span><span class="sxs-lookup"><span data-stu-id="473c3-188">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="473c3-189">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="473c3-189">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="473c3-190">你将使用预先加载`Course`实体和其相关`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-190">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="473c3-191">在这种情况下，可能延迟加载是更高效，因为你需要仅对所选讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="473c3-191">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="473c3-192">但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-192">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="473c3-193">当用户选择一门课程时，与相关的数据从`Enrollments`显示实体集。</span><span class="sxs-lookup"><span data-stu-id="473c3-193">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="473c3-194">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="473c3-194">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="473c3-195">你将添加用于显式加载`Enrollment`实体和其相关`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-195">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="473c3-196">（显式加载无需因为启用了延迟加载，但这将显示如何执行显式加载。）</span><span class="sxs-lookup"><span data-stu-id="473c3-196">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="473c3-197">为讲师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="473c3-197">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="473c3-198">讲师索引页显示了三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="473c3-198">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="473c3-199">因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-199">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="473c3-200">在中*Viewmodel*文件夹中，创建*InstructorIndexData.cs*和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="473c3-200">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="473c3-201">添加所选行的样式</span><span class="sxs-lookup"><span data-stu-id="473c3-201">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="473c3-202">若要将标记所选的行需要不同的背景色。</span><span class="sxs-lookup"><span data-stu-id="473c3-202">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="473c3-203">若要为此用户界面提供一种样式，请将以下突出显示的代码添加到部分`/* info and errors */`中*Content\Site.css*，如下所示：</span><span class="sxs-lookup"><span data-stu-id="473c3-203">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="473c3-204">创建讲师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="473c3-204">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="473c3-205">创建`InstructorController`控制器，如下图中所示：</span><span class="sxs-lookup"><span data-stu-id="473c3-205">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="473c3-207">打开*Controllers\InstructorController.cs*并添加`using`语句`ViewModels`命名空间：</span><span class="sxs-lookup"><span data-stu-id="473c3-207">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="473c3-208">中的基架的代码`Index`方法指定预先加载仅`OfficeAssignment`导航属性：</span><span class="sxs-lookup"><span data-stu-id="473c3-208">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="473c3-209">替换为`Index`方法与以下代码以加载其他相关数据并将其放在视图模型中：</span><span class="sxs-lookup"><span data-stu-id="473c3-209">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="473c3-210">该方法接受可选路由数据 (`id`) 和查询字符串参数 (`courseID`)，提供 ID 值的所选的讲师和课程，并将所有所需的数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="473c3-210">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="473c3-211">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="473c3-211">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP]
> 
> <span data-ttu-id="473c3-212">**路由数据**</span><span class="sxs-lookup"><span data-stu-id="473c3-212">**Route data**</span></span>
> 
> <span data-ttu-id="473c3-213">路由数据是在路由表中指定的 URL 段中找到的模型联编程序的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-213">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="473c3-214">例如，指定默认路由`controller`， `action`，和`id`段：</span><span class="sxs-lookup"><span data-stu-id="473c3-214">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> <span data-ttu-id="473c3-215">routes.MapRoute(</span><span class="sxs-lookup"><span data-stu-id="473c3-215">routes.MapRoute(</span></span>  
>  <span data-ttu-id="473c3-216">名称:"Default"</span><span class="sxs-lookup"><span data-stu-id="473c3-216">name: "Default",</span></span>  
>  <span data-ttu-id="473c3-217">url:"{controller} / {action} / {id}"，</span><span class="sxs-lookup"><span data-stu-id="473c3-217">url: "{controller}/{action}/{id}",</span></span>  
>  <span data-ttu-id="473c3-218">默认值： new {控制器 ="主页"，操作 ="Index"，id = UrlParameter.Optional}</span><span class="sxs-lookup"><span data-stu-id="473c3-218">defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }</span></span>  
> <span data-ttu-id="473c3-219">);</span><span class="sxs-lookup"><span data-stu-id="473c3-219">);</span></span>
> 
> <span data-ttu-id="473c3-220">在以下 URL，默认路由映射`Instructor`作为`controller`，`Index`作为`action`1 赋`id`; 这些是路由数据值。</span><span class="sxs-lookup"><span data-stu-id="473c3-220">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="473c3-221">"？ courseID = 2021年"是一个查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="473c3-221">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="473c3-222">如果传递的模型联编程序也能`id`作为查询字符串值：</span><span class="sxs-lookup"><span data-stu-id="473c3-222">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="473c3-223">通过创建 Url `ActionLink` Razor 视图中的语句。</span><span class="sxs-lookup"><span data-stu-id="473c3-223">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="473c3-224">在下面的代码中，`id`参数匹配的默认路由，因此`id`添加到路由数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-224">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="473c3-225">在下面的代码，`courseID`不匹配默认路由中的参数，因此，它将添加为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="473c3-225">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]


<span data-ttu-id="473c3-226">代码先创建一个视图模型实例，并在其中放入讲师列表。</span><span class="sxs-lookup"><span data-stu-id="473c3-226">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="473c3-227">该代码指定预先加载`Instructor.OfficeAssignment`和`Instructor.Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-227">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="473c3-228">第二个`Include`方法加载课程，并为每个课程加载完成了预先加载`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-228">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="473c3-229">正如前面提到，预先加载不是必需的但做是为了提高性能。</span><span class="sxs-lookup"><span data-stu-id="473c3-229">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="473c3-230">由于视图始终需要`OfficeAssignment`实体，它是更有效地在同一查询中提取的。</span><span class="sxs-lookup"><span data-stu-id="473c3-230">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="473c3-231">`Course` 实体是必需的因此预先加载是优于延迟加载，仅当与选中课程更频繁地显示的页中 web 页上，选择一名讲师时。</span><span class="sxs-lookup"><span data-stu-id="473c3-231">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="473c3-232">如果选择了讲师 ID，则从视图模型中的讲师列表检索所选的讲师。</span><span class="sxs-lookup"><span data-stu-id="473c3-232">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="473c3-233">视图模型`Courses`属性然后加载`Course`讲师实体`Courses`导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-233">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="473c3-234">`Where`方法将返回一个集合，但在这种情况下只有一个在向该方法传入条件`Instructor`所返回的实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-234">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="473c3-235">`Single`方法将集合转换为一个`Instructor`实体，这将使您可以访问该实体的`Courses`属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-235">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="473c3-236">您使用[单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)集合时知道集合上的方法将具有只有一个项。</span><span class="sxs-lookup"><span data-stu-id="473c3-236">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="473c3-237">`Single`方法将引发异常，如果传递给它的集合为空或多个项。</span><span class="sxs-lookup"><span data-stu-id="473c3-237">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="473c3-238">一种替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它返回默认值 (`null`这种情况下) 是否为空集合。</span><span class="sxs-lookup"><span data-stu-id="473c3-238">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="473c3-239">但是，在这种情况下，仍会引发异常 (尝试查找`Courses`属性上的`null`引用)，和异常消息会清楚指出问题的原因。</span><span class="sxs-lookup"><span data-stu-id="473c3-239">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="473c3-240">当您调用`Single`方法，您还可以传入`Where`条件而不是调用`Where`方法分开：</span><span class="sxs-lookup"><span data-stu-id="473c3-240">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="473c3-241">而不是：</span><span class="sxs-lookup"><span data-stu-id="473c3-241">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="473c3-242">接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="473c3-242">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="473c3-243">然后，视图模型的`Enrollments`属性加载`Enrollment`从该课程实体`Enrollments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-243">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="473c3-244">修改讲师索引视图</span><span class="sxs-lookup"><span data-stu-id="473c3-244">Modifying the Instructor Index View</span></span>

<span data-ttu-id="473c3-245">在中*Views\Instructor\Index.cshtml*，现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-245">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="473c3-246">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="473c3-246">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="473c3-247">已对现有代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="473c3-247">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="473c3-248">将模型类更改为了 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="473c3-248">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="473c3-249">将页标题从“索引”更改为了“讲师”。</span><span class="sxs-lookup"><span data-stu-id="473c3-249">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="473c3-250">向左移动行链接列。</span><span class="sxs-lookup"><span data-stu-id="473c3-250">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="473c3-251">删除**FullName**列。</span><span class="sxs-lookup"><span data-stu-id="473c3-251">Removed the **FullName** column.</span></span>
- <span data-ttu-id="473c3-252">添加**Office**显示的列`item.OfficeAssignment.Location`仅当`item.OfficeAssignment`不为 null。</span><span class="sxs-lookup"><span data-stu-id="473c3-252">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="473c3-253">(这是一对零或一一关系，因为可能不会有相关`OfficeAssignment`实体。)</span><span class="sxs-lookup"><span data-stu-id="473c3-253">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="473c3-254">添加了的代码，将动态添加`class="selectedrow"`到`tr`的所选讲师的元素。</span><span class="sxs-lookup"><span data-stu-id="473c3-254">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="473c3-255">此设置使用前面创建的 CSS 类的所选行的背景色。</span><span class="sxs-lookup"><span data-stu-id="473c3-255">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="473c3-256">(`valign`将多行的列添加到表时，将在以下教程中有用属性。)</span><span class="sxs-lookup"><span data-stu-id="473c3-256">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="473c3-257">添加了新`ActionLink`标记为**选择**之前每个行中的其他链接，这将导致所选的讲师 ID 发送到`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="473c3-257">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="473c3-258">运行应用程序，并选择**讲师**选项卡。页将显示`Location`属性的相关`OfficeAssignment`实体和一个空表单元时有无相关`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="473c3-258">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="473c3-260">在中*Views\Instructor\Index.cshtml*文件之后，结束`table`元素 （在文件末尾），添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-260">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="473c3-261">这将显示选择讲师时与讲师相关的课程列表。</span><span class="sxs-lookup"><span data-stu-id="473c3-261">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="473c3-262">此代码读取视图模型的 `Courses` 属性以显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="473c3-262">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="473c3-263">它还提供了`Select`发送到所选课程的 ID 的超链接`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="473c3-263">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="473c3-264">*.Css*由浏览器缓存文件。</span><span class="sxs-lookup"><span data-stu-id="473c3-264">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="473c3-265">如果看不到所做的更改，在运行该应用程序时，请执行硬刷新 (单击时按住 CTRL 键**刷新**按钮或按 CTRL + F5)。</span><span class="sxs-lookup"><span data-stu-id="473c3-265">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>


<span data-ttu-id="473c3-266">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="473c3-266">Run the page and select an instructor.</span></span> <span data-ttu-id="473c3-267">此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。</span><span class="sxs-lookup"><span data-stu-id="473c3-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="473c3-269">在刚刚添加的代码块后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-269">After the code block you just added, add the following code.</span></span> <span data-ttu-id="473c3-270">选择课程后，代码将显示参与课程的学生列表。</span><span class="sxs-lookup"><span data-stu-id="473c3-270">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="473c3-271">此代码读取`Enrollments`以便显示学生列表视图模型属性参加该课程。</span><span class="sxs-lookup"><span data-stu-id="473c3-271">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="473c3-272">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="473c3-272">Run the page and select an instructor.</span></span> <span data-ttu-id="473c3-273">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="473c3-273">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="473c3-275">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="473c3-275">Adding Explicit Loading</span></span>

<span data-ttu-id="473c3-276">打开*InstructorController.cs* ，并查看如何`Index`方法获取所选课程的注册列表：</span><span class="sxs-lookup"><span data-stu-id="473c3-276">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="473c3-277">当检索讲师列表时，您指定了预先加载`Courses`导航属性和`Department`属性的每个课程。</span><span class="sxs-lookup"><span data-stu-id="473c3-277">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="473c3-278">然后您将放`Courses`集合视图模型中，现在正在访问`Enrollments`从该集合中的一个实体的导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-278">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="473c3-279">因为未指定预先加载`Course.Enrollments`导航属性，作为延迟加载结果页中显示来自该属性的数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-279">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="473c3-280">如果无需更改代码以任何方式禁用延迟加载`Enrollments`属性将为 null 而不考虑该课程实际上有多少注册。</span><span class="sxs-lookup"><span data-stu-id="473c3-280">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="473c3-281">在此情况下，若要加载`Enrollments`属性，您将需要指定预先加载还是显式加载。</span><span class="sxs-lookup"><span data-stu-id="473c3-281">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="473c3-282">您所见如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="473c3-282">You've already seen how to do eager loading.</span></span> <span data-ttu-id="473c3-283">若要查看的显式加载示例，请替换`Index`方法显式加载的以下代码替换`Enrollments`属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-283">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="473c3-284">突出显示更改的代码。</span><span class="sxs-lookup"><span data-stu-id="473c3-284">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="473c3-285">获取所选后`Course`实体，新代码，显式加载该课程`Enrollments`导航属性：</span><span class="sxs-lookup"><span data-stu-id="473c3-285">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="473c3-286">然后它显式加载每个`Enrollment`实体的相关`Student`实体：</span><span class="sxs-lookup"><span data-stu-id="473c3-286">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="473c3-287">请注意，使用`Collection`方法以加载集合属性，但对于一个属性，保存只是一个实体，你使用`Reference`方法。</span><span class="sxs-lookup"><span data-stu-id="473c3-287">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="473c3-288">现在可以运行讲师索引页，尽管已经更改数据的检索方式，您将看到的页上，显示的内容没有区别。</span><span class="sxs-lookup"><span data-stu-id="473c3-288">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="473c3-289">总结</span><span class="sxs-lookup"><span data-stu-id="473c3-289">Summary</span></span>

<span data-ttu-id="473c3-290">现在，你已使用所有三种方式 （延迟、 及早计算，和显式） 将相关的数据加载到导航属性。</span><span class="sxs-lookup"><span data-stu-id="473c3-290">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="473c3-291">下一个教程将介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="473c3-291">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="473c3-292">其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="473c3-292">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="473c3-293">[上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="473c3-293">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
