---
title: "使用 EF Core 创建 ASP.NET Core MVC - 高级 - 第 10 个教程（共 10 个）"
author: tdykstra
description: "本教程介绍了除开发使用 Entity Framework Core 的 ASP.NET Web 应用程序的基本知识以外的几个主题，了解这些主题大有益处。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/advanced
ms.openlocfilehash: 458f2dc8a67f8c706d043f0d9d7cb7ce962e52ce
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="advanced-topics---ef-core-with-aspnet-core-mvc-tutorial-10-of-10"></a><span data-ttu-id="3d8e4-103">高级主题 - 使用 EF Core 创建 ASP.NET Core MVC 教程（第 10 个教程，共 10 个）</span><span class="sxs-lookup"><span data-stu-id="3d8e4-103">Advanced topics - EF Core with ASP.NET Core MVC tutorial (10 of 10)</span></span>

<span data-ttu-id="3d8e4-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3d8e4-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="3d8e4-105">Contoso University 示例 Web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-105">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="3d8e4-106">若要了解教程系列，请参阅[本系列中的第一个教程](intro.md)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-106">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="3d8e4-107">之前的教程中已经实现了每个层次结构一个表继承。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-107">In the previous tutorial, you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="3d8e4-108">本教程介绍了除开发使用 Entity Framework Core 的 ASP.NET Core Web 应用程序的基本知识以外的几个主题，了解这些主题大有益处。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-108">This tutorial introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET Core web applications that use Entity Framework Core.</span></span>

## <a name="raw-sql-queries"></a><span data-ttu-id="3d8e4-109">原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="3d8e4-109">Raw SQL Queries</span></span>

<span data-ttu-id="3d8e4-110">使用 Entity Framework 的优点之一是，它可以避免将代码与存储数据的特定方法过于紧密地绑定在一起。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-110">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="3d8e4-111">它通过生成 SQL 查询和命令来实现这一点，这样也可让你免于亲自编写这些内容。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-111">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="3d8e4-112">但需要运行手动创建的特定 SQL 查询时会出现异常情况。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-112">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created.</span></span> <span data-ttu-id="3d8e4-113">对于这些情况，Entity Framework Code First API 包含了可用于将 SQL 命令直接传递到数据库的方法。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-113">For these scenarios, the Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="3d8e4-114">EF Core 1.0 中提供以下选项：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-114">You have the following options in EF Core 1.0:</span></span>

* <span data-ttu-id="3d8e4-115">对返回实体类型的查询使用 `DbSet.FromSql` 方法。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-115">Use the `DbSet.FromSql` method for queries that return entity types.</span></span> <span data-ttu-id="3d8e4-116">返回对象的类型必须是 `DbSet` 对象期望的类型，并且数据库上下文会自动跟踪返回对象，除非[关闭跟踪](crud.md#no-tracking-queries)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-116">The returned objects must be of the type expected by the `DbSet` object, and they're automatically tracked by the database context unless you [turn tracking off](crud.md#no-tracking-queries).</span></span>

* <span data-ttu-id="3d8e4-117">对非查询命令使用 `Database.ExecuteSqlCommand`。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-117">Use the `Database.ExecuteSqlCommand` for non-query commands.</span></span>

<span data-ttu-id="3d8e4-118">如果需要运行返回非实体类型的查询，可将 ADO.NET 与 EF 提供的数据库连接一起使用。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-118">If you need to run a query that returns types that aren't entities, you can use ADO.NET with the database connection provided by EF.</span></span> <span data-ttu-id="3d8e4-119">即便使用此方法来检索实体类型，数据库上下文也不会跟踪返回的数据。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-119">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>

<span data-ttu-id="3d8e4-120">在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-120">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="3d8e4-121">一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-121">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="3d8e4-122">在本教程中，将用户输入集成到查询中时会使用参数化查询。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-122">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

## <a name="call-a-query-that-returns-entities"></a><span data-ttu-id="3d8e4-123">调用返回实体的查询</span><span class="sxs-lookup"><span data-stu-id="3d8e4-123">Call a query that returns entities</span></span>

<span data-ttu-id="3d8e4-124">`DbSet<TEntity>` 类提供了一种方法，可用于执行返回 `TEntity` 类型的实体的查询。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-124">The `DbSet<TEntity>` class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="3d8e4-125">若想查看其作用方式，需更改“院系”控制器的 `Details` 方法中的代码。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-125">To see how this works you'll change the code in the `Details` method of the Department controller.</span></span>

<span data-ttu-id="3d8e4-126">在 DepartmentsController.cs 的 `Details` 方法中，将检索院系的代码替换为 `FromSql` 方法调用，如以下突出显示状态的代码所示：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-126">In *DepartmentsController.cs*, in the `Details` method, replace the code that retrieves a department with a `FromSql` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/DepartmentsController.cs?name=snippet_RawSQL&highlight=8,9,10,13)]

<span data-ttu-id="3d8e4-127">如需验证新代码是否正常工作，请选择“院系”选项卡，然后选择某一院系的“详细信息”。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-127">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![院系详细信息](advanced/_static/department-details.png)

## <a name="call-a-query-that-returns-other-types"></a><span data-ttu-id="3d8e4-129">调用返回其他类型的查询</span><span class="sxs-lookup"><span data-stu-id="3d8e4-129">Call a query that returns other types</span></span>

<span data-ttu-id="3d8e4-130">“关于”页面中显示了每个注册日期的学生数量，之前已为该页面创建了一个学生统计数据网格。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-130">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="3d8e4-131">从 Students 实体集 (`_context.Students`) 获取数据，并使用 LINQ 将该结果投影到 `EnrollmentDateGroup` 视图模型对象的列表中。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-131">You got the data from the Students entity set (`_context.Students`) and used LINQ to project the results into a list of `EnrollmentDateGroup` view model objects.</span></span> <span data-ttu-id="3d8e4-132">假设你想编写 SQL 本身，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-132">Suppose you want to write the SQL itself rather than using LINQ.</span></span> <span data-ttu-id="3d8e4-133">为此，需运行返回非实体对象的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-133">To do that you need to run a SQL query that returns something other than entity objects.</span></span> <span data-ttu-id="3d8e4-134">在 EF Core 1.0 中，实现此操作的一种方法是编写 ADO.NET 代码并从 EF 获取数据库连接。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-134">In EF Core 1.0, one way to do that is write ADO.NET code and get the database connection from EF.</span></span>

<span data-ttu-id="3d8e4-135">在 HomeController.cs 中，将 `About` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-135">In *HomeController.cs*, replace the `About` method with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_UseRawSQL&highlight=3-32)]

<span data-ttu-id="3d8e4-136">添加 using 语句：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-136">Add a using statement:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/HomeController.cs?name=snippet_Usings2)]

<span data-ttu-id="3d8e4-137">运行应用并转到“关于”页。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-137">Run the app and go to the About page.</span></span> <span data-ttu-id="3d8e4-138">页面中显示的数据与之前相同。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-138">It displays the same data it did before.</span></span>

![“关于”页面](advanced/_static/about.png)

## <a name="call-an-update-query"></a><span data-ttu-id="3d8e4-140">调用更新查询</span><span class="sxs-lookup"><span data-stu-id="3d8e4-140">Call an update query</span></span>

<span data-ttu-id="3d8e4-141">假设 Contoso University 管理员想要在数据库中执行全局更改，例如更改每门课程的学分数。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-141">Suppose Contoso University administrators want to perform global changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="3d8e4-142">如果该大学拥有大量课程，将课程全部当作实体进行检索并逐一更改效率很低。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-142">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="3d8e4-143">本部分中将实现一个可让用户指定因素（用于更改所有课程的学分数）的网页，并通过执行 SQL UPDATE 语句进行更改。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-143">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL UPDATE statement.</span></span> <span data-ttu-id="3d8e4-144">该网页如下图所示：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-144">The web page will look like the following illustration:</span></span>

![“更新课程学分”页面](advanced/_static/update-credits.png)

<span data-ttu-id="3d8e4-146">在 CoursesContoller.cs 中，为 HttpGet 和 HttpPost 添加 UpdateCourseCredits 方法：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-146">In *CoursesContoller.cs*, add UpdateCourseCredits methods for HttpGet and HttpPost:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdateGet)]

[!code-csharp[Main](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_UpdatePost)]

<span data-ttu-id="3d8e4-147">控制器处理 HttpGet 请求时，`ViewData["RowsAffected"]` 中不会返回任何内容，并且视图中会显示一个空文本框和一个提交按钮，如上图所示。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-147">When the controller processes an HttpGet request, nothing is returned in `ViewData["RowsAffected"]`, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="3d8e4-148">单击“更新”按钮后，系统会调用 HttpPost 方法，并为乘数赋予在文本框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-148">When the **Update** button is clicked, the HttpPost method is called, and multiplier has the value entered in the text box.</span></span> <span data-ttu-id="3d8e4-149">然后，代码执行更新课程的 SQL，并将受影响的行数返回给 `ViewData` 中的视图。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-149">The code then executes the SQL that updates courses and returns the number of affected rows to the view in `ViewData`.</span></span> <span data-ttu-id="3d8e4-150">视图获得 `RowsAffected` 值时，即显示更新后的行数。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-150">When the view gets a `RowsAffected` value, it displays the number of rows updated.</span></span>

<span data-ttu-id="3d8e4-151">在“解决方案资源管理器”中，右键单击“Views/Courses”文件夹，然后依次单击“添加”和“新建项”。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-151">In **Solution Explorer**, right-click the *Views/Courses* folder, and then click **Add > New Item**.</span></span>

<span data-ttu-id="3d8e4-152">在“添加新项”对话框中，单击左窗格中“已安装”下的“ASP.NET”，单击“MVC 视图页面”并将新视图命名为“UpdateCourseCredits.cshtml”。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-152">In the **Add New Item** dialog, click **ASP.NET** under **Installed** in the left pane, click **MVC View Page**, and name the new view *UpdateCourseCredits.cshtml*.</span></span>

<span data-ttu-id="3d8e4-153">在 Views/Courses/UpdateCourseCredits.cshtml 中，将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-153">In *Views/Courses/UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-html[Main](intro/samples/cu/Views/Courses/UpdateCourseCredits.cshtml)]

<span data-ttu-id="3d8e4-154">通过选择“课程”选项卡运行 `UpdateCourseCredits` 方法，然后将“/UpdateCourseCredits”添加到浏览器地址栏中 URL 的末尾（例如 `http://localhost:5813/Courses/UpdateCourseCredits`）。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-154">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:5813/Courses/UpdateCourseCredits`).</span></span> <span data-ttu-id="3d8e4-155">在文本框中输入数字：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-155">Enter a number in the text box:</span></span>

![“更新课程学分”页面](advanced/_static/update-credits.png)

<span data-ttu-id="3d8e4-157">单击“更新” 。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-157">Click **Update**.</span></span> <span data-ttu-id="3d8e4-158">随即显示受影响的行数：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-158">You see the number of rows affected:</span></span>

![“更新课程学分”页面中受影响的行](advanced/_static/update-credits-rows-affected.png)

<span data-ttu-id="3d8e4-160">单击“返回列表”，查看具有修订后的学分数的课程列表。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-160">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="3d8e4-161">请注意，生产代码可确保更新操作始终能生成有效数据。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-161">Note that production code would ensure that updates always result in valid data.</span></span> <span data-ttu-id="3d8e4-162">此处显示的简化代码可将学分数放大到足够大，以生成 5 以上的数字。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-162">The simplified code shown here could multiply the number of credits enough to result in numbers greater than 5.</span></span> <span data-ttu-id="3d8e4-163">（`Credits` 属性具有 `[Range(0, 5)]` 特性。）更新查询可以工作，但无效数据可能会导致系统中假设学分数小于或等于 5 的其他部分出现异常结果。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-163">(The `Credits` property has a `[Range(0, 5)]` attribute.) The update query would work but the invalid data could cause unexpected results in other parts of the system that assume the number of credits is 5 or less.</span></span>

<span data-ttu-id="3d8e4-164">有关原始 SQL 查询的详细信息，请参阅[原始 SQL 查询](https://docs.microsoft.com/ef/core/querying/raw-sql)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-164">For more information about raw SQL queries, see [Raw SQL Queries](https://docs.microsoft.com/ef/core/querying/raw-sql).</span></span>

## <a name="examine-sql-sent-to-the-database"></a><span data-ttu-id="3d8e4-165">检查发送到数据库的 SQL</span><span class="sxs-lookup"><span data-stu-id="3d8e4-165">Examine SQL sent to the database</span></span>

<span data-ttu-id="3d8e4-166">有时，能够查看发送到数据库的实际 SQL 查询会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-166">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="3d8e4-167">EF Core 会自动使用 ASP.NET Core 内置的日志记录功能来编写包含用于查询和更新的 SQL 的日志。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-167">Built-in logging functionality for ASP.NET Core is automatically used by EF Core to write logs that contain the SQL for queries and updates.</span></span> <span data-ttu-id="3d8e4-168">本部分中将介绍 SQL 日志记录的一些示例。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-168">In this section you'll see some examples of SQL logging.</span></span>

<span data-ttu-id="3d8e4-169">打开 StudentsController.cs，并在 `Details` 方法的 `if (student == null)` 语句上设置断点。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-169">Open *StudentsController.cs* and in the `Details` method set a breakpoint on the `if (student == null)` statement.</span></span>

<span data-ttu-id="3d8e4-170">在调试模式下运行应用，并转到某位学生的“详细信息”页面。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-170">Run the app in debug mode, and go to the Details page for a student.</span></span>

<span data-ttu-id="3d8e4-171">转到显示调试输出的“输出”窗口，可看到以下查询：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-171">Go to the **Output** window showing debug output, and you see the query:</span></span>

```
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (56ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT TOP(2) [s].[ID], [s].[Discriminator], [s].[FirstName], [s].[LastName], [s].[EnrollmentDate]
FROM [Person] AS [s]
WHERE ([s].[Discriminator] = N'Student') AND ([s].[ID] = @__id_0)
ORDER BY [s].[ID]
Microsoft.EntityFrameworkCore.Database.Command:Information: Executed DbCommand (122ms) [Parameters=[@__id_0='?'], CommandType='Text', CommandTimeout='30']
SELECT [s.Enrollments].[EnrollmentID], [s.Enrollments].[CourseID], [s.Enrollments].[Grade], [s.Enrollments].[StudentID], [e.Course].[CourseID], [e.Course].[Credits], [e.Course].[DepartmentID], [e.Course].[Title]
FROM [Enrollment] AS [s.Enrollments]
INNER JOIN [Course] AS [e.Course] ON [s.Enrollments].[CourseID] = [e.Course].[CourseID]
INNER JOIN (
    SELECT TOP(1) [s0].[ID]
    FROM [Person] AS [s0]
    WHERE ([s0].[Discriminator] = N'Student') AND ([s0].[ID] = @__id_0)
    ORDER BY [s0].[ID]
) AS [t] ON [s.Enrollments].[StudentID] = [t].[ID]
ORDER BY [t].[ID]
```

<span data-ttu-id="3d8e4-172">可看到这里可能有意外内容：SQL 从 Person 表中选择的行数多达两行（`TOP(2)`。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-172">You'll notice something here that might surprise you: the SQL selects up to 2 rows (`TOP(2)`) from the Person table.</span></span> <span data-ttu-id="3d8e4-173">`SingleOrDefaultAsync` 方法未解析为服务器上的一行。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-173">The `SingleOrDefaultAsync` method doesn't resolve to 1 row on the server.</span></span> <span data-ttu-id="3d8e4-174">原因如下：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-174">Here's why:</span></span>

* <span data-ttu-id="3d8e4-175">如果查询返回多行，则该方法返回 NULL。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-175">If the query would return multiple rows, the method returns null.</span></span>
* <span data-ttu-id="3d8e4-176">若要确定查询是否返回多行，EF 必须检查它是否至少返回两行。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-176">To determine whether the query would return multiple rows, EF has to check if it returns at least 2.</span></span>

<span data-ttu-id="3d8e4-177">请注意，无需使用调试模式，只需在断点处停止即可获取“输出”窗口中的日志记录输出。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-177">Note that you don't have to use debug mode and stop at a breakpoint to get logging output in the **Output** window.</span></span> <span data-ttu-id="3d8e4-178">这种方法非常便捷，只需在想查看输出时停止日志记录即可。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-178">It's just a convenient way to stop the logging at the point you want to look at the output.</span></span> <span data-ttu-id="3d8e4-179">如果不进行此操作，程序将继续进行日志记录，要查看感兴趣的部分则必须向后滚动。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-179">If you don't do that, logging continues and you have to scroll back to find the parts you're interested in.</span></span>

## <a name="repository-and-unit-of-work-patterns"></a><span data-ttu-id="3d8e4-180">存储库和和工作单元模式</span><span class="sxs-lookup"><span data-stu-id="3d8e4-180">Repository and unit of work patterns</span></span>

<span data-ttu-id="3d8e4-181">许多开发人员通过编写代码将存储库和工作单元模式实现为代码周围的包装器，与 Entity Framework 一起使用。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-181">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="3d8e4-182">这些模式被用于在应用程序的数据访问层和业务逻辑层之间创建一个抽象层。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-182">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="3d8e4-183">实现这些模式有助于使应用程序免受数据存储中所作更改的影响，而且有助于进行自动单元测试或测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-183">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="3d8e4-184">但是对使用 EF 的应用程序而言，通过编写附加代码来实现这些模式并不总是最佳选择，原因如下：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-184">However, writing additional code to implement these patterns isn't always the best choice for applications that use EF, for several reasons:</span></span>

* <span data-ttu-id="3d8e4-185">EF 上下文类本身会将代码与数据存储特定的代码隔离开来。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-185">The EF context class itself insulates your code from data-store-specific code.</span></span>

* <span data-ttu-id="3d8e4-186">对于使用 EF 进行的数据库更新，EF 上下文类可充当工作单元类。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-186">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>

* <span data-ttu-id="3d8e4-187">EF 包含了一些无需编写存储库代码即可实现 TDD 的功能。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-187">EF includes features for implementing TDD without writing repository code.</span></span>

<span data-ttu-id="3d8e4-188">若要了解如何实现存储库和工作单元模式，请参阅[本系列教程的 Entity Framework 5 版本](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-188">For information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application).</span></span>

<span data-ttu-id="3d8e4-189">Entity Framework Core 实现可用于测试的内存中数据库提供程序。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-189">Entity Framework Core implements an in-memory database provider that can be used for testing.</span></span> <span data-ttu-id="3d8e4-190">有关详细信息，请参阅[使用 InMemory 进行测试](https://docs.microsoft.com/ef/core/miscellaneous/testing/in-memory)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-190">For more information, see [Testing with InMemory](https://docs.microsoft.com/ef/core/miscellaneous/testing/in-memory).</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="3d8e4-191">自动更改检测</span><span class="sxs-lookup"><span data-stu-id="3d8e4-191">Automatic change detection</span></span>

<span data-ttu-id="3d8e4-192">Entity Framework 通过比较实体的当前值与原始值来确定实体发生的更改，从而确定需将哪些更改发送给数据库。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-192">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="3d8e4-193">查询或附加实体时，将存储原始值。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-193">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="3d8e4-194">导致自动更改检测的部分方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-194">Some of the methods that cause automatic change detection are the following:</span></span>

* <span data-ttu-id="3d8e4-195">DbContext.SaveChanges</span><span class="sxs-lookup"><span data-stu-id="3d8e4-195">DbContext.SaveChanges</span></span>

* <span data-ttu-id="3d8e4-196">DbContext.Entry</span><span class="sxs-lookup"><span data-stu-id="3d8e4-196">DbContext.Entry</span></span>

* <span data-ttu-id="3d8e4-197">ChangeTracker.Entries</span><span class="sxs-lookup"><span data-stu-id="3d8e4-197">ChangeTracker.Entries</span></span>

<span data-ttu-id="3d8e4-198">如果跟踪的实体数量巨大，且在循环中多次调用其中某种方法，则使用 `ChangeTracker.AutoDetectChangesEnabled` 属性临时关闭自动更改检测即可显著改善性能。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-198">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the `ChangeTracker.AutoDetectChangesEnabled` property.</span></span> <span data-ttu-id="3d8e4-199">例如：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-199">For example:</span></span>

```csharp
_context.ChangeTracker.AutoDetectChangesEnabled = false;
```

## <a name="entity-framework-core-source-code-and-development-plans"></a><span data-ttu-id="3d8e4-200">Entity Framework Core 源代码和开发计划</span><span class="sxs-lookup"><span data-stu-id="3d8e4-200">Entity Framework Core source code and development plans</span></span>

<span data-ttu-id="3d8e4-201">Entity Framework Core 源代码位于 [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-201">The Entity Framework Core source is at [https://github.com/aspnet/EntityFrameworkCore](https://github.com/aspnet/EntityFrameworkCore).</span></span> <span data-ttu-id="3d8e4-202">EF Core 储存库中包含夜间生成、问题跟踪、功能规范、设计会议备注和[后续开发的路线图](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-202">The EF Core repository contains nightly builds, issue tracking, feature specs, design meeting notes, and [the roadmap for future development](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap).</span></span> <span data-ttu-id="3d8e4-203">你可以归档或查找 bug 并进行更改。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-203">You can file or find bugs, and contribute.</span></span>

<span data-ttu-id="3d8e4-204">尽管源代码开源，但是 Entity Framework Core 也被视为 Microsoft 产品受到完全支持。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-204">Although the source code is open, Entity Framework Core is fully supported as a Microsoft product.</span></span> <span data-ttu-id="3d8e4-205">Microsoft Entity Framework 团队持续控制要接受的更改，并对所有代码更改进行测试来确保每个版本的质量。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-205">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="reverse-engineer-from-existing-database"></a><span data-ttu-id="3d8e4-206">从现有数据库进行反向工程</span><span class="sxs-lookup"><span data-stu-id="3d8e4-206">Reverse engineer from existing database</span></span>

<span data-ttu-id="3d8e4-207">若要从现有数据库对数据模型（如实体类）进行反向工程，请使用 [scaffold-dbcontext](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) 命令。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-207">To reverse engineer a data model including entity classes from an existing database, use the [scaffold-dbcontext](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell#scaffold-dbcontext) command.</span></span> <span data-ttu-id="3d8e4-208">请参阅[入门教程](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-208">See the [getting-started tutorial](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span></span>

<a id="dynamic-linq"></a>
## <a name="use-dynamic-linq-to-simplify-sort-selection-code"></a><span data-ttu-id="3d8e4-209">使用动态 LINQ 简化排序选择代码</span><span class="sxs-lookup"><span data-stu-id="3d8e4-209">Use dynamic LINQ to simplify sort selection code</span></span>

<span data-ttu-id="3d8e4-210">[本系列中的第三个教程](sort-filter-page.md)介绍了如何按照 `switch` 语句中的硬编码列名称编写 LINQ 代码。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-210">The [third tutorial in this series](sort-filter-page.md) shows how to write LINQ code by hard-coding column names in a `switch` statement.</span></span> <span data-ttu-id="3d8e4-211">如果只有两列可供选择，这种方法可行，但是如果拥有许多列，代码可能会变得冗长。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-211">With two columns to choose from, this works fine, but if you have many columns the code could get verbose.</span></span> <span data-ttu-id="3d8e4-212">要解决该问题，可使用 `EF.Property` 方法将属性名称指定为一个字符串。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-212">To solve that problem, you can use the `EF.Property` method to specify the name of the property as a string.</span></span> <span data-ttu-id="3d8e4-213">要尝试此方法，请将 `StudentsController` 中的 `Index` 方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-213">To try out this approach, replace the `Index` method in the `StudentsController` with the following code.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_DynamicLinq)]

## <a name="next-steps"></a><span data-ttu-id="3d8e4-214">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3d8e4-214">Next steps</span></span>

<span data-ttu-id="3d8e4-215">至此，在 ASP.NET MVC 应用程序中使用 Entity Framework Core 的系列教程已告一段落。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-215">This completes this series of tutorials on using the Entity Framework Core in an ASP.NET MVC application.</span></span>

<span data-ttu-id="3d8e4-216">有关 EF Core 的详细信息，请参阅 [Entity Framework Core 文档](https://docs.microsoft.com/ef/core)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-216">For more information about EF Core, see the [Entity Framework Core documentation](https://docs.microsoft.com/ef/core).</span></span> <span data-ttu-id="3d8e4-217">另外也可参阅 [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action)（实际运用 Entity Framework Core）一书。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-217">A book is also available: [Entity Framework Core in Action](https://www.manning.com/books/entity-framework-core-in-action).</span></span>

<span data-ttu-id="3d8e4-218">若要了解如何部署 Web 应用，请参阅[托管和部署](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-218">For information on how to deploy a web app, see [Host and deploy](xref:host-and-deploy/index).</span></span>

<span data-ttu-id="3d8e4-219">有关 ASP.NET Core MVC 涉及的其他主题，例如身份验证和授权，请参阅 [ASP.NET Core 文档](https://docs.microsoft.com/aspnet/core/)。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-219">For information about other topics related to ASP.NET Core MVC, such as authentication and authorization, see the [ASP.NET Core documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="3d8e4-220">致谢</span><span class="sxs-lookup"><span data-stu-id="3d8e4-220">Acknowledgments</span></span>

<span data-ttu-id="3d8e4-221">感谢 Tom Dykstra 和 Rick Anderson（twitter @RickAndMSFT）编写本教程。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-221">Tom Dykstra and Rick Anderson (twitter @RickAndMSFT) wrote this tutorial.</span></span> <span data-ttu-id="3d8e4-222">感谢 Rowan Miller、Diego Vega 和 Entity Framework 小组的其他成员帮助进行代码评审，并帮助调试在编写本教程代码时出现的问题。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-222">Rowan Miller, Diego Vega, and other members of the Entity Framework team assisted with code reviews and helped debug issues that arose while we were writing code for the tutorials.</span></span>

## <a name="common-errors"></a><span data-ttu-id="3d8e4-223">常见错误</span><span class="sxs-lookup"><span data-stu-id="3d8e4-223">Common errors</span></span>  

### <a name="contosouniversitydll-used-by-another-process"></a><span data-ttu-id="3d8e4-224">其他进程在使用 ContosoUniversity.dll</span><span class="sxs-lookup"><span data-stu-id="3d8e4-224">ContosoUniversity.dll used by another process</span></span>

<span data-ttu-id="3d8e4-225">错误消息：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-225">Error message:</span></span>

> <span data-ttu-id="3d8e4-226">无法打开“...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' for writing -- ”进程无法访问文件“...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll”，因为它正在由其他进程使用。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-226">Cannot open '...bin\Debug\netcoreapp1.0\ContosoUniversity.dll' for writing -- 'The process cannot access the file '...\bin\Debug\netcoreapp1.0\ContosoUniversity.dll' because it is being used by another process.</span></span>

<span data-ttu-id="3d8e4-227">解决方案：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-227">Solution:</span></span>

<span data-ttu-id="3d8e4-228">在 IIS Express 中停止站点。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-228">Stop the site in IIS Express.</span></span> <span data-ttu-id="3d8e4-229">转到 Windows 系统任务栏，找到 IIS Express 并右键单击其图表，选择 Contoso University 网站，然后单击“停止站点”。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-229">Go to the Windows System Tray, find IIS Express and right-click its icon, select the Contoso University site, and then click **Stop Site**.</span></span>

### <a name="migration-scaffolded-with-no-code-in-up-and-down-methods"></a><span data-ttu-id="3d8e4-230">Up 和 Down 方法中存在没有代码搭建基架的迁移</span><span class="sxs-lookup"><span data-stu-id="3d8e4-230">Migration scaffolded with no code in Up and Down methods</span></span>

<span data-ttu-id="3d8e4-231">可能的原因：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-231">Possible cause:</span></span>

<span data-ttu-id="3d8e4-232">EF CLI 命令不自动关闭和保存代码文件。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-232">The EF CLI commands don't automatically close and save code files.</span></span> <span data-ttu-id="3d8e4-233">如果在运行 `migrations add` 命令时有尚未保存的代码，EF 将找不到该更改。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-233">If you have unsaved changes when you run the `migrations add` command, EF won't find your changes.</span></span>

<span data-ttu-id="3d8e4-234">解决方案：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-234">Solution:</span></span>

<span data-ttu-id="3d8e4-235">运行 `migrations remove` 命令，保存代码更改，然后重新运行 `migrations add` 命令。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-235">Run the `migrations remove` command, save your code changes and rerun the `migrations add` command.</span></span>

### <a name="errors-while-running-database-update"></a><span data-ttu-id="3d8e4-236">运行数据库更新时出错</span><span class="sxs-lookup"><span data-stu-id="3d8e4-236">Errors while running database update</span></span>

<span data-ttu-id="3d8e4-237">在包含现有数据的数据库中更改架构时，可能会发生其他错误。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-237">It's possible to get other errors when making schema changes in a database that has existing data.</span></span> <span data-ttu-id="3d8e4-238">如果出现无法解决的迁移错误，可以在连接字符串中更改数据库名或者删除数据库。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-238">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="3d8e4-239">如果是新数据库，则没有要迁移的数据，因此在完成更新数据库命令时很可能不会出错。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-239">With a new database, there's no data to migrate, and the update-database command is much more likely to complete without errors.</span></span>

<span data-ttu-id="3d8e4-240">最简单的方法是重命名 appsettings.json 中的数据库。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-240">The simplest approach is to rename the database in *appsettings.json*.</span></span> <span data-ttu-id="3d8e4-241">下次运行 `database update` 时将创建一个新的数据库。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-241">The next time you run `database update`, a new database will be created.</span></span>

<span data-ttu-id="3d8e4-242">若要在 SSOX 中删除数据库，请右键单击该数据库，单击“删除”，然后在“删除数据库”对话框中选择“关闭现有连接”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-242">To delete a database in SSOX, right-click the database, click **Delete**, and then in the **Delete Database** dialog box select **Close existing connections** and click **OK**.</span></span>

<span data-ttu-id="3d8e4-243">若要使用 CLI 删除数据库，请运行 `database drop` CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-243">To delete a database by using the CLI, run the `database drop` CLI command:</span></span>

```console
dotnet ef database drop
```

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="3d8e4-244">定位 SQL Server 实例时出错</span><span class="sxs-lookup"><span data-stu-id="3d8e4-244">Error locating SQL Server instance</span></span>

<span data-ttu-id="3d8e4-245">错误消息：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-245">Error Message:</span></span>

> <span data-ttu-id="3d8e4-246">建立到 SQL Server 的连接时出现与网络相关或特定于实例的错误。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-246">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="3d8e4-247">未找到或无法访问服务器。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-247">The server was not found or was not accessible.</span></span> <span data-ttu-id="3d8e4-248">请验证实例名称是否正确，SQL Server 是否已配置为允许远程连接。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-248">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="3d8e4-249">（提供程序：SQL 网络接口，错误：26 - 定位指定的服务器/实例时出错）</span><span class="sxs-lookup"><span data-stu-id="3d8e4-249">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="3d8e4-250">解决方案：</span><span class="sxs-lookup"><span data-stu-id="3d8e4-250">Solution:</span></span>

<span data-ttu-id="3d8e4-251">检查连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-251">Check the connection string.</span></span> <span data-ttu-id="3d8e4-252">如果已手动删除数据库文件，请更改构造字符串中数据库的名称，以使用新数据库重新开始。</span><span class="sxs-lookup"><span data-stu-id="3d8e4-252">If you have manually deleted the database file, change the name of the database in the construction string to start over with a new database.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="3d8e4-253">上一篇</span><span class="sxs-lookup"><span data-stu-id="3d8e4-253">Previous</span></span>](inheritance.md)
