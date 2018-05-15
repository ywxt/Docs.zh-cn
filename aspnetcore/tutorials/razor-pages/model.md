---
title: 在 ASP.NET Core 中向 Razor 页面应用添加模型
author: rick-anderson
description: 了解如何使用 Entity Framework Core (EF Core) 添加用于管理数据库中的影片的类。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 07/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/model
ms.openlocfilehash: a288b454ac1b418ef0deacb3643be22d440cb938
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="2ab1f-103">在 ASP.NET Core 中向 Razor 页面应用添加模型</span><span class="sxs-lookup"><span data-stu-id="2ab1f-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="2ab1f-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="2ab1f-104">Add a data model</span></span>

<span data-ttu-id="2ab1f-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="2ab1f-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-106">Name the folder *Models*.</span></span>

<span data-ttu-id="2ab1f-107">右键单击“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-107">Right click the *Models* folder.</span></span> <span data-ttu-id="2ab1f-108">选择“添加” > “类”。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="2ab1f-109">将类命名为“Movie”，并添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="2ab1f-109">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](../../includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="2ab1f-110">添加数据库连接字符串</span><span class="sxs-lookup"><span data-stu-id="2ab1f-110">Add a database connection string</span></span>

<span data-ttu-id="2ab1f-111">将连接字符串添加到 appsettings.json 文件。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-111">Add a connection string to the *appsettings.json* file.</span></span>

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="2ab1f-112">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="2ab1f-112">Register the database context</span></span>

<span data-ttu-id="2ab1f-113">使用 Startup.cs 文件中的[依存关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-113">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the *Startup.cs* file.</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

<span data-ttu-id="2ab1f-114">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-114">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="2ab1f-115">添加基架工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="2ab1f-115">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="2ab1f-116">在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2ab1f-116">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="2ab1f-117">添加 Visual Studio Web 代码生成包。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-117">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="2ab1f-118">必须添加此包才能运行基架引擎。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-118">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="2ab1f-119">添加初始迁移。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-119">Add an initial migration.</span></span>
* <span data-ttu-id="2ab1f-120">使用初始迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-120">Update the database with the initial migration.</span></span>

<span data-ttu-id="2ab1f-121">从“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-121">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="2ab1f-123">在 PMC 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2ab1f-123">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Add-Migration Initial
Update-Database
```

<span data-ttu-id="2ab1f-124">或者，可使用以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="2ab1f-124">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="2ab1f-125">`Install-Package` 命令安装运行基架引擎所需的工具。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-125">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="2ab1f-126">`Add-Migration` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-126">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="2ab1f-127">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-127">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="2ab1f-128">`Initial` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-128">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="2ab1f-129">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-129">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="2ab1f-130">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-130">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="2ab1f-131">`Update-Database` 命令在用于创建数据库的 Migrations/\<time-stamp>_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-131">The `Update-Database` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](../../includes/RP/model4Win.md)]

[!INCLUDE [model 4](../../includes/RP/model4tbl.md)]

<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="2ab1f-132">测试应用</span><span class="sxs-lookup"><span data-stu-id="2ab1f-132">Test the app</span></span>

* <span data-ttu-id="2ab1f-133">运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-133">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="2ab1f-134">测试“创建”链接。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-134">Test the **Create** link.</span></span>

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="2ab1f-136">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-136">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="2ab1f-137">如果收到 SQL 异常，则验证是否已运行迁移并更新了数据库：</span><span class="sxs-lookup"><span data-stu-id="2ab1f-137">If you get a SQL exception, verify you have run migrations and updated the database:</span></span>

<span data-ttu-id="2ab1f-138">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="2ab1f-138">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2ab1f-139">[上一篇：入门](xref:tutorials/razor-pages/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="2ab1f-139">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>    
