---
title: 在 ASP.NET Core 中向 Razor 页面应用添加模型
author: rick-anderson
description: 了解如何使用 Entity Framework Core (EF Core) 添加用于管理数据库中的影片的类。
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: 0d33901805d6728fb8006f14d41090b874ab28b1
ms.sourcegitcommit: e8d80ff566bfe505b43389d7bc4551edb1c0c872
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52549105"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="9d64f-103">在 ASP.NET Core 中向 Razor 页面应用添加模型</span><span class="sxs-lookup"><span data-stu-id="9d64f-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="9d64f-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="9d64f-104">Add a data model</span></span>

<span data-ttu-id="9d64f-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="9d64f-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-106">Name the folder *Models*.</span></span>

<span data-ttu-id="9d64f-107">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="9d64f-107">Right click the *Models* folder.</span></span> <span data-ttu-id="9d64f-108">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="9d64f-109">将该类命名为 Movie 并将 `Movie` 内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9d64f-109">Name the class **Movie** and replace the contents of the `Movie` class with the following code:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="9d64f-110">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="9d64f-110">Scaffold the movie model</span></span>

<span data-ttu-id="9d64f-111">在此部分，将搭建“电影”模型的基架。</span><span class="sxs-lookup"><span data-stu-id="9d64f-111">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="9d64f-112">确切地说，基架工具将生成页面，用于对“电影”模型执行创建、读取、更新和删除 (CRUD) 操作。</span><span class="sxs-lookup"><span data-stu-id="9d64f-112">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<span data-ttu-id="9d64f-113">创建“Pages/Movies”文件夹：</span><span class="sxs-lookup"><span data-stu-id="9d64f-113">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="9d64f-114">在解决方案资源管理器中，右键单击“Pages”文件夹 >“添加”>“新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-114">In **Solution Explorer**, right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="9d64f-115">将文件夹命名为“Movies”</span><span class="sxs-lookup"><span data-stu-id="9d64f-115">Name the folder *Movies*</span></span>

<span data-ttu-id="9d64f-116">在解决方案资源管理器中，右键单击“Pages/Movies”文件夹 >“添加”>“新搭建基架的项目”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-116">In **Solution Explorer**, right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![上述说明的图像。](model/_static/sca.png)

<span data-ttu-id="9d64f-118">在“添加基架”对话框中，选择“使用实体框架生成 Razor Pages (CRUD)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-118">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **Add**.</span></span>

![上述说明的图像。](model/_static/add_scaffold.png)

<span data-ttu-id="9d64f-120">完成“使用实体框架(CRUD)添加 Razor Pages”对话框：</span><span class="sxs-lookup"><span data-stu-id="9d64f-120">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="9d64f-121">在“模型类”下拉列表中，选择“Movie (RazorPagesMovie.Models)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-121">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="9d64f-122">在“数据上下文类”行中，选择 +（加号）并接受生成的名称“RazorPagesMovie.Models.RazorPagesMovieContext”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-122">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="9d64f-123">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-123">Select **Add**.</span></span>

![上述说明的图像。](model/_static/arp.png)

<span data-ttu-id="9d64f-125">在搭建基架时，会创建并更新以下文件：</span><span class="sxs-lookup"><span data-stu-id="9d64f-125">The scaffold process creates and updates the following files:</span></span>

### <a name="files-created"></a><span data-ttu-id="9d64f-126">创建的文件</span><span class="sxs-lookup"><span data-stu-id="9d64f-126">Files created</span></span>

* <span data-ttu-id="9d64f-127">Pages/Movies：“创建”、“删除”、“详细信息”、“编辑”、“索引”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-127">*Pages/Movies*: Create, Delete, Details, Edit, Index.</span></span> <span data-ttu-id="9d64f-128">将在下一教程中详细介绍这些页面。</span><span class="sxs-lookup"><span data-stu-id="9d64f-128">These pages are detailed in the next tutorial.</span></span>
* <span data-ttu-id="9d64f-129">Data/RazorPagesMovieContext.cs</span><span class="sxs-lookup"><span data-stu-id="9d64f-129">*Data/RazorPagesMovieContext.cs*</span></span>

### <a name="file-updated"></a><span data-ttu-id="9d64f-130">文件已更新</span><span class="sxs-lookup"><span data-stu-id="9d64f-130">File updated</span></span>

* <span data-ttu-id="9d64f-131">Startup.cs：下一部分详细介绍对此文件所作的更改。</span><span class="sxs-lookup"><span data-stu-id="9d64f-131">*Startup.cs*: Changes to this file are detailed in the next section.</span></span>
* <span data-ttu-id="9d64f-132">appsettings.json：添加用于连接到本地数据的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9d64f-132">*appsettings.json*: The connection string used to connect to a local database is added.</span></span>

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="9d64f-133">检查通过依赖关系注入注册的上下文</span><span class="sxs-lookup"><span data-stu-id="9d64f-133">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="9d64f-134">ASP.NET Core 通过[依赖关系注入](xref:fundamentals/dependency-injection)进行生成。</span><span class="sxs-lookup"><span data-stu-id="9d64f-134">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="9d64f-135">服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。</span><span class="sxs-lookup"><span data-stu-id="9d64f-135">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="9d64f-136">需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。</span><span class="sxs-lookup"><span data-stu-id="9d64f-136">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="9d64f-137">本教程的后续部分介绍了用于获取 DB 上下文实例的构造函数代码。</span><span class="sxs-lookup"><span data-stu-id="9d64f-137">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="9d64f-138">基架工具自动创建 DB 上下文并将其注册到依赖关系注入容器。</span><span class="sxs-lookup"><span data-stu-id="9d64f-138">The scaffolding tool automatically created a DB context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="9d64f-139">检查 `Startup.ConfigureServices` 方法。</span><span class="sxs-lookup"><span data-stu-id="9d64f-139">Examine the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="9d64f-140">基架添加了突出显示的行：</span><span class="sxs-lookup"><span data-stu-id="9d64f-140">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

<span data-ttu-id="9d64f-141">数据库上下文类是为给定数据模型协调 EF Core 功能的主类。</span><span class="sxs-lookup"><span data-stu-id="9d64f-141">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="9d64f-142">数据上下文派生自 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-142">The data context is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="9d64f-143">数据上下文指定数据模型中包含哪些实体。</span><span class="sxs-lookup"><span data-stu-id="9d64f-143">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="9d64f-144">在此项目中将数据库上下文类命名为 `RazorPagesMovieContext`。</span><span class="sxs-lookup"><span data-stu-id="9d64f-144">In this project, the class is named `RazorPagesMovieContext`.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Data/RazorPagesMovieContext.cs)]

<span data-ttu-id="9d64f-145">前面的代码为实体集创建 [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 属性。</span><span class="sxs-lookup"><span data-stu-id="9d64f-145">The preceding code creates a [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for the entity set.</span></span> <span data-ttu-id="9d64f-146">在实体框架术语中，实体集通常与数据表相对应。</span><span class="sxs-lookup"><span data-stu-id="9d64f-146">In Entity Framework terminology, an entity set typically corresponds to a database table.</span></span> <span data-ttu-id="9d64f-147">实体对应表中的行。</span><span class="sxs-lookup"><span data-stu-id="9d64f-147">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="9d64f-148">通过调用 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 对象中的一个方法将连接字符串名称传递到上下文。</span><span class="sxs-lookup"><span data-stu-id="9d64f-148">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="9d64f-149">进行本地开发时， [ASP.NET Core 配置系统](xref:fundamentals/configuration/index) 在 *appsettings.json* 文件中读取数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9d64f-149">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<a name="pmc"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="9d64f-150">添加初始迁移</span><span class="sxs-lookup"><span data-stu-id="9d64f-150">Perform initial migration</span></span>

<span data-ttu-id="9d64f-151">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9d64f-151">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="9d64f-152">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="9d64f-152">Add an initial migration.</span></span>
* <span data-ttu-id="9d64f-153">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9d64f-153">Update the database with the initial migration.</span></span>

<span data-ttu-id="9d64f-154">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-154">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="9d64f-156">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9d64f-156">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="9d64f-157">或者，可在项目文件夹中使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="9d64f-157">Alternatively, the following .NET Core CLI commands can be used from the project folder:</span></span>

```console
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="9d64f-158">忽略以下警告消息，后续教程将对此进行修复：</span><span class="sxs-lookup"><span data-stu-id="9d64f-158">Ignore the following warning message, which you fix in a later tutorial:</span></span>

```console
Microsoft.EntityFrameworkCore.Model.Validation[30000]
      No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.
```

<span data-ttu-id="9d64f-159">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="9d64f-159">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="9d64f-160">此架构的依据为 `RazorPagesMovieContext` 中指定的模型（在 Data/RazorPagesMovieContext.cs 文件中）。</span><span class="sxs-lookup"><span data-stu-id="9d64f-160">The schema is based on the model specified in the `RazorPagesMovieContext` (In the *Data/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="9d64f-161">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="9d64f-161">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="9d64f-162">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="9d64f-162">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="9d64f-163">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-163">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="9d64f-164">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="9d64f-164">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<span data-ttu-id="9d64f-165">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="9d64f-165">If you get the error:</span></span>

```console
SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.
```

<span data-ttu-id="9d64f-166">缺少[迁移步骤](#pmc)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-166">You missed the [migrations step](#pmc).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="9d64f-167">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="9d64f-167">Add a data model</span></span>

<span data-ttu-id="9d64f-168">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-168">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="9d64f-169">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-169">Name the folder *Models*.</span></span>

<span data-ttu-id="9d64f-170">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="9d64f-170">Right click the *Models* folder.</span></span> <span data-ttu-id="9d64f-171">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-171">Select **Add** > **Class**.</span></span> <span data-ttu-id="9d64f-172">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="9d64f-172">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="9d64f-173">添加数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="9d64f-173">Add a database connection string</span></span>

<span data-ttu-id="9d64f-174">将连接字符串添加到 appsettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="9d64f-174">Add a connection string to the *appsettings.json* file.</span></span>

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="9d64f-175">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="9d64f-175">Register the database context</span></span>

<span data-ttu-id="9d64f-176">在 [Startup 类的 ConfigureServices 方法](xref:fundamentals/startup#the-startup-class) (Startup.cs) 中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="9d64f-176">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the [ConfigureServices method of the Startup class](xref:fundamentals/startup#the-startup-class) (*Startup.cs*):</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

<span data-ttu-id="9d64f-177">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="9d64f-177">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="9d64f-178">添加基架工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="9d64f-178">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="9d64f-179">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9d64f-179">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="9d64f-180">添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="9d64f-180">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="9d64f-181">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="9d64f-181">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="9d64f-182">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="9d64f-182">Add an initial migration.</span></span>
* <span data-ttu-id="9d64f-183">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9d64f-183">Update the database with the initial migration.</span></span>

<span data-ttu-id="9d64f-184">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="9d64f-184">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="9d64f-186">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9d64f-186">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

<span data-ttu-id="9d64f-187">或者，可使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="9d64f-187">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="9d64f-188">忽略以下消息：</span><span class="sxs-lookup"><span data-stu-id="9d64f-188">Ignore the following message:</span></span>

```console
Microsoft.EntityFrameworkCore.Model.Validation[30000]
      No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'
```

<span data-ttu-id="9d64f-189">下一教程将对此进行修复。</span><span class="sxs-lookup"><span data-stu-id="9d64f-189">You fix that in the next tutorial.</span></span>

<span data-ttu-id="9d64f-190">`Install-Package` 命令安装运行基架引擎所需的工具。</span><span class="sxs-lookup"><span data-stu-id="9d64f-190">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="9d64f-191">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="9d64f-191">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="9d64f-192">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="9d64f-192">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="9d64f-193">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="9d64f-193">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="9d64f-194">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="9d64f-194">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="9d64f-195">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-195">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="9d64f-196">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="9d64f-196">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="9d64f-197">测试应用</span><span class="sxs-lookup"><span data-stu-id="9d64f-197">Test the app</span></span>

* <span data-ttu-id="9d64f-198">运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-198">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="9d64f-199">测试“创建”链接。</span><span class="sxs-lookup"><span data-stu-id="9d64f-199">Test the **Create** link.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9d64f-200">可能无法在 `Price` 字段中输入十进制逗号。</span><span class="sxs-lookup"><span data-stu-id="9d64f-200">You may not be able to enter decimal commas in the `Price` field.</span></span> <span data-ttu-id="9d64f-201">若要使 [jQuery 验证](https://jqueryvalidation.org/)支持使用逗号（“,”）表示小数点的的非英语区域设置，以及支持非美国英语日期格式，必须使应用全球化。</span><span class="sxs-lookup"><span data-stu-id="9d64f-201">To support [jQuery validation](https://jqueryvalidation.org/) for non-English locales that use a comma (",") for a decimal point and for non US-English date formats, you must globalize your app.</span></span> <span data-ttu-id="9d64f-202">有关全球化的说明，请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420)。</span><span class="sxs-lookup"><span data-stu-id="9d64f-202">For globalization instructions, see [this GitHub issue](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420).</span></span>

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="9d64f-204">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="9d64f-204">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="9d64f-205">如果收到 SQL 异常，则验证是否已运行迁移并更新了数据库。</span><span class="sxs-lookup"><span data-stu-id="9d64f-205">If you get a SQL exception, verify you have run migrations and updated the database.</span></span>

<span data-ttu-id="9d64f-206">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="9d64f-206">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d64f-207">[上一篇：入门](xref:tutorials/razor-pages/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="9d64f-207">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>
