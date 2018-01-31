---
title: "将新字段添加到 Razor 页面"
author: rick-anderson
description: "演示如何使用 Entity Framework Core 将新字段添加到 Razor 页面"
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: 36412e9d1f3143f0d1999d0e754e6627f0984ad5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="adding-a-new-field-to-a-razor-page"></a><span data-ttu-id="a76ee-103">将新字段添加到 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="a76ee-103">Adding a new field to a Razor Page</span></span>

<span data-ttu-id="a76ee-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a76ee-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a76ee-105">在本部分中，将使用 [Entity Framework](https://docs.microsoft.com/ef/core/get-started/aspnetcore/new-db) Code First 迁移将新字段添加到模型，并将此更改迁移到数据库。</span><span class="sxs-lookup"><span data-stu-id="a76ee-105">In this section you'll use [Entity Framework](https://docs.microsoft.com/ef/core/get-started/aspnetcore/new-db) Code First Migrations to add a new field to the model and migrate that change to the database.</span></span>

<span data-ttu-id="a76ee-106">使用 EF Code First 自动创建数据库时，Code First 会向数据库添加表格，以帮助跟踪数据库的架构是否与从其中生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="a76ee-106">When you use EF Code First to automatically create a database, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="a76ee-107">如果它们不同步，EF 则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="a76ee-107">If they aren't in sync, EF throws an exception.</span></span> <span data-ttu-id="a76ee-108">这使查找不一致的数据库/代码问题变得更加轻松。</span><span class="sxs-lookup"><span data-stu-id="a76ee-108">This makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="a76ee-109">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="a76ee-109">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="a76ee-110">打开 Models/Movie.cs 文件，并添加 `Rating` 属性：</span><span class="sxs-lookup"><span data-stu-id="a76ee-110">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

<span data-ttu-id="a76ee-111">生成应用 (Ctrl+Shift+B)。</span><span class="sxs-lookup"><span data-stu-id="a76ee-111">Build the app (Ctrl+Shift+B).</span></span>

<span data-ttu-id="a76ee-112">编辑 Pages/Movies/Index.cshtml，并添加 `Rating` 字段：</span><span class="sxs-lookup"><span data-stu-id="a76ee-112">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=40-42,61-63)]

<span data-ttu-id="a76ee-113">将 `Rating` 字段添加到“删除”和“详细信息”页面。</span><span class="sxs-lookup"><span data-stu-id="a76ee-113">Add the `Rating` field to the Delete and Details pages.</span></span>

<span data-ttu-id="a76ee-114">使用 `Rating` 字段更新 Create.cshtml。</span><span class="sxs-lookup"><span data-stu-id="a76ee-114">Update *Create.cshtml* with a `Rating` field.</span></span> <span data-ttu-id="a76ee-115">可以复制/粘贴之前的 `<div>` 元素，并让 intelliSense 帮助更新字段。</span><span class="sxs-lookup"><span data-stu-id="a76ee-115">You can copy/paste the previous `<div>` element and let intelliSense help you update the fields.</span></span> <span data-ttu-id="a76ee-116">IntelliSense 适用于[标记帮助程序](xref:mvc/views/tag-helpers/intro)。</span><span class="sxs-lookup"><span data-stu-id="a76ee-116">IntelliSense works with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

![开发人员已在视图的第二个标签元素中键入字母 R 用作 asp-for 的特性值。](new-field/_static/cr.png)

<span data-ttu-id="a76ee-120">下面的代码显示具有 `Rating` 字段的 Create.cshtml：</span><span class="sxs-lookup"><span data-stu-id="a76ee-120">The following code shows *Create.cshtml* with a `Rating` field:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?highlight=36-40)]

<span data-ttu-id="a76ee-121">将 `Rating` 字段添加到“编辑”页面。</span><span class="sxs-lookup"><span data-stu-id="a76ee-121">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="a76ee-122">在 DB 更新为包括新字段之前，应用将不会正常工作。</span><span class="sxs-lookup"><span data-stu-id="a76ee-122">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="a76ee-123">如果立即运行，应用会引发 `SqlException`：</span><span class="sxs-lookup"><span data-stu-id="a76ee-123">If run now, the app throws a `SqlException`:</span></span>

```
SqlException: Invalid column name 'Rating'.
```

<span data-ttu-id="a76ee-124">此错误是由于更新的 Movie 模型类与数据库的 Movie 表架构不同导致的。</span><span class="sxs-lookup"><span data-stu-id="a76ee-124">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="a76ee-125">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="a76ee-125">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="a76ee-126">可通过几种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="a76ee-126">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="a76ee-127">让 Entity Framework 自动丢弃并使用新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="a76ee-127">Have the Entity Framework automatically drop and re-create the database using  the new model class schema.</span></span> <span data-ttu-id="a76ee-128">此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="a76ee-128">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="a76ee-129">此方法的缺点是会导致数据库中的现有数据丢失。</span><span class="sxs-lookup"><span data-stu-id="a76ee-129">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="a76ee-130">请勿对生产数据库使用此方法！</span><span class="sxs-lookup"><span data-stu-id="a76ee-130">You don't want to use this approach on a production database!</span></span> <span data-ttu-id="a76ee-131">当架构更改时丢弃数据库并使用初始值设定项以使用测试数据自动设定数据库种子，这通常是开发应用的有效方式。</span><span class="sxs-lookup"><span data-stu-id="a76ee-131">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="a76ee-132">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="a76ee-132">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="a76ee-133">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="a76ee-133">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="a76ee-134">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="a76ee-134">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="a76ee-135">使用 Code First 迁移更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="a76ee-135">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="a76ee-136">对于本教程，请使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="a76ee-136">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="a76ee-137">更新 `SeedData` 类，使它提供新列的值。</span><span class="sxs-lookup"><span data-stu-id="a76ee-137">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="a76ee-138">示例更改如下所示，但可能需要对每个 `new Movie` 块做出此更改。</span><span class="sxs-lookup"><span data-stu-id="a76ee-138">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

<span data-ttu-id="a76ee-139">请参阅[已完成的 SeedData.cs 文件](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs)。</span><span class="sxs-lookup"><span data-stu-id="a76ee-139">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="a76ee-140">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="a76ee-140">Build the solution.</span></span>

<a name="pmc"></a> <span data-ttu-id="a76ee-141">从“工具”菜单中，选择“NuGet 包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="a76ee-141">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="a76ee-142">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a76ee-142">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="a76ee-143">`Add-Migration` 命令会通知框架执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a76ee-143">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="a76ee-144">将 `Movie` 模型与 `Movie` DB 架构进行比较。</span><span class="sxs-lookup"><span data-stu-id="a76ee-144">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="a76ee-145">创建代码以将 DB 架构迁移到新模型。</span><span class="sxs-lookup"><span data-stu-id="a76ee-145">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="a76ee-146">名称“Rating”是任意的，用于对迁移文件进行命名。</span><span class="sxs-lookup"><span data-stu-id="a76ee-146">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="a76ee-147">为迁移文件使用有意义的名称是有帮助的。</span><span class="sxs-lookup"><span data-stu-id="a76ee-147">It's helpful to use a meaningful name for the migration file.</span></span>

<a name="ssox"></a> <span data-ttu-id="a76ee-148">如果删除 DB 中的所有记录，种子初始值设定项会设定 DB 种子，并将包括 `Rating` 字段。</span><span class="sxs-lookup"><span data-stu-id="a76ee-148">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="a76ee-149">可以使用浏览器中的删除链接，也可以从 [Sql Server 对象资源管理器](xref:tutorials/razor-pages/sql#ssox) (SSOX) 执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a76ee-149">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span> <span data-ttu-id="a76ee-150">从 SSOX 中删除数据库：</span><span class="sxs-lookup"><span data-stu-id="a76ee-150">To delete the database from SSOX:</span></span>

* <span data-ttu-id="a76ee-151">在 SSOX 中选择数据库。</span><span class="sxs-lookup"><span data-stu-id="a76ee-151">Select the database in SSOX.</span></span>
* <span data-ttu-id="a76ee-152">右键单击数据库，并选择“删除”。</span><span class="sxs-lookup"><span data-stu-id="a76ee-152">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="a76ee-153">检查“关闭现有连接”。</span><span class="sxs-lookup"><span data-stu-id="a76ee-153">Check **Close existing connections**.</span></span>
* <span data-ttu-id="a76ee-154">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="a76ee-154">Select **OK**.</span></span>
* <span data-ttu-id="a76ee-155">在 [PMC](xref:tutorials/razor-pages/new-field#pmc) 中更新数据库：</span><span class="sxs-lookup"><span data-stu-id="a76ee-155">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database:</span></span>

  ```powershell
  Update-Database
  ```

<span data-ttu-id="a76ee-156">运行应用，并验证是否可以创建/编辑/显示具有 `Rating` 字段的电影。</span><span class="sxs-lookup"><span data-stu-id="a76ee-156">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="a76ee-157">如果数据库未设定种子，请先停止 IIS Express，然后再运行应用。</span><span class="sxs-lookup"><span data-stu-id="a76ee-157">If the database isn't seeded, stop IIS Express, and then run the app.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="a76ee-158">[上一篇：添加搜索](xref:tutorials/razor-pages/search)
[下一篇：添加验证](xref:tutorials/razor-pages/validation)</span><span class="sxs-lookup"><span data-stu-id="a76ee-158">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding Validation](xref:tutorials/razor-pages/validation)</span></span>
