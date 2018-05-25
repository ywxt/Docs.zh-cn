---
title: ASP.NET Core 中的 Razor 页面和 EF Core - 读取相关数据 - 第 6 个教程（共 8 个）
author: rick-anderson
description: 在本教程中，将读取并显示相关数据 - 即 Entity Framework 加载到导航属性中的数据。
manager: wpickett
ms.author: riande
ms.date: 11/05/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/read-related-data
ms.openlocfilehash: 1a63246dd81a16bbcca22ad2c50bc2010c852c4e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---read-related-data---6-of-8"></a><span data-ttu-id="2dce6-103">ASP.NET Core 中的 Razor 页面和 EF Core - 读取相关数据 - 第 6 个教程（共 8 个）</span><span class="sxs-lookup"><span data-stu-id="2dce6-103">Razor Pages with EF Core in ASP.NET Core - Read Related Data - 6 of 8</span></span>

<span data-ttu-id="2dce6-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Jon P Smith](https://twitter.com/thereformedprog) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2dce6-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="2dce6-105">在本教程中，将读取和显示相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-105">In this tutorial, related data is read and displayed.</span></span> <span data-ttu-id="2dce6-106">相关数据为 EF Core 加载到导航属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-106">Related data is data that EF Core loads into navigation properties.</span></span>

<span data-ttu-id="2dce6-107">如果遇到无法解决的问题，请下载[本阶段的已完成应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-107">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related).</span></span>

<span data-ttu-id="2dce6-108">下图显示了本教程中已完成的页面：</span><span class="sxs-lookup"><span data-stu-id="2dce6-108">The following illustrations show the completed pages for this tutorial:</span></span>

![“课程索引”页](read-related-data/_static/courses-index.png)

![“讲师索引”页](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a><span data-ttu-id="2dce6-111">相关数据的预先加载、显式加载和延迟加载</span><span class="sxs-lookup"><span data-stu-id="2dce6-111">Eager, explicit, and lazy Loading of related data</span></span>

<span data-ttu-id="2dce6-112">EF Core 可采用多种方式将相关数据加载到实体的导航属性中：</span><span class="sxs-lookup"><span data-stu-id="2dce6-112">There are several ways that EF Core can load related data into the navigation properties of an entity:</span></span>

* <span data-ttu-id="2dce6-113">[预先加载](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-113">[Eager loading](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading).</span></span> <span data-ttu-id="2dce6-114">预先加载是指对查询某类型的实体时一并加载相关实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-114">Eager loading is when a query for one type of entity also loads related entities.</span></span> <span data-ttu-id="2dce6-115">读取实体时，会检索其相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-115">When the entity is read, its related data is retrieved.</span></span> <span data-ttu-id="2dce6-116">此时通常会出现单一联接查询，检索所有必需数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-116">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="2dce6-117">EF Core 将针对预先加载的某些类型发出多个查询。</span><span class="sxs-lookup"><span data-stu-id="2dce6-117">EF Core will issue multiple queries for some types of eager loading.</span></span> <span data-ttu-id="2dce6-118">与存在单一查询的 EF6 中的某些查询相比，发出多个查询可能更有效。</span><span class="sxs-lookup"><span data-stu-id="2dce6-118">Issuing multiple queries can be more efficient than was the case for some queries in EF6 where there was a single query.</span></span> <span data-ttu-id="2dce6-119">预先加载通过 `Include` 和 `ThenInclude` 方法进行指定。</span><span class="sxs-lookup"><span data-stu-id="2dce6-119">Eager loading is specified with the `Include` and `ThenInclude` methods.</span></span>

  ![预先加载示例](read-related-data/_static/eager-loading.png)
 
  <span data-ttu-id="2dce6-121">当包含集合导航时，预先加载会发送多个查询：</span><span class="sxs-lookup"><span data-stu-id="2dce6-121">Eager loading sends multiple queries when a collection navigation is included:</span></span>

  * <span data-ttu-id="2dce6-122">一个查询用于主查询</span><span class="sxs-lookup"><span data-stu-id="2dce6-122">One query for the main query</span></span> 
  * <span data-ttu-id="2dce6-123">一个查询用于加载树中每个集合“边缘”。</span><span class="sxs-lookup"><span data-stu-id="2dce6-123">One query for each collection "edge" in the load tree.</span></span>

* <span data-ttu-id="2dce6-124">使用 `Load` 的单独查询：可在单独的查询中检索数据，EF Core会“修复”导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-124">Separate queries with `Load`: The data can be retrieved in separate queries, and EF Core "fixes up" the navigation properties.</span></span> <span data-ttu-id="2dce6-125">“修复”是指 EF Core 自动填充导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-125">"fixes up" means that EF Core automatically populates the navigation properties.</span></span> <span data-ttu-id="2dce6-126">与预先加载相比，使用 `Load` 的单独查询更像是显式加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-126">Separate queries with `Load` is more like explict loading than eager loading.</span></span>

  ![单独查询示例](read-related-data/_static/separate-queries.png)

  <span data-ttu-id="2dce6-128">请注意：EF Core 会将导航属性自动“修复”为之前加载到上下文实例中的任何其他实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-128">Note: EF Core automatically fixes up navigation properties to any other entities that were previously loaded into the context instance.</span></span> <span data-ttu-id="2dce6-129">即使导航属性的数据非显式包含在内，但如果先前加载了部分或所有相关实体，则仍可能填充该属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-129">Even if the data for a navigation property is *not* explicitly included, the property may still be populated if some or all of the related entities were previously loaded.</span></span>

* <span data-ttu-id="2dce6-130">[显式加载](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-130">[Explicit loading](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading).</span></span> <span data-ttu-id="2dce6-131">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-131">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="2dce6-132">必须编写代码才能在需要时检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-132">Code must be written to retrieve the related data when it's needed.</span></span> <span data-ttu-id="2dce6-133">使用单独查询进行显式加载时，会向数据库发送多个查询。</span><span class="sxs-lookup"><span data-stu-id="2dce6-133">Explicit loading with separate queries results in multiple queries sent to the DB.</span></span> <span data-ttu-id="2dce6-134">该代码通过显式加载指定要加载的导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-134">With explicit loading, the code specifies the navigation properties to be loaded.</span></span> <span data-ttu-id="2dce6-135">使用 `Load` 方法进行显式加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-135">Use the `Load` method to do explicit loading.</span></span> <span data-ttu-id="2dce6-136">例如:</span><span class="sxs-lookup"><span data-stu-id="2dce6-136">For example:</span></span>

  ![显式加载示例](read-related-data/_static/explicit-loading.png)

* <span data-ttu-id="2dce6-138">[延迟加载](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-138">[Lazy loading](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="2dce6-139">[EF Core 当前不支持延迟加载](https://github.com/aspnet/EntityFrameworkCore/issues/3797)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-139">[EF Core doesn't currently support lazy loading](https://github.com/aspnet/EntityFrameworkCore/issues/3797).</span></span> <span data-ttu-id="2dce6-140">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-140">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="2dce6-141">首次访问导航属性时，会自动检索该导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-141">The first time a navigation property is accessed, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="2dce6-142">首次访问导航属性时，都会向数据库发送一个查询。</span><span class="sxs-lookup"><span data-stu-id="2dce6-142">A query is sent to the DB each time a navigation property is accessed for the first time.</span></span>

* <span data-ttu-id="2dce6-143">`Select` 运算符仅加载所需的相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-143">The `Select` operator loads only the related data needed.</span></span>

## <a name="create-a-courses-page-that-displays-department-name"></a><span data-ttu-id="2dce6-144">创建显示院系名称的“课程”页</span><span class="sxs-lookup"><span data-stu-id="2dce6-144">Create a Courses page that displays department name</span></span>

<span data-ttu-id="2dce6-145">课程实体包括一个带 `Department` 实体的导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-145">The Course entity includes a navigation property that contains the `Department` entity.</span></span> <span data-ttu-id="2dce6-146">`Department` 实体包含要分配课程的院系。</span><span class="sxs-lookup"><span data-stu-id="2dce6-146">The `Department` entity contains the department that the course is assigned to.</span></span>

<span data-ttu-id="2dce6-147">要在课程列表中显示已分配院系的名称：</span><span class="sxs-lookup"><span data-stu-id="2dce6-147">To display the name of the assigned department in a list of courses:</span></span>

* <span data-ttu-id="2dce6-148">从 `Department` 实体中获取 `Name` 属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-148">Get the `Name` property from the `Department` entity.</span></span>
* <span data-ttu-id="2dce6-149">`Department` 实体来自于 `Course.Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-149">The `Department` entity comes from the `Course.Department` navigation property.</span></span>

![ourse.Department](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a><span data-ttu-id="2dce6-151">为课程模型创建基架</span><span class="sxs-lookup"><span data-stu-id="2dce6-151">Scaffold the Course model</span></span>

* <span data-ttu-id="2dce6-152">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2dce6-152">Exit Visual Studio.</span></span>
* <span data-ttu-id="2dce6-153">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="2dce6-153">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="2dce6-154">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="2dce6-154">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
  ```

<span data-ttu-id="2dce6-155">上述命令为 `Course` 模型创建基架。</span><span class="sxs-lookup"><span data-stu-id="2dce6-155">The preceding command scaffolds the `Course` model.</span></span> <span data-ttu-id="2dce6-156">在 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="2dce6-156">Open the project in Visual Studio.</span></span>

<span data-ttu-id="2dce6-157">生成项目。</span><span class="sxs-lookup"><span data-stu-id="2dce6-157">Build the project.</span></span> <span data-ttu-id="2dce6-158">此版本生成如下错误：</span><span class="sxs-lookup"><span data-stu-id="2dce6-158">The build generates errors like the following:</span></span>

`1>Pages/Courses/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Course' and no extension method 'Course' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 <span data-ttu-id="2dce6-159">将 `_context.Course` 全局更改为 `_context.Courses`（即向 `Course` 添加一个“s”）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-159">Globally change `_context.Course` to `_context.Courses` (that is, add an "s" to `Course`).</span></span> <span data-ttu-id="2dce6-160">找到并更新 7 个匹配项。</span><span class="sxs-lookup"><span data-stu-id="2dce6-160">7 occurrences are found and updated.</span></span>

<span data-ttu-id="2dce6-161">打开 Pages/Courses/Index.cshtml.cs 并检查 `OnGetAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="2dce6-161">Open *Pages/Courses/Index.cshtml.cs* and examine the `OnGetAsync` method.</span></span> <span data-ttu-id="2dce6-162">基架引擎为 `Department` 导航属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-162">The scaffolding engine specified eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="2dce6-163">`Include` 方法指定预先加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-163">The `Include` method specifies eager loading.</span></span>

<span data-ttu-id="2dce6-164">运行应用并选择“课程”链接。</span><span class="sxs-lookup"><span data-stu-id="2dce6-164">Run the app and select the **Courses** link.</span></span> <span data-ttu-id="2dce6-165">院系列显示 `DepartmentID`（该项无用）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-165">The department column displays the `DepartmentID`, which isn't useful.</span></span>

<span data-ttu-id="2dce6-166">使用以下代码更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="2dce6-166">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

<span data-ttu-id="2dce6-167">上述代码添加了 `AsNoTracking`。</span><span class="sxs-lookup"><span data-stu-id="2dce6-167">The preceding code adds `AsNoTracking`.</span></span> <span data-ttu-id="2dce6-168">由于未跟踪返回的实体，因此 `AsNoTracking` 提升了性能。</span><span class="sxs-lookup"><span data-stu-id="2dce6-168">`AsNoTracking` improves performance because the entities returned are not tracked.</span></span> <span data-ttu-id="2dce6-169">未跟踪实体，因为未在当前上下文中更新这些实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-169">The entities are not tracked because they're not updated in the current context.</span></span>

<span data-ttu-id="2dce6-170">使用以下突出显示的标记更新 Pages/Courses/Index.cshtml：</span><span class="sxs-lookup"><span data-stu-id="2dce6-170">Update *Pages/Courses/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

<span data-ttu-id="2dce6-171">对基架代码进行了以下更改：</span><span class="sxs-lookup"><span data-stu-id="2dce6-171">The following changes have been made to the scaffolded code:</span></span>

* <span data-ttu-id="2dce6-172">将标题从“索引”更改为“课程”。</span><span class="sxs-lookup"><span data-stu-id="2dce6-172">Changed the heading from Index to Courses.</span></span>
* <span data-ttu-id="2dce6-173">添加了显示 `CourseID` 属性值的“数字”列。</span><span class="sxs-lookup"><span data-stu-id="2dce6-173">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="2dce6-174">默认情况下，不针对主键进行架构，因为对最终用户而言，它们通常没有意义。</span><span class="sxs-lookup"><span data-stu-id="2dce6-174">By default, primary keys aren't scaffolded because normally they're meaningless to end users.</span></span> <span data-ttu-id="2dce6-175">但在此情况下主键是有意义的。</span><span class="sxs-lookup"><span data-stu-id="2dce6-175">However, in this case the primary key is meaningful.</span></span>
* <span data-ttu-id="2dce6-176">更改“院系”列，显示院系名称。</span><span class="sxs-lookup"><span data-stu-id="2dce6-176">Changed the **Department** column to display the department name.</span></span> <span data-ttu-id="2dce6-177">该代码显示已加载到 `Department` 导航属性中的 `Department` 实体的 `Name` 属性：</span><span class="sxs-lookup"><span data-stu-id="2dce6-177">The code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

<span data-ttu-id="2dce6-178">运行应用并选择“课程”选项卡，查看包含系名称的列表。</span><span class="sxs-lookup"><span data-stu-id="2dce6-178">Run the app and select the **Courses** tab to see the list with department names.</span></span>

![“课程索引”页](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a><span data-ttu-id="2dce6-180">使用 Select 加载相关数据</span><span class="sxs-lookup"><span data-stu-id="2dce6-180">Loading related data with Select</span></span>

<span data-ttu-id="2dce6-181">`OnGetAsync` 方法使用 `Include` 方法加载相关数据：</span><span class="sxs-lookup"><span data-stu-id="2dce6-181">The `OnGetAsync` method loads related data with the `Include` method:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="2dce6-182">`Select` 运算符仅加载所需的相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-182">The `Select` operator loads only the related data needed.</span></span> <span data-ttu-id="2dce6-183">对于单个项（如 `Department.Name`），它使用 SQL INNER JOIN。</span><span class="sxs-lookup"><span data-stu-id="2dce6-183">For single items, like the `Department.Name` it uses a SQL INNER JOIN.</span></span> <span data-ttu-id="2dce6-184">对于集合，它使用另一个数据库访问，但集合上的 `Include` 运算符也是如此。</span><span class="sxs-lookup"><span data-stu-id="2dce6-184">For collections, it uses another database access, but so does the `Include` operator on collections.</span></span>

<span data-ttu-id="2dce6-185">以下代码使用 `Select` 方法加载相关数据：</span><span class="sxs-lookup"><span data-stu-id="2dce6-185">The following code loads related data with the `Select` method:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="2dce6-186">`CourseViewModel`：</span><span class="sxs-lookup"><span data-stu-id="2dce6-186">The `CourseViewModel`:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

<span data-ttu-id="2dce6-187">有关完整示例的信息，请参阅 [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) 和 [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-187">See [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) and [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) for a complete example.</span></span>

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="2dce6-188">创建显示“课程”和“注册”的“讲师”页</span><span class="sxs-lookup"><span data-stu-id="2dce6-188">Create an Instructors page that shows Courses and Enrollments</span></span>

<span data-ttu-id="2dce6-189">在本部分中，将创建“讲师”页。</span><span class="sxs-lookup"><span data-stu-id="2dce6-189">In this section, the Instructors page is created.</span></span>

<a name="IP"></a>
<span data-ttu-id="2dce6-190">![“讲师索引”页](read-related-data/_static/instructors-index.png)</span><span class="sxs-lookup"><span data-stu-id="2dce6-190">![Instructors Index page](read-related-data/_static/instructors-index.png)</span></span>

<span data-ttu-id="2dce6-191">该页面通过以下方式读取和显示相关数据：</span><span class="sxs-lookup"><span data-stu-id="2dce6-191">This page reads and displays related data in the following ways:</span></span>

* <span data-ttu-id="2dce6-192">讲师列表显示 `OfficeAssignment` 实体（上图中的办公室）的相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-192">The list of instructors displays related data from the `OfficeAssignment` entity (Office in the preceding image).</span></span> <span data-ttu-id="2dce6-193">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="2dce6-193">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="2dce6-194">预先加载适用于 `OfficeAssignment` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-194">Eager loading is used for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="2dce6-195">需要显示相关数据时，预先加载通常更高效。</span><span class="sxs-lookup"><span data-stu-id="2dce6-195">Eager loading is typically more efficient when the related data needs to be displayed.</span></span> <span data-ttu-id="2dce6-196">在此情况下，会显示讲师的办公室分配。</span><span class="sxs-lookup"><span data-stu-id="2dce6-196">In this case, office assignments for the instructors are displayed.</span></span>
* <span data-ttu-id="2dce6-197">当用户选择一名讲师（上图中的 Harui）时，显示相关的 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-197">When the user selects an instructor (Harui in the preceding image), related `Course` entities are displayed.</span></span> <span data-ttu-id="2dce6-198">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="2dce6-198">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="2dce6-199">对 `Course` 实体及其相关的 `Department` 实体使用预先加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-199">Eager loading is used for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="2dce6-200">这种情况下，单独查询可能更有效，因为仅需显示所选讲师的课程。</span><span class="sxs-lookup"><span data-stu-id="2dce6-200">In this case, separate queries might be more efficient because only courses for the selected instructor are needed.</span></span> <span data-ttu-id="2dce6-201">此示例演示如何在位于导航实体内的实体中预先加载这些导航实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-201">This example shows how to use eager loading for navigation properties in entities that are in navigation properties.</span></span>
* <span data-ttu-id="2dce6-202">当用户选择一门课程（上图中的化学）时，显示 `Enrollments` 实体的相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-202">When the user selects a course (Chemistry in the preceding image), related data from the `Enrollments` entity is displayed.</span></span> <span data-ttu-id="2dce6-203">上图中显示了学生姓名和成绩。</span><span class="sxs-lookup"><span data-stu-id="2dce6-203">In the preceding image, student name and grade are displayed.</span></span> <span data-ttu-id="2dce6-204">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="2dce6-204">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="2dce6-205">创建“讲师索引”视图的视图模型</span><span class="sxs-lookup"><span data-stu-id="2dce6-205">Create a view model for the Instructor Index view</span></span>

<span data-ttu-id="2dce6-206">“讲师”页显示来自三个不同表格的数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-206">The instructors page shows data from three different tables.</span></span> <span data-ttu-id="2dce6-207">创建一个视图模型，该模型中包含表示三个表格的三个实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-207">A view model is created that includes the three entities representing the three tables.</span></span>

<span data-ttu-id="2dce6-208">在 SchoolViewModels 文件夹中，使用以下代码创建 InstructorIndexData.cs：</span><span class="sxs-lookup"><span data-stu-id="2dce6-208">In the *SchoolViewModels* folder, create *InstructorIndexData.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a><span data-ttu-id="2dce6-209">为讲师模型创建基架</span><span class="sxs-lookup"><span data-stu-id="2dce6-209">Scaffold the Instructor model</span></span>

* <span data-ttu-id="2dce6-210">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2dce6-210">Exit Visual Studio.</span></span>
* <span data-ttu-id="2dce6-211">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="2dce6-211">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="2dce6-212">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="2dce6-212">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
  ```

<span data-ttu-id="2dce6-213">上述命令为 `Instructor` 模型创建基架。</span><span class="sxs-lookup"><span data-stu-id="2dce6-213">The preceding command scaffolds the `Instructor` model.</span></span> <span data-ttu-id="2dce6-214">在 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="2dce6-214">Open the project in Visual Studio.</span></span>

<span data-ttu-id="2dce6-215">生成项目。</span><span class="sxs-lookup"><span data-stu-id="2dce6-215">Build the project.</span></span> <span data-ttu-id="2dce6-216">此版本生成错误。</span><span class="sxs-lookup"><span data-stu-id="2dce6-216">The build generates errors.</span></span>

<span data-ttu-id="2dce6-217">将 `_context.Instructor` 全局更改为 `_context.Instructors`（即向 `Instructor` 添加一个“s”）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-217">Globally change `_context.Instructor` to `_context.Instructors` (that is, add an "s" to `Instructor`).</span></span> <span data-ttu-id="2dce6-218">找到并更新 7 个匹配项。</span><span class="sxs-lookup"><span data-stu-id="2dce6-218">7 occurrences are found and updated.</span></span>

<span data-ttu-id="2dce6-219">运行应用并导航到“讲师”页。</span><span class="sxs-lookup"><span data-stu-id="2dce6-219">Run the app and navigate to the instructors page.</span></span>

<span data-ttu-id="2dce6-220">将 Pages/Instructors/Index.cshtml.cs 替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2dce6-220">Replace *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,20-99)]

<span data-ttu-id="2dce6-221">`OnGetAsync` 方法接受所选讲师 ID 的可选路由数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-221">The `OnGetAsync` method accepts optional route data for the ID of the selected instructor.</span></span>

<span data-ttu-id="2dce6-222">检查 Pages/Instructors/Index.cshtml 页上的查询：</span><span class="sxs-lookup"><span data-stu-id="2dce6-222">Examine the query on the *Pages/Instructors/Index.cshtml* page:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="2dce6-223">查询包括两项内容：</span><span class="sxs-lookup"><span data-stu-id="2dce6-223">The query has two includes:</span></span>

* <span data-ttu-id="2dce6-224">`OfficeAssignment`：在[讲师视图](#IP)中显示。</span><span class="sxs-lookup"><span data-stu-id="2dce6-224">`OfficeAssignment`: Displayed in the [instructors view](#IP).</span></span>
* <span data-ttu-id="2dce6-225">`CourseAssignments`：课程的教学内容。</span><span class="sxs-lookup"><span data-stu-id="2dce6-225">`CourseAssignments`: Which brings in the courses taught.</span></span>


### <a name="update-the-instructors-index-page"></a><span data-ttu-id="2dce6-226">更新“讲师索引”页</span><span class="sxs-lookup"><span data-stu-id="2dce6-226">Update the instructors Index page</span></span>

<span data-ttu-id="2dce6-227">使用以下标记更新 Pages/Instructors/Index.cshtml：</span><span class="sxs-lookup"><span data-stu-id="2dce6-227">Update *Pages/Instructors/Index.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

<span data-ttu-id="2dce6-228">上述标记进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="2dce6-228">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="2dce6-229">将 `page` 指令从 `@page` 更新为 `@page "{id:int?}"`。</span><span class="sxs-lookup"><span data-stu-id="2dce6-229">Updates the `page` directive from `@page` to `@page "{id:int?}"`.</span></span> <span data-ttu-id="2dce6-230">`"{id:int?}"` 是一个路由模板。</span><span class="sxs-lookup"><span data-stu-id="2dce6-230">`"{id:int?}"` is a route template.</span></span> <span data-ttu-id="2dce6-231">路由模板将 URL 中的整数查询字符串更改为路由数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-231">The route template changes integer query strings in the URL to route data.</span></span> <span data-ttu-id="2dce6-232">例如，单击仅具有 `@page` 指令的讲师的“选择”链接将生成如下 URL：</span><span class="sxs-lookup"><span data-stu-id="2dce6-232">For example, clicking on the **Select** link for an instructor with only the `@page` directive produces a URL like the following:</span></span>

    `http://localhost:1234/Instructors?id=2`

    <span data-ttu-id="2dce6-233">当页面指令是 `@page "{id:int?}"` 时，之前的 URL 为：</span><span class="sxs-lookup"><span data-stu-id="2dce6-233">When the page directive is `@page "{id:int?}"`, the previous URL is:</span></span>

    `http://localhost:1234/Instructors/2`

* <span data-ttu-id="2dce6-234">页标题为“讲师”。</span><span class="sxs-lookup"><span data-stu-id="2dce6-234">Page title is **Instructors**.</span></span>
* <span data-ttu-id="2dce6-235">添加了仅在 `item.OfficeAssignment` 不为 null 时才显示 `item.OfficeAssignment.Location` 的“办公室”列。</span><span class="sxs-lookup"><span data-stu-id="2dce6-235">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` isn't null.</span></span> <span data-ttu-id="2dce6-236">由于这是一对零或一的关系，因此可能没有相关的 OfficeAssignment 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-236">Because this is a one-to-zero-or-one relationship, there might not be a related OfficeAssignment entity.</span></span>

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* <span data-ttu-id="2dce6-237">添加了显示每位讲师所授课程的“课程”列。</span><span class="sxs-lookup"><span data-stu-id="2dce6-237">Added a **Courses** column that displays courses taught by each instructor.</span></span> <span data-ttu-id="2dce6-238">有关此 Razor 语法的详细信息，请参阅[使用 `@:` 进行显式行转换](xref:mvc/views/razor#explicit-line-transition-with-)。</span><span class="sxs-lookup"><span data-stu-id="2dce6-238">See [Explicit Line Transition with `@:`](xref:mvc/views/razor#explicit-line-transition-with-) for more about this razor syntax.</span></span>

* <span data-ttu-id="2dce6-239">添加了向所选讲师的 `tr` 元素中动态添加 `class="success"` 的代码。</span><span class="sxs-lookup"><span data-stu-id="2dce6-239">Added code that dynamically adds `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="2dce6-240">此时会使用 Bootstrap 类为所选行设置背景色。</span><span class="sxs-lookup"><span data-stu-id="2dce6-240">This sets a background color for the selected row using a Bootstrap class.</span></span>

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* <span data-ttu-id="2dce6-241">添加了标记为“选择”的新的超链接。</span><span class="sxs-lookup"><span data-stu-id="2dce6-241">Added a new hyperlink labeled **Select**.</span></span> <span data-ttu-id="2dce6-242">该链接将所选讲师的 ID 发送给 `Index` 方法并设置背景色。</span><span class="sxs-lookup"><span data-stu-id="2dce6-242">This link sends the selected instructor's ID to the `Index` method and sets a background color.</span></span>

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

<span data-ttu-id="2dce6-243">运行应用并选择“讲师”选项卡。该页显示来自相关 `OfficeAssignment` 实体的 `Location`（办公室）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-243">Run the app and select the **Instructors** tab. The page displays the `Location` (office) from the related `OfficeAssignment` entity.</span></span> <span data-ttu-id="2dce6-244">如果 OfficeAssignment\` 为 NULL，则显示空白表格单元格。</span><span class="sxs-lookup"><span data-stu-id="2dce6-244">If OfficeAssignment\` is null, an empty table cell is displayed.</span></span>

![未选择“讲师索引”页中的任何项](read-related-data/_static/instructors-index-no-selection.png)

<span data-ttu-id="2dce6-246">单击“选择”链接。</span><span class="sxs-lookup"><span data-stu-id="2dce6-246">Click on the **Select** link.</span></span> <span data-ttu-id="2dce6-247">随即更改行样式。</span><span class="sxs-lookup"><span data-stu-id="2dce6-247">The row style changes.</span></span>

### <a name="add-courses-taught-by-selected-instructor"></a><span data-ttu-id="2dce6-248">添加由所选讲师教授的课程</span><span class="sxs-lookup"><span data-stu-id="2dce6-248">Add courses taught by selected instructor</span></span>

<span data-ttu-id="2dce6-249">将 Pages/Instructors/Index.cshtml.cs 中的 `OnGetAsync` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="2dce6-249">Update the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-999)]

<span data-ttu-id="2dce6-250">添加 `public int CourseID { get; set; }`</span><span class="sxs-lookup"><span data-stu-id="2dce6-250">Add `public int CourseID { get; set; }`</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_1&highlight=12)]

<span data-ttu-id="2dce6-251">检查更新后的查询：</span><span class="sxs-lookup"><span data-stu-id="2dce6-251">Examine the updated query:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="2dce6-252">先前查询添加了 `Department` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-252">The preceding query adds the `Department` entities.</span></span>

<span data-ttu-id="2dce6-253">选择讲师时 (`id != null`)，将执行以下代码。</span><span class="sxs-lookup"><span data-stu-id="2dce6-253">The following code executes when an instructor is selected (`id != null`).</span></span> <span data-ttu-id="2dce6-254">从视图模型中的讲师列表检索所选讲师。</span><span class="sxs-lookup"><span data-stu-id="2dce6-254">The selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="2dce6-255">向视图模型的 `Courses` 属性加载来自讲师 `CourseAssignments` 导航属性的 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-255">The view model's `Courses` property is loaded with the `Course` entities from that instructor's `CourseAssignments` navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

<span data-ttu-id="2dce6-256">`Where` 方法返回一个集合。</span><span class="sxs-lookup"><span data-stu-id="2dce6-256">The `Where` method returns a collection.</span></span> <span data-ttu-id="2dce6-257">在前面的 `Where` 方法中，仅返回单个 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-257">In the preceding `Where` method, only a single `Instructor` entity is returned.</span></span> <span data-ttu-id="2dce6-258">`Single` 方法将集合转换为单个 `Instructor` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-258">The `Single` method converts the collection into a single `Instructor` entity.</span></span> <span data-ttu-id="2dce6-259">`Instructor` 实体提供对 `CourseAssignments` 属性的访问。</span><span class="sxs-lookup"><span data-stu-id="2dce6-259">The `Instructor` entity provides access to the `CourseAssignments` property.</span></span> <span data-ttu-id="2dce6-260">`CourseAssignments` 提供对相关 `Course` 实体的访问。</span><span class="sxs-lookup"><span data-stu-id="2dce6-260">`CourseAssignments` provides access to the related `Course` entities.</span></span>

![讲师-课程 m:M](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="2dce6-262">当集合仅包含一个项时，集合使用 `Single` 方法。</span><span class="sxs-lookup"><span data-stu-id="2dce6-262">The `Single` method is used on a collection when the collection has only one item.</span></span> <span data-ttu-id="2dce6-263">如果集合为空或包含多个项，`Single` 方法会引发异常。</span><span class="sxs-lookup"><span data-stu-id="2dce6-263">The `Single` method throws an exception if the collection is empty or if there's more than one item.</span></span> <span data-ttu-id="2dce6-264">还可使用 `SingleOrDefault`，该方式在集合为空时返回默认值（本例中为 null）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-264">An alternative is `SingleOrDefault`, which returns a default value (null in this case) if the collection is empty.</span></span> <span data-ttu-id="2dce6-265">在空集合上使用 `SingleOrDefault`：</span><span class="sxs-lookup"><span data-stu-id="2dce6-265">Using `SingleOrDefault` on an empty collection:</span></span>

* <span data-ttu-id="2dce6-266">引发异常（因为尝试在空引用上找到 `Courses` 属性）。</span><span class="sxs-lookup"><span data-stu-id="2dce6-266">Results in an exception (from trying to find a `Courses` property on a null reference).</span></span>
* <span data-ttu-id="2dce6-267">异常信息不太能清楚指出问题原因。</span><span class="sxs-lookup"><span data-stu-id="2dce6-267">The exception message would less clearly indicate the cause of the problem.</span></span>

<span data-ttu-id="2dce6-268">选中课程时，视图模型的 `Enrollments` 属性将填充以下代码：</span><span class="sxs-lookup"><span data-stu-id="2dce6-268">The following code populates the view model's `Enrollments` property when a course is selected:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

<span data-ttu-id="2dce6-269">在 Pages/Courses/Index.cshtml Razor 页面末尾添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="2dce6-269">Add the following markup to the end of the *Pages/Courses/Index.cshtml* Razor Page:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-999)]

<span data-ttu-id="2dce6-270">上述标记显示选中某讲师时与该讲师相关的课程列表。</span><span class="sxs-lookup"><span data-stu-id="2dce6-270">The preceding markup displays a list of courses related to an instructor when an instructor is selected.</span></span>

<span data-ttu-id="2dce6-271">测试应用。</span><span class="sxs-lookup"><span data-stu-id="2dce6-271">Test the app.</span></span> <span data-ttu-id="2dce6-272">单击讲师页面上的“选择”链接。</span><span class="sxs-lookup"><span data-stu-id="2dce6-272">Click on a **Select** link on the instructors page.</span></span>

![已选择“讲师索引”页中的讲师](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a><span data-ttu-id="2dce6-274">显示学生数据</span><span class="sxs-lookup"><span data-stu-id="2dce6-274">Show student data</span></span>

<span data-ttu-id="2dce6-275">在本部分中，更新应用以显示所选课程的学生数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-275">In this section, the app is updated to show the student data for a selected course.</span></span>

<span data-ttu-id="2dce6-276">使用以下代码在 Pages/Instructors/Index.cshtml.cs 中更新 `OnGetAsync` 方法中的查询：</span><span class="sxs-lookup"><span data-stu-id="2dce6-276">Update the query in the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="2dce6-277">更新 Pages/Instructors/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="2dce6-277">Update *Pages/Instructors/Index.cshtml*.</span></span> <span data-ttu-id="2dce6-278">在文件末尾添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="2dce6-278">Add the following markup to the end of the file:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

<span data-ttu-id="2dce6-279">上述标记显示已注册所选课程的学生列表。</span><span class="sxs-lookup"><span data-stu-id="2dce6-279">The preceding markup displays a list of the students who are enrolled in the selected course.</span></span>

<span data-ttu-id="2dce6-280">刷新页面并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="2dce6-280">Refresh the page and select an instructor.</span></span> <span data-ttu-id="2dce6-281">选择一门课程，查看已注册的学生及其成绩列表。</span><span class="sxs-lookup"><span data-stu-id="2dce6-281">Select a course to see the list of enrolled students and their grades.</span></span>

![已选择“讲师索引”页中的讲师和课程](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a><span data-ttu-id="2dce6-283">使用 Single 方法</span><span class="sxs-lookup"><span data-stu-id="2dce6-283">Using Single</span></span>

<span data-ttu-id="2dce6-284">`Single` 方法可在 `Where` 条件中进行传递，无需分别调用 `Where` 方法：</span><span class="sxs-lookup"><span data-stu-id="2dce6-284">The `Single` method can pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21,28-29)]

<span data-ttu-id="2dce6-285">使用 `Where` 时，前面的 `Single` 方法不适用。</span><span class="sxs-lookup"><span data-stu-id="2dce6-285">The preceding `Single` approach provides no benefits over using `Where`.</span></span> <span data-ttu-id="2dce6-286">一些开发人员更喜欢 `Single` 方法样式。</span><span class="sxs-lookup"><span data-stu-id="2dce6-286">Some developers prefer the `Single` approach style.</span></span>

## <a name="explicit-loading"></a><span data-ttu-id="2dce6-287">显式加载</span><span class="sxs-lookup"><span data-stu-id="2dce6-287">Explicit loading</span></span>

<span data-ttu-id="2dce6-288">当前代码为 `Enrollments` 和 `Students` 指定预先加载：</span><span class="sxs-lookup"><span data-stu-id="2dce6-288">The current code specifies eager loading for `Enrollments` and `Students`:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="2dce6-289">假设用户几乎不希望课程中显示注册情况。</span><span class="sxs-lookup"><span data-stu-id="2dce6-289">Suppose users rarely want to see enrollments in a course.</span></span> <span data-ttu-id="2dce6-290">在此情况下，可仅在请求时加载注册数据进行优化。</span><span class="sxs-lookup"><span data-stu-id="2dce6-290">In that case, an optimization would be to only load the enrollment data if it's requested.</span></span> <span data-ttu-id="2dce6-291">在本部分中，会更新 `OnGetAsync` 以使用 `Enrollments` 和 `Students` 的显式加载。</span><span class="sxs-lookup"><span data-stu-id="2dce6-291">In this section, the `OnGetAsync` is updated to use explicit loading of `Enrollments` and `Students`.</span></span>

<span data-ttu-id="2dce6-292">使用以下代码更新 `OnGetAsync`：</span><span class="sxs-lookup"><span data-stu-id="2dce6-292">Update the `OnGetAsync` with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

<span data-ttu-id="2dce6-293">上述代码取消针对注册和学生数据的 ThenInclude 方法调用。</span><span class="sxs-lookup"><span data-stu-id="2dce6-293">The preceding code drops the *ThenInclude* method calls for enrollment and student data.</span></span> <span data-ttu-id="2dce6-294">如果已选中课程，则突出显示的代码会检索：</span><span class="sxs-lookup"><span data-stu-id="2dce6-294">If a course is selected, the highlighted code retrieves:</span></span>

* <span data-ttu-id="2dce6-295">所选课程的 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-295">The `Enrollment` entities for the selected course.</span></span>
* <span data-ttu-id="2dce6-296">每个 `Enrollment` 的 `Student` 实体。</span><span class="sxs-lookup"><span data-stu-id="2dce6-296">The `Student` entities for each `Enrollment`.</span></span>

<span data-ttu-id="2dce6-297">请注意，上述代码为 `.AsNoTracking()` 加上注释。</span><span class="sxs-lookup"><span data-stu-id="2dce6-297">Notice the preceding code comments out `.AsNoTracking()`.</span></span> <span data-ttu-id="2dce6-298">对于跟踪的实体，仅可显式加载导航属性。</span><span class="sxs-lookup"><span data-stu-id="2dce6-298">Navigation properties can only be explicitly loaded for tracked entities.</span></span>

<span data-ttu-id="2dce6-299">测试应用。</span><span class="sxs-lookup"><span data-stu-id="2dce6-299">Test the app.</span></span> <span data-ttu-id="2dce6-300">对用户而言，该应用的行为与上一版本相同。</span><span class="sxs-lookup"><span data-stu-id="2dce6-300">From a users perspective, the app behaves identically to the previous version.</span></span>

<span data-ttu-id="2dce6-301">下一个教程将介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="2dce6-301">The next tutorial shows how to update related data.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="2dce6-302">[上一页](xref:data/ef-rp/complex-data-model)
>[下一页](xref:data/ef-rp/update-related-data)</span><span class="sxs-lookup"><span data-stu-id="2dce6-302">[Previous](xref:data/ef-rp/complex-data-model)
[Next](xref:data/ef-rp/update-related-data)</span></span>
