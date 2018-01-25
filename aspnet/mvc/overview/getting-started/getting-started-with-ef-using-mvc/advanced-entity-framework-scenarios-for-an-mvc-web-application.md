---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: "MVC 5 Web 应用程序 (12 的 12) 的高级实体框架 6 方案 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85276377671b96e65406639c8584d9ebf8d77ff7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="advanced-entity-framework-6-scenarios-for-an-mvc-5-web-application-12-of-12"></a><span data-ttu-id="b1058-103">MVC 5 Web 应用程序 (12 的 12) 的高级的实体框架 6 方案</span><span class="sxs-lookup"><span data-stu-id="b1058-103">Advanced Entity Framework 6 Scenarios for an MVC 5 Web Application (12 of 12)</span></span>
====================
<span data-ttu-id="b1058-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b1058-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="b1058-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="b1058-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="b1058-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1058-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="b1058-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="b1058-108">在以前的教程，你实现的每个层次结构一个表继承。</span><span class="sxs-lookup"><span data-stu-id="b1058-108">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="b1058-109">本教程包括以下引入了几个有用需要注意的时要考虑的因素的基础知识的开发使用 Entity Framework Code First 的 ASP.NET web 应用程序的主题。</span><span class="sxs-lookup"><span data-stu-id="b1058-109">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="b1058-110">分步说明将引导你完成的代码和使用 Visual Studio 的下列主题：</span><span class="sxs-lookup"><span data-stu-id="b1058-110">Step-by-step instructions walk you through the code and using Visual Studio for the following topics:</span></span>

- [<span data-ttu-id="b1058-111">执行原始的 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="b1058-111">Performing raw SQL queries</span></span>](#rawsql)
- [<span data-ttu-id="b1058-112">执行无跟踪查询</span><span class="sxs-lookup"><span data-stu-id="b1058-112">Performing no-tracking queries</span></span>](#notracking)
- [<span data-ttu-id="b1058-113">检查 SQL 发送到数据库</span><span class="sxs-lookup"><span data-stu-id="b1058-113">Examining SQL sent to the database</span></span>](#sql)

<span data-ttu-id="b1058-114">本教程介绍与跟对资源的详细信息的链接的简要介绍几个主题：</span><span class="sxs-lookup"><span data-stu-id="b1058-114">The tutorial introduces several topics with brief introductions followed by links to resources for more information:</span></span>

- [<span data-ttu-id="b1058-115">存储库和单元的工作模式</span><span class="sxs-lookup"><span data-stu-id="b1058-115">Repository and unit of work patterns</span></span>](#repo)
- [<span data-ttu-id="b1058-116">代理类</span><span class="sxs-lookup"><span data-stu-id="b1058-116">Proxy classes</span></span>](#proxies)
- [<span data-ttu-id="b1058-117">自动更改检测</span><span class="sxs-lookup"><span data-stu-id="b1058-117">Automatic change detection</span></span>](#changedetection)
- [<span data-ttu-id="b1058-118">自动验证</span><span class="sxs-lookup"><span data-stu-id="b1058-118">Automatic validation</span></span>](#validation)
- [<span data-ttu-id="b1058-119">Visual Studio 的 EF 工具</span><span class="sxs-lookup"><span data-stu-id="b1058-119">EF tools for Visual Studio</span></span>](#tools)
- [<span data-ttu-id="b1058-120">实体框架的源代码</span><span class="sxs-lookup"><span data-stu-id="b1058-120">Entity Framework source code</span></span>](#source)

<span data-ttu-id="b1058-121">本教程还包括以下各节：</span><span class="sxs-lookup"><span data-stu-id="b1058-121">The tutorial also includes the following sections:</span></span>

- [<span data-ttu-id="b1058-122">摘要</span><span class="sxs-lookup"><span data-stu-id="b1058-122">Summary</span></span>](#summary)
- [<span data-ttu-id="b1058-123">确认</span><span class="sxs-lookup"><span data-stu-id="b1058-123">Acknowledgments</span></span>](#acknowledgments)
- [<span data-ttu-id="b1058-124">有关 VB 的注意事项</span><span class="sxs-lookup"><span data-stu-id="b1058-124">A note about VB</span></span>](#vb)
- [<span data-ttu-id="b1058-125">常见错误，以及解决方案或解决办法它们</span><span class="sxs-lookup"><span data-stu-id="b1058-125">Common errors, and solutions or workarounds for them</span></span>](#errors)

<span data-ttu-id="b1058-126">对于大多数这些主题，你将使用已创建的页。</span><span class="sxs-lookup"><span data-stu-id="b1058-126">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="b1058-127">若要使用原始 SQL 执行批量更新将创建一个新页更新的数据库中的所有课程的信用额度数：</span><span class="sxs-lookup"><span data-stu-id="b1058-127">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<a id="rawsql"></a>
## <a name="performing-raw-sql-queries"></a><span data-ttu-id="b1058-129">执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="b1058-129">Performing Raw SQL Queries</span></span>

<span data-ttu-id="b1058-130">实体框架代码的第一个 API 包括使您能够 SQL 命令将直接传递到数据库的方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-130">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="b1058-131">有下列选项：</span><span class="sxs-lookup"><span data-stu-id="b1058-131">You have the following options:</span></span>

- <span data-ttu-id="b1058-132">使用[DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)返回实体类型的查询的方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-132">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="b1058-133">返回的对象必须是期望的类型的`DbSet`对象，并且它们是否自动跟踪数据库上下文中的除非关闭跟踪。</span><span class="sxs-lookup"><span data-stu-id="b1058-133">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="b1058-134">(参见下一节[AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)方法。)</span><span class="sxs-lookup"><span data-stu-id="b1058-134">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="b1058-135">使用[Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)方法用于返回不是实体类型的查询。</span><span class="sxs-lookup"><span data-stu-id="b1058-135">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="b1058-136">返回的数据不跟踪数据库上下文中，即使你使用此方法来检索实体类型。</span><span class="sxs-lookup"><span data-stu-id="b1058-136">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="b1058-137">使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx)非查询命令。</span><span class="sxs-lookup"><span data-stu-id="b1058-137">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="b1058-138">使用实体框架的优点之一是它可避免将你过于仔细存储数据的特定方法的代码。</span><span class="sxs-lookup"><span data-stu-id="b1058-138">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="b1058-139">此，它会生成 SQL 查询和命令，其中还使你无需自行编写。</span><span class="sxs-lookup"><span data-stu-id="b1058-139">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="b1058-140">但没有特殊情况下当你需要运行特定的 SQL 查询，你已手动创建的并且这些方法使你可以处理此类异常。</span><span class="sxs-lookup"><span data-stu-id="b1058-140">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="b1058-141">因为时，将始终 true web 应用程序中执行 SQL 命令，你必须采取预防措施来保护你的站点对 SQL 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="b1058-141">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="b1058-142">若要这样做的一种方法是使用参数化的查询来确保由网页上提交的字符串，不能解释为 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="b1058-142">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="b1058-143">在本教程中将用户输入集成到查询时，将使用参数化的查询。</span><span class="sxs-lookup"><span data-stu-id="b1058-143">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="b1058-144">调用一个查询返回实体</span><span class="sxs-lookup"><span data-stu-id="b1058-144">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="b1058-145">[DbSet&lt;TEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx)类提供了可用于执行该查询将返回类型的实体的方法`TEntity`。</span><span class="sxs-lookup"><span data-stu-id="b1058-145">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="b1058-146">若要查看你原理将更改中的代码`Details`方法`Department`控制器。</span><span class="sxs-lookup"><span data-stu-id="b1058-146">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="b1058-147">在*DepartmentController.cs*中`Details`方法，替换`db.Departments.FindAsync`方法调用与`db.Departments.SqlQuery`方法调用，如以下突出显示的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="b1058-147">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="b1058-148">若要验证新代码是否工作正常，请选择**部门**选项卡，然后**详细信息**部门之一。</span><span class="sxs-lookup"><span data-stu-id="b1058-148">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![部门详细信息](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="b1058-150">调用一个查询返回其他类型的对象</span><span class="sxs-lookup"><span data-stu-id="b1058-150">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="b1058-151">前面你创建的每个注册日期显示学生的数量关于页面的学生统计信息网格。</span><span class="sxs-lookup"><span data-stu-id="b1058-151">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="b1058-152">在执行此代码*HomeController.cs*使用 LINQ:</span><span class="sxs-lookup"><span data-stu-id="b1058-152">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="b1058-153">假设你想要编写代码，以便检索直接在 SQL 中而不使用 LINQ 此数据。</span><span class="sxs-lookup"><span data-stu-id="b1058-153">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="b1058-154">若要执行需要运行该查询将返回实体对象以外，这意味着你需要使用[Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-154">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="b1058-155">在*HomeController.cs*，替换中的 LINQ 语句`About`方法与 SQL 语句，如以下突出显示的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="b1058-155">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="b1058-156">运行关于页面。</span><span class="sxs-lookup"><span data-stu-id="b1058-156">Run the About page.</span></span> <span data-ttu-id="b1058-157">它显示它以前的相同数据。</span><span class="sxs-lookup"><span data-stu-id="b1058-157">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="b1058-159">调用更新查询</span><span class="sxs-lookup"><span data-stu-id="b1058-159">Calling an Update Query</span></span>

<span data-ttu-id="b1058-160">假设 Contoso 大学管理员想要能够在数据库中，如更改的每个课程的信用额度数执行大容量更改。</span><span class="sxs-lookup"><span data-stu-id="b1058-160">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="b1058-161">如果该大学具有大量的课程，这会降低效率要检索其所有项作为实体并单独更改。</span><span class="sxs-lookup"><span data-stu-id="b1058-161">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="b1058-162">在本部分中，你将实施一个网页，使用户能够指定要更改用于所有课程的信用额度次数因子和则将进行的更改，通过执行 SQL`UPDATE`语句。</span><span class="sxs-lookup"><span data-stu-id="b1058-162">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="b1058-163">网页外观类似于下图：</span><span class="sxs-lookup"><span data-stu-id="b1058-163">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

<span data-ttu-id="b1058-165">在*CourseContoller.cs*，添加`UpdateCourseCredits`方法`HttpGet`和`HttpPost`:</span><span class="sxs-lookup"><span data-stu-id="b1058-165">In *CourseContoller.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="b1058-166">当控制器处理`HttpGet`请求，未返回任何内容中`ViewBag.RowsAffected`变量，并查看显示的空文本框和提交按钮，如在上图中所示。</span><span class="sxs-lookup"><span data-stu-id="b1058-166">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="b1058-167">当**更新**单击按钮时，`HttpPost`调用方法时，和`multiplier`已在文本框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="b1058-167">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="b1058-168">然后执行的代码更新课程，并返回受影响的行数中的视图的 SQL`ViewBag.RowsAffected`变量。</span><span class="sxs-lookup"><span data-stu-id="b1058-168">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="b1058-169">当视图中，获取一个值变量，它显示的更新而不是文本框中的行数并提交按钮，如下面的插图中所示：</span><span class="sxs-lookup"><span data-stu-id="b1058-169">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="b1058-171">在*CourseController.cs*，右键单击其中一个`UpdateCourseCredits`方法，，然后单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="b1058-171">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="b1058-173">在*Views\Course\UpdateCourseCredits.cshtml*，模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b1058-173">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="b1058-174">运行`UpdateCourseCredits`方法通过选择**课程**选项卡上，然后添加"/ UpdateCourseCredits"到末尾的浏览器的地址栏中的 URL (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。</span><span class="sxs-lookup"><span data-stu-id="b1058-174">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="b1058-175">在文本框中输入数字：</span><span class="sxs-lookup"><span data-stu-id="b1058-175">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="b1058-177">单击“更新” 。</span><span class="sxs-lookup"><span data-stu-id="b1058-177">Click **Update**.</span></span> <span data-ttu-id="b1058-178">你看到受影响的行数：</span><span class="sxs-lookup"><span data-stu-id="b1058-178">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="b1058-180">单击**回列表**若要查看的课程替换信用额度的修订号的列表。</span><span class="sxs-lookup"><span data-stu-id="b1058-180">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="b1058-182">有关原始的 SQL 查询的详细信息，请参阅[原始的 SQL 查询](https://msdn.microsoft.com/data/jj592907)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="b1058-182">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

<a id="notracking"></a>
## <a name="no-tracking-queries"></a><span data-ttu-id="b1058-183">否跟踪查询</span><span class="sxs-lookup"><span data-stu-id="b1058-183">No-Tracking Queries</span></span>

<span data-ttu-id="b1058-184">当数据库上下文检索表行，并创建表示它们的实体对象时，默认情况下它将跟踪的内存中的实体是否同步，与数据库中。</span><span class="sxs-lookup"><span data-stu-id="b1058-184">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="b1058-185">内存中的数据充当缓存，并更新实体时使用。</span><span class="sxs-lookup"><span data-stu-id="b1058-185">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="b1058-186">此缓存通常是不必要的 web 应用中由于上下文实例是否通常生存期较短 （新功能之一是创建和释放为每个请求） 和上下文读取再次使用该实体通常释放实体。</span><span class="sxs-lookup"><span data-stu-id="b1058-186">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="b1058-187">你可以通过使用禁用的实体对象在内存中的跟踪[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-187">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="b1058-188">在其中你可能想要执行此操作的典型方案包括：</span><span class="sxs-lookup"><span data-stu-id="b1058-188">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="b1058-189">查询检索此类大型卷数据的关闭跟踪可能会显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="b1058-189">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="b1058-190">你想要将实体附加以便其进行更新，但前面为不同的用途检索相同的实体。</span><span class="sxs-lookup"><span data-stu-id="b1058-190">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="b1058-191">因为该实体已跟踪数据库上下文时，不能将附加你想要更改的实体。</span><span class="sxs-lookup"><span data-stu-id="b1058-191">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="b1058-192">处理这种情况的一种方法是使用`AsNoTracking`与前面的查询的选项。</span><span class="sxs-lookup"><span data-stu-id="b1058-192">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="b1058-193">有关示例，演示如何使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法，请参阅[本教程的早期版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-193">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="b1058-194">本教程的此版本不修改时间标志实体上设置模型联编程序创建在编辑方法中，因此它不需要`AsNoTracking`。</span><span class="sxs-lookup"><span data-stu-id="b1058-194">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

<a id="sql"></a>
## <a name="examining-sql-sent-to-the-database"></a><span data-ttu-id="b1058-195">检查 SQL 发送到数据库</span><span class="sxs-lookup"><span data-stu-id="b1058-195">Examining SQL sent to the database</span></span>

<span data-ttu-id="b1058-196">有时很有用，能够以查看发送到数据库的实际 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="b1058-196">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="b1058-197">在早期的教程中，您将了解如何执行该操作在侦听器代码;现在，你将看到执行此操作而无需编写拦截器代码的一些方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-197">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="b1058-198">若要试用此项，将查看一个简单查询，并再看会发生什么情况向其添加选项时，此类 eager 加载、 筛选和排序。</span><span class="sxs-lookup"><span data-stu-id="b1058-198">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="b1058-199">在*控制器/CourseController*，替换`Index`方法替换为以下代码，若要暂时停止预先加载：</span><span class="sxs-lookup"><span data-stu-id="b1058-199">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="b1058-200">现在上设置断点`return`语句 (F9 在该行上光标)。</span><span class="sxs-lookup"><span data-stu-id="b1058-200">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="b1058-201">按 F5 在调试模式下运行该项目并选择课程索引页。</span><span class="sxs-lookup"><span data-stu-id="b1058-201">Press F5 to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="b1058-202">当代码达到断点时，检查`sql`变量。</span><span class="sxs-lookup"><span data-stu-id="b1058-202">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="b1058-203">你看到发送到 SQL Server 查询。</span><span class="sxs-lookup"><span data-stu-id="b1058-203">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="b1058-204">它是一个简单`Select`语句。</span><span class="sxs-lookup"><span data-stu-id="b1058-204">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="b1058-205">单击要查看的查询中的放大镜类**文本可视化工具**。</span><span class="sxs-lookup"><span data-stu-id="b1058-205">Click the magnifying class to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="b1058-206">现在将向课程索引页添加下拉列表，以便用户可以筛选特定部门。</span><span class="sxs-lookup"><span data-stu-id="b1058-206">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="b1058-207">你将排序课程标题，并且你将指定的预先加载`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-207">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="b1058-208">在*CourseController.cs*，替换`Index`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b1058-208">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="b1058-209">在还原断点`return`语句。</span><span class="sxs-lookup"><span data-stu-id="b1058-209">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="b1058-210">该方法接收的下拉列表中的所选的值`SelectedDepartment`参数。</span><span class="sxs-lookup"><span data-stu-id="b1058-210">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="b1058-211">如果未选择任何内容，此参数将为 null。</span><span class="sxs-lookup"><span data-stu-id="b1058-211">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="b1058-212">A`SelectList`为下拉列表包含所有部门集合传递到视图。</span><span class="sxs-lookup"><span data-stu-id="b1058-212">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="b1058-213">参数传递给`SelectList`构造函数指定的值字段名称、 文本字段名称和选定的项。</span><span class="sxs-lookup"><span data-stu-id="b1058-213">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="b1058-214">有关`Get`方法`Course`存储库，该代码指定筛选表达式、 排序顺序和预先加载的`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-214">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="b1058-215">筛选器表达式始终返回`true`如果则不选择下拉列表中 (即，`SelectedDepartment`为 null)。</span><span class="sxs-lookup"><span data-stu-id="b1058-215">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="b1058-216">在*Views\Course\Index.cshtml*，立即在打开之前`table`标记中，添加以下代码以创建下拉列表和提交按钮：</span><span class="sxs-lookup"><span data-stu-id="b1058-216">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="b1058-217">断点仍然组之前，运行课程索引页。</span><span class="sxs-lookup"><span data-stu-id="b1058-217">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="b1058-218">继续代码达到断点的行，第一次，以便在浏览器中显示的页面。</span><span class="sxs-lookup"><span data-stu-id="b1058-218">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="b1058-219">从下拉列表中选择一个部门，然后单击**筛选器**:</span><span class="sxs-lookup"><span data-stu-id="b1058-219">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="b1058-221">这一次部门 query for 下拉列表将第一个断点。</span><span class="sxs-lookup"><span data-stu-id="b1058-221">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="b1058-222">跳过，并查看`query`变量下次代码达到断点才能看到什么`Course`查询现在如下所示。</span><span class="sxs-lookup"><span data-stu-id="b1058-222">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="b1058-223">你将看到类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="b1058-223">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="b1058-224">你可以看到，现在是查询`JOIN`加载的查询`Department`数据以及`Course`数据，并包含`WHERE`子句。</span><span class="sxs-lookup"><span data-stu-id="b1058-224">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="b1058-225">删除`var sql = courses.ToString()`行。</span><span class="sxs-lookup"><span data-stu-id="b1058-225">Remove the `var sql = courses.ToString()` line.</span></span>

<a id="repo"></a>

## <a name="repository-and-unit-of-work-patterns"></a><span data-ttu-id="b1058-226">存储库和单元的工作模式</span><span class="sxs-lookup"><span data-stu-id="b1058-226">Repository and unit of work patterns</span></span>

<span data-ttu-id="b1058-227">许多开发人员编写代码以作为使用实体框架代码的周围的包装器实现的存储库和单元的工作模式。</span><span class="sxs-lookup"><span data-stu-id="b1058-227">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="b1058-228">这些模式用于创建数据访问层和应用程序的业务逻辑层之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="b1058-228">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="b1058-229">实现这些模式可帮助防止你的应用程序数据存储区中的更改，而且很容易自动的单元测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="b1058-229">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="b1058-230">但是，编写附加代码以实现这些模式并不总是使用 EF，有几个原因的应用程序的最佳选择：</span><span class="sxs-lookup"><span data-stu-id="b1058-230">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="b1058-231">EF 上下文类本身使应用商店数据特有的代码中的代码。</span><span class="sxs-lookup"><span data-stu-id="b1058-231">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="b1058-232">EF 上下文类可以充当数据库的工作单位类更新你不要使用 EF。</span><span class="sxs-lookup"><span data-stu-id="b1058-232">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="b1058-233">Entity Framework 6 中引入的功能更加轻松地实现 TDD 而无需编写存储库代码。</span><span class="sxs-lookup"><span data-stu-id="b1058-233">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="b1058-234">有关如何实现的存储库和单元的工作模式的详细信息，请参阅[本系列教程的实体框架 5 版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-234">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="b1058-235">有关如何在 Entity Framework 6 中实现 TDD 的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="b1058-235">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="b1058-236">如何从 EF6 更轻松地通过 Mocking Dbset 时</span><span class="sxs-lookup"><span data-stu-id="b1058-236">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="b1058-237">使用模拟框架进行测试</span><span class="sxs-lookup"><span data-stu-id="b1058-237">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="b1058-238">使用你自己的测试替身测试</span><span class="sxs-lookup"><span data-stu-id="b1058-238">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>
## <a name="proxy-classes"></a><span data-ttu-id="b1058-239">代理类</span><span class="sxs-lookup"><span data-stu-id="b1058-239">Proxy classes</span></span>

<span data-ttu-id="b1058-240">当实体框架创建 （例如，在执行查询时） 的实体实例时，它通常创建它们作为动态生成的派生类型，它就像该实体的代理的实例。</span><span class="sxs-lookup"><span data-stu-id="b1058-240">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="b1058-241">有关示例，请参阅以下两个调试器映像。</span><span class="sxs-lookup"><span data-stu-id="b1058-241">For example, see the following two debugger images.</span></span> <span data-ttu-id="b1058-242">中的第一个图像，请参阅，`student`变量是预期`Student`键入实例化实体后立即。</span><span class="sxs-lookup"><span data-stu-id="b1058-242">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="b1058-243">在第二个图中，已使用 EF 来从数据库中读取学生实体后你将看到的代理类。</span><span class="sxs-lookup"><span data-stu-id="b1058-243">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![代理类之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![代理类之后](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="b1058-246">此代理类重写插入挂钩，以便在访问属性时自动执行操作的实体的某些虚拟属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-246">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="b1058-247">此机制适用于的一个函数是延迟加载。</span><span class="sxs-lookup"><span data-stu-id="b1058-247">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="b1058-248">大多数情况下不需要要注意的此使用代理服务器，但有例外情况：</span><span class="sxs-lookup"><span data-stu-id="b1058-248">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="b1058-249">在某些情况下你可能想要阻止实体框架创建代理实例。</span><span class="sxs-lookup"><span data-stu-id="b1058-249">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="b1058-250">例如，在正在序列化实体时你通常想 POCO 类，不使用代理类。</span><span class="sxs-lookup"><span data-stu-id="b1058-250">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="b1058-251">若要避免序列化问题的一种方法是序列化而不是实体对象的数据传输对象 (Dto) 中所示[使用实体框架使用 Web API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="b1058-251">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="b1058-252">另一种方法是[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b1058-252">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="b1058-253">当实例化实体类使用`new`运算符，你不会获得代理实例。</span><span class="sxs-lookup"><span data-stu-id="b1058-253">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="b1058-254">这意味着不遇到功能，如延迟加载和自动更改跟踪。</span><span class="sxs-lookup"><span data-stu-id="b1058-254">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="b1058-255">这通常是好了;你通常不需要延迟加载，因为你要创建新的实体不在数据库中，且通常无需更改跟踪如果您显式标记为实体`Added`。</span><span class="sxs-lookup"><span data-stu-id="b1058-255">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="b1058-256">但是，如果你需要延迟加载，并且你需要更改跟踪，你可以创建新实体实例与代理使用[创建](https://msdn.microsoft.com/library/gg679504.aspx)方法`DbSet`类。</span><span class="sxs-lookup"><span data-stu-id="b1058-256">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="b1058-257">你可能想要获得的代理类型的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="b1058-257">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="b1058-258">你可以使用[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)方法`ObjectContext`类，以获取代理类型实例的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="b1058-258">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="b1058-259">有关详细信息，请参阅[使用代理](https://msdn.microsoft.com/data/JJ592886.aspx)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="b1058-259">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

<a id="changedetection"></a>
## <a name="automatic-change-detection"></a><span data-ttu-id="b1058-260">自动更改检测</span><span class="sxs-lookup"><span data-stu-id="b1058-260">Automatic change detection</span></span>

<span data-ttu-id="b1058-261">实体框架通过比较的实体的当前值与原始值确定更改实体的方式 （并因此需要发送到数据库的更新）。</span><span class="sxs-lookup"><span data-stu-id="b1058-261">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="b1058-262">查询或附加该实体时，存储的原始值。</span><span class="sxs-lookup"><span data-stu-id="b1058-262">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="b1058-263">某些会导致自动更改检测的方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="b1058-263">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="b1058-264">如果您跟踪的大量实体，并且你调用这些方法之一多次在循环中，你可能会显著的性能改进，通过暂时关闭自动更改检测使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-264">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="b1058-265">有关详细信息，请参阅[自动检测更改](https://msdn.microsoft.com/data/jj556205)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="b1058-265">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

<a id="validation"></a>
## <a name="automatic-validation"></a><span data-ttu-id="b1058-266">自动验证</span><span class="sxs-lookup"><span data-stu-id="b1058-266">Automatic validation</span></span>

<span data-ttu-id="b1058-267">当调用`SaveChanges`方法，默认情况下，实体框架中的所有更改的实体的所有属性的数据之前验证更新的数据库。</span><span class="sxs-lookup"><span data-stu-id="b1058-267">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="b1058-268">如果你已更新的大量实体，并且你已验证数据，这一工作是不必要和无法使保存的过程所做的更改通过暂时关闭验证花费更少时间。</span><span class="sxs-lookup"><span data-stu-id="b1058-268">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="b1058-269">你可以执行，使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-269">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="b1058-270">有关详细信息，请参阅[验证](https://msdn.microsoft.com/data/gg193959)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="b1058-270">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

<a id="tools"></a>
## <a name="entity-framework-power-tools"></a><span data-ttu-id="b1058-271">实体框架 Power 工具</span><span class="sxs-lookup"><span data-stu-id="b1058-271">Entity Framework Power Tools</span></span>

<span data-ttu-id="b1058-272">[实体框架 Power 工具](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)一个 Visual Studio 外接程序，用于创建数据模型关系图中所示这些教程。</span><span class="sxs-lookup"><span data-stu-id="b1058-272">[Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="b1058-273">这些工具还可以执行其他函数，如生成实体类基于现有数据库中的表，以便你可以使用代码优先使用数据库。</span><span class="sxs-lookup"><span data-stu-id="b1058-273">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="b1058-274">安装工具后，在上下文菜单中显示一些附加选项。</span><span class="sxs-lookup"><span data-stu-id="b1058-274">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="b1058-275">例如，当您右击你上下文类中的**解决方案资源管理器**，获取一个选项以生成关系图。</span><span class="sxs-lookup"><span data-stu-id="b1058-275">For example, when you right-click your context class in **Solution Explorer**, you get an option to generate a diagram.</span></span> <span data-ttu-id="b1058-276">在你使用 Code First 时无法更改关系图中中的数据模型，但可以来回移动操作，以使其更易于理解。</span><span class="sxs-lookup"><span data-stu-id="b1058-276">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![上下文菜单中的 EF](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image14.png)

![EF 关系图](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

<a id="source"></a>
## <a name="entity-framework-source-code"></a><span data-ttu-id="b1058-279">实体框架的源代码</span><span class="sxs-lookup"><span data-stu-id="b1058-279">Entity Framework source code</span></span>

<span data-ttu-id="b1058-280">Entity Framework 6 的源代码位于[GitHub](https://github.com/aspnet/EntityFramework6)。</span><span class="sxs-lookup"><span data-stu-id="b1058-280">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="b1058-281">你可以报告 bug，并可以提供你自己的 EF 源代码的增强功能。</span><span class="sxs-lookup"><span data-stu-id="b1058-281">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="b1058-282">尽管源代码处于打开状态，实体框架完全支持的 Microsoft 产品。</span><span class="sxs-lookup"><span data-stu-id="b1058-282">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="b1058-283">Microsoft 实体框架团队将控制哪些接受的贡献保持和测试所有代码更改，以确保每个版本的质量。</span><span class="sxs-lookup"><span data-stu-id="b1058-283">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="b1058-284">摘要</span><span class="sxs-lookup"><span data-stu-id="b1058-284">Summary</span></span>

<span data-ttu-id="b1058-285">这将完成这一系列的 ASP.NET MVC 应用程序中使用实体框架的教程。</span><span class="sxs-lookup"><span data-stu-id="b1058-285">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="b1058-286">有关如何使用实体框架处理数据的详细信息，请参阅[EF MSDN 上的文档页](https://msdn.microsoft.com/data/ee712907)和[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-286">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="b1058-287">有关如何部署 web 应用程序，你已生成后的详细信息，请参阅[ASP.NET Web 部署的推荐资源](../../../../whitepapers/aspnet-web-deployment-content-map.md)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="b1058-287">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="b1058-288">有关与相关的 MVC，例如身份验证和授权，其他主题信息请参阅[ASP.NET MVC 的推荐资源](../recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-288">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a><span data-ttu-id="b1058-289">确认</span><span class="sxs-lookup"><span data-stu-id="b1058-289">Acknowledgments</span></span>

- <span data-ttu-id="b1058-290">Tom Dykstra 编写本教程的原始版本，共同撰写了 EF 5 更新，和编写 EF 6 更新。</span><span class="sxs-lookup"><span data-stu-id="b1058-290">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="b1058-291">Tom 是上的 Microsoft Web 平台和工具内容团队的高级编程编写器。</span><span class="sxs-lookup"><span data-stu-id="b1058-291">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="b1058-292">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 未的大部分更新本教程适用于 EF 5 和 MVC 4 工作，共同创作 EF 6 更新。</span><span class="sxs-lookup"><span data-stu-id="b1058-292">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="b1058-293">Rick 是 Microsoft 将重点放在 Azure 和 MVC 的高级编程编写器。</span><span class="sxs-lookup"><span data-stu-id="b1058-293">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="b1058-294">[Rowan Miller](http://www.romiller.com)和实体框架团队其他成员的辅助与代码评审，并帮助调试借助迁移所引起时我们已为 EF 5 和 EF 6 更新本教程的许多问题。</span><span class="sxs-lookup"><span data-stu-id="b1058-294">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

<a id="vb"></a>
## <a name="vb"></a><span data-ttu-id="b1058-295">VB</span><span class="sxs-lookup"><span data-stu-id="b1058-295">VB</span></span>

<span data-ttu-id="b1058-296">当的 EF 4.1 中最初产生了本教程时，我们将提供已完成的下载项目的 C# 和 VB 的版本。</span><span class="sxs-lookup"><span data-stu-id="b1058-296">When the tutorial was originally produced for EF 4.1, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="b1058-297">由于时间限制和其他优先级我们不完成该操作对于此版本。</span><span class="sxs-lookup"><span data-stu-id="b1058-297">Due to time limitations and other priorities we have not done that for this version.</span></span> <span data-ttu-id="b1058-298">如果您生成使用这些教程为 VB 项目，并且会愿意与他人共享的请让我们知道。</span><span class="sxs-lookup"><span data-stu-id="b1058-298">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>
## <a name="common-errors-and-solutions-or-workarounds-for-them"></a><span data-ttu-id="b1058-299">常见错误，以及解决方案或解决办法它们</span><span class="sxs-lookup"><span data-stu-id="b1058-299">Common errors, and solutions or workarounds for them</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="b1058-300">无法创建/卷影副本</span><span class="sxs-lookup"><span data-stu-id="b1058-300">Cannot create/shadow copy</span></span>

<span data-ttu-id="b1058-301">错误消息：</span><span class="sxs-lookup"><span data-stu-id="b1058-301">Error Message:</span></span>

> <span data-ttu-id="b1058-302">无法创建/卷影副本&lt;filename&gt;该文件已存在。</span><span class="sxs-lookup"><span data-stu-id="b1058-302">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>


<span data-ttu-id="b1058-303">解决方案</span><span class="sxs-lookup"><span data-stu-id="b1058-303">Solution</span></span>

<span data-ttu-id="b1058-304">等待几秒钟，并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="b1058-304">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="b1058-305">更新数据库无法识别</span><span class="sxs-lookup"><span data-stu-id="b1058-305">Update-Database not recognized</span></span>

<span data-ttu-id="b1058-306">错误消息 (从`Update-Database`PMC 命令):</span><span class="sxs-lookup"><span data-stu-id="b1058-306">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="b1058-307">术语更新数据库未被识别为 cmdlet、 函数、 脚本文件或可操作程序的名称。</span><span class="sxs-lookup"><span data-stu-id="b1058-307">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="b1058-308">请检查拼写的名称，或如果包括路径，请验证路径正确，然后重试。</span><span class="sxs-lookup"><span data-stu-id="b1058-308">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>


<span data-ttu-id="b1058-309">解决方案</span><span class="sxs-lookup"><span data-stu-id="b1058-309">Solution</span></span>

<span data-ttu-id="b1058-310">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b1058-310">Exit Visual Studio.</span></span> <span data-ttu-id="b1058-311">重新打开项目，然后重试。</span><span class="sxs-lookup"><span data-stu-id="b1058-311">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="b1058-312">验证失败</span><span class="sxs-lookup"><span data-stu-id="b1058-312">Validation failed</span></span>

<span data-ttu-id="b1058-313">错误消息 (从`Update-Database`PMC 命令):</span><span class="sxs-lookup"><span data-stu-id="b1058-313">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="b1058-314">一个或多个实体的验证失败。</span><span class="sxs-lookup"><span data-stu-id="b1058-314">Validation failed for one or more entities.</span></span> <span data-ttu-id="b1058-315">请参阅 EntityValidationErrors 属性的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="b1058-315">See 'EntityValidationErrors' property for more details.</span></span>


<span data-ttu-id="b1058-316">解决方案</span><span class="sxs-lookup"><span data-stu-id="b1058-316">Solution</span></span>

<span data-ttu-id="b1058-317">此问题的一个原因是验证错误时`Seed`方法运行。</span><span class="sxs-lookup"><span data-stu-id="b1058-317">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="b1058-318">请参阅[进行种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)调试的提示和技巧`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="b1058-318">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="b1058-319">HTTP 500.19 错误</span><span class="sxs-lookup"><span data-stu-id="b1058-319">HTTP 500.19 error</span></span>

<span data-ttu-id="b1058-320">错误消息：</span><span class="sxs-lookup"><span data-stu-id="b1058-320">Error Message:</span></span>

> <span data-ttu-id="b1058-321">HTTP 错误 500.19-内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="b1058-321">HTTP Error 500.19 - Internal Server Error</span></span>  
> <span data-ttu-id="b1058-322">无法访问所请求的页面，因为该页的相关的配置数据无效。</span><span class="sxs-lookup"><span data-stu-id="b1058-322">The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>


<span data-ttu-id="b1058-323">解决方案</span><span class="sxs-lookup"><span data-stu-id="b1058-323">Solution</span></span>

<span data-ttu-id="b1058-324">可能发生此错误的一种方法是从拥有该解决方案，每个使用相同的端口号的多个副本。</span><span class="sxs-lookup"><span data-stu-id="b1058-324">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="b1058-325">通常可以通过退出的 Visual Studio 中，所有实例，然后重新启动您正在处理的项目来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="b1058-325">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="b1058-326">如果这不起作用，请尝试更改端口号。</span><span class="sxs-lookup"><span data-stu-id="b1058-326">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="b1058-327">右键单击项目文件，然后单击属性。</span><span class="sxs-lookup"><span data-stu-id="b1058-327">Right click on the project file and then click properties.</span></span> <span data-ttu-id="b1058-328">选择**Web**选项卡上，然后将更改中的端口号**项目 Url**文本框。</span><span class="sxs-lookup"><span data-stu-id="b1058-328">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="b1058-329">错误找到 SQL Server 实例</span><span class="sxs-lookup"><span data-stu-id="b1058-329">Error locating SQL Server instance</span></span>

<span data-ttu-id="b1058-330">错误消息：</span><span class="sxs-lookup"><span data-stu-id="b1058-330">Error Message:</span></span>

> <span data-ttu-id="b1058-331">建立与 SQL Server 的连接时发生与网络相关或特定于实例的错误。</span><span class="sxs-lookup"><span data-stu-id="b1058-331">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="b1058-332">未找到或无法访问服务器。</span><span class="sxs-lookup"><span data-stu-id="b1058-332">The server was not found or was not accessible.</span></span> <span data-ttu-id="b1058-333">请验证实例名称是否正确，SQL Server 是否已配置为允许远程连接。</span><span class="sxs-lookup"><span data-stu-id="b1058-333">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="b1058-334">(提供程序： SQL 网络接口，错误： 26-错误查找服务器/实例指定)</span><span class="sxs-lookup"><span data-stu-id="b1058-334">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>


<span data-ttu-id="b1058-335">解决方案</span><span class="sxs-lookup"><span data-stu-id="b1058-335">Solution</span></span>

<span data-ttu-id="b1058-336">请检查连接字符串。</span><span class="sxs-lookup"><span data-stu-id="b1058-336">Check the connection string.</span></span> <span data-ttu-id="b1058-337">如果你已手动删除数据库，更改构造字符串中数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="b1058-337">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="b1058-338">上一篇</span><span class="sxs-lookup"><span data-stu-id="b1058-338">Previous</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
