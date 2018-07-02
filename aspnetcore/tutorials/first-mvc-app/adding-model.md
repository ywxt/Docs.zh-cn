---
title: 将模型添加到 ASP.NET Core MVC 应用
author: rick-anderson
description: 将模型添加到简单的 ASP.NET Core 应用。
ms.author: riande
ms.date: 12/8/2017
uid: tutorials/first-mvc-app/adding-model
ms.openlocfilehash: 28a63498bc1a3c7b6ad6be038209dacdb49e44ee
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36960663"
---
[!INCLUDE [adding-model](~/Includes/mvc-intro/adding-model1.md)]

<span data-ttu-id="12471-103">右键单击 Models 文件夹，然后单击“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="12471-103">Right-click the *Models* folder > **Add** > **Class**.</span></span> <span data-ttu-id="12471-104">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="12471-104">Name the class **Movie** and add the following properties:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="12471-105">数据库需要 `ID` 字段以获取主键。</span><span class="sxs-lookup"><span data-stu-id="12471-105">The `ID` field is required by the database for the primary key.</span></span> 

<span data-ttu-id="12471-106">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="12471-106">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="12471-107">现在 MVC 应用中已具有模型。</span><span class="sxs-lookup"><span data-stu-id="12471-107">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="scaffolding-a-controller"></a><span data-ttu-id="12471-108">搭建控制器基架</span><span class="sxs-lookup"><span data-stu-id="12471-108">Scaffolding a controller</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="12471-109">在解决方案资源管理器中，右键单击“Controllers”文件夹 >“添加”>“新搭建基架的项目”。</span><span class="sxs-lookup"><span data-stu-id="12471-109">In **Solution Explorer**, right-click the *Controllers* folder **> Add > New Scaffolded Item**.</span></span>

![上述步骤的视图](adding-model/_static/add_controller21.png)

<span data-ttu-id="12471-111">在“添加基架”对话框中，点击“包含视图的 MVC 控制器(使用 Entity Framework)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="12471-111">In the **Add Scaffold** dialog, tap **MVC Controller with views, using Entity Framework > Add**.</span></span>

![“添加基架”对话框](adding-model/_static/add_scaffold21.png)

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="12471-113">在“解决方案资源管理器”中，右键单击“控制器”文件夹，然后单击“添加”>“控制器”。</span><span class="sxs-lookup"><span data-stu-id="12471-113">In **Solution Explorer**, right-click the *Controllers* folder **> Add > Controller**.</span></span>

![上述步骤的视图](adding-model/_static/add_controller.png)

<span data-ttu-id="12471-115">如果出现“添加 MVC 依赖项”对话框：</span><span class="sxs-lookup"><span data-stu-id="12471-115">If the **Add MVC Dependencies** dialog appears:</span></span>

* <span data-ttu-id="12471-116">[将 Visual Studio 更新到最新版本](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="12471-116">[Update Visual Studio to the latest version](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="12471-117">15.5 之前的 Visual Studio 版本显示此对话框。</span><span class="sxs-lookup"><span data-stu-id="12471-117">Visual Studio versions prior to 15.5 show this dialog.</span></span>
* <span data-ttu-id="12471-118">如果无法更新，请选择“添加”，然后再次按照添加控制器步骤操作。</span><span class="sxs-lookup"><span data-stu-id="12471-118">If you can't update, select **ADD**, and then follow the add controller steps again.</span></span>

<span data-ttu-id="12471-119">在“添加基架”对话框中，点击“包含视图的 MVC 控制器(使用 Entity Framework)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="12471-119">In the **Add Scaffold** dialog, tap **MVC Controller with views, using Entity Framework > Add**.</span></span>

![“添加基架”对话框](adding-model/_static/add_scaffold2.png)

::: moniker-end

<span data-ttu-id="12471-121">填写“添加控制器”对话框：</span><span class="sxs-lookup"><span data-stu-id="12471-121">Complete the **Add Controller** dialog:</span></span>

* <span data-ttu-id="12471-122">模型类：Movie（MvcMovie.Models）</span><span class="sxs-lookup"><span data-stu-id="12471-122">**Model class:** *Movie (MvcMovie.Models)*</span></span>
* <span data-ttu-id="12471-123">数据上下文类：选择 + 图标并添加默认的 MvcMovie.Models.MvcMovieContext </span><span class="sxs-lookup"><span data-stu-id="12471-123">**Data context class:** Select the **+** icon and add the default **MvcMovie.Models.MvcMovieContext**</span></span>

![“添加数据”上下文](adding-model/_static/dc.png)

* <span data-ttu-id="12471-125">视图：将每个选项保持为默认选中状态</span><span class="sxs-lookup"><span data-stu-id="12471-125">**Views:** Keep the default of each option checked</span></span>
* <span data-ttu-id="12471-126">控制器名称：保留默认的 MoviesController</span><span class="sxs-lookup"><span data-stu-id="12471-126">**Controller name:** Keep the default *MoviesController*</span></span>
* <span data-ttu-id="12471-127">点击“添加”</span><span class="sxs-lookup"><span data-stu-id="12471-127">Tap **Add**</span></span>

![“添加控制器”对话框](adding-model/_static/add_controller2.png)

<span data-ttu-id="12471-129">Visual Studio 将创建：</span><span class="sxs-lookup"><span data-stu-id="12471-129">Visual Studio creates:</span></span>

* <span data-ttu-id="12471-130">Entity Framework Core [数据库上下文类](xref:data/ef-mvc/intro#create-the-database-context) (Data/MvcMovieContext.cs)</span><span class="sxs-lookup"><span data-stu-id="12471-130">An Entity Framework Core [database context class](xref:data/ef-mvc/intro#create-the-database-context) (*Data/MvcMovieContext.cs*)</span></span>
* <span data-ttu-id="12471-131">电影控制器 (Controllers/MoviesController.cs)</span><span class="sxs-lookup"><span data-stu-id="12471-131">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="12471-132">“创建”、“删除”、“详细信息”、“编辑”和“索引”页面的 Razor 视图文件 (Views/Movies/&ast;.cshtml)</span><span class="sxs-lookup"><span data-stu-id="12471-132">Razor view files for Create, Delete, Details, Edit, and Index pages (<em>Views/Movies/&ast;.cshtml</em>)</span></span>

<span data-ttu-id="12471-133">自动创建数据库上下文和 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)（创建、读取、更新和删除）操作方法和视图的过程称为“搭建基架”。</span><span class="sxs-lookup"><span data-stu-id="12471-133">The automatic creation of the database context and [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="12471-134">你很快将具有功能完整的 Web 应用程序，可使用此应用程序管理电影数据库。</span><span class="sxs-lookup"><span data-stu-id="12471-134">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

<span data-ttu-id="12471-135">如果运行应用并单击“Mvc 电影”链接，则会出现以下类似的错误：</span><span class="sxs-lookup"><span data-stu-id="12471-135">If you run the app and click on the **Mvc Movie** link, you get an error similar to the following:</span></span>

``` error
An unhandled exception occurred while processing the request.

SqlException: Cannot open database "MvcMovieContext-<GUID removed>" requested by the login. The login failed.
Login failed for user 'Rick'.

System.Data.SqlClient.SqlInternalConnectionTds..ctor(DbConnectionPoolIdentity identity, SqlConnectionString 
```

<span data-ttu-id="12471-136">你需要创建数据库，并且使用 EF Core [迁移](xref:data/ef-mvc/migrations)功能来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="12471-136">You need to create the database, and you'll use the EF Core [Migrations](xref:data/ef-mvc/migrations) feature to do that.</span></span> <span data-ttu-id="12471-137">通过迁移可创建与数据模型匹配的数据库，并在数据模型更改时更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="12471-137">Migrations lets you create a database that matches your data model and update the database schema when your data model changes.</span></span>

## <a name="add-ef-tooling-and-perform-initial-migration"></a><span data-ttu-id="12471-138">添加 EF 工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="12471-138">Add EF tooling and perform initial migration</span></span>

<span data-ttu-id="12471-139">在本部分中，将使用包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="12471-139">In this section you'll use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="12471-140">添加 Entity Framework Core 工具包。</span><span class="sxs-lookup"><span data-stu-id="12471-140">Add the Entity Framework Core Tools package.</span></span> <span data-ttu-id="12471-141">添加迁移并更新数据库需要此工具包。</span><span class="sxs-lookup"><span data-stu-id="12471-141">This package is required to add migrations and update the database.</span></span>
* <span data-ttu-id="12471-142">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="12471-142">Add an initial migration.</span></span>
* <span data-ttu-id="12471-143">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="12471-143">Update the database with the initial migration.</span></span>

<span data-ttu-id="12471-144">从“工具”菜单中，选择“NuGet 包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="12471-144">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>

<span data-ttu-id="12471-145"><!-- following image shared with uid: tutorials/razor-pages/model --> ![PMC 菜单](adding-model/_static/pmc.png)</span><span class="sxs-lookup"><span data-stu-id="12471-145"><!-- following image shared with uid: tutorials/razor-pages/model --> ![PMC menu](adding-model/_static/pmc.png)</span></span>

<span data-ttu-id="12471-146">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="12471-146">In the PMC, enter the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"
``` PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="12471-147">忽略以下错误消息，我们将在下一教程中修复：</span><span class="sxs-lookup"><span data-stu-id="12471-147">Ignore the following error message, we fix it in the next tutorial:</span></span>

<span data-ttu-id="12471-148">*Microsoft.EntityFrameworkCore.Model.Validation[30000]*</span><span class="sxs-lookup"><span data-stu-id="12471-148">*Microsoft.EntityFrameworkCore.Model.Validation[30000]*</span></span>  
      <span data-ttu-id="12471-149">未对实体类型“Movie”上的十进制列“Price”指定任何类型。当值不符合默认精确度和小数位数时，会在无提示的情况下截断该值。使用“ForHasColumnType()”显式指定可以容纳所有值的 SQL Server 列类型。</span><span class="sxs-lookup"><span data-stu-id="12471-149">*No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*</span></span>

::: moniker-end
::: moniker range="<= aspnetcore-2.0"

``` PMC
Install-Package Microsoft.EntityFrameworkCore.Tools
Add-Migration Initial
Update-Database
```

<span data-ttu-id="12471-150">请注意：如果在使用 `Install-Package` 命令时收到错误，请打开 NuGet 包管理器并搜索 `Microsoft.EntityFrameworkCore.Tools` 包。</span><span class="sxs-lookup"><span data-stu-id="12471-150">**Note:** If you receive an error with the `Install-Package` command, open NuGet Package Manager and search for the `Microsoft.EntityFrameworkCore.Tools` package.</span></span> <span data-ttu-id="12471-151">通过此操作，可以安装包或检查是否已安装包。</span><span class="sxs-lookup"><span data-stu-id="12471-151">This allows you to install the package or check if it's already installed.</span></span> <span data-ttu-id="12471-152">或者，如果 PMC 存在任何问题，请参阅 [CLI 方法](#cli)。</span><span class="sxs-lookup"><span data-stu-id="12471-152">Alternatively, see the [CLI approach](#cli) if you have problems with the PMC.</span></span>

::: moniker-end

<span data-ttu-id="12471-153">`Add-Migration` 命令创建代码以创建初始数据库架构。</span><span class="sxs-lookup"><span data-stu-id="12471-153">The `Add-Migration` command creates code to create the initial database schema.</span></span> <span data-ttu-id="12471-154">此架构基于（Data/MvcMovieContext.cs 文件中的）`DbContext` 中指定的模型。</span><span class="sxs-lookup"><span data-stu-id="12471-154">The schema is based on the model specified in the `DbContext`(In the *Data/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="12471-155">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="12471-155">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="12471-156">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="12471-156">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="12471-157">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="12471-157">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="12471-158">`Update-Database` 命令在用于创建数据库的 Migrations/\<time-stamp>_Initial.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="12471-158">The `Update-Database` command runs the `Up` method in the *Migrations/\<time-stamp>_Initial.cs* file, which creates the database.</span></span>

<a name="cli"></a> <span data-ttu-id="12471-159">还可以使用命令行接口 (CLI) 来执行前面的步骤，而不使用 PMC：</span><span class="sxs-lookup"><span data-stu-id="12471-159">You can perform the preceeding steps using the command-line interface (CLI) rather than the PMC:</span></span>

* <span data-ttu-id="12471-160">将 [EF Core 工具](xref:data/ef-mvc/migrations#entity-framework-core-nuget-packages-for-migrations)添加到 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="12471-160">Add [EF Core tooling](xref:data/ef-mvc/migrations#entity-framework-core-nuget-packages-for-migrations) to the *.csproj* file.</span></span>
* <span data-ttu-id="12471-161">从控制台（在项目目录中）运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="12471-161">Run the following commands from the console (in the project directory):</span></span>

  ```console
  dotnet ef migrations add Initial
  dotnet ef database update
  ```

  <span data-ttu-id="12471-162">如果运行应用并收到错误消息：</span><span class="sxs-lookup"><span data-stu-id="12471-162">If you run the app and get the error:</span></span>

  ```text
  SqlException: Cannot open database "Movie" requested by the login.
  The login failed.
  Login failed for user 'user name'.
  ```

<span data-ttu-id="12471-163">可能尚未运行 `dotnet ef database update`。</span><span class="sxs-lookup"><span data-stu-id="12471-163">You probably have not run `dotnet ef database update`.</span></span>

[!INCLUDE [adding-model](~/Includes/mvc-intro/adding-model3.md)]

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Startup.cs?name=ConfigureServices&highlight=13-99)]
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]
::: moniker-end

[!INCLUDE [adding-model](~/Includes/mvc-intro/adding-model4.md)]

![Model 项上的 Intellisense 上下文菜单，列出了 ID、价格、发布日期和标题的可用属性](adding-model/_static/ints.png)

## <a name="additional-resources"></a><span data-ttu-id="12471-165">其他资源</span><span class="sxs-lookup"><span data-stu-id="12471-165">Additional resources</span></span>

* [<span data-ttu-id="12471-166">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="12471-166">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="12471-167">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="12471-167">Globalization and localization</span></span>](xref:fundamentals/localization)

> [!div class="step-by-step"]
> <span data-ttu-id="12471-168">[上一篇：添加视图](adding-view.md)
> [下一篇：使用 SQL](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="12471-168">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  
