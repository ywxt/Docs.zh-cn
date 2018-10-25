---
title: 在 ASP.NET Core 中向 Razor 页面应用添加模型
author: rick-anderson
description: 了解如何使用 Entity Framework Core (EF Core) 添加用于管理数据库中的影片的类。
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: 5cd1e08ac52d352be23a280419d7456f685a03ad
ms.sourcegitcommit: 317f9be24db600499e79d25872d743af74bd86c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48045596"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="61853-103">在 ASP.NET Core 中向 Razor 页面应用添加模型</span><span class="sxs-lookup"><span data-stu-id="61853-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="61853-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="61853-104">Add a data model</span></span>

<span data-ttu-id="61853-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="61853-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="61853-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="61853-106">Name the folder *Models*.</span></span>

<span data-ttu-id="61853-107">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="61853-107">Right click the *Models* folder.</span></span> <span data-ttu-id="61853-108">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="61853-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="61853-109">将该类命名为 Movie 并将 `Movie` 内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="61853-109">Name the class **Movie** and replace the contents of the `Movie` class with the following code:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="61853-110">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="61853-110">Scaffold the movie model</span></span>

<span data-ttu-id="61853-111">在此部分，将搭建“电影”模型的基架。</span><span class="sxs-lookup"><span data-stu-id="61853-111">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="61853-112">确切地说，基架工具将生成页面，用于对“电影”模型执行创建、读取、更新和删除 (CRUD) 操作。</span><span class="sxs-lookup"><span data-stu-id="61853-112">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<span data-ttu-id="61853-113">创建“Pages/Movies”文件夹：</span><span class="sxs-lookup"><span data-stu-id="61853-113">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="61853-114">在解决方案资源管理器中，右键单击“Pages”文件夹 >“添加”>“新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="61853-114">In **Solution Explorer**, right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="61853-115">将文件夹命名为“Movies”</span><span class="sxs-lookup"><span data-stu-id="61853-115">Name the folder *Movies*</span></span>

<span data-ttu-id="61853-116">在解决方案资源管理器中，右键单击“Pages/Movies”文件夹 >“添加”>“新搭建基架的项目”。</span><span class="sxs-lookup"><span data-stu-id="61853-116">In **Solution Explorer**, right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![上述说明的图像。](model/_static/sca.png)

<span data-ttu-id="61853-118">在“添加基架”对话框中，选择“使用实体框架生成 Razor Pages (CRUD)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="61853-118">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **Add**.</span></span>

![上述说明的图像。](model/_static/add_scaffold.png)

<span data-ttu-id="61853-120">完成“使用实体框架(CRUD)添加 Razor Pages”对话框：</span><span class="sxs-lookup"><span data-stu-id="61853-120">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="61853-121">在“模型类”下拉列表中，选择“Movie (RazorPagesMovie.Models)。</span><span class="sxs-lookup"><span data-stu-id="61853-121">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="61853-122">在“数据上下文类”行中，选择 +（加号）并接受生成的名称“RazorPagesMovie.Models.RazorPagesMovieContext”。</span><span class="sxs-lookup"><span data-stu-id="61853-122">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="61853-123">在“数据上下文类”下拉列表中，选择“RazorPagesMovie.Models.RazorPagesMovieContext”</span><span class="sxs-lookup"><span data-stu-id="61853-123">In the **Data context class** drop down, select **RazorPagesMovie.Models.RazorPagesMovieContext**</span></span>
* <span data-ttu-id="61853-124">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="61853-124">Select **Add**.</span></span>

![上述说明的图像。](model/_static/arp.png)

<span data-ttu-id="61853-126">搭建基架的过程会创建并更改以下文件：</span><span class="sxs-lookup"><span data-stu-id="61853-126">The scaffold process created and changed the following files:</span></span>

### <a name="files-created"></a><span data-ttu-id="61853-127">创建的文件</span><span class="sxs-lookup"><span data-stu-id="61853-127">Files created</span></span>

* <span data-ttu-id="61853-128">Pages/Movies：“创建”、“删除”、“详细信息”、“编辑”、“索引”。</span><span class="sxs-lookup"><span data-stu-id="61853-128">*Pages/Movies*: Create, Delete, Details, Edit, Index.</span></span> <span data-ttu-id="61853-129">将在下一教程中详细介绍这些页面。</span><span class="sxs-lookup"><span data-stu-id="61853-129">These pages are detailed in the next tutorial.</span></span>
* <span data-ttu-id="61853-130">Data/RazorPagesMovieContext.cs</span><span class="sxs-lookup"><span data-stu-id="61853-130">*Data/RazorPagesMovieContext.cs*</span></span>

### <a name="file-updates"></a><span data-ttu-id="61853-131">文件更新</span><span class="sxs-lookup"><span data-stu-id="61853-131">File updates</span></span>

* <span data-ttu-id="61853-132">Startup.cs：下一部分详细介绍对此文件所作的更改。</span><span class="sxs-lookup"><span data-stu-id="61853-132">*Startup.cs*: Changes to this file are detailed in the next section.</span></span>
* <span data-ttu-id="61853-133">appsettings.json：添加用于连接到本地数据的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="61853-133">*appsettings.json*: The connection string used to connect to a local database is added.</span></span>

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="61853-134">检查通过依赖关系注入注册的上下文</span><span class="sxs-lookup"><span data-stu-id="61853-134">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="61853-135">ASP.NET Core 通过[依赖关系注入](xref:fundamentals/dependency-injection)进行生成。</span><span class="sxs-lookup"><span data-stu-id="61853-135">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="61853-136">服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="61853-136">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="61853-137">需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="61853-137">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="61853-138">本教程的后续部分介绍了用于获取 DB 上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="61853-138">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="61853-139">基架工具自动创建 DB 上下文并将其注册到依赖关系注入容器。</span><span class="sxs-lookup"><span data-stu-id="61853-139">The scaffolding tool automatically created a DB context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="61853-140">检查 `Startup.ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="61853-140">Examine the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="61853-141">基架添加了突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="61853-141">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

<span data-ttu-id="61853-142">数据库上下文类是为给定数据模型协调 EF Core 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="61853-142">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="61853-143">数据上下文派生自 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)。</span><span class="sxs-lookup"><span data-stu-id="61853-143">The data context is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="61853-144">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="61853-144">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="61853-145">在此项目中将数据库上下文类命名为 `RazorPagesMovieContext`。</span><span class="sxs-lookup"><span data-stu-id="61853-145">In this project, the class is named `RazorPagesMovieContext`.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Data/RazorPagesMovieContext.cs)]

<span data-ttu-id="61853-146">前面的代码为实体集创建 [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 属性。</span><span class="sxs-lookup"><span data-stu-id="61853-146">The preceding code creates a [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for the entity set.</span></span> <span data-ttu-id="61853-147">在实体框架术语中，实体集通常与数据表相对应。</span><span class="sxs-lookup"><span data-stu-id="61853-147">In Entity Framework terminology, an entity set typically corresponds to a database table.</span></span> <span data-ttu-id="61853-148">实体对应表中的行。</span><span class="sxs-lookup"><span data-stu-id="61853-148">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="61853-149">通过调用 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 对象中的一个方法将连接字符串名称传递到上下文。</span><span class="sxs-lookup"><span data-stu-id="61853-149">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="61853-150">进行本地开发时， [ASP.NET Core 配置系统](xref:fundamentals/configuration/index) 在 *appsettings.json* 文件中读取数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="61853-150">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<a name="pmc"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="61853-151">添加初始迁移</span><span class="sxs-lookup"><span data-stu-id="61853-151">Perform initial migration</span></span>

<span data-ttu-id="61853-152">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="61853-152">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="61853-153">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="61853-153">Add an initial migration.</span></span>
* <span data-ttu-id="61853-154">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="61853-154">Update the database with the initial migration.</span></span>

<span data-ttu-id="61853-155">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="61853-155">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="61853-157">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="61853-157">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="61853-158">或者，可在项目文件夹中使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="61853-158">Alternatively, the following .NET Core CLI commands can be used from the project folder:</span></span>

```console
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="61853-159">忽略以下警告消息，后续教程将对此进行修复：</span><span class="sxs-lookup"><span data-stu-id="61853-159">Ignore the following warning message, you fix that in a a later tutorial:</span></span>

`Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*

<span data-ttu-id="61853-160">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="61853-160">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="61853-161">此架构的依据为 `RazorPagesMovieContext` 中指定的模型（在 Data/RazorPagesMovieContext.cs 文件中）。</span><span class="sxs-lookup"><span data-stu-id="61853-161">The schema is based on the model specified in the `RazorPagesMovieContext` (In the *Data/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="61853-162">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="61853-162">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="61853-163">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="61853-163">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="61853-164">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="61853-164">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="61853-165">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="61853-165">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<span data-ttu-id="61853-166">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="61853-166">If you get the error:</span></span>

`SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.`

<span data-ttu-id="61853-167">缺少[迁移步骤](#pmc)。</span><span class="sxs-lookup"><span data-stu-id="61853-167">You missed the [migrations step](#pmc).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="61853-168">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="61853-168">Add a data model</span></span>

<span data-ttu-id="61853-169">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="61853-169">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="61853-170">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="61853-170">Name the folder *Models*.</span></span>

<span data-ttu-id="61853-171">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="61853-171">Right click the *Models* folder.</span></span> <span data-ttu-id="61853-172">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="61853-172">Select **Add** > **Class**.</span></span> <span data-ttu-id="61853-173">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="61853-173">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="61853-174">添加数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="61853-174">Add a database connection string</span></span>

<span data-ttu-id="61853-175">将连接字符串添加到 appsettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="61853-175">Add a connection string to the *appsettings.json* file.</span></span>

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="61853-176">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="61853-176">Register the database context</span></span>

<span data-ttu-id="61853-177">在 [Startup 类的 ConfigureServices 方法](xref:fundamentals/startup#the-startup-class) (Startup.cs) 中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="61853-177">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the [ConfigureServices method of the Startup class](xref:fundamentals/startup#the-startup-class) (*Startup.cs*):</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

<span data-ttu-id="61853-178">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="61853-178">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="61853-179">添加基架工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="61853-179">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="61853-180">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="61853-180">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="61853-181">添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="61853-181">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="61853-182">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="61853-182">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="61853-183">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="61853-183">Add an initial migration.</span></span>
* <span data-ttu-id="61853-184">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="61853-184">Update the database with the initial migration.</span></span>

<span data-ttu-id="61853-185">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="61853-185">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="61853-187">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="61853-187">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

<span data-ttu-id="61853-188">或者，可使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="61853-188">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="61853-189">忽略以下消息：</span><span class="sxs-lookup"><span data-stu-id="61853-189">Ignore the following message:</span></span>

    `Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'*

<span data-ttu-id="61853-190">下一教程将对此进行修复。</span><span class="sxs-lookup"><span data-stu-id="61853-190">You fix that in the next tutorial.</span></span>

<span data-ttu-id="61853-191">`Install-Package` 命令安装运行基架引擎所需的工具。</span><span class="sxs-lookup"><span data-stu-id="61853-191">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="61853-192">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="61853-192">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="61853-193">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="61853-193">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="61853-194">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="61853-194">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="61853-195">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="61853-195">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="61853-196">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="61853-196">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="61853-197">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="61853-197">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="61853-198">测试应用</span><span class="sxs-lookup"><span data-stu-id="61853-198">Test the app</span></span>

* <span data-ttu-id="61853-199">运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="61853-199">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="61853-200">测试“创建”链接。</span><span class="sxs-lookup"><span data-stu-id="61853-200">Test the **Create** link.</span></span>

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="61853-202">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="61853-202">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="61853-203">如果收到 SQL 异常，则验证是否已运行迁移并更新了数据库。</span><span class="sxs-lookup"><span data-stu-id="61853-203">If you get a SQL exception, verify you have run migrations and updated the database.</span></span>

<span data-ttu-id="61853-204">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="61853-204">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="61853-205">[上一篇：入门](xref:tutorials/razor-pages/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="61853-205">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>
