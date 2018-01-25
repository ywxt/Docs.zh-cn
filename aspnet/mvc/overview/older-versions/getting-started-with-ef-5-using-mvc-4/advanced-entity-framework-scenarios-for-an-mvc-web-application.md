---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: "MVC Web 应用程序 (10/10) 的高级实体框架方案 |Microsoft 文档"
author: tdykstra
description: "Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 148a1aa33f6f713ae471ab14c7180f6c08a8679a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="c0ad8-103">MVC Web 应用程序 (10/10) 的高级的实体框架方案</span><span class="sxs-lookup"><span data-stu-id="c0ad8-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>
====================
<span data-ttu-id="c0ad8-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c0ad8-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="c0ad8-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="c0ad8-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="c0ad8-107">有关教程系列的信息，请参阅[序列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="c0ad8-108">你可以从头开始教程系列或[下载这一章的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)和从这里开始。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="c0ad8-109">如果你遇到无法解决的问题[下载已完成的章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="c0ad8-110">你通常可以通过比较你的代码已完成的代码会发现问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="c0ad8-111">一些常见的错误和如何解决它们，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="c0ad8-112">在以前的教程，你可以实现的存储库和单元的工作模式。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-112">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="c0ad8-113">本教程涵盖以下主题：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-113">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="c0ad8-114">执行原始的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-114">Performing raw SQL queries.</span></span>
- <span data-ttu-id="c0ad8-115">执行无跟踪查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-115">Performing no-tracking queries.</span></span>
- <span data-ttu-id="c0ad8-116">检查查询发送到数据库。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-116">Examining queries sent to the database.</span></span>
- <span data-ttu-id="c0ad8-117">使用代理类。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-117">Working with proxy classes.</span></span>
- <span data-ttu-id="c0ad8-118">禁用自动检测的更改。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-118">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="c0ad8-119">禁用验证，在保存时更改。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-119">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="c0ad8-120">错误和解决方法</span><span class="sxs-lookup"><span data-stu-id="c0ad8-120">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="c0ad8-121">对于大多数这些主题，你将使用已创建的页。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-121">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="c0ad8-122">若要使用原始 SQL 执行批量更新将创建一个新页更新的数据库中的所有课程的信用额度数：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-122">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="c0ad8-124">并使用否跟踪查询来查询你将新的验证逻辑添加到部门编辑页：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-124">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="c0ad8-126">执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="c0ad8-126">Performing Raw SQL Queries</span></span>

<span data-ttu-id="c0ad8-127">实体框架代码的第一个 API 包括使您能够 SQL 命令将直接传递到数据库的方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-127">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="c0ad8-128">有下列选项：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-128">You have the following options:</span></span>

- <span data-ttu-id="c0ad8-129">使用`DbSet.SqlQuery`返回实体类型的查询的方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-129">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="c0ad8-130">返回的对象必须是期望的类型的`DbSet`对象，并且它们是否自动跟踪数据库上下文中的除非关闭跟踪。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-130">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="c0ad8-131">(参见下一节`AsNoTracking`方法。)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-131">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="c0ad8-132">使用`Database.SqlQuery`方法用于返回不是实体类型的查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-132">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="c0ad8-133">返回的数据不跟踪数据库上下文中，即使你使用此方法来检索实体类型。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-133">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="c0ad8-134">使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx)非查询命令。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-134">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="c0ad8-135">使用实体框架的优点之一是它可避免将你过于仔细存储数据的特定方法的代码。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-135">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="c0ad8-136">此，它会生成 SQL 查询和命令，其中还使你无需自行编写。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-136">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="c0ad8-137">但没有特殊情况下当你需要运行特定的 SQL 查询，你已手动创建的并且这些方法使你可以处理此类异常。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-137">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="c0ad8-138">因为时，将始终 true web 应用程序中执行 SQL 命令，你必须采取预防措施来保护你的站点对 SQL 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-138">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="c0ad8-139">若要这样做的一种方法是使用参数化的查询来确保由网页上提交的字符串，不能解释为 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-139">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="c0ad8-140">在本教程中将用户输入集成到查询时，将使用参数化的查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-140">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="c0ad8-141">调用一个查询返回实体</span><span class="sxs-lookup"><span data-stu-id="c0ad8-141">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="c0ad8-142">假设你想`GenericRepository`类以提供附加的筛选和排序灵活性而无需使用其他方法创建一个派生的类。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-142">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="c0ad8-143">实现此目的的一种方法将添加接受 SQL 查询的方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-143">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="c0ad8-144">你可以指定任何类型的筛选或排序你想在控制器中，如`Where`取决于联接或子查询的子句。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-144">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="c0ad8-145">在本部分中，你将看到如何实现此类方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-145">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="c0ad8-146">创建`GetWithRawSql`通过添加以下代码的方法*GenericRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="c0ad8-146">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="c0ad8-147">在*CourseController.cs*，调用中的新方法`Details`方法，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-147">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="c0ad8-148">你无法在此情况下使用`GetByID`方法，但你正在使用`GetWithRawSql`方法来验证是否`GetWithRawSQL`方法的用法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-148">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="c0ad8-149">运行要验证的选择查询工作原理的详细信息页 (选择**课程**选项卡，然后**详细信息**一个课程)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-149">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="c0ad8-151">调用一个查询返回其他类型的对象</span><span class="sxs-lookup"><span data-stu-id="c0ad8-151">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="c0ad8-152">前面你创建的每个注册日期显示学生的数量关于页面的学生统计信息网格。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-152">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="c0ad8-153">在执行此代码*HomeController.cs*使用 LINQ:</span><span class="sxs-lookup"><span data-stu-id="c0ad8-153">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="c0ad8-154">假设你想要编写代码，以便检索直接在 SQL 中而不使用 LINQ 此数据。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-154">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="c0ad8-155">若要执行需要运行该查询将返回实体对象以外，这意味着你需要使用`Database.SqlQuery`方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-155">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="c0ad8-156">在*HomeController.cs*，替换中的 LINQ 语句`About`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-156">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="c0ad8-157">运行关于页面。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-157">Run the About page.</span></span> <span data-ttu-id="c0ad8-158">它显示它以前的相同数据。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-158">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="c0ad8-160">调用更新查询</span><span class="sxs-lookup"><span data-stu-id="c0ad8-160">Calling an Update Query</span></span>

<span data-ttu-id="c0ad8-161">假设 Contoso 大学管理员想要能够在数据库中，如更改的每个课程的信用额度数执行大容量更改。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-161">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="c0ad8-162">如果该大学具有大量的课程，这会降低效率要检索其所有项作为实体并单独更改。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-162">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="c0ad8-163">在本部分中，你将实施一个网页，允许用户指定用来更改用于所有课程的信用额度数因子和则将进行的更改，通过执行 SQL`UPDATE`语句。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-163">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="c0ad8-164">网页外观类似于下图：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-164">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="c0ad8-166">在以前的教程，你用于泛型存储库读取和更新`Course`中的实体`Course`控制器。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-166">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="c0ad8-167">对于此大容量更新操作，你需要创建一个新的存储库方法不属于泛型存储库。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-167">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="c0ad8-168">若要做到这一点，你将创建专用`CourseRepository`派生自的类`GenericRepository`类。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-168">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="c0ad8-169">在*DAL*文件夹中，创建*CourseRepository.cs*和替换为以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-169">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="c0ad8-170">在*UnitOfWork.cs*，更改`Course`从存储库类型`GenericRepository<Course>`到`CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="c0ad8-170">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="c0ad8-171">在*CourseContoller.cs*，添加`UpdateCourseCredits`方法：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-171">In *CourseContoller.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="c0ad8-172">此方法将为两者使用`HttpGet`和`HttpPost`。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-172">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="c0ad8-173">当`HttpGet``UpdateCourseCredits`方法运行`multiplier`变量将为 null，并且视图将显示的空文本框和提交按钮，如在上图中所示。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-173">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="c0ad8-174">当**更新**单击按钮和`HttpPost`方法运行`multiplier`将具有在文本框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-174">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="c0ad8-175">然后，代码调用的存储库`UpdateCourseCredits`方法，返回的数目影响的行，而该值将存储在`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-175">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="c0ad8-176">当视图收到受影响行数`ViewBag`对象，它显示该数字，而非文本框中，将提交按钮下, 图中所示：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-176">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="c0ad8-178">中创建视图*Views\Course*更新课程信用额度页的文件夹：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-178">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="c0ad8-180">在*Views\Course\UpdateCourseCredits.cshtml*，模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-180">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="c0ad8-181">运行`UpdateCourseCredits`方法通过选择**课程**选项卡上，然后添加"/ UpdateCourseCredits"到末尾的浏览器的地址栏中的 URL (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-181">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="c0ad8-182">在文本框中输入数字：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-182">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="c0ad8-184">单击“更新” 。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-184">Click **Update**.</span></span> <span data-ttu-id="c0ad8-185">你看到受影响的行数：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-185">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="c0ad8-187">单击**回列表**若要查看的课程替换信用额度的修订号的列表。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-187">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="c0ad8-189">有关原始的 SQL 查询的详细信息，请参阅[原始的 SQL 查询](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)实体框架团队博客上。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-189">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="c0ad8-190">否跟踪查询</span><span class="sxs-lookup"><span data-stu-id="c0ad8-190">No-Tracking Queries</span></span>

<span data-ttu-id="c0ad8-191">当数据库上下文检索数据库行，并创建表示它们的实体对象时，默认情况下它将跟踪的内存中的实体是否同步，与数据库中。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-191">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="c0ad8-192">内存中的数据充当缓存，并更新实体时使用。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-192">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="c0ad8-193">此缓存通常是不必要的 web 应用中由于上下文实例是否通常生存期较短 （新功能之一是创建和释放为每个请求） 和上下文读取再次使用该实体通常释放实体。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-193">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="c0ad8-194">你可以指定上下文是否通过使用跟踪查询的实体对象`AsNoTracking`方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-194">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="c0ad8-195">在其中你可能想要执行此操作的典型方案包括：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-195">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="c0ad8-196">该查询将检索此类大型卷数据的关闭跟踪可能会显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-196">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="c0ad8-197">你想要将实体附加以便其进行更新，但前面为不同的用途检索相同的实体。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-197">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="c0ad8-198">因为该实体已跟踪数据库上下文时，不能将附加你想要更改的实体。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-198">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="c0ad8-199">要防止此类情况发生的一种方法是使用`AsNoTracking`与前面的查询的选项。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-199">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="c0ad8-200">在本部分中，你将实施阐释了这些方案中的第二个的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-200">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="c0ad8-201">具体而言，你将强制实施业务规则指出一个教师不能为多个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-201">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="c0ad8-202">在*DepartmentController.cs*，添加新方法，可以从调用`Edit`和`Create`方法以确保没有两个部门具有相同的管理员：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-202">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="c0ad8-203">中添加代码`try`块`HttpPost``Edit`方法调用此新方法，如果没有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-203">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="c0ad8-204">`try`块现在看起来像下面的示例：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-204">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="c0ad8-205">运行部门编辑页面，尝试更改到已经是另一个部门的管理员的教师部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-205">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="c0ad8-206">您收到预期的错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-206">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="c0ad8-208">现在运行部门编辑页再次和此时间更改**预算**量。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-208">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="c0ad8-209">当你单击**保存**，你看到一个错误页面：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-209">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="c0ad8-211">异常错误消息为"`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`"这是由于以下事件序列：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-211">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="c0ad8-212">`Edit`方法调用`ValidateOneAdministratorAssignmentPerInstructor`方法，检索所有具有 Kim Abercrombie 以其管理员身份的部门。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-212">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="c0ad8-213">从而导致要读取的英语部门。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-213">That causes the English department to be read.</span></span> <span data-ttu-id="c0ad8-214">因为这是正在编辑的部门，不会报告错误。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-214">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="c0ad8-215">由于此读取操作，但是，已从数据库读取的英语的部门实体现在正在跟踪的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-215">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="c0ad8-216">`Edit`方法尝试设置`Modified`能在英语版的标志部门实体创建的 MVC 模型联编程序，但该失败，因为上下文已跟踪英语的部门实体。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-216">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="c0ad8-217">此问题的一种解决方案是防止上下文跟踪验证查询检索到的内存中部门实体。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-217">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="c0ad8-218">这样做，因为你不会更新此实体或从其缓存在内存中受益的方式再次读取它没有缺点。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-218">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="c0ad8-219">在*DepartmentController.cs*中`ValidateOneAdministratorAssignmentPerInstructor`方法，不指定任何跟踪，如在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-219">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="c0ad8-220">重复你尝试编辑**预算**某个部门的量。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-220">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="c0ad8-221">这一次操作成功，并预计将于部门索引页上，显示修订的预算值返回站点。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-221">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="c0ad8-222">检查查询发送到数据库</span><span class="sxs-lookup"><span data-stu-id="c0ad8-222">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="c0ad8-223">有时很有用，能够以查看发送到数据库的实际 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-223">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="c0ad8-224">若要执行此操作，你可以检查在调试器中的查询变量，或调用查询的`ToString`方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-224">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="c0ad8-225">若要试用此项，将查看一个简单查询，并再看会发生什么情况向其添加选项时，此类 eager 加载、 筛选和排序。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-225">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="c0ad8-226">在*控制器/CourseController*，替换`Index`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-226">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="c0ad8-227">现在中设置断点*GenericRepository.cs*上`return query.ToList();`和`return orderBy(query).ToList();`的语句`Get`方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-227">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="c0ad8-228">在调试模式下运行该项目并选择课程索引页。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-228">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="c0ad8-229">当代码达到断点时，检查`query`变量。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-229">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="c0ad8-230">你看到发送到 SQL Server 查询。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-230">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="c0ad8-231">它是一个简单`Select`语句：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-231">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="c0ad8-232">查询会很长时间才能在 Visual Studio 中的调试窗口中显示。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-232">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="c0ad8-233">若要查看整个查询，可以复制变量的值，并将其粘贴到文本编辑器：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-233">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="c0ad8-235">现在将向课程索引页添加下拉列表，以便用户可以筛选特定部门。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-235">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="c0ad8-236">你将排序课程标题，并且你将指定的预先加载`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-236">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="c0ad8-237">在*CourseController.cs*，替换`Index`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-237">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="c0ad8-238">该方法接收的下拉列表中的所选的值`SelectedDepartment`参数。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-238">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="c0ad8-239">如果未选择任何内容，此参数将为 null。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-239">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="c0ad8-240">A`SelectList`为下拉列表包含所有部门集合传递到视图。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-240">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="c0ad8-241">参数传递给`SelectList`构造函数指定的值字段名称、 文本字段名称和选定的项。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-241">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="c0ad8-242">有关`Get`方法`Course`存储库，该代码指定筛选表达式、 排序顺序和预先加载的`Department`导航属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-242">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="c0ad8-243">筛选器表达式始终返回`true`如果则不选择下拉列表中 (即，`SelectedDepartment`为 null)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-243">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="c0ad8-244">在*Views\Course\Index.cshtml*，立即在打开之前`table`标记中，添加以下代码以创建下拉列表和提交按钮：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-244">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="c0ad8-245">仍中设置的断点与`GenericRepository`类，运行课程索引页。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-245">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="c0ad8-246">继续代码达到断点、 的前两个时间，以便在浏览器中显示的页面。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-246">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="c0ad8-247">从下拉列表中选择一个部门，然后单击**筛选器**:</span><span class="sxs-lookup"><span data-stu-id="c0ad8-247">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="c0ad8-249">这一次部门 query for 下拉列表将第一个断点。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-249">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="c0ad8-250">跳过，并查看`query`变量下次代码达到断点才能看到什么`Course`查询现在如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-250">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="c0ad8-251">你将看到类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-251">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

<span data-ttu-id="c0ad8-252">你可以看到，现在是查询`JOIN`加载的查询`Department`数据以及`Course`数据，并包含`WHERE`子句。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-252">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="c0ad8-253">使用代理类</span><span class="sxs-lookup"><span data-stu-id="c0ad8-253">Working with Proxy Classes</span></span>

<span data-ttu-id="c0ad8-254">当实体框架创建 （例如，在执行查询时） 的实体实例时，它通常创建它们作为动态生成的派生类型，它就像该实体的代理的实例。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-254">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="c0ad8-255">此代理将重写插入挂钩，以便在访问属性时自动执行操作的实体的某些虚拟属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-255">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="c0ad8-256">例如，此机制用于支持延迟加载的关系。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-256">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="c0ad8-257">大多数情况下不需要要注意的此使用代理服务器，但有例外情况：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-257">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="c0ad8-258">在某些情况下你可能想要阻止实体框架创建代理实例。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-258">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="c0ad8-259">例如，序列化非代理实例可能比序列化代理实例更高效。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-259">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="c0ad8-260">当实例化实体类使用`new`运算符，你不会获得代理实例。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-260">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="c0ad8-261">这意味着不遇到功能，如延迟加载和自动更改跟踪。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-261">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="c0ad8-262">这通常是好了;你通常不需要延迟加载，因为你要创建新的实体不在数据库中，且通常无需更改跟踪如果您显式标记为实体`Added`。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-262">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="c0ad8-263">但是，如果你需要延迟加载，并且你需要更改跟踪，你可以创建新实体实例与代理使用`Create`方法`DbSet`类。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-263">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="c0ad8-264">你可能想要获得的代理类型的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-264">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="c0ad8-265">你可以使用`GetObjectType`方法`ObjectContext`类，以获取代理类型实例的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-265">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="c0ad8-266">有关详细信息，请参阅[使用代理](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)实体框架团队博客上。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-266">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="c0ad8-267">禁用自动检测更改</span><span class="sxs-lookup"><span data-stu-id="c0ad8-267">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="c0ad8-268">实体框架通过比较的实体的当前值与原始值确定更改实体的方式 （并因此需要发送到数据库的更新）。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-268">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="c0ad8-269">如果该实体已查询或附加，存储的原始值。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-269">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="c0ad8-270">某些会导致自动更改检测的方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-270">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="c0ad8-271">如果您跟踪的大量实体，并且你调用这些方法之一多次在循环中，你可能会显著的性能改进，通过暂时关闭自动更改检测使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-271">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="c0ad8-272">有关详细信息，请参阅[自动检测更改](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-272">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="c0ad8-273">禁用验证，在保存时更改</span><span class="sxs-lookup"><span data-stu-id="c0ad8-273">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="c0ad8-274">当调用`SaveChanges`方法，默认情况下，实体框架中的所有更改的实体的所有属性的数据之前验证更新的数据库。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-274">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="c0ad8-275">如果你已更新的大量实体，并且你已验证数据，这一工作是不必要和无法使保存的过程所做的更改通过暂时关闭验证花费更少时间。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-275">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="c0ad8-276">你可以执行，使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-276">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="c0ad8-277">有关详细信息，请参阅[验证](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-277">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="c0ad8-278">摘要</span><span class="sxs-lookup"><span data-stu-id="c0ad8-278">Summary</span></span>

<span data-ttu-id="c0ad8-279">这将完成这一系列的 ASP.NET MVC 应用程序中使用实体框架的教程。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-279">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="c0ad8-280">在找不到其他实体框架资源的链接[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-280">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="c0ad8-281">有关如何部署 web 应用程序，你已生成后的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-281">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="c0ad8-282">有关与相关的 MVC，例如身份验证和授权，其他主题信息请参阅[MVC 的推荐资源](../../getting-started/recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-282">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="c0ad8-283">确认</span><span class="sxs-lookup"><span data-stu-id="c0ad8-283">Acknowledgments</span></span>

- <span data-ttu-id="c0ad8-284">Tom Dykstra 编写本教程的原始版本和是上的 Microsoft Web 平台和工具内容团队高级编程的编写器。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-284">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="c0ad8-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 共同撰写本教程并确实执行操作的大部分工作的 EF 5 和 MVC 4 对它进行更新。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="c0ad8-286">Rick 是 Microsoft 将重点放在 Azure 和 MVC 的高级编程编写器。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-286">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="c0ad8-287">[Rowan Miller](http://www.romiller.com)和实体框架团队其他成员的辅助与代码评审，并帮助调试借助迁移所引起时我们已 EF 5 更新本教程的许多问题。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-287">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="c0ad8-288">VB</span><span class="sxs-lookup"><span data-stu-id="c0ad8-288">VB</span></span>

<span data-ttu-id="c0ad8-289">当最初生成本教程时，我们将提供已完成的下载项目的 C# 和 VB 的版本。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-289">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="c0ad8-290">我们利用此更新提供每个章节，以使其更轻松地开始任意位置在系列中，但由于时间限制和我们未不执行该操作 VB.其他优先级的 C# 可下载项目</span><span class="sxs-lookup"><span data-stu-id="c0ad8-290">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="c0ad8-291">如果您生成使用这些教程为 VB 项目，并且会愿意与他人共享的请让我们知道。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-291">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="c0ad8-292">错误和解决方法</span><span class="sxs-lookup"><span data-stu-id="c0ad8-292">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="c0ad8-293">无法创建/卷影副本</span><span class="sxs-lookup"><span data-stu-id="c0ad8-293">Cannot create/shadow copy</span></span>

<span data-ttu-id="c0ad8-294">错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-294">Error Message:</span></span>

<span data-ttu-id="c0ad8-295">*无法创建/卷影副本 DotNetOpenAuth.OpenId 该文件已存在时。*</span><span class="sxs-lookup"><span data-stu-id="c0ad8-295">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="c0ad8-296">解决方案：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-296">Solution:</span></span>

<span data-ttu-id="c0ad8-297">等待几秒钟，并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-297">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="c0ad8-298">更新数据库无法识别</span><span class="sxs-lookup"><span data-stu-id="c0ad8-298">Update-Database not recognized</span></span>

<span data-ttu-id="c0ad8-299">错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-299">Error Message:</span></span>

<span data-ttu-id="c0ad8-300">*术语更新数据库未被识别为 cmdlet、 函数、 脚本文件或可操作程序的名称。请检查拼写的名称，或如果包括路径，请验证路径正确，然后重试。*(从 *`Update-Database`*  PMC 命令。)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-300">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="c0ad8-301">解决方案：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-301">Solution:</span></span>

<span data-ttu-id="c0ad8-302">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-302">Exit Visual Studio.</span></span> <span data-ttu-id="c0ad8-303">重新打开项目，然后重试。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-303">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="c0ad8-304">验证失败</span><span class="sxs-lookup"><span data-stu-id="c0ad8-304">Validation failed</span></span>

<span data-ttu-id="c0ad8-305">错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-305">Error Message:</span></span>

<span data-ttu-id="c0ad8-306">*一个或多个实体的验证失败。请参阅 EntityValidationErrors 属性的更多详细信息。*</span><span class="sxs-lookup"><span data-stu-id="c0ad8-306">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="c0ad8-307">(从 *`Update-Database`*  PMC 命令。)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-307">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="c0ad8-308">解决方案：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-308">Solution:</span></span>

<span data-ttu-id="c0ad8-309">此问题的一个原因是验证错误时`Seed`方法运行。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-309">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="c0ad8-310">请参阅[进行种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)调试的提示和技巧`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-310">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="c0ad8-311">HTTP 500.19 错误</span><span class="sxs-lookup"><span data-stu-id="c0ad8-311">HTTP 500.19 error</span></span>

<span data-ttu-id="c0ad8-312">错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-312">Error Message:</span></span>

<span data-ttu-id="c0ad8-313">*无法访问 HTTP 错误 500.19-内部服务器错误的请求页面，因为该页的相关的配置数据无效。*</span><span class="sxs-lookup"><span data-stu-id="c0ad8-313">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="c0ad8-314">解决方案：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-314">Solution:</span></span>

<span data-ttu-id="c0ad8-315">可能发生此错误的一种方法是从拥有该解决方案，每个使用相同的端口号的多个副本。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-315">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="c0ad8-316">通常可以通过退出的 Visual Studio 中，所有实例，然后重新项目启动你正在致力于解决此问题。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-316">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="c0ad8-317">如果这不起作用，请尝试更改端口号。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-317">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="c0ad8-318">右键单击项目文件，然后单击属性。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-318">Right click on the project file and then click properties.</span></span> <span data-ttu-id="c0ad8-319">选择**Web**选项卡上，然后将更改中的端口号**项目 Url**文本框。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-319">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="c0ad8-320">错误找到 SQL Server 实例</span><span class="sxs-lookup"><span data-stu-id="c0ad8-320">Error locating SQL Server instance</span></span>

<span data-ttu-id="c0ad8-321">错误消息：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-321">Error Message:</span></span>

<span data-ttu-id="c0ad8-322">*建立与 SQL Server 的连接时发生与网络相关或特定于实例的错误。未找到或无法访问服务器。请验证实例名称正确以及 SQL Server 配置为允许远程连接。(提供程序： SQL 网络接口，错误： 26-错误查找服务器/实例指定)*</span><span class="sxs-lookup"><span data-stu-id="c0ad8-322">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="c0ad8-323">解决方案：</span><span class="sxs-lookup"><span data-stu-id="c0ad8-323">Solution:</span></span>

<span data-ttu-id="c0ad8-324">请检查连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-324">Check connection string.</span></span> <span data-ttu-id="c0ad8-325">如果你已手动删除数据库，更改构造字符串中数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="c0ad8-325">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c0ad8-326">[上一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[下一页](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="c0ad8-326">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>
