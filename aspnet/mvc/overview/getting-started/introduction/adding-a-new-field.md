---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 添加新字段 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: a4eb759646fc77bbba687d8b4914465d58cd3aaa
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38151452"
---
<a name="adding-a-new-field"></a><span data-ttu-id="5397b-102">添加新字段</span><span class="sxs-lookup"><span data-stu-id="5397b-102">Adding a New Field</span></span>
====================
<span data-ttu-id="5397b-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5397b-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="5397b-104">在本部分中将使用 Entity Framework Code First 迁移来迁移到模型类的一些更改，因此更改被应用到数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="5397b-105">默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="5397b-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="5397b-106">如果它们不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="5397b-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="5397b-107">这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。</span><span class="sxs-lookup"><span data-stu-id="5397b-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="5397b-108">为模型更改设置 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="5397b-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="5397b-109">导航到解决方案资源管理器。</span><span class="sxs-lookup"><span data-stu-id="5397b-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="5397b-110">右键单击*Movies.mdf*文件，然后选择**删除**删除电影数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="5397b-111">如果没有看到*Movies.mdf*文件中，单击**显示所有文件**图标中的红色框如下所示。</span><span class="sxs-lookup"><span data-stu-id="5397b-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="5397b-112">生成应用程序以确保没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="5397b-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="5397b-113">从**工具**菜单上，单击**NuGet 包管理器**，然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="5397b-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![添加包 Man](adding-a-new-field/_static/image2.png)

<span data-ttu-id="5397b-115">在中**程序包管理器控制台**处窗口`PM>`提示输入</span><span class="sxs-lookup"><span data-stu-id="5397b-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="5397b-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="5397b-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="5397b-117">**Enable-migrations** （如上所示） 的命令将创建*Configuration.cs*文件中的新*迁移*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5397b-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="5397b-118">Visual Studio 将打开*Configuration.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5397b-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="5397b-119">替换`Seed`中的方法*Configuration.cs*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="5397b-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="5397b-120">将鼠标悬停在红色的波浪线`Movie`然后单击`Show Potential Fixes`，然后单击**使用** **MvcMovie.Models;**</span><span class="sxs-lookup"><span data-stu-id="5397b-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="5397b-121">执行此操作将添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="5397b-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="5397b-122">代码优先迁移调用`Seed`每个迁移后的方法 (即，调用**更新数据库**程序包管理器控制台)，，此方法更新行，具有已插入，或将其插入，如果它们尚不存在。</span><span class="sxs-lookup"><span data-stu-id="5397b-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="5397b-123">[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)下面的代码中的方法执行的"upsert"操作：</span><span class="sxs-lookup"><span data-stu-id="5397b-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="5397b-124">因为[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法运行与每个迁移，您不能只是插入数据，因为你尝试添加的行已存在后将创建数据库的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="5397b-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="5397b-125">"[Upsert](http://en.wikipedia.org/wiki/Upsert)"操作可以防止当尝试插入的行已存在，将会发生的错误，但它将替代对测试应用程序时可能已做的数据的任何更改。</span><span class="sxs-lookup"><span data-stu-id="5397b-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="5397b-126">使用测试数据的某些表中您可能不希望发生这种情况： 在某些情况下测试时更改数据时所需数据库更新后保留所做的更改。</span><span class="sxs-lookup"><span data-stu-id="5397b-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="5397b-127">在这种情况下想要执行条件插入操作： 插入行，仅当它尚不存在。</span><span class="sxs-lookup"><span data-stu-id="5397b-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="5397b-128">第一个参数传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法指定要用于检查行是否已存在的属性。</span><span class="sxs-lookup"><span data-stu-id="5397b-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="5397b-129">提供的，测试电影数据`Title`属性可用于此目的，因为每个标题在列表中的是唯一的：</span><span class="sxs-lookup"><span data-stu-id="5397b-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="5397b-130">此代码假定标题是唯一的。</span><span class="sxs-lookup"><span data-stu-id="5397b-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="5397b-131">如果你手动添加重复的标题，您将得到以下异常执行迁移的下一个时间。</span><span class="sxs-lookup"><span data-stu-id="5397b-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
>  <span data-ttu-id="5397b-132">*序列包含多个元素*</span><span class="sxs-lookup"><span data-stu-id="5397b-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="5397b-133">有关详细信息[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法，请参阅[负责使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)...</span><span class="sxs-lookup"><span data-stu-id="5397b-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>


<span data-ttu-id="5397b-134">**按 CTRL-SHIFT-B 以生成项目。**（以下步骤将失败，如果此时不生成。）</span><span class="sxs-lookup"><span data-stu-id="5397b-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="5397b-135">下一步是创建`DbMigration`类适用于初始迁移。</span><span class="sxs-lookup"><span data-stu-id="5397b-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="5397b-136">此迁移过程将创建一个新的数据库，这就是为什么你删除*movie.mdf*上一步中的文件。</span><span class="sxs-lookup"><span data-stu-id="5397b-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="5397b-137">在中**程序包管理器控制台**窗口中，输入命令`add-migration Initial`创建初始迁移。</span><span class="sxs-lookup"><span data-stu-id="5397b-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="5397b-138">"初始"的名称是任意参数并用于命名创建的迁移文件。</span><span class="sxs-lookup"><span data-stu-id="5397b-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="5397b-139">Code First 迁移创建另一个类文件中的*迁移*文件夹 (具有名称 *{日期戳}\_Initial.cs* )，并且此类包含创建数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="5397b-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="5397b-140">预先使用时间戳修复迁移文件名以帮助进行排序。</span><span class="sxs-lookup"><span data-stu-id="5397b-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="5397b-141">检查 *{日期戳}\_Initial.cs*文件，它包含的说明创建`Movies`电影数据库的表。</span><span class="sxs-lookup"><span data-stu-id="5397b-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="5397b-142">更新以下，这说明中的数据库时 *{日期戳}\_Initial.cs*文件将运行并创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="5397b-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="5397b-143">然后**种子**方法将运行以填充具有测试数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="5397b-144">在中**程序包管理器控制台**，输入命令`update-database`若要创建数据库并运行`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="5397b-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="5397b-145">如果收到一个错误，指示表已存在，无法创建，则可能是因为删除了该数据库后，您在执行前运行应用程序`update-database`。</span><span class="sxs-lookup"><span data-stu-id="5397b-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="5397b-146">在这种情况下，删除*Movies.mdf*再次文件，然后重试`update-database`命令。</span><span class="sxs-lookup"><span data-stu-id="5397b-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="5397b-147">如果仍遇到错误，删除的 migrations 文件夹和内容，然后开始在此页顶部的说明进行操作 (这是 delete *Movies.mdf*文件，然后转到 Enable-migrations)。</span><span class="sxs-lookup"><span data-stu-id="5397b-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="5397b-148">如果仍收到项错误而失败，打开 SQL Server 对象资源管理器，并从列表中删除数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-148">If you still get an eror, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="5397b-149">运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="5397b-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="5397b-150">将显示种子数据。</span><span class="sxs-lookup"><span data-stu-id="5397b-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="5397b-151">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="5397b-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="5397b-152">首先，通过添加一个新`Rating`属性设置为现有`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="5397b-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="5397b-153">打开*Models\Movie.cs*文件，并添加`Rating`如下属性：</span><span class="sxs-lookup"><span data-stu-id="5397b-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="5397b-154">完整`Movie`类现在看起来如以下代码：</span><span class="sxs-lookup"><span data-stu-id="5397b-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="5397b-155">生成应用程序 (Ctrl + Shift + B)。</span><span class="sxs-lookup"><span data-stu-id="5397b-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="5397b-156">因为你已将新字段添加到`Movie`类，你还需要更新绑定允许列表以便将包含此新属性。</span><span class="sxs-lookup"><span data-stu-id="5397b-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="5397b-157">更新`bind`特性`Create`并`Edit`操作方法，以包含`Rating`属性：</span><span class="sxs-lookup"><span data-stu-id="5397b-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="5397b-158">还需要更新视图模板，以便在浏览器视图中显示、创建和编辑新的 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="5397b-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="5397b-159">打开 *\Views\Movies\Index.cshtml* 文件，并添加`<th>Rating</th>`列标题之后**价格**列。</span><span class="sxs-lookup"><span data-stu-id="5397b-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="5397b-160">然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。</span><span class="sxs-lookup"><span data-stu-id="5397b-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="5397b-161">下面是哪些更新 *Index.cshtml* 视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="5397b-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="5397b-162">接下来，打开 *\Views\Movies\Create.cshtml* 文件，并添加`Rating`字段使用以下 highlighed 标记。</span><span class="sxs-lookup"><span data-stu-id="5397b-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighed markup.</span></span> <span data-ttu-id="5397b-163">这会使文本框中，以便创建新电影时，可以指定一个级别。</span><span class="sxs-lookup"><span data-stu-id="5397b-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="5397b-164">现已更新以支持新的应用程序代码`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="5397b-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="5397b-165">运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="5397b-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="5397b-166">执行此操作，不过，将看到以下错误之一：</span><span class="sxs-lookup"><span data-stu-id="5397b-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="5397b-167">创建数据库后，支持 MovieDBContext 上下文的模型已更改。</span><span class="sxs-lookup"><span data-stu-id="5397b-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="5397b-168">请考虑使用 Code First 迁移来更新数据库 (https://go.microsoft.com/fwlink/?LinkId=238269)。</span><span class="sxs-lookup"><span data-stu-id="5397b-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="5397b-169">之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。</span><span class="sxs-lookup"><span data-stu-id="5397b-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="5397b-170">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="5397b-170">(There's no `Rating` column in the database table.)</span></span>


<span data-ttu-id="5397b-171">可通过几种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="5397b-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="5397b-172">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="5397b-173">在测试数据库上进行开发时，此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="5397b-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="5397b-174">缺点，不过，是会丢失数据库中的现有数据，因此您*不*需要生产数据库上使用此方法 ！</span><span class="sxs-lookup"><span data-stu-id="5397b-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="5397b-175">使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用程序的有效方式。</span><span class="sxs-lookup"><span data-stu-id="5397b-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="5397b-176">有关实体框架数据库初始值设定项的详细信息，请参阅[ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="5397b-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="5397b-177">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="5397b-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="5397b-178">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="5397b-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="5397b-179">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="5397b-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="5397b-180">使用 Code First 迁移更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="5397b-180">Use Code First Migrations to update the database schema.</span></span>


<span data-ttu-id="5397b-181">本教程使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="5397b-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="5397b-182">更新 Seed 方法，使它向新列提供值。</span><span class="sxs-lookup"><span data-stu-id="5397b-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="5397b-183">打开 Migrations\Configuration.cs 文件并将评级字段添加到每个电影对象。</span><span class="sxs-lookup"><span data-stu-id="5397b-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="5397b-184">生成解决方案，然后打开**程序包管理器控制台**窗口并输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="5397b-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="5397b-185">`add-migration`命令会通知迁移框架以检查当前电影模型与当前的电影数据库架构并创建必要的代码以将数据库迁移到新模型。</span><span class="sxs-lookup"><span data-stu-id="5397b-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="5397b-186">名称*评级*是任意参数并用于命名迁移文件。</span><span class="sxs-lookup"><span data-stu-id="5397b-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="5397b-187">最好使用迁移步骤有意义的名称。</span><span class="sxs-lookup"><span data-stu-id="5397b-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="5397b-188">此命令完成后，Visual Studio 会打开定义新的类文件`DbMigration`派生的类，然后在`Up`方法您可以看到创建的新列的代码。</span><span class="sxs-lookup"><span data-stu-id="5397b-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="5397b-189">生成解决方案，并输入`update-database`命令，在**程序包管理器控制台**窗口。</span><span class="sxs-lookup"><span data-stu-id="5397b-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="5397b-190">下图显示了中的输出**程序包管理器控制台**窗口 (日期戳追加*评级*会有所不同。)</span><span class="sxs-lookup"><span data-stu-id="5397b-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="5397b-191">重新运行该应用程序并导航到 /Movies URL。</span><span class="sxs-lookup"><span data-stu-id="5397b-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="5397b-192">您可以看到新的评级字段。</span><span class="sxs-lookup"><span data-stu-id="5397b-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="5397b-193">单击**创建新**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="5397b-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="5397b-194">请注意，您可以添加一个级别。</span><span class="sxs-lookup"><span data-stu-id="5397b-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="5397b-196">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="5397b-196">Click **Create**.</span></span> <span data-ttu-id="5397b-197">新电影，包括分级，现在显示在列表的电影：</span><span class="sxs-lookup"><span data-stu-id="5397b-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="5397b-199">现在，项目使用迁移，不需要将新字段添加或更新架构，否则时删除数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="5397b-200">在下一步部分中，我们将进行更多架构更改，并使用迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="5397b-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="5397b-201">您还应添加`Rating`字段编辑、 详细信息和删除视图模板。</span><span class="sxs-lookup"><span data-stu-id="5397b-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="5397b-202">可以输入中的"更新数据库"命令**程序包管理器控制台**再次窗口和没有迁移代码会运行，因为该架构与模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="5397b-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="5397b-203">但是，运行"更新数据库"将运行`Seed`方法同样，如果您更改了任何种子数据，所做的更改都将丢失，因为`Seed`方法更新插入数据。</span><span class="sxs-lookup"><span data-stu-id="5397b-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="5397b-204">可以阅读更多有关`Seed`方法在 Tom Dykstra 的常用[ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="5397b-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="5397b-205">在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。</span><span class="sxs-lookup"><span data-stu-id="5397b-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="5397b-206">你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="5397b-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="5397b-207">这是只需向 Code First 简介，请参阅[为 ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)有关主题的更完整教程。</span><span class="sxs-lookup"><span data-stu-id="5397b-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="5397b-208">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。</span><span class="sxs-lookup"><span data-stu-id="5397b-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5397b-209">[上一页](adding-search.md)
> [下一页](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="5397b-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
