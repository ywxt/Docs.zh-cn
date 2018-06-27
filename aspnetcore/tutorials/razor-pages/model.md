---
title: 在 ASP.NET Core 中向 Razor 页面应用添加模型
author: rick-anderson
description: 了解如何使用 Entity Framework Core (EF Core) 添加用于管理数据库中的影片的类。
manager: wpickett
ms.author: riande
ms.date: 5/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/model
ms.openlocfilehash: 50b1b01448ad870a2889db7dfe8367ab9e661840
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729958"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="68143-103">在 ASP.NET Core 中向 Razor 页面应用添加模型</span><span class="sxs-lookup"><span data-stu-id="68143-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="68143-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="68143-104">Add a data model</span></span>

<span data-ttu-id="68143-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="68143-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="68143-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="68143-106">Name the folder *Models*.</span></span>

<span data-ttu-id="68143-107">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="68143-107">Right click the *Models* folder.</span></span> <span data-ttu-id="68143-108">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="68143-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="68143-109">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="68143-109">Name the class **Movie** and add the following properties:</span></span>

<span data-ttu-id="68143-110">将 `Movie` 类的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="68143-110">Replace the contents of the `Movie` class with the following code:</span></span>

<span data-ttu-id="68143-111">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]</span><span class="sxs-lookup"><span data-stu-id="68143-111">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]</span></span>

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="68143-112">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="68143-112">Scaffold the movie model</span></span>

<span data-ttu-id="68143-113">在此部分，将搭建“电影”模型的基架。</span><span class="sxs-lookup"><span data-stu-id="68143-113">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="68143-114">确切地说，基架工具将生成页面，用于对“电影”模型执行创建、读取、更新和删除 (CRUD) 操作。</span><span class="sxs-lookup"><span data-stu-id="68143-114">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<span data-ttu-id="68143-115">创建“Pages/Movies”文件夹：</span><span class="sxs-lookup"><span data-stu-id="68143-115">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="68143-116">在解决方案资源管理器中，右键单击“Pages”文件夹 >“添加”>“新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="68143-116">In **Solution Explorer**, right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="68143-117">将文件夹命名为“Movies”</span><span class="sxs-lookup"><span data-stu-id="68143-117">Name the folder *Movies*</span></span>

<span data-ttu-id="68143-118">在解决方案资源管理器中，右键单击“Pages/Movies”文件夹 >“添加”>“新搭建基架的项目”。</span><span class="sxs-lookup"><span data-stu-id="68143-118">In **Solution Explorer**, right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![上述说明的图像。](model/_static/sca.png)

<span data-ttu-id="68143-120">在“添加基架”对话框中，选择“使用实体框架生成 Razor Pages (CRUD)”>“添加”。</span><span class="sxs-lookup"><span data-stu-id="68143-120">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **ADD**.</span></span>

![上述说明的图像。](model/_static/add_scaffold.png)

<span data-ttu-id="68143-122">完成“使用实体框架(CRUD)添加 Razor Pages”对话框：</span><span class="sxs-lookup"><span data-stu-id="68143-122">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="68143-123">在“模型类”下拉列表中，选择“Movie (RazorPagesMovie.Models)。</span><span class="sxs-lookup"><span data-stu-id="68143-123">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="68143-124">在“数据上下文类”行中，选择 +（加号）并接受生成的名称“RazorPagesMovie.Models.RazorPagesMovieContext”。</span><span class="sxs-lookup"><span data-stu-id="68143-124">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="68143-125">在“数据上下文类”下拉列表中，选择“RazorPagesMovie.Models.RazorPagesMovieContext”</span><span class="sxs-lookup"><span data-stu-id="68143-125">In the **Data context class** drop down,  select **RazorPagesMovie.Models.RazorPagesMovieContext**</span></span>
* <span data-ttu-id="68143-126">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="68143-126">Select **Add**.</span></span>

![上述说明的图像。](model/_static/arp.png)

<a name="pmc"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="68143-128">添加初始迁移</span><span class="sxs-lookup"><span data-stu-id="68143-128">Perform initial migration</span></span>

<span data-ttu-id="68143-129">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="68143-129">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="68143-130">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="68143-130">Add an initial migration.</span></span>
* <span data-ttu-id="68143-131">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="68143-131">Update the database with the initial migration.</span></span>

<span data-ttu-id="68143-132">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="68143-132">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="68143-134">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="68143-134">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="68143-135">或者，可使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="68143-135">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="68143-136">忽略以下警告消息，下一教程将对此进行修复：</span><span class="sxs-lookup"><span data-stu-id="68143-136">Ignore the following warning message, you fix that in the next tutorial:</span></span>

`Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*

<span data-ttu-id="68143-137">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="68143-137">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="68143-138">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="68143-138">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="68143-139">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="68143-139">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="68143-140">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="68143-140">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="68143-141">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="68143-141">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="68143-142">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="68143-142">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<span data-ttu-id="68143-143">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="68143-143">If you get the error:</span></span>

<span data-ttu-id="68143-144">SqlException：无法打开登录请求的数据库“RazorPagesMovieContext-GUID”。</span><span class="sxs-lookup"><span data-stu-id="68143-144">SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login.</span></span> <span data-ttu-id="68143-145">登录失败。</span><span class="sxs-lookup"><span data-stu-id="68143-145">The login failed.</span></span>
<span data-ttu-id="68143-146">用户“用户名”登录失败。</span><span class="sxs-lookup"><span data-stu-id="68143-146">Login failed for user 'User-name'.</span></span>

<span data-ttu-id="68143-147">缺少[迁移步骤](#pmc)。</span><span class="sxs-lookup"><span data-stu-id="68143-147">You missed the [migrations step](#pmc).</span></span>
::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="68143-148">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="68143-148">Add a data model</span></span>

<span data-ttu-id="68143-149">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="68143-149">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="68143-150">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="68143-150">Name the folder *Models*.</span></span>

<span data-ttu-id="68143-151">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="68143-151">Right click the *Models* folder.</span></span> <span data-ttu-id="68143-152">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="68143-152">Select **Add** > **Class**.</span></span> <span data-ttu-id="68143-153">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="68143-153">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="68143-154">添加数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="68143-154">Add a database connection string</span></span>

<span data-ttu-id="68143-155">将连接字符串添加到 appsettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="68143-155">Add a connection string to the *appsettings.json* file.</span></span>

<span data-ttu-id="68143-156">[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]</span><span class="sxs-lookup"><span data-stu-id="68143-156">[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]</span></span>

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="68143-157">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="68143-157">Register the database context</span></span>

<span data-ttu-id="68143-158">在 [Startup 类的 ConfigureServices 方法](xref:fundamentals/startup#the-startup-class) (Startup.cs) 中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="68143-158">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the [ConfigureServices method of the Startup class](xref:fundamentals/startup#the-startup-class) (*Startup.cs*):</span></span>

<span data-ttu-id="68143-159">[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]</span><span class="sxs-lookup"><span data-stu-id="68143-159">[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]</span></span>

<span data-ttu-id="68143-160">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="68143-160">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="68143-161">添加基架工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="68143-161">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="68143-162">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="68143-162">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="68143-163">添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="68143-163">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="68143-164">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="68143-164">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="68143-165">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="68143-165">Add an initial migration.</span></span>
* <span data-ttu-id="68143-166">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="68143-166">Update the database with the initial migration.</span></span>

<span data-ttu-id="68143-167">从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="68143-167">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="68143-169">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="68143-169">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

<span data-ttu-id="68143-170">或者，可使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="68143-170">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="68143-171">忽略以下消息：</span><span class="sxs-lookup"><span data-stu-id="68143-171">Ignore the following message:</span></span>

    `Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'*

<span data-ttu-id="68143-172">下一教程将对此进行修复。</span><span class="sxs-lookup"><span data-stu-id="68143-172">You fix that in the next tutorial.</span></span>

<span data-ttu-id="68143-173">`Install-Package` 命令安装运行基架引擎所需的工具。</span><span class="sxs-lookup"><span data-stu-id="68143-173">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="68143-174">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="68143-174">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="68143-175">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="68143-175">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="68143-176">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="68143-176">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="68143-177">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="68143-177">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="68143-178">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="68143-178">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="68143-179">`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="68143-179">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="68143-180">测试应用</span><span class="sxs-lookup"><span data-stu-id="68143-180">Test the app</span></span>

* <span data-ttu-id="68143-181">运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="68143-181">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="68143-182">测试“创建”链接。</span><span class="sxs-lookup"><span data-stu-id="68143-182">Test the **Create** link.</span></span>

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="68143-184">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="68143-184">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="68143-185">如果收到 SQL 异常，则验证是否已运行迁移并更新了数据库。</span><span class="sxs-lookup"><span data-stu-id="68143-185">If you get a SQL exception, verify you have run migrations and updated the database.</span></span>

<span data-ttu-id="68143-186">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="68143-186">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="68143-187">[上一篇：入门](xref:tutorials/razor-pages/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="68143-187">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>    
