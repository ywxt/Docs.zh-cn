---
title: 将新字段添加到 ASP.NET Core 中的 Razor 页面
author: rick-anderson
description: 演示如何使用 Entity Framework Core 将新字段添加到 Razor 页面
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/5/2018
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: e280bc9553113982a1f1a77eabab32575c905237
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862286"
---
# <a name="add-a-new-field-to-a-razor-page-in-aspnet-core"></a><span data-ttu-id="af933-103">将新字段添加到 ASP.NET Core 中的 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="af933-103">Add a new field to a Razor Page in ASP.NET Core</span></span>

<span data-ttu-id="af933-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="af933-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="af933-105">在此部分中，[Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First 迁移用于：</span><span class="sxs-lookup"><span data-stu-id="af933-105">In this section [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First Migrations is used to:</span></span>

* <span data-ttu-id="af933-106">将新字段添加到模型。</span><span class="sxs-lookup"><span data-stu-id="af933-106">Add a new field to the model.</span></span>
* <span data-ttu-id="af933-107">将新字段架构更改迁移到数据库。</span><span class="sxs-lookup"><span data-stu-id="af933-107">Migrate the new field schema change to the database.</span></span>

<span data-ttu-id="af933-108">使用 EF Code First 自动创建数据库时，Code First 将：</span><span class="sxs-lookup"><span data-stu-id="af933-108">When using EF Code First to automatically create a database, Code First:</span></span>

* <span data-ttu-id="af933-109">向数据库添加表格，以跟踪数据库的架构是否与从生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="af933-109">Adds a table to the database to track whether the schema of the database is in sync with the model classes it was generated from.</span></span>
* <span data-ttu-id="af933-110">如果该模型类未与数据库同步，EF 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="af933-110">If the model classes aren't in sync with the DB, EF throws an exception.</span></span>

<span data-ttu-id="af933-111">通过自动验证同步的架构/模型可以更容易地发现不一致的数据库/代码问题。</span><span class="sxs-lookup"><span data-stu-id="af933-111">Automatic verification of schema/model in sync makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="af933-112">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="af933-112">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="af933-113">打开 Models/Movie.cs 文件，并添加 `Rating` 属性：</span><span class="sxs-lookup"><span data-stu-id="af933-113">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

<span data-ttu-id="af933-114">构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="af933-114">Build the app.</span></span>

<span data-ttu-id="af933-115">编辑 Pages/Movies/Index.cshtml，并添加 `Rating` 字段：</span><span class="sxs-lookup"><span data-stu-id="af933-115">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexRating.cshtml.?highlight=40-42,61-63)]

<span data-ttu-id="af933-116">更新以下页面：</span><span class="sxs-lookup"><span data-stu-id="af933-116">Update the following pages:</span></span>

* <span data-ttu-id="af933-117">将 `Rating` 字段添加到“删除”和“详细信息”页面。</span><span class="sxs-lookup"><span data-stu-id="af933-117">Add the `Rating` field to the Delete and Details pages.</span></span>
* <span data-ttu-id="af933-118">使用 `Rating` 字段更新 [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="af933-118">Update [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml) with a `Rating` field.</span></span>
* <span data-ttu-id="af933-119">将 `Rating` 字段添加到“编辑”页面。</span><span class="sxs-lookup"><span data-stu-id="af933-119">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="af933-120">在 DB 更新为包括新字段之前，应用将不会正常工作。</span><span class="sxs-lookup"><span data-stu-id="af933-120">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="af933-121">如果立即运行，应用会引发 `SqlException`：</span><span class="sxs-lookup"><span data-stu-id="af933-121">If run now, the app throws a `SqlException`:</span></span>

`SqlException: Invalid column name 'Rating'.`

<span data-ttu-id="af933-122">此错误是由于更新的 Movie 模型类与数据库的 Movie 表架构不同导致的。</span><span class="sxs-lookup"><span data-stu-id="af933-122">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="af933-123">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="af933-123">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="af933-124">可通过几种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="af933-124">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="af933-125">让 Entity Framework 自动丢弃并使用新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="af933-125">Have the Entity Framework automatically drop and re-create the database using the new model class schema.</span></span> <span data-ttu-id="af933-126">此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="af933-126">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="af933-127">此方法的缺点是会导致数据库中的现有数据丢失。</span><span class="sxs-lookup"><span data-stu-id="af933-127">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="af933-128">请勿对生产数据库使用此方法！</span><span class="sxs-lookup"><span data-stu-id="af933-128">Don't use this approach on a production database!</span></span> <span data-ttu-id="af933-129">当架构更改时丢弃数据库并使用初始值设定项以使用测试数据自动设定数据库种子，这通常是开发应用的有效方式。</span><span class="sxs-lookup"><span data-stu-id="af933-129">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="af933-130">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="af933-130">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="af933-131">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="af933-131">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="af933-132">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="af933-132">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="af933-133">使用 Code First 迁移更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="af933-133">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="af933-134">对于本教程，请使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="af933-134">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="af933-135">更新 `SeedData` 类，使它提供新列的值。</span><span class="sxs-lookup"><span data-stu-id="af933-135">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="af933-136">示例更改如下所示，但可能需要对每个 `new Movie` 块做出此更改。</span><span class="sxs-lookup"><span data-stu-id="af933-136">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

<span data-ttu-id="af933-137">请参阅[已完成的 SeedData.cs 文件](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs)。</span><span class="sxs-lookup"><span data-stu-id="af933-137">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="af933-138">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="af933-138">Build the solution.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="af933-139">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af933-139">Visual Studio</span></span>](#tab/visual-studio)

<a name="pmc"></a>

### <a name="add-a-migration-for-the-rating-field"></a><span data-ttu-id="af933-140">添加用于评级字段的迁移</span><span class="sxs-lookup"><span data-stu-id="af933-140">Add a migration for the rating field</span></span>

<span data-ttu-id="af933-141">从“工具”菜单中，选择“NuGet 包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="af933-141">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="af933-142">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="af933-142">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="af933-143">`Add-Migration` 命令会通知框架执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="af933-143">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="af933-144">将 `Movie` 模型与 `Movie` DB 架构进行比较。</span><span class="sxs-lookup"><span data-stu-id="af933-144">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="af933-145">创建代码以将 DB 架构迁移到新模型。</span><span class="sxs-lookup"><span data-stu-id="af933-145">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="af933-146">名称“Rating”是任意的，用于对迁移文件进行命名。</span><span class="sxs-lookup"><span data-stu-id="af933-146">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="af933-147">为迁移文件使用有意义的名称是有帮助的。</span><span class="sxs-lookup"><span data-stu-id="af933-147">It's helpful to use a meaningful name for the migration file.</span></span>

<a name="ssox"></a>

<span data-ttu-id="af933-148">如果删除 DB 中的所有记录，种子初始值设定项会设定 DB 种子，并将包括 `Rating` 字段。</span><span class="sxs-lookup"><span data-stu-id="af933-148">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="af933-149">可以使用浏览器中的删除链接，也可以从 [Sql Server 对象资源管理器](xref:tutorials/razor-pages/sql#ssox) (SSOX) 执行此操作。</span><span class="sxs-lookup"><span data-stu-id="af933-149">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span> <span data-ttu-id="af933-150">从 SSOX 中删除数据库：</span><span class="sxs-lookup"><span data-stu-id="af933-150">To delete the database from SSOX:</span></span>

* <span data-ttu-id="af933-151">在 SSOX 中选择数据库。</span><span class="sxs-lookup"><span data-stu-id="af933-151">Select the database in SSOX.</span></span>
* <span data-ttu-id="af933-152">右键单击数据库，并选择“删除”。</span><span class="sxs-lookup"><span data-stu-id="af933-152">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="af933-153">检查“关闭现有连接”。</span><span class="sxs-lookup"><span data-stu-id="af933-153">Check **Close existing connections**.</span></span>
* <span data-ttu-id="af933-154">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="af933-154">Select **OK**.</span></span>
* <span data-ttu-id="af933-155">在 [PMC](xref:tutorials/razor-pages/new-field#pmc) 中更新数据库：</span><span class="sxs-lookup"><span data-stu-id="af933-155">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database:</span></span>

  ```powershell
  Update-Database
  ```

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="af933-156">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="af933-156">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="af933-157"><!-- copy/paste this tab to the next. Not worth an include  --> SQLite 不支持迁移。</span><span class="sxs-lookup"><span data-stu-id="af933-157"><!-- copy/paste this tab to the next. Not worth an include  --> SQLite doesn't support migrations.</span></span>

* <span data-ttu-id="af933-158">删除数据库或更改 appsettings.json 文件中的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="af933-158">Delete the database or change the database name in the *appsettings.json* file.</span></span>
* <span data-ttu-id="af933-159">删除 Migrations 文件夹（和该文件夹中的所有文件）。</span><span class="sxs-lookup"><span data-stu-id="af933-159">Delete the *Migrations* folder (and all the files in the folder).</span></span>

<span data-ttu-id="af933-160">运行以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="af933-160">Run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add Rating
dotnet ef database update
```

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="af933-161">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="af933-161">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="af933-162">SQLite 不支持迁移。</span><span class="sxs-lookup"><span data-stu-id="af933-162">SQLite doesn't support migrations.</span></span>

* <span data-ttu-id="af933-163">删除数据库或更改 appsettings.json 文件中的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="af933-163">Delete the database or change the database name in the *appsettings.json* file.</span></span>
* <span data-ttu-id="af933-164">删除 Migrations 文件夹（和该文件夹中的所有文件）。</span><span class="sxs-lookup"><span data-stu-id="af933-164">Delete the *Migrations* folder (and all the files in the folder).</span></span>

<span data-ttu-id="af933-165">运行以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="af933-165">Run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add Rating
dotnet ef database update
```

---  
<!-- End of VS tabs -->

<span data-ttu-id="af933-166">运行应用，并验证是否可以创建/编辑/显示具有 `Rating` 字段的电影。</span><span class="sxs-lookup"><span data-stu-id="af933-166">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="af933-167">如果数据库未设定种子，则在 `SeedData.Initialize` 方法中设置断点。</span><span class="sxs-lookup"><span data-stu-id="af933-167">If the database isn't seeded, set a break point in the `SeedData.Initialize` method.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="af933-168">[上一篇：添加搜索](xref:tutorials/razor-pages/search)
> [下一篇：添加验证](xref:tutorials/razor-pages/validation)</span><span class="sxs-lookup"><span data-stu-id="af933-168">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding Validation](xref:tutorials/razor-pages/validation)</span></span>
