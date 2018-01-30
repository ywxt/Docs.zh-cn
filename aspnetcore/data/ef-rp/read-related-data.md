---
title: "与 EF 核心-razor 页读取相关的数据-8 6"
author: rick-anderson
description: "在本教程中你已阅读并显示相关的数据-即，实体框架将加载到导航属性的数据。"
manager: wpickett
ms.author: riande
ms.date: 11/05/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/read-related-data
ms.openlocfilehash: ccb1e95ae2b43fd0a4c4b1ac9ed58a4d474ab3b6
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="reading-related-data---ef-core-with-razor-pages-6-of-8"></a><span data-ttu-id="c93ac-103">读取与相关的数据的 EF 内核，它们有 Razor 页 (6 的 8)</span><span class="sxs-lookup"><span data-stu-id="c93ac-103">Reading related data - EF Core with Razor Pages (6 of 8)</span></span>

<span data-ttu-id="c93ac-104">通过[Tom Dykstra](https://github.com/tdykstra)， [Jon P Smith](https://twitter.com/thereformedprog)，和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c93ac-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="c93ac-105">在本教程中，是读取和显示相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-105">In this tutorial, related data is read and displayed.</span></span> <span data-ttu-id="c93ac-106">相关的数据是 EF 核心将加载到导航属性的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-106">Related data is data that EF Core loads into navigation properties.</span></span>

<span data-ttu-id="c93ac-107">如果你遇到无法解决的问题，请下载[对此阶段已完成应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-107">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related).</span></span>

<span data-ttu-id="c93ac-108">下图显示了本教程已完成的页：</span><span class="sxs-lookup"><span data-stu-id="c93ac-108">The following illustrations show the completed pages for this tutorial:</span></span>

![课程索引页](read-related-data/_static/courses-index.png)

![教师索引页](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a><span data-ttu-id="c93ac-111">Eager、 显式，和延迟加载的相关数据</span><span class="sxs-lookup"><span data-stu-id="c93ac-111">Eager, explicit, and lazy Loading of related data</span></span>

<span data-ttu-id="c93ac-112">有多种 EF 核心可以加载到实体的导航属性的相关的数据：</span><span class="sxs-lookup"><span data-stu-id="c93ac-112">There are several ways that EF Core can load related data into the navigation properties of an entity:</span></span>

* <span data-ttu-id="c93ac-113">[预先加载](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-113">[Eager loading](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading).</span></span> <span data-ttu-id="c93ac-114">预先加载是实体的一种类型的查询还加载相关的实体时。</span><span class="sxs-lookup"><span data-stu-id="c93ac-114">Eager loading is when a query for one type of entity also loads related entities.</span></span> <span data-ttu-id="c93ac-115">实体中读取时，会检索其相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-115">When the entity is read, its related data is retrieved.</span></span> <span data-ttu-id="c93ac-116">这通常会导致检索所有具有所需的数据的单一联接查询。</span><span class="sxs-lookup"><span data-stu-id="c93ac-116">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="c93ac-117">EF 核心将颁发某些类型的预先加载多个的查询。</span><span class="sxs-lookup"><span data-stu-id="c93ac-117">EF Core will issue multiple queries for some types of eager loading.</span></span> <span data-ttu-id="c93ac-118">发出多个查询可以是效率更高，比 ef6 更高版本中的某些查询这种情况其中没有单个查询。</span><span class="sxs-lookup"><span data-stu-id="c93ac-118">Issuing multiple queries can be more efficient than was the case for some queries in EF6 where there was a single query.</span></span> <span data-ttu-id="c93ac-119">使用指定预先加载`Include`和`ThenInclude`方法。</span><span class="sxs-lookup"><span data-stu-id="c93ac-119">Eager loading is specified with the `Include` and `ThenInclude` methods.</span></span>

 ![预先加载示例](read-related-data/_static/eager-loading.png)
 
 <span data-ttu-id="c93ac-121">包含集合 nvavigation 时，预先加载将发送多个查询：</span><span class="sxs-lookup"><span data-stu-id="c93ac-121">Eager loading sends multiple queries when a collection nvavigation is included:</span></span>

 * <span data-ttu-id="c93ac-122">一个查询主查询</span><span class="sxs-lookup"><span data-stu-id="c93ac-122">One query for the main query</span></span> 
 * <span data-ttu-id="c93ac-123">每个集合"边缘"负载树中的的一个查询。</span><span class="sxs-lookup"><span data-stu-id="c93ac-123">One query for each collection "edge" in the load tree.</span></span>

* <span data-ttu-id="c93ac-124">单独的查询与`Load`： 可以在单独的查询中检索数据并 EF 核心"修复"的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-124">Separate queries with `Load`: The data can be retrieved in separate queries, and EF Core "fixes up" the navigation properties.</span></span> <span data-ttu-id="c93ac-125">"向上修复"意味着 EF 核心自动填充的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-125">"fixes up" means that EF Core automatically populates the navigation properties.</span></span> <span data-ttu-id="c93ac-126">单独的查询与`Load`很像 explict 加载比预先加载。</span><span class="sxs-lookup"><span data-stu-id="c93ac-126">Separate queries with `Load` is more like explict loading than eager loading.</span></span>

 ![单独的查询示例](read-related-data/_static/separate-queries.png)

 <span data-ttu-id="c93ac-128">注意： EF 核心与以前已加载到上下文实例的任何其他实体的导航属性将自动修复。</span><span class="sxs-lookup"><span data-stu-id="c93ac-128">Note: EF Core automatically fixes up navigation properties to any other entities that were previously loaded into the context instance.</span></span> <span data-ttu-id="c93ac-129">即使一个导航属性的数据已*不*显式包含，可能仍填充属性，如果某些或所有相关实体先前已加载。</span><span class="sxs-lookup"><span data-stu-id="c93ac-129">Even if the data for a navigation property is *not* explicitly included, the property may still be populated if some or all of the related entities were previously loaded.</span></span>

* <span data-ttu-id="c93ac-130">[显式加载](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-130">[Explicit loading](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading).</span></span> <span data-ttu-id="c93ac-131">当第一次读取实体时，不检索相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-131">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="c93ac-132">必须编写代码，当需要时检索相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-132">Code must be written to retrieve the related data when it's needed.</span></span> <span data-ttu-id="c93ac-133">显式加载与单独的查询会导致发送到的数据库的多个查询。</span><span class="sxs-lookup"><span data-stu-id="c93ac-133">Explicit loading with separate queries results in multiple queries sent to the DB.</span></span> <span data-ttu-id="c93ac-134">显式加载，该代码指定要加载的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-134">With explicit loading, the code specifies the navigation properties to be loaded.</span></span> <span data-ttu-id="c93ac-135">使用`Load`方法执行显式加载。</span><span class="sxs-lookup"><span data-stu-id="c93ac-135">Use the `Load` method to do explicit loading.</span></span> <span data-ttu-id="c93ac-136">例如:</span><span class="sxs-lookup"><span data-stu-id="c93ac-136">For example:</span></span>

 ![显式加载示例](read-related-data/_static/explicit-loading.png)

* <span data-ttu-id="c93ac-138">[延迟加载](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-138">[Lazy loading](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="c93ac-139">[EF 核心当前不支持延迟加载](https://github.com/aspnet/EntityFrameworkCore/issues/3797)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-139">[EF Core doesn't currently support lazy loading](https://github.com/aspnet/EntityFrameworkCore/issues/3797).</span></span> <span data-ttu-id="c93ac-140">当第一次读取实体时，不检索相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-140">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="c93ac-141">第一次访问导航属性时，将自动检索该导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-141">The first time a navigation property is accessed, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="c93ac-142">查询发送到每个时间导航属性访问第一次数据库。</span><span class="sxs-lookup"><span data-stu-id="c93ac-142">A query is sent to the DB each time a navigation property is accessed for the first time.</span></span>

* <span data-ttu-id="c93ac-143">`Select`运算符加载仅所需的相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-143">The `Select` operator loads only the related data needed.</span></span>

## <a name="create-a-courses-page-that-displays-department-name"></a><span data-ttu-id="c93ac-144">创建显示部门名称的课程页</span><span class="sxs-lookup"><span data-stu-id="c93ac-144">Create a Courses page that displays department name</span></span>

<span data-ttu-id="c93ac-145">课程实体包括一个导航属性，包含`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-145">The Course entity includes a navigation property that contains the `Department` entity.</span></span> <span data-ttu-id="c93ac-146">`Department`实体包含过程分配给的部门。</span><span class="sxs-lookup"><span data-stu-id="c93ac-146">The `Department` entity contains the department that the course is assigned to.</span></span>

<span data-ttu-id="c93ac-147">若要在课程的列表中显示分配的部门的名称：</span><span class="sxs-lookup"><span data-stu-id="c93ac-147">To display the name of the assigned department in a list of courses:</span></span>

* <span data-ttu-id="c93ac-148">获取`Name`属性从`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-148">Get the `Name` property from the `Department` entity.</span></span>
* <span data-ttu-id="c93ac-149">`Department`实体来自于`Course.Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-149">The `Department` entity comes from the `Course.Department` navigation property.</span></span>

![ourse.Department](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a><span data-ttu-id="c93ac-151">基架过程模型</span><span class="sxs-lookup"><span data-stu-id="c93ac-151">Scaffold the Course model</span></span>

* <span data-ttu-id="c93ac-152">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c93ac-152">Exit Visual Studio.</span></span>
* <span data-ttu-id="c93ac-153">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="c93ac-153">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="c93ac-154">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="c93ac-154">Run the following command:</span></span>

 ```console
dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
 ```

<span data-ttu-id="c93ac-155">前面的命令基架`Course`模型。</span><span class="sxs-lookup"><span data-stu-id="c93ac-155">The preceding command scaffolds the `Course` model.</span></span> <span data-ttu-id="c93ac-156">在 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="c93ac-156">Open the project in Visual Studio.</span></span>

<span data-ttu-id="c93ac-157">生成项目。</span><span class="sxs-lookup"><span data-stu-id="c93ac-157">Build the project.</span></span> <span data-ttu-id="c93ac-158">生成将生成如下所示的错误：</span><span class="sxs-lookup"><span data-stu-id="c93ac-158">The build generates errors like the following:</span></span>

`1>Pages/Courses/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Course' and no extension method 'Course' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 <span data-ttu-id="c93ac-159">全局更改`_context.Course`到`_context.Courses`(即，将"s"添加到`Course`)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-159">Globally change `_context.Course` to `_context.Courses` (that is, add an "s" to `Course`).</span></span> <span data-ttu-id="c93ac-160">7 匹配项的发现和更新。</span><span class="sxs-lookup"><span data-stu-id="c93ac-160">7 occurrences are found and updated.</span></span>

<span data-ttu-id="c93ac-161">打开*Pages/Courses/Index.cshtml.cs*并检查`OnGetAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="c93ac-161">Open *Pages/Courses/Index.cshtml.cs* and examine the `OnGetAsync` method.</span></span> <span data-ttu-id="c93ac-162">基架引擎指定为预先加载`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-162">The scaffolding engine specified eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="c93ac-163">`Include`方法指定预先加载。</span><span class="sxs-lookup"><span data-stu-id="c93ac-163">The `Include` method specifies eager loading.</span></span>

<span data-ttu-id="c93ac-164">运行应用并选择**课程**链接。</span><span class="sxs-lookup"><span data-stu-id="c93ac-164">Run the app and select the **Courses** link.</span></span> <span data-ttu-id="c93ac-165">部门列显示`DepartmentID`，这并不很有用。</span><span class="sxs-lookup"><span data-stu-id="c93ac-165">The department column displays the `DepartmentID`, which isn't useful.</span></span>

<span data-ttu-id="c93ac-166">使用以下代码更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="c93ac-166">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

<span data-ttu-id="c93ac-167">前面的代码将添加`AsNoTracking`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-167">The preceding code adds `AsNoTracking`.</span></span> <span data-ttu-id="c93ac-168">`AsNoTracking`因为返回的实体不会跟踪，可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="c93ac-168">`AsNoTracking` improves performance because the entities returned are not tracked.</span></span> <span data-ttu-id="c93ac-169">因为它们不更新当前上下文中，不会跟踪实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-169">The entities are not tracked because they're not updated in the current context.</span></span>

<span data-ttu-id="c93ac-170">更新*Views/Courses/Index.cshtml*替换为以下突出显示的标记：</span><span class="sxs-lookup"><span data-stu-id="c93ac-170">Update *Views/Courses/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

<span data-ttu-id="c93ac-171">基架的代码进行了以下更改：</span><span class="sxs-lookup"><span data-stu-id="c93ac-171">The following changes have been made to the scaffolded code:</span></span>

* <span data-ttu-id="c93ac-172">从索引的标题更改为课程。</span><span class="sxs-lookup"><span data-stu-id="c93ac-172">Changed the heading from Index to Courses.</span></span>
* <span data-ttu-id="c93ac-173">添加**数**显示的列`CourseID`属性值。</span><span class="sxs-lookup"><span data-stu-id="c93ac-173">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="c93ac-174">默认情况下，主键不基架，因为它们通常是向最终用户无意义。</span><span class="sxs-lookup"><span data-stu-id="c93ac-174">By default, primary keys aren't scaffolded because normally they're meaningless to end users.</span></span> <span data-ttu-id="c93ac-175">但是，在这种情况下的主键是有意义。</span><span class="sxs-lookup"><span data-stu-id="c93ac-175">However, in this case the primary key is meaningful.</span></span>
* <span data-ttu-id="c93ac-176">更改**部门**列以显示部门名称。</span><span class="sxs-lookup"><span data-stu-id="c93ac-176">Changed the **Department** column to display the department name.</span></span> <span data-ttu-id="c93ac-177">该代码将显示`Name`属性`Department`实体加载到`Department`导航属性：</span><span class="sxs-lookup"><span data-stu-id="c93ac-177">The code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

<span data-ttu-id="c93ac-178">运行应用并选择**课程**选项卡以查看使用部门名称的列表。</span><span class="sxs-lookup"><span data-stu-id="c93ac-178">Run the app and select the **Courses** tab to see the list with department names.</span></span>

![课程索引页](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a><span data-ttu-id="c93ac-180">正在加载相关与选择的数据</span><span class="sxs-lookup"><span data-stu-id="c93ac-180">Loading related data with Select</span></span>

<span data-ttu-id="c93ac-181">`OnGetAsync`方法将加载相关的数据与`Include`方法：</span><span class="sxs-lookup"><span data-stu-id="c93ac-181">The `OnGetAsync` method loads related data with the `Include` method:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="c93ac-182">`Select`运算符加载仅所需的相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-182">The `Select` operator loads only the related data needed.</span></span> <span data-ttu-id="c93ac-183">为单个项目，如`Department.Name`它使用 SQL INNER JOIN。</span><span class="sxs-lookup"><span data-stu-id="c93ac-183">For single items, like the `Department.Name` it uses a SQL INNER JOIN.</span></span> <span data-ttu-id="c93ac-184">对于集合，它使用与另一个数据库访问，但也会更激烈。`Include`</span><span class="sxs-lookup"><span data-stu-id="c93ac-184">For collections it uses another database access, but so does the .`Include`</span></span> <span data-ttu-id="c93ac-185">集合的运算符。</span><span class="sxs-lookup"><span data-stu-id="c93ac-185">operator on collections.</span></span>

<span data-ttu-id="c93ac-186">下面的代码加载与相关的数据`Select`方法：</span><span class="sxs-lookup"><span data-stu-id="c93ac-186">The following code loads related data with the `Select` method:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="c93ac-187">`CourseViewModel`:</span><span class="sxs-lookup"><span data-stu-id="c93ac-187">The `CourseViewModel`:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

<span data-ttu-id="c93ac-188">请参阅[IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml)和[IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs)有关完整示例。</span><span class="sxs-lookup"><span data-stu-id="c93ac-188">See [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) and [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) for a complete example.</span></span>

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="c93ac-189">创建显示 Courses，并将注册一个教师页面</span><span class="sxs-lookup"><span data-stu-id="c93ac-189">Create an Instructors page that shows Courses and Enrollments</span></span>

<span data-ttu-id="c93ac-190">在此部分中，创建教师页面。</span><span class="sxs-lookup"><span data-stu-id="c93ac-190">In this section, the Instructors page is created.</span></span>

<a name="IP"></a>
<span data-ttu-id="c93ac-191">![教师索引页](read-related-data/_static/instructors-index.png)</span><span class="sxs-lookup"><span data-stu-id="c93ac-191">![Instructors Index page](read-related-data/_static/instructors-index.png)</span></span>

<span data-ttu-id="c93ac-192">此页读取，并通过以下方式显示相关的数据：</span><span class="sxs-lookup"><span data-stu-id="c93ac-192">This page reads and displays related data in the following ways:</span></span>

* <span data-ttu-id="c93ac-193">教师的列表显示来自的相关的数据`OfficeAssignment`实体 (上图中的 Office)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-193">The list of instructors displays related data from the `OfficeAssignment` entity (Office in the preceding image).</span></span> <span data-ttu-id="c93ac-194">`Instructor`和`OfficeAssignment`实体位于对零或一一个关系。</span><span class="sxs-lookup"><span data-stu-id="c93ac-194">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="c93ac-195">用于预先加载`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-195">Eager loading is used for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="c93ac-196">预先加载需要显示相关的数据时通常效率更高。</span><span class="sxs-lookup"><span data-stu-id="c93ac-196">Eager loading is typically more efficient when the related data needs to be displayed.</span></span> <span data-ttu-id="c93ac-197">在这种情况下，将显示讲师办公室分配。</span><span class="sxs-lookup"><span data-stu-id="c93ac-197">In this case, office assignments for the instructors are displayed.</span></span>
* <span data-ttu-id="c93ac-198">当用户选择教师 (上图中的 Harui) 相关`Course`显示实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-198">When the user selects an instructor (Harui in the preceding image), related `Course` entities are displayed.</span></span> <span data-ttu-id="c93ac-199">`Instructor`和`Course`实体位于多对多关系。</span><span class="sxs-lookup"><span data-stu-id="c93ac-199">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="c93ac-200">预先加载的`Course`实体和其相关`Department`使用实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-200">Eager loading for the `Course` entities and their related `Department` entities is used.</span></span> <span data-ttu-id="c93ac-201">在这种情况下，因为需要仅为所选教师的课程，单独的查询可能会更有效。</span><span class="sxs-lookup"><span data-stu-id="c93ac-201">In this case, separate queries might be more efficient because only courses for the selected instructor are needed.</span></span> <span data-ttu-id="c93ac-202">此示例演示如何使用预先加载用于导航属性中的实体中的导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-202">This example shows how to use eager loading for navigation properties in entities that are in navigation properties.</span></span>
* <span data-ttu-id="c93ac-203">当用户选择课程 （上图中的化学） 与相关的数据从`Enrollments`显示实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-203">When the user selects a course (Chemistry in the preceding image), related data from the `Enrollments` entity is displayed.</span></span> <span data-ttu-id="c93ac-204">在前面的图中，显示学生名称，并将评分。</span><span class="sxs-lookup"><span data-stu-id="c93ac-204">In the preceding image, student name and grade are displayed.</span></span> <span data-ttu-id="c93ac-205">`Course`和`Enrollment`实体位于一个对多关系。</span><span class="sxs-lookup"><span data-stu-id="c93ac-205">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="c93ac-206">创建教师索引视图的视图模型</span><span class="sxs-lookup"><span data-stu-id="c93ac-206">Create a view model for the Instructor Index view</span></span>

<span data-ttu-id="c93ac-207">教师页显示三个不同的表中的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-207">The instructors page shows data from three different tables.</span></span> <span data-ttu-id="c93ac-208">创建视图模型，包括表示三个表的三个实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-208">A view model is created that includes the three entities representing the three tables.</span></span>

<span data-ttu-id="c93ac-209">在*SchoolViewModels*文件夹中，创建*InstructorIndexData.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c93ac-209">In the *SchoolViewModels* folder, create *InstructorIndexData.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a><span data-ttu-id="c93ac-210">基架教师模型</span><span class="sxs-lookup"><span data-stu-id="c93ac-210">Scaffold the Instructor model</span></span>

* <span data-ttu-id="c93ac-211">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c93ac-211">Exit Visual Studio.</span></span>
* <span data-ttu-id="c93ac-212">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="c93ac-212">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="c93ac-213">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="c93ac-213">Run the following command:</span></span>

 ```console
dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
 ```

<span data-ttu-id="c93ac-214">前面的命令基架`Instructor`模型。</span><span class="sxs-lookup"><span data-stu-id="c93ac-214">The preceding command scaffolds the `Instructor` model.</span></span> <span data-ttu-id="c93ac-215">在 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="c93ac-215">Open the project in Visual Studio.</span></span>

<span data-ttu-id="c93ac-216">生成项目。</span><span class="sxs-lookup"><span data-stu-id="c93ac-216">Build the project.</span></span> <span data-ttu-id="c93ac-217">生成生成错误。</span><span class="sxs-lookup"><span data-stu-id="c93ac-217">The build generates errors.</span></span>

<span data-ttu-id="c93ac-218">全局更改`_context.Instructor`到`_context.Instructors`(即，将"s"添加到`Instructor`)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-218">Globally change `_context.Instructor` to `_context.Instructors` (that is, add an "s" to `Instructor`).</span></span> <span data-ttu-id="c93ac-219">7 匹配项的发现和更新。</span><span class="sxs-lookup"><span data-stu-id="c93ac-219">7 occurrences are found and updated.</span></span>

<span data-ttu-id="c93ac-220">运行应用并导航到教师页。</span><span class="sxs-lookup"><span data-stu-id="c93ac-220">Run the app and navigate to the instructors page.</span></span>

<span data-ttu-id="c93ac-221">替换*Pages/Instructors/Index.cshtml.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c93ac-221">Replace *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,20-)]

<span data-ttu-id="c93ac-222">`OnGetAsync`方法用于所选教师的 ID 将接受可选路线数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-222">The `OnGetAsync` method accepts optional route data for the ID of the selected instructor.</span></span>

<span data-ttu-id="c93ac-223">在检查查询*Pages/Instructors/Index.cshtml*页：</span><span class="sxs-lookup"><span data-stu-id="c93ac-223">Examine the query on the *Pages/Instructors/Index.cshtml* page:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="c93ac-224">查询具有两个包括：</span><span class="sxs-lookup"><span data-stu-id="c93ac-224">The query has two includes:</span></span>

* <span data-ttu-id="c93ac-225">`OfficeAssignment`： 显示在[教师视图](#IP)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-225">`OfficeAssignment`: Displayed in the [instructors view](#IP).</span></span>
* <span data-ttu-id="c93ac-226">`CourseAssignments`： 它可提供讲授的课程中。</span><span class="sxs-lookup"><span data-stu-id="c93ac-226">`CourseAssignments`: Which brings in the courses taught.</span></span>


### <a name="update-the-instructors-index-page"></a><span data-ttu-id="c93ac-227">更新教师索引页</span><span class="sxs-lookup"><span data-stu-id="c93ac-227">Update the instructors Index page</span></span>

<span data-ttu-id="c93ac-228">更新*Pages/Instructors/Index.cshtml*替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="c93ac-228">Update *Pages/Instructors/Index.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

<span data-ttu-id="c93ac-229">前面的标记进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="c93ac-229">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="c93ac-230">更新`page`指令从`@page`到`@page "{id:int?}"`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-230">Updates the `page` directive from `@page` to `@page "{id:int?}"`.</span></span> <span data-ttu-id="c93ac-231">`"{id:int?}"`是一个路由模板。</span><span class="sxs-lookup"><span data-stu-id="c93ac-231">`"{id:int?}"` is a route template.</span></span> <span data-ttu-id="c93ac-232">路由模板更改为路由数据整数在 URL 中的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="c93ac-232">The route template changes integer query strings in the URL to route data.</span></span> <span data-ttu-id="c93ac-233">例如，单击**选择**教师当页面指令产生类似于下面的 URL 的链接：</span><span class="sxs-lookup"><span data-stu-id="c93ac-233">For example, clicking on the **Select** link for an instructor when the page directive produces a URL like the following:</span></span>

    `http://localhost:1234/Instructors?id=2`

    <span data-ttu-id="c93ac-234">Page 指令时`@page "{id:int?}"`，以前的 URL 是：</span><span class="sxs-lookup"><span data-stu-id="c93ac-234">When the page directive is `@page "{id:int?}"`, the previous URL is:</span></span>

    `http://localhost:1234/Instructors/2`

* <span data-ttu-id="c93ac-235">页标题**教师**。</span><span class="sxs-lookup"><span data-stu-id="c93ac-235">Page title is **Instructors**.</span></span>
* <span data-ttu-id="c93ac-236">添加**Office**显示的列`item.OfficeAssignment.Location`才`item.OfficeAssignment`不为 null。</span><span class="sxs-lookup"><span data-stu-id="c93ac-236">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` isn't null.</span></span> <span data-ttu-id="c93ac-237">这是一个对零或一一个关系，因为不可能的相关的 OfficeAssignment 实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-237">Because this is a one-to-zero-or-one relationship, there might not be a related OfficeAssignment entity.</span></span>

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* <span data-ttu-id="c93ac-238">添加**课程**通过每个教师讲授显示课程的列。</span><span class="sxs-lookup"><span data-stu-id="c93ac-238">Added a **Courses** column that displays courses taught by each instructor.</span></span> <span data-ttu-id="c93ac-239">请参阅[显式行转换与`@:`](xref:mvc/views/razor#explicit-line-transition-with-)有关此 razor 语法的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c93ac-239">See [Explicit Line Transition with `@:`](xref:mvc/views/razor#explicit-line-transition-with-) for more about this razor syntax.</span></span>

* <span data-ttu-id="c93ac-240">添加动态添加的代码`class="success"`到`tr`的所选教师的元素。</span><span class="sxs-lookup"><span data-stu-id="c93ac-240">Added code that dynamically adds `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="c93ac-241">此设置使用 Bootstrap 类所选行的背景色。</span><span class="sxs-lookup"><span data-stu-id="c93ac-241">This sets a background color for the selected row using a Bootstrap class.</span></span>

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* <span data-ttu-id="c93ac-242">添加新的超链接标记为**选择**。</span><span class="sxs-lookup"><span data-stu-id="c93ac-242">Added a new hyperlink labeled **Select**.</span></span> <span data-ttu-id="c93ac-243">此链接将发送到所选的教师 ID`Index`方法，并设置背景色。</span><span class="sxs-lookup"><span data-stu-id="c93ac-243">This link sends the selected instructor's ID to the `Index` method and sets a background color.</span></span>

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

<span data-ttu-id="c93ac-244">运行应用并选择**教师**选项卡。该页面将显示`Location`(office) 从相关`OfficeAssignment`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-244">Run the app and select the **Instructors** tab. The page displays the `Location` (office) from the related `OfficeAssignment` entity.</span></span> <span data-ttu-id="c93ac-245">如果 OfficeAssignment' 是 null，则将显示空表单元格。</span><span class="sxs-lookup"><span data-stu-id="c93ac-245">If OfficeAssignment\` is null, an empty table cell is displayed.</span></span>

![未选择任何项教师索引页](read-related-data/_static/instructors-index-no-selection.png)

<span data-ttu-id="c93ac-247">单击**选择**链接。</span><span class="sxs-lookup"><span data-stu-id="c93ac-247">Click on the **Select** link.</span></span> <span data-ttu-id="c93ac-248">行样式更改。</span><span class="sxs-lookup"><span data-stu-id="c93ac-248">The row style changes.</span></span>

### <a name="add-courses-taught-by-selected-instructor"></a><span data-ttu-id="c93ac-249">添加由选教师讲授的课程</span><span class="sxs-lookup"><span data-stu-id="c93ac-249">Add courses taught by selected instructor</span></span>

<span data-ttu-id="c93ac-250">更新`OnGetAsync`中的方法*Pages/Instructors/Index.cshtml.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c93ac-250">Update the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-)]

<span data-ttu-id="c93ac-251">检查更新的查询：</span><span class="sxs-lookup"><span data-stu-id="c93ac-251">Examine the updated query:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="c93ac-252">前面的查询添加`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-252">The preceding query adds the `Department` entities.</span></span>

<span data-ttu-id="c93ac-253">下面的代码执行时选择一个教师 (`id != null`)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-253">The following code executes when an instructor is selected (`id != null`).</span></span> <span data-ttu-id="c93ac-254">所选的教师检索从教师视图模型中的列表中。</span><span class="sxs-lookup"><span data-stu-id="c93ac-254">The selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="c93ac-255">视图模型`Courses`属性加载与`Course`从该 instructor 实体`CourseAssignments`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-255">The view model's `Courses` property is loaded with the `Course` entities from that instructor's `CourseAssignments` navigation property.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

<span data-ttu-id="c93ac-256">`Where`方法返回的集合。</span><span class="sxs-lookup"><span data-stu-id="c93ac-256">The `Where` method returns a collection.</span></span> <span data-ttu-id="c93ac-257">在前面`Where`方法，只有一个`Instructor`返回实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-257">In the preceding `Where` method, only a single `Instructor` entity is returned.</span></span> <span data-ttu-id="c93ac-258">`Single`方法将集合转换为单个`Instructor`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-258">The `Single` method converts the collection into a single `Instructor` entity.</span></span> <span data-ttu-id="c93ac-259">`Instructor`实体提供访问`CourseAssignments`属性。</span><span class="sxs-lookup"><span data-stu-id="c93ac-259">The `Instructor` entity provides access to the `CourseAssignments` property.</span></span> <span data-ttu-id="c93ac-260">`CourseAssignments`提供对相关访问`Course`实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-260">`CourseAssignments` provides access to the related `Course` entities.</span></span>

![教师课程多对多](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="c93ac-262">`Single`在集合具有只有一个项目时，使用方法的集合。</span><span class="sxs-lookup"><span data-stu-id="c93ac-262">The `Single` method is used on a collection when the collection has only one item.</span></span> <span data-ttu-id="c93ac-263">`Single`方法引发异常，如果该集合为空或没有多个项。</span><span class="sxs-lookup"><span data-stu-id="c93ac-263">The `Single` method throws an exception if the collection is empty or if there's more than one item.</span></span> <span data-ttu-id="c93ac-264">替代方法是`SingleOrDefault`，它返回默认值 (在此情况下 null) 如果该集合为空。</span><span class="sxs-lookup"><span data-stu-id="c93ac-264">An alternative is `SingleOrDefault`, which returns a default value (null in this case) if the collection is empty.</span></span> <span data-ttu-id="c93ac-265">使用`SingleOrDefault`对空集合：</span><span class="sxs-lookup"><span data-stu-id="c93ac-265">Using `SingleOrDefault` on an empty collection:</span></span>

* <span data-ttu-id="c93ac-266">将引发异常 (从尝试查找`Courses`上的 null 引用的属性)。</span><span class="sxs-lookup"><span data-stu-id="c93ac-266">Results in an exception (from trying to find a `Courses` property on a null reference).</span></span>
* <span data-ttu-id="c93ac-267">异常消息将不太清楚地指示问题的原因。</span><span class="sxs-lookup"><span data-stu-id="c93ac-267">The exception message would less clearly indicate the cause of the problem.</span></span>

<span data-ttu-id="c93ac-268">下面的代码填充视图模型`Enrollments`属性选择某一课程时：</span><span class="sxs-lookup"><span data-stu-id="c93ac-268">The following code populates the view model's `Enrollments` property when a course is selected:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

<span data-ttu-id="c93ac-269">将以下标记添加到末尾*Pages/Courses/Index.cshtml* Razor 页：</span><span class="sxs-lookup"><span data-stu-id="c93ac-269">Add the following markup to the end of the *Pages/Courses/Index.cshtml* Razor Page:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-)]

<span data-ttu-id="c93ac-270">前面的标记显示选中一个教师与一个教师相关的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="c93ac-270">The preceding markup displays a list of courses related to an instructor when an instructor is selected.</span></span>

<span data-ttu-id="c93ac-271">测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="c93ac-271">Test the app.</span></span> <span data-ttu-id="c93ac-272">单击**选择**教师页上的链接。</span><span class="sxs-lookup"><span data-stu-id="c93ac-272">Click on a **Select** link on the instructors page.</span></span>

![选择教师索引页教师](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a><span data-ttu-id="c93ac-274">显示学生的数据</span><span class="sxs-lookup"><span data-stu-id="c93ac-274">Show student data</span></span>

<span data-ttu-id="c93ac-275">在此部分中，应用更新以显示所选过程的学生数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-275">In this section, the app is updated to show the student data for a selected course.</span></span>

<span data-ttu-id="c93ac-276">更新中的查询`OnGetAsync`中的方法*Pages/Instructors/Index.cshtml.cs*替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c93ac-276">Update the query in the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="c93ac-277">更新*Pages/Instructors/Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="c93ac-277">Update *Pages/Instructors/Index.cshtml*.</span></span> <span data-ttu-id="c93ac-278">将以下标记添加到文件末尾：</span><span class="sxs-lookup"><span data-stu-id="c93ac-278">Add the following markup to the end of the file:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

<span data-ttu-id="c93ac-279">前面的标记显示所选课程中注册的学生的列表。</span><span class="sxs-lookup"><span data-stu-id="c93ac-279">The preceding markup displays a list of the students who are enrolled in the selected course.</span></span>

<span data-ttu-id="c93ac-280">刷新页面并选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="c93ac-280">Refresh the page and select an instructor.</span></span> <span data-ttu-id="c93ac-281">选择要查看的已注册的学生和其年级列表课程。</span><span class="sxs-lookup"><span data-stu-id="c93ac-281">Select a course to see the list of enrolled students and their grades.</span></span>

![教师索引页教师和所选课程](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a><span data-ttu-id="c93ac-283">使用单个</span><span class="sxs-lookup"><span data-stu-id="c93ac-283">Using Single</span></span>

<span data-ttu-id="c93ac-284">`Single`方法可以传入`Where`条件而不是调用`Where`方法单独：</span><span class="sxs-lookup"><span data-stu-id="c93ac-284">The `Single` method can pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21,28-29)]

<span data-ttu-id="c93ac-285">前面`Single`方法通过使用未提供任何好处`Where`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-285">The preceding `Single` approach provides no benefits over using `Where`.</span></span> <span data-ttu-id="c93ac-286">一些开发人员更喜欢`Single`接近样式。</span><span class="sxs-lookup"><span data-stu-id="c93ac-286">Some developers prefer the `Single` approach style.</span></span>

## <a name="explicit-loading"></a><span data-ttu-id="c93ac-287">显式加载</span><span class="sxs-lookup"><span data-stu-id="c93ac-287">Explicit loading</span></span>

<span data-ttu-id="c93ac-288">当前的代码指定为预先加载`Enrollments`和`Students`:</span><span class="sxs-lookup"><span data-stu-id="c93ac-288">The current code specifies eager loading for `Enrollments` and `Students`:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="c93ac-289">假设用户很少会想要查看在课程中的注册。</span><span class="sxs-lookup"><span data-stu-id="c93ac-289">Suppose users rarely want to see enrollments in a course.</span></span> <span data-ttu-id="c93ac-290">在这种情况下，是一种优化仅加载注册数据，如果它请求。</span><span class="sxs-lookup"><span data-stu-id="c93ac-290">In that case, an optimization would be to only load the enrollment data if it's requested.</span></span> <span data-ttu-id="c93ac-291">在本部分中，`OnGetAsync`更新为使用显式加载`Enrollments`和`Students`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-291">In this section, the `OnGetAsync` is updated to use explicit loading of `Enrollments` and `Students`.</span></span>

<span data-ttu-id="c93ac-292">更新`OnGetAsync`替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c93ac-292">Update the `OnGetAsync` with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

<span data-ttu-id="c93ac-293">前面的代码将删除*ThenInclude*方法调用注册和学生数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-293">The preceding code drops the *ThenInclude* method calls for enrollment and student data.</span></span> <span data-ttu-id="c93ac-294">如果选择了某一课程，突出显示的代码检索：</span><span class="sxs-lookup"><span data-stu-id="c93ac-294">If a course is selected, the highlighted code retrieves:</span></span>

* <span data-ttu-id="c93ac-295">`Enrollment`所选课程的实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-295">The `Enrollment` entities for the selected course.</span></span>
* <span data-ttu-id="c93ac-296">`Student`每个实体`Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-296">The `Student` entities for each `Enrollment`.</span></span>

<span data-ttu-id="c93ac-297">请注意上述代码注释掉`.AsNoTracking()`。</span><span class="sxs-lookup"><span data-stu-id="c93ac-297">Notice the preceding code comments out `.AsNoTracking()`.</span></span> <span data-ttu-id="c93ac-298">只能为导航属性显式加载的跟踪的实体。</span><span class="sxs-lookup"><span data-stu-id="c93ac-298">Navigation properties can only be explicitly loaded for tracked entities.</span></span>

<span data-ttu-id="c93ac-299">测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="c93ac-299">Test the app.</span></span> <span data-ttu-id="c93ac-300">从用户角度看，应用程序的行为会与以前的版本相同。</span><span class="sxs-lookup"><span data-stu-id="c93ac-300">From a users perspective, the app behaves identically to the previous version.</span></span>

<span data-ttu-id="c93ac-301">下一教程演示如何更新相关的数据。</span><span class="sxs-lookup"><span data-stu-id="c93ac-301">The next tutorial shows how to update related data.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="c93ac-302">[上一页](xref:data/ef-rp/complex-data-model)
>[下一页](xref:data/ef-rp/update-related-data)</span><span class="sxs-lookup"><span data-stu-id="c93ac-302">[Previous](xref:data/ef-rp/complex-data-model)
[Next](xref:data/ef-rp/update-related-data)</span></span>
