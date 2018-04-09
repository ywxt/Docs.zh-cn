---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 处理与实体框架 6 ASP.NET MVC 5 应用程序 (以 10 为 12) 中的并发 |Microsoft 文档
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b92aded80ad6b435a2409a137bb96fe4d0a726f4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="handling-concurrency-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-10-of-12"></a><span data-ttu-id="e8439-103">处理与实体框架 6 ASP.NET MVC 5 应用程序 (以 10 为 12) 中的并发</span><span class="sxs-lookup"><span data-stu-id="e8439-103">Handling Concurrency with the Entity Framework 6 in an ASP.NET MVC 5 Application (10 of 12)</span></span>
====================
<span data-ttu-id="e8439-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e8439-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="e8439-105">[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="e8439-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="e8439-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8439-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="e8439-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="e8439-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="e8439-108">在前面的教程中，您学习了如何更新数据。</span><span class="sxs-lookup"><span data-stu-id="e8439-108">In earlier tutorials you learned how to update data.</span></span> <span data-ttu-id="e8439-109">本教程介绍如何处理多个用户同时更新同一实体时出现的冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-109">This tutorial shows how to handle conflicts when multiple users update the same entity at the same time.</span></span>

<span data-ttu-id="e8439-110">你将更改使用的网页`Department`实体以使它们处理并发错误。</span><span class="sxs-lookup"><span data-stu-id="e8439-110">You'll change the web pages that work with the `Department` entity so that they handle concurrency errors.</span></span> <span data-ttu-id="e8439-111">下图显示的索引和删除页，包括某些并发冲突发生时显示的消息。</span><span class="sxs-lookup"><span data-stu-id="e8439-111">The following illustrations show the Index and Delete pages, including some messages that are displayed if a concurrency conflict occurs.</span></span>

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a><span data-ttu-id="e8439-114">并发冲突</span><span class="sxs-lookup"><span data-stu-id="e8439-114">Concurrency Conflicts</span></span>

<span data-ttu-id="e8439-115">当某用户显示实体数据以对其进行编辑，而另一用户在上一用户的更改写入数据库之前更新同一实体的数据时，会发生并发冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-115">A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates the same entity's data before the first user's change is written to the database.</span></span> <span data-ttu-id="e8439-116">如果不启用此类冲突的检测，则最后更新数据库的人员将覆盖其他用户的更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-116">If you don't enable the detection of such conflicts, whoever updates the database last overwrites the other user's changes.</span></span> <span data-ttu-id="e8439-117">在许多应用程序中，此风险是可接受的：如果用户很少或更新很少，或者一些更改被覆盖并不重要，则并发编程可能弊大于利。</span><span class="sxs-lookup"><span data-stu-id="e8439-117">In many applications, this risk is acceptable: if there are few users, or few updates, or if isn't really critical if some changes are overwritten, the cost of programming for concurrency might outweigh the benefit.</span></span> <span data-ttu-id="e8439-118">在此情况下，不必配置应用程序来处理并发冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-118">In that case, you don't have to configure the application to handle concurrency conflicts.</span></span>

### <a name="pessimistic-concurrency-locking"></a><span data-ttu-id="e8439-119">保守式并发 （锁定）</span><span class="sxs-lookup"><span data-stu-id="e8439-119">Pessimistic Concurrency (Locking)</span></span>

<span data-ttu-id="e8439-120">如果应用程序确实需要防止并发情况下出现意外数据丢失，一种方法是使用数据库锁定。</span><span class="sxs-lookup"><span data-stu-id="e8439-120">If your application does need to prevent accidental data loss in concurrency scenarios, one way to do that is to use database locks.</span></span> <span data-ttu-id="e8439-121">这称为*保守式并发*。</span><span class="sxs-lookup"><span data-stu-id="e8439-121">This is called *pessimistic concurrency*.</span></span> <span data-ttu-id="e8439-122">例如，在从数据库读取一行内容之前，请求锁定为只读或更新访问。</span><span class="sxs-lookup"><span data-stu-id="e8439-122">For example, before you read a row from a database, you request a lock for read-only or for update access.</span></span> <span data-ttu-id="e8439-123">如果将一行锁定为更新访问，则其他用户无法将该行锁定为只读或更新访问，因为那样会使他们得到正在更改的数据的副本。</span><span class="sxs-lookup"><span data-stu-id="e8439-123">If you lock a row for update access, no other users are allowed to lock the row either for read-only or update access, because they would get a copy of data that's in the process of being changed.</span></span> <span data-ttu-id="e8439-124">如果将一行锁定为只读访问，则其他人也可将其锁定为只读访问，但不能进行更新。</span><span class="sxs-lookup"><span data-stu-id="e8439-124">If you lock a row for read-only access, others can also lock it for read-only access but not for update.</span></span>

<span data-ttu-id="e8439-125">管理锁定有缺点。</span><span class="sxs-lookup"><span data-stu-id="e8439-125">Managing locks has disadvantages.</span></span> <span data-ttu-id="e8439-126">编程可能很复杂。</span><span class="sxs-lookup"><span data-stu-id="e8439-126">It can be complex to program.</span></span> <span data-ttu-id="e8439-127">它需要大量的数据库管理资源，且随着应用程序用户数量的增加，可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="e8439-127">It requires significant database management resources, and it can cause performance problems as the number of users of an application increases.</span></span> <span data-ttu-id="e8439-128">由于这些原因，并不是所有的数据库管理系统都支持悲观并发。</span><span class="sxs-lookup"><span data-stu-id="e8439-128">For these reasons, not all database management systems support pessimistic concurrency.</span></span> <span data-ttu-id="e8439-129">本教程不向你展示如何实现它，并且实体框架提供，没有内置支持。</span><span class="sxs-lookup"><span data-stu-id="e8439-129">The Entity Framework provides no built-in support for it, and this tutorial doesn't show you how to implement it.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="e8439-130">开放式并发</span><span class="sxs-lookup"><span data-stu-id="e8439-130">Optimistic Concurrency</span></span>

<span data-ttu-id="e8439-131">保守式并发替代方法是*开放式并发*。</span><span class="sxs-lookup"><span data-stu-id="e8439-131">The alternative to pessimistic concurrency is *optimistic concurrency*.</span></span> <span data-ttu-id="e8439-132">乐观并发是指允许发生并发冲突，并在并发冲突发生时作出正确反应。</span><span class="sxs-lookup"><span data-stu-id="e8439-132">Optimistic concurrency means allowing concurrency conflicts to happen, and then reacting appropriately if they do.</span></span> <span data-ttu-id="e8439-133">例如，John 运行部门编辑页上，更改**预算**量从 $350,000.00 0.00 美元到英语的部门。</span><span class="sxs-lookup"><span data-stu-id="e8439-133">For example, John runs the Departments Edit page, changes the **Budget** amount for the English department from $350,000.00 to $0.00.</span></span>

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="e8439-135">John 单击之前**保存**，Jane 运行相同的页和更改**开始日期**字段从 2007 年 9 月 1 日到 2013 年 8 月 8 日。</span><span class="sxs-lookup"><span data-stu-id="e8439-135">Before John clicks **Save**, Jane runs the same page and changes the **Start Date** field from 9/1/2007 to 8/8/2013.</span></span>

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="e8439-137">John 单击**保存**第一个并查看他的更改时浏览器返回到索引页面，然后 Jane 单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="e8439-137">John clicks **Save** first and sees his change when the browser returns to the Index page, then Jane clicks **Save**.</span></span> <span data-ttu-id="e8439-138">接下来的情况取决于并发冲突的处理方式。</span><span class="sxs-lookup"><span data-stu-id="e8439-138">What happens next is determined by how you handle concurrency conflicts.</span></span> <span data-ttu-id="e8439-139">其中一些选项包括：</span><span class="sxs-lookup"><span data-stu-id="e8439-139">Some of the options include the following:</span></span>

- <span data-ttu-id="e8439-140">可以跟踪用户已修改的属性，并仅更新数据库中相应的列。</span><span class="sxs-lookup"><span data-stu-id="e8439-140">You can keep track of which property a user has modified and update only the corresponding columns in the database.</span></span> <span data-ttu-id="e8439-141">在示例方案中，不会有数据丢失，因为是由两个用户更新不同的属性。</span><span class="sxs-lookup"><span data-stu-id="e8439-141">In the example scenario, no data would be lost, because different properties were updated by the two users.</span></span> <span data-ttu-id="e8439-142">下一次有人浏览英语部门时，他们将看到 John 的和 Jane 的更改 — 2013 年 8 月 8 日开始日期和零美元的预算。</span><span class="sxs-lookup"><span data-stu-id="e8439-142">The next time someone browses the English department, they'll see both John's and Jane's changes — a start date of 8/8/2013 and a budget of Zero dollars.</span></span>

    <span data-ttu-id="e8439-143">这种更新方法可减少可能导致数据丢失的冲突次数，但是如果对实体的同一属性进行竞争性更改，则数据难免会丢失。</span><span class="sxs-lookup"><span data-stu-id="e8439-143">This method of updating can reduce the number of conflicts that could result in data loss, but it can't avoid data loss if competing changes are made to the same property of an entity.</span></span> <span data-ttu-id="e8439-144">Entity Framework 是否以这种方式工作取决于更新代码的实现方式。</span><span class="sxs-lookup"><span data-stu-id="e8439-144">Whether the Entity Framework works this way depends on how you implement your update code.</span></span> <span data-ttu-id="e8439-145">通常不适合在 Web 应用程序中使用，因为它要求保持大量的状态，以便跟踪实体的所有原始属性值以及新值。</span><span class="sxs-lookup"><span data-stu-id="e8439-145">It's often not practical in a web application, because it can require that you maintain large amounts of state in order to keep track of all original property values for an entity as well as new values.</span></span> <span data-ttu-id="e8439-146">维护大量的状态可能会影响应用程序的性能，因为它需要服务器资源或必须包含在网页本身（例如隐藏字段）或 Cookie 中。</span><span class="sxs-lookup"><span data-stu-id="e8439-146">Maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself (for example, in hidden fields) or in a cookie.</span></span>
- <span data-ttu-id="e8439-147">你可以让 Jane 的更改覆盖 John 的更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-147">You can let Jane's change overwrite John's change.</span></span> <span data-ttu-id="e8439-148">下一次有人浏览英语部门时，他们将看到 2013 年 8 月 8 日和还原的 $350,000.00 值。</span><span class="sxs-lookup"><span data-stu-id="e8439-148">The next time someone browses the English department, they'll see 8/8/2013 and the restored $350,000.00 value.</span></span> <span data-ttu-id="e8439-149">这称为*客户端优先*或*最后一个优先*。</span><span class="sxs-lookup"><span data-stu-id="e8439-149">This is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="e8439-150">（客户端的所有值优先于数据存储的值。）正如本部分的介绍所述，如果不为并发处理编写任何代码，则自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e8439-150">(All values from the client take precedence over what's in the data store.) As noted in the introduction to this section, if you don't do any coding for concurrency handling, this will happen automatically.</span></span>
- <span data-ttu-id="e8439-151">你可以防止在数据库中正在更新 Jane 的更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-151">You can prevent Jane's change from being updated in the database.</span></span> <span data-ttu-id="e8439-152">通常情况下，将显示一条错误消息、 她显示的数据的当前状态和让她可以如果她仍然想要对它们进行重新应用其更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-152">Typically, you would display an error message, show her the current state of the data, and allow her to reapply her changes if she still wants to make them.</span></span> <span data-ttu-id="e8439-153">这称为“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="e8439-153">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="e8439-154">（数据存储值优先于客户端提交的值。）本教程将执行“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="e8439-154">(The data-store values take precedence over the values submitted by the client.) You'll implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="e8439-155">此方法可确保用户在未收到具体发生内容的警报时，不会覆盖任何更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-155">This method ensures that no changes are overwritten without a user being alerted to what's happening.</span></span>

### <a name="detecting-concurrency-conflicts"></a><span data-ttu-id="e8439-156">检测并发冲突</span><span class="sxs-lookup"><span data-stu-id="e8439-156">Detecting Concurrency Conflicts</span></span>

<span data-ttu-id="e8439-157">您可以通过处理中解决冲突[OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx)实体框架引发的异常。</span><span class="sxs-lookup"><span data-stu-id="e8439-157">You can resolve conflicts by handling [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) exceptions that the Entity Framework throws.</span></span> <span data-ttu-id="e8439-158">为了知道何时引发这些异常，Entity Framework 必须能够检测到冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-158">In order to know when to throw these exceptions, the Entity Framework must be able to detect conflicts.</span></span> <span data-ttu-id="e8439-159">因此，你必须正确配置数据库和数据模型。</span><span class="sxs-lookup"><span data-stu-id="e8439-159">Therefore, you must configure the database and the data model appropriately.</span></span> <span data-ttu-id="e8439-160">启用冲突检测的某些选项包括：</span><span class="sxs-lookup"><span data-stu-id="e8439-160">Some options for enabling conflict detection include the following:</span></span>

- <span data-ttu-id="e8439-161">数据库表中包含一个可用于确定某行更改时间的跟踪列。</span><span class="sxs-lookup"><span data-stu-id="e8439-161">In the database table, include a tracking column that can be used to determine when a row has been changed.</span></span> <span data-ttu-id="e8439-162">然后，你可以配置实体框架可以包括中的列`Where`的 SQL 子句`Update`或`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="e8439-162">You can then configure the Entity Framework to include that column in the `Where` clause of SQL `Update` or `Delete` commands.</span></span>

    <span data-ttu-id="e8439-163">跟踪列的数据类型通常是[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8439-163">The data type of the tracking column is typically [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx).</span></span> <span data-ttu-id="e8439-164">[Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新行时递增序列号。</span><span class="sxs-lookup"><span data-stu-id="e8439-164">The [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) value is a sequential number that's incremented each time the row is updated.</span></span> <span data-ttu-id="e8439-165">在`Update`或`Delete`命令，`Where`子句包括跟踪列 （原始行版本） 的原始值。</span><span class="sxs-lookup"><span data-stu-id="e8439-165">In an `Update` or `Delete` command, the `Where` clause includes the original value of the tracking column (the original row version).</span></span> <span data-ttu-id="e8439-166">如果正在更新的行已由其他用户时中的值更改`rowversion`列是不同于原始值，因此`Update`或`Delete`语句找不到要由于更新的行`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="e8439-166">If the row being updated has been changed by another user, the value in the `rowversion` column is different than the original value, so the `Update` or `Delete` statement can't find the row to update because of the `Where` clause.</span></span> <span data-ttu-id="e8439-167">在实体框架查找已通过更新了任何行`Update`或`Delete`命令 （即，在受影响的行数为零） 时，它将，解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-167">When the Entity Framework finds that no rows have been updated by the `Update` or `Delete` command (that is, when the number of affected rows is zero), it interprets that as a concurrency conflict.</span></span>
- <span data-ttu-id="e8439-168">配置实体框架可以包括在表中的每个列的原始值`Where`子句`Update`和`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="e8439-168">Configure the Entity Framework to include the original values of every column in the table in the `Where` clause of `Update` and `Delete` commands.</span></span>

    <span data-ttu-id="e8439-169">如下所示的第一个选项，如果自第一次读取一行，行中的任何内容已更改`Where`子句不会返回的行，若要更新，该实体框架会将解释为并发冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-169">As in the first option, if anything in the row has changed since the row was first read, the `Where` clause won't return a row to update, which the Entity Framework interprets as a concurrency conflict.</span></span> <span data-ttu-id="e8439-170">对于有多列的数据库表，这种方法可能会导致非常大`Where`子句，并可能需要维护大量的状态。</span><span class="sxs-lookup"><span data-stu-id="e8439-170">For database tables that have many columns, this approach can result in very large `Where` clauses, and can require that you maintain large amounts of state.</span></span> <span data-ttu-id="e8439-171">如前所述，维持大量的状态会影响应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="e8439-171">As noted earlier, maintaining large amounts of state can affect application performance.</span></span> <span data-ttu-id="e8439-172">因此通常不建议使用此方法，并且它也不是本教程中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="e8439-172">Therefore this approach is generally not recommended, and it isn't the method used in this tutorial.</span></span>

    <span data-ttu-id="e8439-173">如果您想要实现这种并发的方法，则必须将你想要通过添加跟踪的并发性实体中的所有非主键属性标记[ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx)属性设为它们。</span><span class="sxs-lookup"><span data-stu-id="e8439-173">If you do want to implement this approach to concurrency, you have to mark all non-primary-key properties in the entity you want to track concurrency for by adding the [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) attribute to them.</span></span> <span data-ttu-id="e8439-174">更改使实体框架能够在 SQL 中包括所有列`WHERE`子句`UPDATE`语句。</span><span class="sxs-lookup"><span data-stu-id="e8439-174">That change enables the Entity Framework to include all columns in the SQL `WHERE` clause of `UPDATE` statements.</span></span>

<span data-ttu-id="e8439-175">本教程的其余部分中将添加[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)跟踪属性`Department`实体，创建控制器和视图，并进行测试以验证一切是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="e8439-175">In the remainder of this tutorial you'll add a [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tracking property to the `Department` entity, create a controller and views, and test to verify that everything works correctly.</span></span>

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a><span data-ttu-id="e8439-176">将开放式并发属性添加到部门实体</span><span class="sxs-lookup"><span data-stu-id="e8439-176">Add an Optimistic Concurrency Property to the Department Entity</span></span>

<span data-ttu-id="e8439-177">在*Models\Department.cs*，添加名为的跟踪属性`RowVersion`:</span><span class="sxs-lookup"><span data-stu-id="e8439-177">In *Models\Department.cs*, add a tracking property named `RowVersion`:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

<span data-ttu-id="e8439-178">[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)属性指定此列将包含在`Where`子句`Update`和`Delete`命令发送到数据库。</span><span class="sxs-lookup"><span data-stu-id="e8439-178">The [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) attribute specifies that this column will be included in the `Where` clause of `Update` and `Delete` commands sent to the database.</span></span> <span data-ttu-id="e8439-179">该属性称为[时间戳](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)因为以前版本的 SQL Server 使用 SQL[时间戳](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)之前 SQL 数据类型[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)替换它。</span><span class="sxs-lookup"><span data-stu-id="e8439-179">The attribute is called [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) because previous versions of SQL Server used a SQL [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) data type before the SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) replaced it.</span></span> <span data-ttu-id="e8439-180">.Net 类型[rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)为字节数组。</span><span class="sxs-lookup"><span data-stu-id="e8439-180">The .Net type for [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) is a byte array.</span></span>

<span data-ttu-id="e8439-181">如果想要使用 fluent API，则可以使用[IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx)方法，以指定跟踪属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="e8439-181">If you prefer to use the fluent API, you can use the [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) method to specify the tracking property, as shown in the following example:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="e8439-182">通过添加属性，更改了数据库模型，因此需要再执行一次迁移。</span><span class="sxs-lookup"><span data-stu-id="e8439-182">By adding a property you changed the database model, so you need to do another migration.</span></span> <span data-ttu-id="e8439-183">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="e8439-183">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-the-department-controller"></a><span data-ttu-id="e8439-184">修改部门控制器</span><span class="sxs-lookup"><span data-stu-id="e8439-184">Modify the Department Controller</span></span>

<span data-ttu-id="e8439-185">在*Controllers\DepartmentController.cs*，添加`using`语句：</span><span class="sxs-lookup"><span data-stu-id="e8439-185">In *Controllers\DepartmentController.cs*, add a `using` statement:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="e8439-186">在*DepartmentController.cs*文件中，将所有四个出现的"LastName"更改为"FullName"，以便部门管理员下拉列表将包含教师的完整名称而不是只是最后一个名称。</span><span class="sxs-lookup"><span data-stu-id="e8439-186">In the *DepartmentController.cs* file, change all four occurrences of "LastName" to "FullName" so that the department administrator drop-down lists will contain the full name of the instructor rather than just the last name.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

<span data-ttu-id="e8439-187">替换现有代码，以`HttpPost``Edit`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e8439-187">Replace the existing code for the `HttpPost` `Edit` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="e8439-188">如果 `FindAsync` 方法返回 NULL，则该院系已被另一用户删除。</span><span class="sxs-lookup"><span data-stu-id="e8439-188">If the `FindAsync` method returns null, the department was deleted by another user.</span></span> <span data-ttu-id="e8439-189">所示的代码使用已发布的窗体值创建部门实体，以便编辑页可以重新显示并显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="e8439-189">The code shown uses the posted form values to create a department entity so that the Edit page can be redisplayed with an error message.</span></span> <span data-ttu-id="e8439-190">或者，如果仅显示错误消息而未重新显示院系字段，则不必重新创建 Department 实体。</span><span class="sxs-lookup"><span data-stu-id="e8439-190">As an alternative, you wouldn't have to re-create the department entity if you display only an error message without redisplaying the department fields.</span></span>

<span data-ttu-id="e8439-191">该视图将存储原始`RowVersion`值的隐藏的字段和方法中接收在`rowVersion`参数。</span><span class="sxs-lookup"><span data-stu-id="e8439-191">The view stores the original `RowVersion` value in a hidden field, and the method receives it in the `rowVersion` parameter.</span></span> <span data-ttu-id="e8439-192">在调用 `SaveChanges` 之前，必须将该原始 `RowVersion` 属性值置于实体的 `OriginalValues` 集合中。</span><span class="sxs-lookup"><span data-stu-id="e8439-192">Before you call `SaveChanges`, you have to put that original `RowVersion` property value in the `OriginalValues` collection for the entity.</span></span> <span data-ttu-id="e8439-193">然后创建时实体框架 SQL`UPDATE`命令时，命令将包括`WHERE`查找具有原始行的子句`RowVersion`值。</span><span class="sxs-lookup"><span data-stu-id="e8439-193">Then when the Entity Framework creates a SQL `UPDATE` command, that command will include a `WHERE` clause that looks for a row that has the original `RowVersion` value.</span></span>

<span data-ttu-id="e8439-194">如果任何行不受`UPDATE`命令 (任何行具有原始`RowVersion`值)，实体框架将引发`DbUpdateConcurrencyException`异常，并且中的代码`catch`块可获取在受影响`Department`的异常中的实体对象。</span><span class="sxs-lookup"><span data-stu-id="e8439-194">If no rows are affected by the `UPDATE` command (no rows have the original `RowVersion` value), the Entity Framework throws a `DbUpdateConcurrencyException` exception, and the code in the `catch` block gets the affected `Department` entity from the exception object.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="e8439-195">此对象具有新值中的用户输入其`Entity`属性，并且可以通过调用从数据库读取的值`GetDatabaseValues`方法。</span><span class="sxs-lookup"><span data-stu-id="e8439-195">This object has the new values entered by the user in its `Entity` property, and you can get the values read from the database by calling the `GetDatabaseValues` method.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="e8439-196">`GetDatabaseValues`方法将返回有人已从数据库中删除行的情况下为 null; 否则，你必须强制转换为返回的对象`Department`类才能访问`Department`属性。</span><span class="sxs-lookup"><span data-stu-id="e8439-196">The `GetDatabaseValues` method returns null if someone has deleted the row from the database; otherwise, you have to cast the returned object to the `Department` class in order to access the `Department` properties.</span></span> <span data-ttu-id="e8439-197">(已选中为删除，因为`databaseEntry`将 null 部门已删除后，才`FindAsync`执行和之前`SaveChanges`执行。)</span><span class="sxs-lookup"><span data-stu-id="e8439-197">(Because you already checked for deletion, `databaseEntry` would be null only if the department was deleted after `FindAsync` executes and before `SaveChanges` executes.)</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="e8439-198">接下来，代码将添加每个列都具有数据库值不同于在编辑页上输入的用户自定义错误消息：</span><span class="sxs-lookup"><span data-stu-id="e8439-198">Next, the code adds a custom error message for each column that has database values different from what the user entered on the Edit page:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="e8439-199">较长的错误消息说明发生了什么情况以及如何对它执行的操作：</span><span class="sxs-lookup"><span data-stu-id="e8439-199">A longer error message explains what happened and what to do about it:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="e8439-200">最后，代码设置`RowVersion`值`Department`从数据库中检索到的新值的对象。</span><span class="sxs-lookup"><span data-stu-id="e8439-200">Finally, the code sets the `RowVersion` value of the `Department` object to the new value retrieved from the database.</span></span> <span data-ttu-id="e8439-201">重新显示“编辑”页时，这个新的 `RowVersion` 值将存储在隐藏字段中，当用户下次单击“保存”时，将只捕获自“编辑”页重新显示起发生的并发错误。</span><span class="sxs-lookup"><span data-stu-id="e8439-201">This new `RowVersion` value will be stored in the hidden field when the Edit page is redisplayed, and the next time the user clicks **Save**, only concurrency errors that happen since the redisplay of the Edit page will be caught.</span></span>

<span data-ttu-id="e8439-202">在*Views\Department\Edit.cshtml*，添加隐藏的字段以保存`RowVersion`立即之后的隐藏的字段的属性值`DepartmentID`属性：</span><span class="sxs-lookup"><span data-stu-id="e8439-202">In *Views\Department\Edit.cshtml*, add a hidden field to save the `RowVersion` property value, immediately following the hidden field for the `DepartmentID` property:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="testing-optimistic-concurrency-handling"></a><span data-ttu-id="e8439-203">测试乐观并发处理</span><span class="sxs-lookup"><span data-stu-id="e8439-203">Testing Optimistic Concurrency Handling</span></span>

<span data-ttu-id="e8439-204">运行站点，然后单击**部门**:</span><span class="sxs-lookup"><span data-stu-id="e8439-204">Run the site and click **Departments**:</span></span>

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="e8439-206">右键单击**编辑**英语部门和选择的超链接**在新的选项卡中打开**然后单击**编辑**英语部门的超链接。</span><span class="sxs-lookup"><span data-stu-id="e8439-206">Right click the **Edit** hyperlink for the English department and select **Open in new tab,** then click the **Edit** hyperlink for the English department.</span></span> <span data-ttu-id="e8439-207">两个选项卡显示相同的信息。</span><span class="sxs-lookup"><span data-stu-id="e8439-207">The two tabs display the same information.</span></span>

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="e8439-209">在第一个浏览器选项卡中更改一个字段，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="e8439-209">Change a field in the first browser tab and click **Save**.</span></span>

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="e8439-211">浏览器显示具有更改值的索引页。</span><span class="sxs-lookup"><span data-stu-id="e8439-211">The browser shows the Index page with the changed value.</span></span>

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="e8439-213">更改第二个浏览器选项卡中的字段，然后单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="e8439-213">Change a field in the second browser tab and click **Save**.</span></span>

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="e8439-215">单击**保存**第二个浏览器选项卡中。看见一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="e8439-215">Click **Save** in the second browser tab. You see an error message:</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="e8439-217">再次单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="e8439-217">Click **Save** again.</span></span> <span data-ttu-id="e8439-218">在第二个浏览器选项卡中输入的值与在第一个浏览器中更改的数据的原始值一起保存。</span><span class="sxs-lookup"><span data-stu-id="e8439-218">The value you entered in the second browser tab is saved along with the original value of the data you changed in the first browser.</span></span> <span data-ttu-id="e8439-219">在索引页中出现时，可以看到已保存的值。</span><span class="sxs-lookup"><span data-stu-id="e8439-219">You see the saved values when the Index page appears.</span></span>

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a><span data-ttu-id="e8439-221">更新删除页</span><span class="sxs-lookup"><span data-stu-id="e8439-221">Updating the Delete Page</span></span>

<span data-ttu-id="e8439-222">对于“删除”页，Entity Framework 以类似方式检测其他人编辑院系所引起的并发冲突。</span><span class="sxs-lookup"><span data-stu-id="e8439-222">For the Delete page, the Entity Framework detects concurrency conflicts caused by someone else editing the department in a similar manner.</span></span> <span data-ttu-id="e8439-223">当`HttpGet``Delete`方法会显示确认视图，则视图包括原始`RowVersion`隐藏字段中的值。</span><span class="sxs-lookup"><span data-stu-id="e8439-223">When the `HttpGet` `Delete` method displays the confirmation view, the view includes the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="e8439-224">然后，该值将可供`HttpPost``Delete`用户确认删除时调用的方法。</span><span class="sxs-lookup"><span data-stu-id="e8439-224">That value is then available to the `HttpPost` `Delete` method that's called when the user confirms the deletion.</span></span> <span data-ttu-id="e8439-225">当实体框架创建 SQL`DELETE`命令时，它包括`WHERE`子句与原始`RowVersion`值。</span><span class="sxs-lookup"><span data-stu-id="e8439-225">When the Entity Framework creates the SQL `DELETE` command, it includes a `WHERE` clause with the original `RowVersion` value.</span></span> <span data-ttu-id="e8439-226">如果零行中的命令结果的影响 （含义后显示删除确认页，已更改行），则会引发一个并发异常，和`HttpGet Delete`调用方法时，将设置为错误标志`true`以重新显示确认页，并一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="e8439-226">If the command results in zero rows affected (meaning the row was changed after the Delete confirmation page was displayed), a concurrency exception is thrown, and the `HttpGet Delete` method is called with an error flag set to `true` in order to redisplay the confirmation page with an error message.</span></span> <span data-ttu-id="e8439-227">还有可能因为行由其他用户时，删除，因此不同的错误消息显示在此情况下影响了零行。</span><span class="sxs-lookup"><span data-stu-id="e8439-227">It's also possible that zero rows were affected because the row was deleted by another user, so in that case a different error message is displayed.</span></span>

<span data-ttu-id="e8439-228">在*DepartmentController.cs*，替换`HttpGet``Delete`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e8439-228">In *DepartmentController.cs*, replace the `HttpGet` `Delete` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="e8439-229">该方法接受可选参数，该参数指示是否在并发错误之后重新显示页面。</span><span class="sxs-lookup"><span data-stu-id="e8439-229">The method accepts an optional parameter that indicates whether the page is being redisplayed after a concurrency error.</span></span> <span data-ttu-id="e8439-230">如果此标志为`true`，一条错误消息发送到视图使用`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="e8439-230">If this flag is `true`, an error message is sent to the view using a `ViewBag` property.</span></span>

<span data-ttu-id="e8439-231">中的代码替换`HttpPost``Delete`方法 (名为`DeleteConfirmed`) 替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e8439-231">Replace the code in the `HttpPost` `Delete` method (named `DeleteConfirmed`) with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="e8439-232">在刚替换的基架代码中，此方法仅接受记录 ID：</span><span class="sxs-lookup"><span data-stu-id="e8439-232">In the scaffolded code that you just replaced, this method accepted only a record ID:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="e8439-233">你已更改此参数设为`Department`实体实例创建的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="e8439-233">You've changed this parameter to a `Department` entity instance created by the model binder.</span></span> <span data-ttu-id="e8439-234">这使您可以访问`RowVersion`除了的记录密钥的属性值。</span><span class="sxs-lookup"><span data-stu-id="e8439-234">This gives you access to the `RowVersion` property value in addition to the record key.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="e8439-235">你还将操作方法名称从`DeleteConfirmed`更改为了`Delete`。</span><span class="sxs-lookup"><span data-stu-id="e8439-235">You have also changed the action method name from `DeleteConfirmed` to `Delete`.</span></span> <span data-ttu-id="e8439-236">名为的基架的代码`HttpPost``Delete`方法`DeleteConfirmed`以便`HttpPost`方法一个唯一的签名。</span><span class="sxs-lookup"><span data-stu-id="e8439-236">The scaffolded code named the `HttpPost` `Delete` method `DeleteConfirmed` to give the `HttpPost` method a unique signature.</span></span> <span data-ttu-id="e8439-237">（CLR 需要具有不同的方法参数的重载的方法。）签名是唯一的现在可以坚持使用 MVC 约定，使用相同的名称用于`HttpPost`和`HttpGet`删除方法。</span><span class="sxs-lookup"><span data-stu-id="e8439-237">( The CLR requires overloaded methods to have different method parameters.) Now that the signatures are unique, you can stick with the MVC convention and use the same name for the `HttpPost` and `HttpGet` delete methods.</span></span>

<span data-ttu-id="e8439-238">如果捕获到并发错误，代码将重新显示“删除”确认页，并提供一个指示它应显示并发错误消息的标志。</span><span class="sxs-lookup"><span data-stu-id="e8439-238">If a concurrency error is caught, the code redisplays the Delete confirmation page and provides a flag that indicates it should display a concurrency error message.</span></span>

<span data-ttu-id="e8439-239">在*Views\Department\Delete.cshtml*，基架的代码替换为下面的代码用于添加一个错误消息字段和 DepartmentID 和 RowVersion 属性的隐藏的字段。</span><span class="sxs-lookup"><span data-stu-id="e8439-239">In *Views\Department\Delete.cshtml*, replace the scaffolded code with the following code that adds an error message field and hidden fields for the DepartmentID and RowVersion properties.</span></span> <span data-ttu-id="e8439-240">突出显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-240">The changes are highlighted.</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

<span data-ttu-id="e8439-241">此代码将添加一条错误消息之间`h2`和`h3`标题：</span><span class="sxs-lookup"><span data-stu-id="e8439-241">This code adds an error message between the `h2` and `h3` headings:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="e8439-242">它将替换`LastName`与`FullName`中`Administrator`字段：</span><span class="sxs-lookup"><span data-stu-id="e8439-242">It replaces `LastName` with `FullName` in the `Administrator` field:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="e8439-243">最后，它将添加隐藏的字段`DepartmentID`和`RowVersion`后的属性`Html.BeginForm`语句：</span><span class="sxs-lookup"><span data-stu-id="e8439-243">Finally, it adds hidden fields for the `DepartmentID` and `RowVersion` properties after the `Html.BeginForm` statement:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

<span data-ttu-id="e8439-244">运行部门索引页。</span><span class="sxs-lookup"><span data-stu-id="e8439-244">Run the Departments Index page.</span></span> <span data-ttu-id="e8439-245">右键单击**删除**英语部门和选择的超链接**在新的选项卡中打开**然后在第一个选项卡中单击**编辑**英语部门的超链接。</span><span class="sxs-lookup"><span data-stu-id="e8439-245">Right click the **Delete** hyperlink for the English department and select **Open in new tab,** then in the first tab click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="e8439-246">在第一个窗口中，更改一个值，然后单击**保存**:</span><span class="sxs-lookup"><span data-stu-id="e8439-246">In the first window, change one of the values, and click **Save** :</span></span>

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="e8439-248">索引页确认更改。</span><span class="sxs-lookup"><span data-stu-id="e8439-248">The Index page confirms the change.</span></span>

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="e8439-250">在第二个选项卡中，单击“删除”。</span><span class="sxs-lookup"><span data-stu-id="e8439-250">In the second tab, click **Delete**.</span></span>

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="e8439-252">你将看到并发错误消息，且已使用数据库中的当前内容刷新了“院系”值。</span><span class="sxs-lookup"><span data-stu-id="e8439-252">You see the concurrency error message, and the Department values are refreshed with what's currently in the database.</span></span>

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="e8439-254">如果再次单击**删除**，会重定向到索引页，表明院系已删除。</span><span class="sxs-lookup"><span data-stu-id="e8439-254">If you click **Delete** again, you're redirected to the Index page, which shows that the department has been deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="e8439-255">总结</span><span class="sxs-lookup"><span data-stu-id="e8439-255">Summary</span></span>

<span data-ttu-id="e8439-256">处理并发冲突已介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="e8439-256">This completes the introduction to handling concurrency conflicts.</span></span> <span data-ttu-id="e8439-257">有关其他方法来处理各种并发方案的信息，请参阅[乐观并发模式](https://msdn.microsoft.com/data/jj592904)和[使用属性值](https://msdn.microsoft.com/data/jj592677)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="e8439-257">For information about other ways to handle various concurrency scenarios, see [Optimistic Concurrency Patterns](https://msdn.microsoft.com/data/jj592904) and [Working with Property Values](https://msdn.microsoft.com/data/jj592677) on MSDN.</span></span> <span data-ttu-id="e8439-258">下一教程演示如何实现的每个层次结构一个表继承`Instructor`和`Student`实体。</span><span class="sxs-lookup"><span data-stu-id="e8439-258">The next tutorial shows how to implement table-per-hierarchy inheritance for the `Instructor` and `Student` entities.</span></span>

<span data-ttu-id="e8439-259">在找不到其他实体框架资源的链接[ASP.NET 数据访问的推荐资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="e8439-259">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e8439-260">[上一页](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="e8439-260">[Previous](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
