---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 将新字段添加到电影模型和表 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: 25a29e783f02e66e1713d8120eb526e1a02961a3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366471"
---
<a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="9254a-104">将新字段添加到电影模型和表</span><span class="sxs-lookup"><span data-stu-id="9254a-104">Adding a New Field to the Movie Model and Table</span></span>
====================
<span data-ttu-id="9254a-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="9254a-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="9254a-106">本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="9254a-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="9254a-107">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="9254a-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="9254a-108">在本部分中将使用 Entity Framework Code First 迁移来迁移到模型类的一些更改，因此更改被应用到数据库。</span><span class="sxs-lookup"><span data-stu-id="9254a-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="9254a-109">默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="9254a-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="9254a-110">如果它们不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="9254a-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="9254a-111">这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。</span><span class="sxs-lookup"><span data-stu-id="9254a-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="9254a-112">为模型更改设置 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="9254a-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="9254a-113">如果使用 Visual Studio 2012，双击*Movies.mdf*从解决方案资源管理器中打开数据库工具的文件。</span><span class="sxs-lookup"><span data-stu-id="9254a-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="9254a-114">Visual Studio Express for Web 将显示数据库资源管理器，Visual Studio 2012 将显示服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="9254a-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="9254a-115">如果使用 Visual Studio 2010，使用 SQL Server 对象资源管理器。</span><span class="sxs-lookup"><span data-stu-id="9254a-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="9254a-116">在数据库工具 （数据库资源管理器、 服务器资源管理器或 SQL Server 对象资源管理器） 中，右键单击`MovieDBContext`，然后选择**删除**以删除电影数据库。</span><span class="sxs-lookup"><span data-stu-id="9254a-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="9254a-117">导航回到解决方案资源管理器。</span><span class="sxs-lookup"><span data-stu-id="9254a-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="9254a-118">右键单击*Movies.mdf*文件，然后选择**删除**删除电影数据库。</span><span class="sxs-lookup"><span data-stu-id="9254a-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="9254a-119">生成应用程序以确保没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="9254a-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="9254a-120">从**工具**菜单上，单击**库程序包管理器**，然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="9254a-120">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span>

![添加包 Man](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="9254a-122">在中**程序包管理器控制台**处窗口`PM>`提示符处输入"Enable-migrations ContextTypeName MvcMovie.Models.MovieDBContext"。</span><span class="sxs-lookup"><span data-stu-id="9254a-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="9254a-123">**Enable-migrations** （如上所示） 的命令将创建*Configuration.cs*文件中的新*迁移*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9254a-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="9254a-124">Visual Studio 将打开*Configuration.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="9254a-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="9254a-125">替换`Seed`中的方法*Configuration.cs*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="9254a-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="9254a-126">右键单击下的红色波浪线`Movie`，然后选择**解决**然后**使用** **MvcMovie.Models;**</span><span class="sxs-lookup"><span data-stu-id="9254a-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="9254a-127">执行此操作将添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="9254a-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="9254a-128">代码优先迁移调用`Seed`每个迁移后的方法 (即，调用**更新数据库**程序包管理器控制台)，，此方法更新行，具有已插入，或将其插入，如果它们尚不存在。</span><span class="sxs-lookup"><span data-stu-id="9254a-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>


<span data-ttu-id="9254a-129">**按 CTRL-SHIFT-B 以生成项目。**(以下步骤将失败，如果你不在此时生成。)</span><span class="sxs-lookup"><span data-stu-id="9254a-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="9254a-130">下一步是创建`DbMigration`类适用于初始迁移。</span><span class="sxs-lookup"><span data-stu-id="9254a-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="9254a-131">为此迁移过程将创建一个新的数据库，这就是为什么你删除*movie.mdf*上一步中的文件。</span><span class="sxs-lookup"><span data-stu-id="9254a-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="9254a-132">在中**程序包管理器控制台**窗口中，输入命令"add-migration Initial"若要创建初始迁移。</span><span class="sxs-lookup"><span data-stu-id="9254a-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="9254a-133">"初始"的名称是任意参数并用于命名创建的迁移文件。</span><span class="sxs-lookup"><span data-stu-id="9254a-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="9254a-134">Code First 迁移创建另一个类文件中的*迁移*文件夹 (具有名称 *{日期戳}\_Initial.cs* )，并且此类包含创建数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="9254a-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="9254a-135">预先使用时间戳修复迁移文件名以帮助进行排序。</span><span class="sxs-lookup"><span data-stu-id="9254a-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="9254a-136">检查 *{日期戳}\_Initial.cs*文件，它包含为电影数据库创建电影表的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="9254a-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="9254a-137">更新以下，这说明中的数据库时 *{日期戳}\_Initial.cs*文件将运行并创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="9254a-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="9254a-138">然后**种子**方法将运行以填充具有测试数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="9254a-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="9254a-139">在中**程序包管理器控制台**，输入命令"更新数据库"以创建数据库并运行**种子**方法。</span><span class="sxs-lookup"><span data-stu-id="9254a-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="9254a-140">如果收到一个错误，指示表已存在，无法创建，则可能是因为删除了该数据库后，您在执行前运行应用程序`update-database`。</span><span class="sxs-lookup"><span data-stu-id="9254a-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="9254a-141">在这种情况下，删除*Movies.mdf*再次文件，然后重试`update-database`命令。</span><span class="sxs-lookup"><span data-stu-id="9254a-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="9254a-142">如果仍遇到错误，删除的 migrations 文件夹和内容，然后开始在此页顶部的说明进行操作 (这是 delete *Movies.mdf*文件，然后转到 Enable-migrations)。</span><span class="sxs-lookup"><span data-stu-id="9254a-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="9254a-143">运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="9254a-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="9254a-144">将显示种子数据。</span><span class="sxs-lookup"><span data-stu-id="9254a-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="9254a-145">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="9254a-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="9254a-146">首先，通过添加一个新`Rating`属性设置为现有`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="9254a-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="9254a-147">打开*Models\Movie.cs*文件，并添加`Rating`如下属性：</span><span class="sxs-lookup"><span data-stu-id="9254a-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="9254a-148">完整`Movie`类现在看起来如以下代码：</span><span class="sxs-lookup"><span data-stu-id="9254a-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="9254a-149">生成应用程序中使用**构建** &gt;**构建电影**菜单命令或通过按 CTRL-B SHIFT。</span><span class="sxs-lookup"><span data-stu-id="9254a-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="9254a-150">现在，已更新`Model`类，您还需要更新*\Views\Movies\Index.cshtml*并*\Views\Movies\Create.cshtml*查看模板以显示新`Rating`浏览器视图中的属性。</span><span class="sxs-lookup"><span data-stu-id="9254a-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="9254a-151">打开<em>\Views\Movies\Index.cshtml</em>文件，并添加`<th>Rating</th>`列标题之后<strong>价格</strong>列。</span><span class="sxs-lookup"><span data-stu-id="9254a-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="9254a-152">然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。</span><span class="sxs-lookup"><span data-stu-id="9254a-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="9254a-153">下面是哪些更新<em>Index.cshtml</em>视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="9254a-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="9254a-154">接下来，打开*\Views\Movies\Create.cshtml*文件，并添加以下标记窗体的结尾附近。</span><span class="sxs-lookup"><span data-stu-id="9254a-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="9254a-155">这会使文本框中，以便创建新电影时，可以指定一个级别。</span><span class="sxs-lookup"><span data-stu-id="9254a-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="9254a-156">现已更新以支持新的应用程序代码`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="9254a-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="9254a-157">现在，运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="9254a-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="9254a-158">执行此操作，不过，将看到以下错误之一：</span><span class="sxs-lookup"><span data-stu-id="9254a-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="9254a-159">之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。</span><span class="sxs-lookup"><span data-stu-id="9254a-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="9254a-160">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="9254a-160">(There's no `Rating` column in the database table.)</span></span>


<span data-ttu-id="9254a-161">可通过几种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="9254a-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="9254a-162">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="9254a-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="9254a-163">这种方法就是很方便时测试数据库; 上进行开发它可以一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="9254a-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="9254a-164">缺点，不过，是会丢失数据库中的现有数据，因此您*不*需要生产数据库上使用此方法 ！</span><span class="sxs-lookup"><span data-stu-id="9254a-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="9254a-165">使用初始值设定项以自动设定种子使用测试数据的数据库通常是开发的应用程序的有效方式。</span><span class="sxs-lookup"><span data-stu-id="9254a-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="9254a-166">有关实体框架数据库初始值设定项的详细信息，请参阅 Tom Dykstra [ASP.NET MVC/实体框架教程](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9254a-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="9254a-167">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="9254a-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="9254a-168">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="9254a-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="9254a-169">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="9254a-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="9254a-170">使用 Code First 迁移更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="9254a-170">Use Code First Migrations to update the database schema.</span></span>


<span data-ttu-id="9254a-171">本教程使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="9254a-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="9254a-172">更新 Seed 方法，使它向新列提供值。</span><span class="sxs-lookup"><span data-stu-id="9254a-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="9254a-173">打开 Migrations\Configuration.cs 文件并将评级字段添加到每个电影对象。</span><span class="sxs-lookup"><span data-stu-id="9254a-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="9254a-174">生成解决方案，然后打开**程序包管理器控制台**窗口并输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9254a-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="9254a-175">`add-migration`命令会通知迁移框架以检查当前电影模型与当前的电影数据库架构并创建必要的代码以将数据库迁移到新模型。</span><span class="sxs-lookup"><span data-stu-id="9254a-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="9254a-176">AddRatingMig 是任意参数并用于命名迁移文件。</span><span class="sxs-lookup"><span data-stu-id="9254a-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="9254a-177">最好使用迁移步骤有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="9254a-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="9254a-178">此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`派生的类，然后在`Up`方法您可以看到创建的新列的代码。</span><span class="sxs-lookup"><span data-stu-id="9254a-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="9254a-179">生成解决方案，并输入中的"更新数据库"命令**程序包管理器控制台**窗口。</span><span class="sxs-lookup"><span data-stu-id="9254a-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="9254a-180">下图显示了中的输出**程序包管理器控制台**窗口 （预先计算 AddRatingMig 的日期戳将与此不同。）</span><span class="sxs-lookup"><span data-stu-id="9254a-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="9254a-181">重新运行该应用程序并导航到 /Movies URL。</span><span class="sxs-lookup"><span data-stu-id="9254a-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="9254a-182">您可以看到新的评级字段。</span><span class="sxs-lookup"><span data-stu-id="9254a-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="9254a-183">单击**创建新**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="9254a-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="9254a-184">请注意，您可以添加一个级别。</span><span class="sxs-lookup"><span data-stu-id="9254a-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="9254a-186">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="9254a-186">Click **Create**.</span></span> <span data-ttu-id="9254a-187">新电影，包括分级，现在显示在列表的电影：</span><span class="sxs-lookup"><span data-stu-id="9254a-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="9254a-189">您还应添加`Rating`字段编辑、 详细信息和 SearchIndex 视图模板。</span><span class="sxs-lookup"><span data-stu-id="9254a-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="9254a-190">可以输入中的"更新数据库"命令**程序包管理器控制台**再次窗口和任何更改将会发生，因为该架构与模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="9254a-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="9254a-191">在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。</span><span class="sxs-lookup"><span data-stu-id="9254a-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="9254a-192">你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="9254a-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="9254a-193">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。</span><span class="sxs-lookup"><span data-stu-id="9254a-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9254a-194">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="9254a-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
