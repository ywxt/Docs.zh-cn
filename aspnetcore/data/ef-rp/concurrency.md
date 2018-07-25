---
title: ASP.NET Core 中的 Razor 页面和 EF Core - 并发 - 第 8 个教程（共 8 个）
author: rick-anderson
description: 本教程介绍如何处理多个用户同时更新同一实体时出现的冲突。
ms.author: riande
ms.date: 11/15/2017
uid: data/ef-rp/concurrency
ms.openlocfilehash: ff9e52df63f9c9f47ee659a68beb28b773a114a1
ms.sourcegitcommit: a3675f9704e4e73ecc7cbbbf016a13d2a5c4d725
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2018
ms.locfileid: "39202687"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---concurrency---8-of-8"></a><span data-ttu-id="8a17e-103">ASP.NET Core 中的 Razor 页面和 EF Core - 并发 - 第 8 个教程（共 8 个）</span><span class="sxs-lookup"><span data-stu-id="8a17e-103">Razor Pages with EF Core in ASP.NET Core - Concurrency - 8 of 8</span></span>

<span data-ttu-id="8a17e-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)、[Tom Dykstra](https://github.com/tdykstra) 和 [Jon P Smith](https://twitter.com/thereformedprog)</span><span class="sxs-lookup"><span data-stu-id="8a17e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), and [Jon P Smith](https://twitter.com/thereformedprog)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="8a17e-105">本教程介绍如何处理多个用户并发更新同一实体（同时）时出现的冲突。</span><span class="sxs-lookup"><span data-stu-id="8a17e-105">This tutorial shows how to handle conflicts when multiple users update an entity concurrently (at the same time).</span></span> <span data-ttu-id="8a17e-106">如果遇到无法解决的问题，请下载[本阶段的已完成应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part8)。</span><span class="sxs-lookup"><span data-stu-id="8a17e-106">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part8).</span></span>

## <a name="concurrency-conflicts"></a><span data-ttu-id="8a17e-107">并发冲突</span><span class="sxs-lookup"><span data-stu-id="8a17e-107">Concurrency conflicts</span></span>

<span data-ttu-id="8a17e-108">在以下情况下，会发生并发冲突：</span><span class="sxs-lookup"><span data-stu-id="8a17e-108">A concurrency conflict occurs when:</span></span>

* <span data-ttu-id="8a17e-109">用户导航到实体的编辑页面。</span><span class="sxs-lookup"><span data-stu-id="8a17e-109">A user navigates to the edit page for an entity.</span></span>
* <span data-ttu-id="8a17e-110">第一个用户的更改还未写入数据库之前，另一用户更新同一实体。</span><span class="sxs-lookup"><span data-stu-id="8a17e-110">Another user updates the same entity before the first user's change is written to the DB.</span></span>

<span data-ttu-id="8a17e-111">如果未启用并发检测，当发生并发更新时：</span><span class="sxs-lookup"><span data-stu-id="8a17e-111">If concurrency detection isn't enabled, when concurrent updates occur:</span></span>

* <span data-ttu-id="8a17e-112">最后一个更新优先。</span><span class="sxs-lookup"><span data-stu-id="8a17e-112">The last update wins.</span></span> <span data-ttu-id="8a17e-113">也就是最后一个更新的值保存至数据库。</span><span class="sxs-lookup"><span data-stu-id="8a17e-113">That is, the last update values are saved to the DB.</span></span>
* <span data-ttu-id="8a17e-114">第一个并发更新将会丢失。</span><span class="sxs-lookup"><span data-stu-id="8a17e-114">The first of the current updates are lost.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="8a17e-115">开放式并发</span><span class="sxs-lookup"><span data-stu-id="8a17e-115">Optimistic concurrency</span></span>

<span data-ttu-id="8a17e-116">乐观并发允许发生并发冲突，并在并发冲突发生时作出正确反应。</span><span class="sxs-lookup"><span data-stu-id="8a17e-116">Optimistic concurrency allows concurrency conflicts to happen, and then reacts appropriately when they do.</span></span> <span data-ttu-id="8a17e-117">例如，Jane 访问院系编辑页面，将英语系的预算从 350,000.00 美元更改为 0.00 美元。</span><span class="sxs-lookup"><span data-stu-id="8a17e-117">For example, Jane visits the Department edit page and changes the budget for the English department from $350,000.00 to $0.00.</span></span>

![将预算更改为零](concurrency/_static/change-budget.png)

<span data-ttu-id="8a17e-119">在 Jane 单击“保存”之前，John 访问了相同页面，并将开始日期字段从 2007/1/9 更改为 2013/1/9。</span><span class="sxs-lookup"><span data-stu-id="8a17e-119">Before Jane clicks **Save**, John visits the same page and changes the Start Date field from 9/1/2007 to 9/1/2013.</span></span>

![将开始日期更改为 2013](concurrency/_static/change-date.png)

<span data-ttu-id="8a17e-121">Jane 先单击“保存”，并在浏览器显示索引页时看到她的更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-121">Jane clicks **Save** first and sees her change when the browser displays the Index page.</span></span>

![预算已更改为零](concurrency/_static/budget-zero.png)

<span data-ttu-id="8a17e-123">John 单击“编辑”页面上的“保存”，但页面的预算仍显示为 350,000.00 美元。</span><span class="sxs-lookup"><span data-stu-id="8a17e-123">John clicks **Save** on an Edit page that still shows a budget of $350,000.00.</span></span> <span data-ttu-id="8a17e-124">接下来的情况取决于并发冲突的处理方式。</span><span class="sxs-lookup"><span data-stu-id="8a17e-124">What happens next is determined by how you handle concurrency conflicts.</span></span>

<span data-ttu-id="8a17e-125">乐观并发包括以下选项：</span><span class="sxs-lookup"><span data-stu-id="8a17e-125">Optimistic concurrency includes the following options:</span></span>

* <span data-ttu-id="8a17e-126">可以跟踪用户已修改的属性，并仅更新数据库中相应的列。</span><span class="sxs-lookup"><span data-stu-id="8a17e-126">You can keep track of which property a user has modified and update only the corresponding columns in the DB.</span></span>

  <span data-ttu-id="8a17e-127">在这种情况下，数据不会丢失。</span><span class="sxs-lookup"><span data-stu-id="8a17e-127">In the scenario, no data would be lost.</span></span> <span data-ttu-id="8a17e-128">两个用户更新了不同的属性。</span><span class="sxs-lookup"><span data-stu-id="8a17e-128">Different properties were updated by the two users.</span></span> <span data-ttu-id="8a17e-129">下次有人浏览英语系时，将看到 Jane 和 John 两个人的更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-129">The next time someone browses the English department, they will see both Jane's and John's changes.</span></span> <span data-ttu-id="8a17e-130">这种更新方法可以减少导致数据丢失的冲突数。</span><span class="sxs-lookup"><span data-stu-id="8a17e-130">This method of updating can reduce the number of conflicts that could result in data loss.</span></span> <span data-ttu-id="8a17e-131">这种方法：</span><span class="sxs-lookup"><span data-stu-id="8a17e-131">This approach:</span></span>
 
  * <span data-ttu-id="8a17e-132">无法避免数据丢失，如果对同一属性进行竞争性更改的话。</span><span class="sxs-lookup"><span data-stu-id="8a17e-132">Can't avoid data loss if competing changes are made to the same property.</span></span>
  * <span data-ttu-id="8a17e-133">通常不适用于 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a17e-133">Is generally not practical in a web app.</span></span> <span data-ttu-id="8a17e-134">它需要维持重要状态，以便跟踪所有提取值和新值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-134">It requires maintaining significant state in order to keep track of all fetched values and new values.</span></span> <span data-ttu-id="8a17e-135">维持大量状态可能影响应用性能。</span><span class="sxs-lookup"><span data-stu-id="8a17e-135">Maintaining large amounts of state can affect app performance.</span></span>
  * <span data-ttu-id="8a17e-136">可能会增加应用复杂性（与实体上的并发检测相比）。</span><span class="sxs-lookup"><span data-stu-id="8a17e-136">Can increase app complexity compared to concurrency detection on an entity.</span></span>

* <span data-ttu-id="8a17e-137">可让 John 的更改覆盖 Jane 的更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-137">You can let John's change overwrite Jane's change.</span></span>

  <span data-ttu-id="8a17e-138">下次有人浏览英语系时，将看到 2013/9/1 和提取的值 350,000.00 美元。</span><span class="sxs-lookup"><span data-stu-id="8a17e-138">The next time someone browses the English department, they will see 9/1/2013 and the fetched $350,000.00 value.</span></span> <span data-ttu-id="8a17e-139">这种方法称为“客户端优先”或“最后一个优先”方案。</span><span class="sxs-lookup"><span data-stu-id="8a17e-139">This approach is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="8a17e-140">（客户端的所有值优先于数据存储的值。）如果不对并发处理进行任何编码，则自动执行“客户端优先”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-140">(All values from the client take precedence over what's in the data store.) If you don't do any coding for concurrency handling, Client Wins happens automatically.</span></span>

* <span data-ttu-id="8a17e-141">可以阻止在数据库中更新 John 的更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-141">You can prevent John's change from being updated in the DB.</span></span> <span data-ttu-id="8a17e-142">应用通常会：</span><span class="sxs-lookup"><span data-stu-id="8a17e-142">Typically, the app would:</span></span>

  * <span data-ttu-id="8a17e-143">显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="8a17e-143">Display an error message.</span></span>
  * <span data-ttu-id="8a17e-144">显示数据的当前状态。</span><span class="sxs-lookup"><span data-stu-id="8a17e-144">Show the current state of the data.</span></span>
  * <span data-ttu-id="8a17e-145">允许用户重新应用更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-145">Allow the user to reapply the changes.</span></span>

  <span data-ttu-id="8a17e-146">这称为“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="8a17e-146">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="8a17e-147">（数据存储值优先于客户端提交的值。）本教程实施“存储优先”方案。</span><span class="sxs-lookup"><span data-stu-id="8a17e-147">(The data-store values take precedence over the values submitted by the client.) You implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="8a17e-148">此方法可确保用户在未收到警报时不会覆盖任何更改。</span><span class="sxs-lookup"><span data-stu-id="8a17e-148">This method ensures that no changes are overwritten without a user being alerted.</span></span>

## <a name="handling-concurrency"></a><span data-ttu-id="8a17e-149">处理并发</span><span class="sxs-lookup"><span data-stu-id="8a17e-149">Handling concurrency</span></span> 

<span data-ttu-id="8a17e-150">当属性配置为[并发令牌](https://docs.microsoft.com/ef/core/modeling/concurrency)时：</span><span class="sxs-lookup"><span data-stu-id="8a17e-150">When a property is configured as a [concurrency token](https://docs.microsoft.com/ef/core/modeling/concurrency):</span></span>

* <span data-ttu-id="8a17e-151">EF Core 验证提取属性后是否未更改属性。</span><span class="sxs-lookup"><span data-stu-id="8a17e-151">EF Core verifies that property has not been modified after it was fetched.</span></span> <span data-ttu-id="8a17e-152">调用 [SaveChanges](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChanges) 或 [SaveChangesAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) 时会执行此检查。</span><span class="sxs-lookup"><span data-stu-id="8a17e-152">The check occurs when [SaveChanges](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChanges) or [SaveChangesAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) is called.</span></span>
* <span data-ttu-id="8a17e-153">如果提取属性后更改了属性，将引发 [DbUpdateConcurrencyException](/dotnet/api/microsoft.entityframeworkcore.dbupdateconcurrencyexception?view=efcore-2.0)。</span><span class="sxs-lookup"><span data-stu-id="8a17e-153">If the property has been changed after it was fetched, a [DbUpdateConcurrencyException](/dotnet/api/microsoft.entityframeworkcore.dbupdateconcurrencyexception?view=efcore-2.0) is thrown.</span></span> 

<span data-ttu-id="8a17e-154">数据库和数据模型必须配置为支持引发 `DbUpdateConcurrencyException`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-154">The DB and data model must be configured to support throwing `DbUpdateConcurrencyException`.</span></span>

### <a name="detecting-concurrency-conflicts-on-a-property"></a><span data-ttu-id="8a17e-155">检测属性的并发冲突</span><span class="sxs-lookup"><span data-stu-id="8a17e-155">Detecting concurrency conflicts on a property</span></span>

<span data-ttu-id="8a17e-156">可使用 [ConcurrencyCheck](/dotnet/api/system.componentmodel.dataannotations.concurrencycheckattribute?view=netcore-2.0) 特性在属性级别检测并发冲突。</span><span class="sxs-lookup"><span data-stu-id="8a17e-156">Concurrency conflicts can be detected at the property level with the [ConcurrencyCheck](/dotnet/api/system.componentmodel.dataannotations.concurrencycheckattribute?view=netcore-2.0) attribute.</span></span> <span data-ttu-id="8a17e-157">该特性可应用于模型上的多个属性。</span><span class="sxs-lookup"><span data-stu-id="8a17e-157">The attribute can be applied to multiple properties on the model.</span></span> <span data-ttu-id="8a17e-158">有关详细信息，请参阅[数据注释 - ConcurrencyCheck](/ef/core/modeling/concurrency#data-annotations)。</span><span class="sxs-lookup"><span data-stu-id="8a17e-158">For more information, see [Data Annotations-ConcurrencyCheck](/ef/core/modeling/concurrency#data-annotations).</span></span>

<span data-ttu-id="8a17e-159">本教程中不使用 `[ConcurrencyCheck]` 特性。</span><span class="sxs-lookup"><span data-stu-id="8a17e-159">The `[ConcurrencyCheck]` attribute isn't used in this tutorial.</span></span>

### <a name="detecting-concurrency-conflicts-on-a-row"></a><span data-ttu-id="8a17e-160">检测行的并发冲突</span><span class="sxs-lookup"><span data-stu-id="8a17e-160">Detecting concurrency conflicts on a row</span></span>

<span data-ttu-id="8a17e-161">要检测并发冲突，请将 [rowversion](/sql/t-sql/data-types/rowversion-transact-sql) 跟踪列添加到模型。</span><span class="sxs-lookup"><span data-stu-id="8a17e-161">To detect concurrency conflicts, a [rowversion](/sql/t-sql/data-types/rowversion-transact-sql) tracking column is added to the model.</span></span>  <span data-ttu-id="8a17e-162">`rowversion`：</span><span class="sxs-lookup"><span data-stu-id="8a17e-162">`rowversion` :</span></span>

* <span data-ttu-id="8a17e-163">是 SQL Server 特定的。</span><span class="sxs-lookup"><span data-stu-id="8a17e-163">Is SQL Server specific.</span></span> <span data-ttu-id="8a17e-164">其他数据库可能无法提供类似功能。</span><span class="sxs-lookup"><span data-stu-id="8a17e-164">Other databases may not provide a similar feature.</span></span>
* <span data-ttu-id="8a17e-165">用于确定从数据库提取实体后未更改实体。</span><span class="sxs-lookup"><span data-stu-id="8a17e-165">Is used to determine that an entity has not been changed since it was fetched from the DB.</span></span> 

<span data-ttu-id="8a17e-166">数据库生成 `rowversion` 序号，该数字随着每次行的更新递增。</span><span class="sxs-lookup"><span data-stu-id="8a17e-166">The DB generates a sequential `rowversion` number that's incremented each time the row is updated.</span></span> <span data-ttu-id="8a17e-167">在 `Update` 或 `Delete` 命令中，`Where` 子句包括 `rowversion` 的提取值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-167">In an `Update` or `Delete` command, the `Where` clause includes the fetched value of `rowversion`.</span></span> <span data-ttu-id="8a17e-168">如果要更新的行已更改：</span><span class="sxs-lookup"><span data-stu-id="8a17e-168">If the row being updated has changed:</span></span>

 * <span data-ttu-id="8a17e-169">`rowversion` 不匹配提取值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-169">`rowversion` doesn't match the fetched value.</span></span>
 * <span data-ttu-id="8a17e-170">`Update` 或 `Delete` 命令不能找到行，因为 `Where` 子句包含提取的 `rowversion`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-170">The `Update` or `Delete` commands don't find a row because the `Where` clause includes the fetched `rowversion`.</span></span>
 * <span data-ttu-id="8a17e-171">引发一个 `DbUpdateConcurrencyException`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-171">A `DbUpdateConcurrencyException` is thrown.</span></span>

<span data-ttu-id="8a17e-172">在 EF Core 中，如果未通过 `Update` 或 `Delete` 命令更新行，则引发并发异常。</span><span class="sxs-lookup"><span data-stu-id="8a17e-172">In EF Core, when no rows have been updated by an `Update` or `Delete` command, a concurrency exception is thrown.</span></span>

### <a name="add-a-tracking-property-to-the-department-entity"></a><span data-ttu-id="8a17e-173">向 Department 实体添加跟踪属性</span><span class="sxs-lookup"><span data-stu-id="8a17e-173">Add a tracking property to the Department entity</span></span>

<span data-ttu-id="8a17e-174">在 Models/Department.cs 中，添加名为 RowVersion 的跟踪属性：</span><span class="sxs-lookup"><span data-stu-id="8a17e-174">In *Models/Department.cs*, add a tracking property named RowVersion:</span></span>

[!code-csharp[](intro/samples/cu/Models/Department.cs?name=snippet_Final&highlight=26,27)]

<span data-ttu-id="8a17e-175">[Timestamp](/dotnet/api/system.componentmodel.dataannotations.timestampattribute) 特性指定此列包含在 `Update` 和 `Delete` 命令的 `Where` 子句中。</span><span class="sxs-lookup"><span data-stu-id="8a17e-175">The [Timestamp](/dotnet/api/system.componentmodel.dataannotations.timestampattribute) attribute specifies that this column is included in the `Where` clause of `Update` and `Delete` commands.</span></span> <span data-ttu-id="8a17e-176">该特性称为 `Timestamp`，因为之前版本的 SQL Server 在 SQL `rowversion` 类型将其替换之前使用 SQL `timestamp` 数据类型。</span><span class="sxs-lookup"><span data-stu-id="8a17e-176">The attribute is called `Timestamp` because previous versions of SQL Server used a SQL `timestamp` data type before the SQL `rowversion` type replaced it.</span></span>

<span data-ttu-id="8a17e-177">Fluent API 还可指定跟踪属性：</span><span class="sxs-lookup"><span data-stu-id="8a17e-177">The fluent API can also specify the tracking property:</span></span>

```csharp
modelBuilder.Entity<Department>()
  .Property<byte[]>("RowVersion")
  .IsRowVersion();
```

<span data-ttu-id="8a17e-178">以下代码显示更新 Department 名称时由 EF Core 生成的部分 T-SQL：</span><span class="sxs-lookup"><span data-stu-id="8a17e-178">The following code shows a portion of the T-SQL generated by EF Core when the Department name is updated:</span></span>

[!code-sql[](intro/samples/sql.txt?highlight=2-3)]

<span data-ttu-id="8a17e-179">前面突出显示的代码显示包含 `RowVersion` 的 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="8a17e-179">The preceding highlighted code shows the `WHERE` clause containing `RowVersion`.</span></span> <span data-ttu-id="8a17e-180">如果数据库 `RowVersion` 不等于 `RowVersion` 参数（`@p2`），则不更新行。</span><span class="sxs-lookup"><span data-stu-id="8a17e-180">If the DB `RowVersion` doesn't equal the `RowVersion` parameter (`@p2`), no rows are updated.</span></span>

<span data-ttu-id="8a17e-181">以下突出显示的代码显示验证更新哪一行的 T-SQL：</span><span class="sxs-lookup"><span data-stu-id="8a17e-181">The following highlighted code shows the T-SQL that verifies exactly one row was updated:</span></span>

[!code-sql[](intro/samples/sql.txt?highlight=4-6)]

<span data-ttu-id="8a17e-182">[@@ROWCOUNT](/sql/t-sql/functions/rowcount-transact-sql) 返回受上一语句影响的行数。</span><span class="sxs-lookup"><span data-stu-id="8a17e-182">[@@ROWCOUNT](/sql/t-sql/functions/rowcount-transact-sql) returns the number of rows affected by the last statement.</span></span> <span data-ttu-id="8a17e-183">在没有行更新的情况下，EF Core 引发 `DbUpdateConcurrencyException`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-183">In no rows are updated, EF Core throws a `DbUpdateConcurrencyException`.</span></span>

<span data-ttu-id="8a17e-184">在 Visual Studio 的输出窗口中可看见 EF Core 生成的 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="8a17e-184">You can see the T-SQL EF Core generates in the output window of Visual Studio.</span></span>

### <a name="update-the-db"></a><span data-ttu-id="8a17e-185">更新数据库</span><span class="sxs-lookup"><span data-stu-id="8a17e-185">Update the DB</span></span>

<span data-ttu-id="8a17e-186">添加 `RowVersion` 属性可更改数据库模型，这需要迁移。</span><span class="sxs-lookup"><span data-stu-id="8a17e-186">Adding the `RowVersion` property changes the DB model, which requires a migration.</span></span>

<span data-ttu-id="8a17e-187">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8a17e-187">Build the project.</span></span> <span data-ttu-id="8a17e-188">在命令窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="8a17e-188">Enter the following in a command window:</span></span>

```console
dotnet ef migrations add RowVersion
dotnet ef database update
```

<span data-ttu-id="8a17e-189">前面的命令：</span><span class="sxs-lookup"><span data-stu-id="8a17e-189">The preceding commands:</span></span>

* <span data-ttu-id="8a17e-190">添加 Migrations/{time stamp}_RowVersion.cs 迁移文件。</span><span class="sxs-lookup"><span data-stu-id="8a17e-190">Adds the *Migrations/{time stamp}_RowVersion.cs* migration file.</span></span>
* <span data-ttu-id="8a17e-191">更新 Migrations/SchoolContextModelSnapshot.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="8a17e-191">Updates the *Migrations/SchoolContextModelSnapshot.cs* file.</span></span> <span data-ttu-id="8a17e-192">此次更新将以下突出显示的代码添加到 `BuildModel` 方法：</span><span class="sxs-lookup"><span data-stu-id="8a17e-192">The update adds the following highlighted code to the `BuildModel` method:</span></span>

  [!code-csharp[](intro/samples/cu/Migrations/SchoolContextModelSnapshot2.cs?name=snippet&highlight=14-16)]

* <span data-ttu-id="8a17e-193">运行迁移以更新数据库。</span><span class="sxs-lookup"><span data-stu-id="8a17e-193">Runs migrations to update the DB.</span></span>

<a name="scaffold"></a>
## <a name="scaffold-the-departments-model"></a><span data-ttu-id="8a17e-194">构架院系模型</span><span class="sxs-lookup"><span data-stu-id="8a17e-194">Scaffold the Departments model</span></span>

* <span data-ttu-id="8a17e-195">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8a17e-195">Exit Visual Studio.</span></span>
* <span data-ttu-id="8a17e-196">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="8a17e-196">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="8a17e-197">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="8a17e-197">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Department -dc SchoolContext -udl -outDir Pages\Departments --referenceScriptLibraries
  ```

<span data-ttu-id="8a17e-198">上述命令为 `Department` 模型创建基架。</span><span class="sxs-lookup"><span data-stu-id="8a17e-198">The preceding command scaffolds the `Department` model.</span></span> <span data-ttu-id="8a17e-199">在 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="8a17e-199">Open the project in Visual Studio.</span></span>

<span data-ttu-id="8a17e-200">生成项目。</span><span class="sxs-lookup"><span data-stu-id="8a17e-200">Build the project.</span></span> <span data-ttu-id="8a17e-201">此版本生成如下错误：</span><span class="sxs-lookup"><span data-stu-id="8a17e-201">The build generates errors like the following:</span></span>

`1>Pages/Departments/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Department' and no extension method 'Department' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 <span data-ttu-id="8a17e-202">将 `_context.Department` 全局更改为 `_context.Departments`（即向 `Department` 添加一个“s”）。</span><span class="sxs-lookup"><span data-stu-id="8a17e-202">Globally change `_context.Department` to `_context.Departments` (that is, add an "s" to `Department`).</span></span> <span data-ttu-id="8a17e-203">找到并更新 7 个匹配项。</span><span class="sxs-lookup"><span data-stu-id="8a17e-203">7 occurrences are found and updated.</span></span>

### <a name="update-the-departments-index-page"></a><span data-ttu-id="8a17e-204">更新院系索引页</span><span class="sxs-lookup"><span data-stu-id="8a17e-204">Update the Departments Index page</span></span>

<span data-ttu-id="8a17e-205">基架引擎为索引页创建 `RowVersion` 列，但不应显示该字段。</span><span class="sxs-lookup"><span data-stu-id="8a17e-205">The scaffolding engine created a `RowVersion` column for the Index page, but that field shouldn't be displayed.</span></span> <span data-ttu-id="8a17e-206">本教程中显示 `RowVersion` 的最后一个字节，以帮助理解并发。</span><span class="sxs-lookup"><span data-stu-id="8a17e-206">In this tutorial, the last byte of the `RowVersion` is displayed to help understand concurrency.</span></span> <span data-ttu-id="8a17e-207">不能保证最后一个字节是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8a17e-207">The last byte isn't guaranteed to be unique.</span></span> <span data-ttu-id="8a17e-208">实际应用不会显示 `RowVersion` 或 `RowVersion` 的最后一个字节。</span><span class="sxs-lookup"><span data-stu-id="8a17e-208">A real app wouldn't display `RowVersion` or the last byte of `RowVersion`.</span></span>

<span data-ttu-id="8a17e-209">更新索引页：</span><span class="sxs-lookup"><span data-stu-id="8a17e-209">Update the Index page:</span></span>

* <span data-ttu-id="8a17e-210">用院系替换索引。</span><span class="sxs-lookup"><span data-stu-id="8a17e-210">Replace Index with Departments.</span></span>
* <span data-ttu-id="8a17e-211">将包含 `RowVersion` 的标记替换为 `RowVersion` 的最后一个字节。</span><span class="sxs-lookup"><span data-stu-id="8a17e-211">Replace the markup containing `RowVersion` with the last byte of `RowVersion`.</span></span>
* <span data-ttu-id="8a17e-212">将 FirstMidName 替换为 FullName。</span><span class="sxs-lookup"><span data-stu-id="8a17e-212">Replace FirstMidName with FullName.</span></span>

<span data-ttu-id="8a17e-213">以下标记显示更新后的页面：</span><span class="sxs-lookup"><span data-stu-id="8a17e-213">The following markup shows the updated page:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Index.cshtml?highlight=5,8,29,47,50)]

### <a name="update-the-edit-page-model"></a><span data-ttu-id="8a17e-214">更新编辑页模型</span><span class="sxs-lookup"><span data-stu-id="8a17e-214">Update the Edit page model</span></span>

<span data-ttu-id="8a17e-215">使用以下代码更新 pages\departments\edit.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="8a17e-215">Update *pages\departments\edit.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet)]

<span data-ttu-id="8a17e-216">要检测并发问题，请使用来自所提取实体的 `rowVersion` 值更新 [OriginalValue](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyentry.originalvalue?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyEntry_OriginalValue)。</span><span class="sxs-lookup"><span data-stu-id="8a17e-216">To detect a concurrency issue, the [OriginalValue](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyentry.originalvalue?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyEntry_OriginalValue) is updated with the `rowVersion` value from the entity it was fetched.</span></span> <span data-ttu-id="8a17e-217">EF Core 使用包含原始 `RowVersion` 值的 WHERE 子句生成 SQL UPDATE 命令。</span><span class="sxs-lookup"><span data-stu-id="8a17e-217">EF Core generates a SQL UPDATE command with a WHERE clause containing the original `RowVersion` value.</span></span> <span data-ttu-id="8a17e-218">如果没有行受到 UPDATE 命令影响（没有行具有原始 `RowVersion` 值），将引发 `DbUpdateConcurrencyException` 异常。</span><span class="sxs-lookup"><span data-stu-id="8a17e-218">If no rows are affected by the UPDATE command (no rows have the original `RowVersion` value), a `DbUpdateConcurrencyException` exception is thrown.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_rv&highlight=24-999)]

<span data-ttu-id="8a17e-219">在前面的代码中，`Department.RowVersion` 为实体提取后的值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-219">In the preceding code, `Department.RowVersion` is the value when the entity was fetched.</span></span> <span data-ttu-id="8a17e-220">使用此方法调用 `FirstOrDefaultAsync` 时，`OriginalValue` 为数据库中的值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-220">`OriginalValue` is the value in the DB when `FirstOrDefaultAsync` was called in this method.</span></span>

<span data-ttu-id="8a17e-221">以下代码获取客户端值（向此方法发布的值）和数据库值：</span><span class="sxs-lookup"><span data-stu-id="8a17e-221">The following code gets the client values (the values posted to this method) and the DB values:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=9,18)]

<span data-ttu-id="8a17e-222">以下代码为每列添加自定义错误消息，这些列中的数据库值与发布到 `OnPostAsync` 的值不同：</span><span class="sxs-lookup"><span data-stu-id="8a17e-222">The follwing code adds a custom error message for each column that has DB values different from what was posted to `OnPostAsync`:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_err)]

<span data-ttu-id="8a17e-223">以下突出显示的代码将 `RowVersion` 值设置为从数据库检索的新值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-223">The following highlighted code sets the `RowVersion` value to the new value retrieved from the DB.</span></span> <span data-ttu-id="8a17e-224">用户下次单击“保存”时，将仅捕获最后一次显示编辑页后发生的并发错误。</span><span class="sxs-lookup"><span data-stu-id="8a17e-224">The next time the user clicks **Save**, only concurrency errors that happen since the last display of the Edit page will be caught.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=23)]

<span data-ttu-id="8a17e-225">`ModelState` 具有旧的 `RowVersion` 值，因此需使用 `ModelState.Remove` 语句。</span><span class="sxs-lookup"><span data-stu-id="8a17e-225">The `ModelState.Remove` statement is required because `ModelState` has the old `RowVersion` value.</span></span> <span data-ttu-id="8a17e-226">在 Razor 页面中，当两者都存在时，字段的 `ModelState` 值优于模型属性值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-226">In the Razor Page, the `ModelState` value for a field takes precedence over the model property values when both are present.</span></span>

## <a name="update-the-edit-page"></a><span data-ttu-id="8a17e-227">更新“编辑”页</span><span class="sxs-lookup"><span data-stu-id="8a17e-227">Update the Edit page</span></span>

<span data-ttu-id="8a17e-228">使用以下标记更新 Pages/Departments/Edit.cshtml：</span><span class="sxs-lookup"><span data-stu-id="8a17e-228">Update *Pages/Departments/Edit.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Edit.cshtml?highlight=1,14,16-17,37-39)]

<span data-ttu-id="8a17e-229">前面的标记：</span><span class="sxs-lookup"><span data-stu-id="8a17e-229">The preceding markup:</span></span>

* <span data-ttu-id="8a17e-230">将 `page` 指令从 `@page` 更新为 `@page "{id:int}"`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-230">Updates the `page` directive from `@page` to `@page "{id:int}"`.</span></span>
* <span data-ttu-id="8a17e-231">添加隐藏的行版本。</span><span class="sxs-lookup"><span data-stu-id="8a17e-231">Adds a hidden row version.</span></span> <span data-ttu-id="8a17e-232">必须添加 `RowVersion`，以便回发绑定值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-232">`RowVersion` must be added so post back binds the value.</span></span>
* <span data-ttu-id="8a17e-233">显示 `RowVersion` 的最后一个字节以进行调试。</span><span class="sxs-lookup"><span data-stu-id="8a17e-233">Displays the last byte of `RowVersion` for debugging purposes.</span></span>
* <span data-ttu-id="8a17e-234">将 `ViewData` 替换为强类型 `InstructorNameSL`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-234">Replaces `ViewData` with the strongly-typed `InstructorNameSL`.</span></span>

## <a name="test-concurrency-conflicts-with-the-edit-page"></a><span data-ttu-id="8a17e-235">使用编辑页测试并发冲突</span><span class="sxs-lookup"><span data-stu-id="8a17e-235">Test concurrency conflicts with the Edit page</span></span>

<span data-ttu-id="8a17e-236">在英语系打开编辑的两个浏览器实例：</span><span class="sxs-lookup"><span data-stu-id="8a17e-236">Open two browsers instances of Edit on the English department:</span></span>

* <span data-ttu-id="8a17e-237">运行应用，然后选择“院系”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-237">Run the app and select Departments.</span></span>
* <span data-ttu-id="8a17e-238">右键单击英语系的“编辑”超链接，然后选择“在新选项卡中打开”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-238">Right-click the **Edit** hyperlink for the English department and select **Open in new tab**.</span></span>
* <span data-ttu-id="8a17e-239">在第一个选项卡中，单击英语系的“编辑”超链接。</span><span class="sxs-lookup"><span data-stu-id="8a17e-239">In the first tab, click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="8a17e-240">两个浏览器选项卡显示相同信息。</span><span class="sxs-lookup"><span data-stu-id="8a17e-240">The two browser tabs display the same information.</span></span>

<span data-ttu-id="8a17e-241">在第一个浏览器选项卡中更改名称，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-241">Change the name in the first browser tab and click **Save**.</span></span>

![更改后的“院系编辑”页 1](concurrency/_static/edit-after-change-1.png)

<span data-ttu-id="8a17e-243">浏览器显示更改值并更新 rowVersion 标记后的索引页。</span><span class="sxs-lookup"><span data-stu-id="8a17e-243">The browser shows the Index page with the changed value and updated rowVersion indicator.</span></span> <span data-ttu-id="8a17e-244">请注意更新后的 rowVersion 标记，它在其他选项卡的第二回发中显示。</span><span class="sxs-lookup"><span data-stu-id="8a17e-244">Note the updated rowVersion indicator, it's displayed on the second postback in the other tab.</span></span>

<span data-ttu-id="8a17e-245">在第二个浏览器选项卡中更改不同字段。</span><span class="sxs-lookup"><span data-stu-id="8a17e-245">Change a different field in the second browser tab.</span></span>

![更改后的“院系编辑”页 2](concurrency/_static/edit-after-change-2.png)

<span data-ttu-id="8a17e-247">单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="8a17e-247">Click **Save**.</span></span> <span data-ttu-id="8a17e-248">可看见所有不匹配数据库值的字段的错误消息：</span><span class="sxs-lookup"><span data-stu-id="8a17e-248">You see error messages for all fields that don't match the DB values:</span></span>

![“院系编辑”页错误消息](concurrency/_static/edit-error.png)

<span data-ttu-id="8a17e-250">此浏览器窗口将不会更改名称字段。</span><span class="sxs-lookup"><span data-stu-id="8a17e-250">This browser window didn't intend to change the Name field.</span></span> <span data-ttu-id="8a17e-251">将当前值（语言）复制并粘贴到名称字段。</span><span class="sxs-lookup"><span data-stu-id="8a17e-251">Copy and paste the current value (Languages) into the Name field.</span></span> <span data-ttu-id="8a17e-252">退出选项卡。客户端验证将删除错误消息。</span><span class="sxs-lookup"><span data-stu-id="8a17e-252">Tab out. Client-side validation removes the error message.</span></span>

![“院系编辑”页错误消息](concurrency/_static/cv.png)

<span data-ttu-id="8a17e-254">再次单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-254">Click **Save** again.</span></span> <span data-ttu-id="8a17e-255">保存在第二个浏览器选项卡中输入的值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-255">The value you entered in the second browser tab is saved.</span></span> <span data-ttu-id="8a17e-256">在索引页中可以看到保存的值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-256">You see the saved values in the Index page.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="8a17e-257">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="8a17e-257">Update the Delete page</span></span>

<span data-ttu-id="8a17e-258">使用以下代码更新“删除”页模型：</span><span class="sxs-lookup"><span data-stu-id="8a17e-258">Update the Delete page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Delete.cshtml.cs)]

<span data-ttu-id="8a17e-259">删除页检测提取实体并更改时的并发冲突。</span><span class="sxs-lookup"><span data-stu-id="8a17e-259">The Delete page detects concurrency conflicts when the entity has changed after it was fetched.</span></span> <span data-ttu-id="8a17e-260">提取实体后，`Department.RowVersion` 为行版本。</span><span class="sxs-lookup"><span data-stu-id="8a17e-260">`Department.RowVersion` is the row version when the entity was fetched.</span></span> <span data-ttu-id="8a17e-261">EF Core 创建 SQL DELETE 命令时，它包括具有 `RowVersion` 的 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="8a17e-261">When EF Core creates the SQL DELETE command, it includes a WHERE clause with `RowVersion`.</span></span> <span data-ttu-id="8a17e-262">如果 SQL DELETE 命令导致零行受影响：</span><span class="sxs-lookup"><span data-stu-id="8a17e-262">If the SQL DELETE command results in zero rows affected:</span></span>

* <span data-ttu-id="8a17e-263">SQL DELETE 命令中的 `RowVersion` 与数据库中的 `RowVersion` 不匹配。</span><span class="sxs-lookup"><span data-stu-id="8a17e-263">The `RowVersion` in the SQL DELETE command doesn't match `RowVersion` in the DB.</span></span>
* <span data-ttu-id="8a17e-264">引发 DbUpdateConcurrencyException 异常。</span><span class="sxs-lookup"><span data-stu-id="8a17e-264">A DbUpdateConcurrencyException exception is thrown.</span></span>
* <span data-ttu-id="8a17e-265">使用 `concurrencyError` 调用 `OnGetAsync`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-265">`OnGetAsync` is called with the `concurrencyError`.</span></span>

### <a name="update-the-delete-page"></a><span data-ttu-id="8a17e-266">更新“删除”页</span><span class="sxs-lookup"><span data-stu-id="8a17e-266">Update the Delete page</span></span>

<span data-ttu-id="8a17e-267">使用以下代码更新 Pages/Departments/Delete.cshtml：</span><span class="sxs-lookup"><span data-stu-id="8a17e-267">Update *Pages/Departments/Delete.cshtml* with the following code:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Delete.cshtml?highlight=1,10,36,51)]


<span data-ttu-id="8a17e-268">上述标记进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="8a17e-268">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="8a17e-269">将 `page` 指令从 `@page` 更新为 `@page "{id:int}"`。</span><span class="sxs-lookup"><span data-stu-id="8a17e-269">Updates the `page` directive from `@page` to `@page "{id:int}"`.</span></span>
* <span data-ttu-id="8a17e-270">添加错误消息。</span><span class="sxs-lookup"><span data-stu-id="8a17e-270">Adds an error message.</span></span>
* <span data-ttu-id="8a17e-271">将“管理员”字段中的 FirstMidName 替换为 FullName。</span><span class="sxs-lookup"><span data-stu-id="8a17e-271">Replaces FirstMidName with FullName in the **Administrator** field.</span></span>
* <span data-ttu-id="8a17e-272">更改 `RowVersion` 以显示最后一个字节。</span><span class="sxs-lookup"><span data-stu-id="8a17e-272">Changes `RowVersion` to display the last byte.</span></span>
* <span data-ttu-id="8a17e-273">添加隐藏的行版本。</span><span class="sxs-lookup"><span data-stu-id="8a17e-273">Adds a hidden row version.</span></span> <span data-ttu-id="8a17e-274">必须添加 `RowVersion`，以便回发绑定值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-274">`RowVersion` must be added so post back binds the value.</span></span>

### <a name="test-concurrency-conflicts-with-the-delete-page"></a><span data-ttu-id="8a17e-275">使用删除页测试并发冲突</span><span class="sxs-lookup"><span data-stu-id="8a17e-275">Test concurrency conflicts with the Delete page</span></span>

<span data-ttu-id="8a17e-276">创建测试系。</span><span class="sxs-lookup"><span data-stu-id="8a17e-276">Create a test department.</span></span>

<span data-ttu-id="8a17e-277">在测试系打开删除的两个浏览器实例：</span><span class="sxs-lookup"><span data-stu-id="8a17e-277">Open two browsers instances of Delete on the test department:</span></span>

* <span data-ttu-id="8a17e-278">运行应用，然后选择“院系”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-278">Run the app and select Departments.</span></span>
* <span data-ttu-id="8a17e-279">右键单击测试系的“删除”超链接，然后选择“在新选项卡中打开”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-279">Right-click the **Delete** hyperlink for the test department and select **Open in new tab**.</span></span>
* <span data-ttu-id="8a17e-280">单击测试系的“编辑”超链接。</span><span class="sxs-lookup"><span data-stu-id="8a17e-280">Click the **Edit** hyperlink for the test department.</span></span>

<span data-ttu-id="8a17e-281">两个浏览器选项卡显示相同信息。</span><span class="sxs-lookup"><span data-stu-id="8a17e-281">The two browser tabs display the same information.</span></span>

<span data-ttu-id="8a17e-282">在第一个浏览器选项卡中更改预算，然后单击“保存”。</span><span class="sxs-lookup"><span data-stu-id="8a17e-282">Change the budget in the first browser tab and click **Save**.</span></span>

<span data-ttu-id="8a17e-283">浏览器显示更改值并更新 rowVersion 标记后的索引页。</span><span class="sxs-lookup"><span data-stu-id="8a17e-283">The browser shows the Index page with the changed value and updated rowVersion indicator.</span></span> <span data-ttu-id="8a17e-284">请注意更新后的 rowVersion 标记，它在其他选项卡的第二回发中显示。</span><span class="sxs-lookup"><span data-stu-id="8a17e-284">Note the updated rowVersion indicator, it's displayed on the second postback in the other tab.</span></span>

<span data-ttu-id="8a17e-285">从第二个选项卡中删除测试部门。并发错误显示来自数据库的当前值。</span><span class="sxs-lookup"><span data-stu-id="8a17e-285">Delete the test department from the second tab. A concurrency error is display with the current values from the DB.</span></span> <span data-ttu-id="8a17e-286">单击“删除”将删除实体，除非 `RowVersion` 已更新，院系已删除。</span><span class="sxs-lookup"><span data-stu-id="8a17e-286">Clicking **Delete** deletes the entity, unless `RowVersion` has been updated.department has been deleted.</span></span>

<span data-ttu-id="8a17e-287">请参阅[继承](xref:data/ef-mvc/inheritance)了解如何继承数据模型。</span><span class="sxs-lookup"><span data-stu-id="8a17e-287">See [Inheritance](xref:data/ef-mvc/inheritance) on how to inherit a data model.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="8a17e-288">其他资源</span><span class="sxs-lookup"><span data-stu-id="8a17e-288">Additional resources</span></span>

* [<span data-ttu-id="8a17e-289">EF Core 中的并发令牌</span><span class="sxs-lookup"><span data-stu-id="8a17e-289">Concurrency Tokens in EF Core</span></span>](/ef/core/modeling/concurrency)
* [<span data-ttu-id="8a17e-290">EF Core 中的并发处理</span><span class="sxs-lookup"><span data-stu-id="8a17e-290">Handle concurrency in EF Core</span></span>](/ef/core/saving/concurrency)

> [!div class="step-by-step"]
> [<span data-ttu-id="8a17e-291">上一篇</span><span class="sxs-lookup"><span data-stu-id="8a17e-291">Previous</span></span>](xref:data/ef-rp/update-related-data)
