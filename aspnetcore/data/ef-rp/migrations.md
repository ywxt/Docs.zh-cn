---
title: ASP.NET Core 中的 Razor 页面和 EF Core - 迁移 - 第 4 个教程（共 8 个）
author: rick-anderson
description: 本教程使用 EF Core 迁移功能管理 ASP.NET Core MVC 应用中的数据模型更改。
manager: wpickett
ms.author: riande
ms.date: 10/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/migrations
ms.openlocfilehash: 690beaabeab098cf9b764730b1bf1bd04bf6b003
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---migrations---4-of-8"></a><span data-ttu-id="3b87e-103">ASP.NET Core 中的 Razor 页面和 EF Core - 迁移 - 第 4 个教程（共 8 个）</span><span class="sxs-lookup"><span data-stu-id="3b87e-103">Razor Pages with EF Core in ASP.NET Core - Migrations - 4 of 8</span></span>

<span data-ttu-id="3b87e-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Jon P Smith](https://twitter.com/thereformedprog) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3b87e-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="3b87e-105">本教程使用 EF Core 迁移功能管理数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="3b87e-105">In this tutorial, the EF Core migrations feature for managing data model changes is used.</span></span>

<span data-ttu-id="3b87e-106">如果遇到无法解决的问题，请下载[本阶段的已完成应用](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-106">If you run into problems you can't solve, download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="3b87e-107">开发新应用时，数据模型会频繁更改。</span><span class="sxs-lookup"><span data-stu-id="3b87e-107">When a new app is developed, the data model changes frequently.</span></span> <span data-ttu-id="3b87e-108">每当模型发生更改时，都无法与数据库进行同步。</span><span class="sxs-lookup"><span data-stu-id="3b87e-108">Each time the model changes, the model gets out of sync with the database.</span></span> <span data-ttu-id="3b87e-109">本教程首先配置 Entity Framework 以创建数据库（如果不存在）。</span><span class="sxs-lookup"><span data-stu-id="3b87e-109">This tutorial started by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="3b87e-110">每当数据模型发生更改时：</span><span class="sxs-lookup"><span data-stu-id="3b87e-110">Each time the data model changes:</span></span>

* <span data-ttu-id="3b87e-111">DB 都会被删除。</span><span class="sxs-lookup"><span data-stu-id="3b87e-111">The DB is dropped.</span></span>
* <span data-ttu-id="3b87e-112">EF 都会创建一个新数据库来匹配该模型。</span><span class="sxs-lookup"><span data-stu-id="3b87e-112">EF creates a new one that matches the model.</span></span>
* <span data-ttu-id="3b87e-113">应用使用测试数据为 DB 设定种子。</span><span class="sxs-lookup"><span data-stu-id="3b87e-113">The app seeds the DB with test data.</span></span>

<span data-ttu-id="3b87e-114">这种使 DB 与数据模型保持同步的方法适用于多种情况，但将应用部署到生产环境的情况除外。</span><span class="sxs-lookup"><span data-stu-id="3b87e-114">This approach to keeping the DB in sync with the data model works well until you deploy the app to production.</span></span> <span data-ttu-id="3b87e-115">当应用在生产环境中运行时，应用通常会存储需要保留的数据。</span><span class="sxs-lookup"><span data-stu-id="3b87e-115">When the app is running in production, it's usually storing data that needs to be maintained.</span></span> <span data-ttu-id="3b87e-116">每当发生更改（例如添加新列）时，应用都无法在具有测试 DB 的环境下启动。</span><span class="sxs-lookup"><span data-stu-id="3b87e-116">The app can't start with a test DB each time a change is made (such as adding a new column).</span></span> <span data-ttu-id="3b87e-117">EF Core 迁移功能可通过使 EF Core 更新 DB 架构而不是创建新 DB 来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="3b87e-117">The EF Core Migrations feature solves this problem by enabling EF Core to update the DB schema instead of creating a new DB.</span></span>

<span data-ttu-id="3b87e-118">数据模型发生更改时，迁移将更新架构并保留现有数据，而无需删除或重新创建 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-118">Rather than dropping and recreating the DB when the data model changes, migrations updates the schema and retains existing data.</span></span>

## <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="3b87e-119">用于进行迁移的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="3b87e-119">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="3b87e-120">要使用迁移，请使用“包管理器控制台”(PMC) 或命令行接口 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-120">To work with migrations, use the **Package Manager Console** (PMC) or the command-line interface (CLI).</span></span> <span data-ttu-id="3b87e-121">以下教程演示如何使用 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-121">These tutorials show how to use CLI commands.</span></span> <span data-ttu-id="3b87e-122">有关 PMC 的信息，请转到[本教程末尾](#pmc)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-122">Information about the PMC is at [the end of this tutorial](#pmc).</span></span>

<span data-ttu-id="3b87e-123">[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了适用于命令行接口 (CLI) 的 EF Core 工具。</span><span class="sxs-lookup"><span data-stu-id="3b87e-123">The EF Core tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="3b87e-124">若要安装此程序包，请将它添加到 .csproj 文件中的 `DotNetCliToolReference` 集合，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3b87e-124">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file, as shown.</span></span> <span data-ttu-id="3b87e-125">**注意：** 必须通过编辑 .csproj 文件来安装此程序包。</span><span class="sxs-lookup"><span data-stu-id="3b87e-125">**Note:** This package must be installed by editing the *.csproj* file.</span></span> <span data-ttu-id="3b87e-126">不能使用 `install-package` 命令或包管理器 GUI 安装此程序包。</span><span class="sxs-lookup"><span data-stu-id="3b87e-126">The`install-package` command or the package manager GUI cannot be used to install this package.</span></span> <span data-ttu-id="3b87e-127">要编辑 .csproj 文件，请右键单击解决方案资源管理器中的项目名称，然后选择“编辑 ContosoUniversity.csproj”。</span><span class="sxs-lookup"><span data-stu-id="3b87e-127">Edit the *.csproj* file by right-clicking the project name in **Solution Explorer** and selecting **Edit ContosoUniversity.csproj**.</span></span>

<span data-ttu-id="3b87e-128">以下标记显示已更新的 .csproj 文件，其中突出显示了 EF Core CLI 工具：</span><span class="sxs-lookup"><span data-stu-id="3b87e-128">The following markup shows the updated *.csproj* file with the EF Core CLI tools highlighted:</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
<span data-ttu-id="3b87e-129">编写本教程时，前面示例中的版本号是最新的。</span><span class="sxs-lookup"><span data-stu-id="3b87e-129">The version numbers in the preceding example were current when the tutorial was written.</span></span> <span data-ttu-id="3b87e-130">请对在其他程序包中发现的 EF Core CLI 工具使用相同的版本。</span><span class="sxs-lookup"><span data-stu-id="3b87e-130">Use the same version for the EF Core CLI tools found in the other packages.</span></span>

## <a name="change-the-connection-string"></a><span data-ttu-id="3b87e-131">更改连接字符串</span><span class="sxs-lookup"><span data-stu-id="3b87e-131">Change the connection string</span></span>

<span data-ttu-id="3b87e-132">在 appsettings.json 文件中，将连接字符串中 DB 名称更改为 ContosoUniversity2。</span><span class="sxs-lookup"><span data-stu-id="3b87e-132">In the *appsettings.json* file, change the name of the DB in the connection string to ContosoUniversity2.</span></span>

[!code-json[](intro/samples/cu/appsettings2.json?range=1-4)]

<span data-ttu-id="3b87e-133">更改连接字符串中的 DB 名称会导致初始迁移创建新的 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-133">Changing the DB name in the connection string causes the first migration to create a new DB.</span></span> <span data-ttu-id="3b87e-134">之所以会创建新的 DB，是因为不存在具有该名称的 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-134">A new DB is created because one with that name doesn't exist.</span></span> <span data-ttu-id="3b87e-135">使用迁移无需更改连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3b87e-135">Changing the connection string isn't required for getting started with migrations.</span></span>

<span data-ttu-id="3b87e-136">更改 DB 名称的另一种方法是删除 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-136">An alternative to changing the DB name is deleting the DB.</span></span> <span data-ttu-id="3b87e-137">使用 SQL Server 对象资源管理器 (SSOX) 或 `database drop` CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="3b87e-137">Use **SQL Server Object Explorer** (SSOX) or the `database drop` CLI command:</span></span>

 ```console
 dotnet ef database drop
 ```

<span data-ttu-id="3b87e-138">下面的部分说明如何运行 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-138">The following section explains how to run CLI commands.</span></span>

## <a name="create-an-initial-migration"></a><span data-ttu-id="3b87e-139">创建初始迁移</span><span class="sxs-lookup"><span data-stu-id="3b87e-139">Create an initial migration</span></span>

<span data-ttu-id="3b87e-140">生成项目。</span><span class="sxs-lookup"><span data-stu-id="3b87e-140">Build the project.</span></span>

<span data-ttu-id="3b87e-141">打开命令窗口并导航到项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="3b87e-141">Open a command window and navigate to the project folder.</span></span> <span data-ttu-id="3b87e-142">项目文件夹包含 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="3b87e-142">The project folder contains the *Startup.cs* file.</span></span>

<span data-ttu-id="3b87e-143">在命令窗口中输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="3b87e-143">Enter the following in the command window:</span></span>

```console
dotnet ef migrations add InitialCreate
```

<span data-ttu-id="3b87e-144">命令窗口显示类似于以下内容的信息：</span><span class="sxs-lookup"><span data-stu-id="3b87e-144">The command window displays information similar to the following:</span></span>

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="3b87e-145">如果迁移失败，并出现消息“无法访问文件...ContosoUniversity.dll，因为它正被另一个进程使用。”</span><span class="sxs-lookup"><span data-stu-id="3b87e-145">If the migration fails with the message "*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*"</span></span> <span data-ttu-id="3b87e-146">：</span><span class="sxs-lookup"><span data-stu-id="3b87e-146">is displayed:</span></span>

* <span data-ttu-id="3b87e-147">停止 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="3b87e-147">Stop IIS Express.</span></span>

   * <span data-ttu-id="3b87e-148">退出并重启 Visual Studio，或</span><span class="sxs-lookup"><span data-stu-id="3b87e-148">Exit and restart Visual Studio, or</span></span>
   * <span data-ttu-id="3b87e-149">在 Windows 系统托盘中找到 IIS Express 图标。</span><span class="sxs-lookup"><span data-stu-id="3b87e-149">Find the IIS Express icon in the Windows System Tray.</span></span>
   * <span data-ttu-id="3b87e-150">右键单击 IIS Express 图标，然后单击“ContosoUniversity”>“停止站点”。</span><span class="sxs-lookup"><span data-stu-id="3b87e-150">Right-click the IIS Express icon, and then click **ContosoUniversity > Stop Site**.</span></span>

<span data-ttu-id="3b87e-151">如果出现错误消息“生成失败。”，</span><span class="sxs-lookup"><span data-stu-id="3b87e-151">If the error message "Build failed."</span></span> <span data-ttu-id="3b87e-152">请再次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-152">is displayed, run the command again.</span></span> <span data-ttu-id="3b87e-153">如果收到此错误，请在本教程底部留下说明。</span><span class="sxs-lookup"><span data-stu-id="3b87e-153">If you get this error, leave a note at the bottom of this tutorial.</span></span>

### <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="3b87e-154">了解 Up 和 Down 方法</span><span class="sxs-lookup"><span data-stu-id="3b87e-154">Examine the Up and Down methods</span></span>

<span data-ttu-id="3b87e-155">EF Core 命令 `migrations add` 已生成用于创建 DB 的代码。</span><span class="sxs-lookup"><span data-stu-id="3b87e-155">The EF Core command `migrations add` generated code to create the DB from.</span></span> <span data-ttu-id="3b87e-156">此迁移代码位于 Migrations\<timestamp>_InitialCreate.cs 文件中。</span><span class="sxs-lookup"><span data-stu-id="3b87e-156">This migrations code is in the *Migrations\<timestamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="3b87e-157">`InitialCreate` 类的 `Up` 的方法创建与数据模型实体集相对应的 DB 表。</span><span class="sxs-lookup"><span data-stu-id="3b87e-157">The `Up` method of the `InitialCreate` class creates the DB tables that correspond to the data model entity sets.</span></span> <span data-ttu-id="3b87e-158">`Down` 方法删除这些表，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="3b87e-158">The `Down` method deletes them, as shown in the following example:</span></span>

[!code-csharp[](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

<span data-ttu-id="3b87e-159">迁移调用 `Up` 方法为迁移实现数据模型更改。</span><span class="sxs-lookup"><span data-stu-id="3b87e-159">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="3b87e-160">输入用于回退更新的命令时，迁移调用 `Down` 方法。</span><span class="sxs-lookup"><span data-stu-id="3b87e-160">When you enter a command to roll back the update, migrations calls the `Down` method.</span></span>

<span data-ttu-id="3b87e-161">前面的代码适用于初始迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-161">The preceding code is for the initial migration.</span></span> <span data-ttu-id="3b87e-162">该代码是运行 `migrations add InitialCreate` 命令时创建的。</span><span class="sxs-lookup"><span data-stu-id="3b87e-162">That code was created when the `migrations add InitialCreate` command was run.</span></span> <span data-ttu-id="3b87e-163">迁移名称参数（本示例中为“InitialCreate”）用于指定文件名。</span><span class="sxs-lookup"><span data-stu-id="3b87e-163">The migration name parameter ("InitialCreate" in the example) is used for the file name.</span></span> <span data-ttu-id="3b87e-164">迁移名称可以是任何有效的文件名。</span><span class="sxs-lookup"><span data-stu-id="3b87e-164">The migration name can be any valid file name.</span></span> <span data-ttu-id="3b87e-165">最好选择能概括迁移中所执行操作的字词或短语。</span><span class="sxs-lookup"><span data-stu-id="3b87e-165">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="3b87e-166">例如，添加了系表的迁移可称为“AddDepartmentTable”。</span><span class="sxs-lookup"><span data-stu-id="3b87e-166">For example, a migration that added a department table might be called "AddDepartmentTable."</span></span>

<span data-ttu-id="3b87e-167">如果创建了初始迁移并且存在 DB：</span><span class="sxs-lookup"><span data-stu-id="3b87e-167">If the initial migration is created and the DB exists:</span></span>

* <span data-ttu-id="3b87e-168">会生成 DB 创建代码。</span><span class="sxs-lookup"><span data-stu-id="3b87e-168">The DB creation code is generated.</span></span>
* <span data-ttu-id="3b87e-169">DB 创建代码不需要运行，因为 DB 已与数据模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="3b87e-169">The DB creation code doesn't need to run because the DB already matches the data model.</span></span> <span data-ttu-id="3b87e-170">即使 DB 创建代码运行也不会做出任何更改，因为 DB 已与数据模型相匹配。</span><span class="sxs-lookup"><span data-stu-id="3b87e-170">If the DB creation code is run, it doesn't make any changes because the DB already matches the data model.</span></span>

<span data-ttu-id="3b87e-171">如果将应用部署到新环境，则必须运行 DB 创建代码才能创建 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-171">When the app is deployed to a new environment, the DB creation code must be run to create the DB.</span></span>

<span data-ttu-id="3b87e-172">以前，需要更改连接字符串才能使用 DB 的新名称。</span><span class="sxs-lookup"><span data-stu-id="3b87e-172">Previously the connection string was changed to use a new name for the DB.</span></span> <span data-ttu-id="3b87e-173">指定的 DB 不存在，因此迁移会创建 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-173">The specified DB doesn't exist, so migrations creates the DB.</span></span>

### <a name="the-data-model-snapshot"></a><span data-ttu-id="3b87e-174">数据模型快照</span><span class="sxs-lookup"><span data-stu-id="3b87e-174">The data model snapshot</span></span>

<span data-ttu-id="3b87e-175">迁移在 Migrations/SchoolContextModelSnapshot.cs 中创建当前数据库架构的快照。</span><span class="sxs-lookup"><span data-stu-id="3b87e-175">Migrations creates a *snapshot* of the current database schema in *Migrations/SchoolContextModelSnapshot.cs*.</span></span> <span data-ttu-id="3b87e-176">添加迁移时，EF 会通过将数据模型与快照文件进行对比来确定已更改的内容。</span><span class="sxs-lookup"><span data-stu-id="3b87e-176">When you add a migration, EF determines what changed by comparing the data model to the snapshot file.</span></span>

<span data-ttu-id="3b87e-177">删除迁移时，请使用 [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-177">When deleting a migration, use the [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) command.</span></span> <span data-ttu-id="3b87e-178">`dotnet ef migrations remove` 删除迁移，并确保正确重置快照。</span><span class="sxs-lookup"><span data-stu-id="3b87e-178">`dotnet ef migrations remove` deletes the migration and ensures the snapshot is correctly reset.</span></span>

<span data-ttu-id="3b87e-179">有关如何使用快照文件的详细信息，请参阅[团队环境中的 EF Core 迁移](/ef/core/managing-schemas/migrations/teams)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-179">See [EF Core Migrations in Team Environments](/ef/core/managing-schemas/migrations/teams) for more information about how the snapshot file is used.</span></span>

## <a name="remove-ensurecreated"></a><span data-ttu-id="3b87e-180">删除 EnsureCreated</span><span class="sxs-lookup"><span data-stu-id="3b87e-180">Remove EnsureCreated</span></span>

<span data-ttu-id="3b87e-181">以前的开发通常使用 `EnsureCreated` 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-181">For early development, the `EnsureCreated` command was used.</span></span> <span data-ttu-id="3b87e-182">本教程将使用迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-182">In this tutorial, migrations is used.</span></span> <span data-ttu-id="3b87e-183">`EnsureCreated` 具有以下限制：</span><span class="sxs-lookup"><span data-stu-id="3b87e-183">`EnsureCreated` has the following limitations:</span></span>

* <span data-ttu-id="3b87e-184">绕过迁移并创建 DB 和架构。</span><span class="sxs-lookup"><span data-stu-id="3b87e-184">Bypasses migrations and creates the DB and schema.</span></span>
* <span data-ttu-id="3b87e-185">不会创建迁移表。</span><span class="sxs-lookup"><span data-stu-id="3b87e-185">Doesn't create a migrations table.</span></span>
* <span data-ttu-id="3b87e-186">不能与迁移一起使用。</span><span class="sxs-lookup"><span data-stu-id="3b87e-186">Can *not* be used with migrations.</span></span>
* <span data-ttu-id="3b87e-187">专门用于在频繁删除并重新创建 DB 的情况下进行测试或快速制作原型。</span><span class="sxs-lookup"><span data-stu-id="3b87e-187">Is designed for testing or rapid prototyping where the DB is dropped and re-created frequently.</span></span>

<span data-ttu-id="3b87e-188">删除 `DbInitializer` 中的以下行：</span><span class="sxs-lookup"><span data-stu-id="3b87e-188">Remove the following line from `DbInitializer`:</span></span>

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a><span data-ttu-id="3b87e-189">在开发过程中将迁移应用于 DB</span><span class="sxs-lookup"><span data-stu-id="3b87e-189">Apply the migration to the DB in development</span></span>

<span data-ttu-id="3b87e-190">在命令窗口中，输入以下内容以创建 DB 和表。</span><span class="sxs-lookup"><span data-stu-id="3b87e-190">In the command window, enter the following to create the DB and tables.</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="3b87e-191">注意：如果 `update` 命令返回“生成失败。”错误：</span><span class="sxs-lookup"><span data-stu-id="3b87e-191">Note: If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="3b87e-192">请再次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-192">Run the command again.</span></span>
* <span data-ttu-id="3b87e-193">如果再次失败，请退出 Visual Studio，然后运行 `update` 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-193">If it fails again, exit Visual Studio and then run the `update` command.</span></span>
* <span data-ttu-id="3b87e-194">请在页面底部留言。</span><span class="sxs-lookup"><span data-stu-id="3b87e-194">Leave a message at the bottom of the page.</span></span>

<span data-ttu-id="3b87e-195">该命令的输出与 `migrations add` 命令的输出相似。</span><span class="sxs-lookup"><span data-stu-id="3b87e-195">The output from the command is similar to the `migrations add` command output.</span></span> <span data-ttu-id="3b87e-196">上面的命令中显示了用于设置 DB 的 SQL 命令的日志。</span><span class="sxs-lookup"><span data-stu-id="3b87e-196">In the preceding command, logs for the SQL commands that set up the DB are displayed.</span></span> <span data-ttu-id="3b87e-197">下面的示例输出中省略了大部分日志：</span><span class="sxs-lookup"><span data-stu-id="3b87e-197">Most of the logs are omitted in the following sample output:</span></span>

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

<span data-ttu-id="3b87e-198">要降低日志消息的详细级别，请更改 appsettings.Development.json 文件中的日志级别。</span><span class="sxs-lookup"><span data-stu-id="3b87e-198">To reduce the level of detail in log messages, change the log levels in the *appsettings.Development.json* file.</span></span> <span data-ttu-id="3b87e-199">有关详细信息，请参阅[日志记录介绍](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-199">For more information, see [Introduction to logging](xref:fundamentals/logging/index).</span></span>

<span data-ttu-id="3b87e-200">使用 SQL Server 对象资源管理器检查 DB。</span><span class="sxs-lookup"><span data-stu-id="3b87e-200">Use **SQL Server Object Explorer** to inspect the DB.</span></span> <span data-ttu-id="3b87e-201">请注意，增加了 `__EFMigrationsHistory` 表。</span><span class="sxs-lookup"><span data-stu-id="3b87e-201">Notice the addition of an `__EFMigrationsHistory` table.</span></span> <span data-ttu-id="3b87e-202">`__EFMigrationsHistory` 表跟踪已应用到 DB 的迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-202">The `__EFMigrationsHistory` table keeps track of which migrations have been applied to the DB.</span></span> <span data-ttu-id="3b87e-203">查看 `__EFMigrationsHistory` 表中的数据，其中显示对应初始迁移的一行数据。</span><span class="sxs-lookup"><span data-stu-id="3b87e-203">View the data in the `__EFMigrationsHistory` table, it shows one row for the first migration.</span></span> <span data-ttu-id="3b87e-204">上面的 CLI 输出示例中最后部分的日志显示了创建此行的 INSERT 语句。</span><span class="sxs-lookup"><span data-stu-id="3b87e-204">The last log in the preceding CLI output example shows the INSERT statement that creates this row.</span></span>

<span data-ttu-id="3b87e-205">运行应用并验证一切正常运行。</span><span class="sxs-lookup"><span data-stu-id="3b87e-205">Run the app and verify that everything works.</span></span>

## <a name="applying-migrations-in-production"></a><span data-ttu-id="3b87e-206">在生产环境中应用迁移</span><span class="sxs-lookup"><span data-stu-id="3b87e-206">Applying migrations in production</span></span>

<span data-ttu-id="3b87e-207">不建议生产应用在应用程序启动时调用 [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-207">We recommend production apps should **not** call [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) at application startup.</span></span> <span data-ttu-id="3b87e-208">不应从服务器场中的应用调用 `Migrate`。</span><span class="sxs-lookup"><span data-stu-id="3b87e-208">`Migrate` shouldn't be called from an app in server farm.</span></span> <span data-ttu-id="3b87e-209">例如，已将应用在云中部署为横向扩展（运行应用的多个示例）的情况。</span><span class="sxs-lookup"><span data-stu-id="3b87e-209">For example, if the app has been cloud deployed with scale-out (multiple instances of the app are running).</span></span>

<span data-ttu-id="3b87e-210">应在部署过程中以受控的方式执行数据库迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-210">Database migration should be done as part of deployment, and in a controlled way.</span></span> <span data-ttu-id="3b87e-211">生产数据库迁移方法包括：</span><span class="sxs-lookup"><span data-stu-id="3b87e-211">Production database migration approaches include:</span></span>

* <span data-ttu-id="3b87e-212">使用迁移创建 SQL 脚本，并在部署过程中使用 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="3b87e-212">Using migrations to create SQL scripts and using the SQL scripts in deployment.</span></span>
* <span data-ttu-id="3b87e-213">在受控的环境中运行 `dotnet ef database update`。</span><span class="sxs-lookup"><span data-stu-id="3b87e-213">Running `dotnet ef database update` from a controlled environment.</span></span>

<span data-ttu-id="3b87e-214">EF Core 使用 `__MigrationsHistory` 表查看是否需要运行任何迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-214">EF Core uses the `__MigrationsHistory` table to see if any migrations need to run.</span></span> <span data-ttu-id="3b87e-215">如果 DB 已是最新，则无需运行迁移。</span><span class="sxs-lookup"><span data-stu-id="3b87e-215">If the DB is up to date, no migration is run.</span></span>

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a><span data-ttu-id="3b87e-216">命令行接口 (CLI) 与包管理器控制台 (PMC)</span><span class="sxs-lookup"><span data-stu-id="3b87e-216">Command-line interface (CLI) vs. Package Manager Console (PMC)</span></span>

<span data-ttu-id="3b87e-217">可通过以下项使用可管理迁移的 EF Core 工具：</span><span class="sxs-lookup"><span data-stu-id="3b87e-217">The EF Core tooling for managing migrations is available from:</span></span>

* <span data-ttu-id="3b87e-218">.NET Core CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-218">.NET Core CLI commands.</span></span>
* <span data-ttu-id="3b87e-219">Visual Studio 包管理器控制台 (PMC) 窗口中的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3b87e-219">The PowerShell cmdlets in the Visual Studio **Package Manager Console** (PMC) window.</span></span>

<span data-ttu-id="3b87e-220">本教程演示如何使用 CLI，但某些开发人员更倾向于使用 PMC。</span><span class="sxs-lookup"><span data-stu-id="3b87e-220">This tutorial shows how to use the CLI, some developers prefer using the PMC.</span></span>

<span data-ttu-id="3b87e-221">适用于 PMC 的 EF Core 命令位于 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 程序包中。</span><span class="sxs-lookup"><span data-stu-id="3b87e-221">The EF Core commands for the PMC are in the [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) package.</span></span> <span data-ttu-id="3b87e-222">此包包含在 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 元包中，因此无需另外安装。</span><span class="sxs-lookup"><span data-stu-id="3b87e-222">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="3b87e-223">**重要说明：** 此程序包与通过编辑 .csproj 文件为 CLI 安装的程序包不同。</span><span class="sxs-lookup"><span data-stu-id="3b87e-223">**Important:** This isn't the same package as the one you install for the CLI by editing the *.csproj* file.</span></span> <span data-ttu-id="3b87e-224">此程序包的名称以 `Tools` 结尾，而 CLI 程序包的名称以 `Tools.DotNet` 结尾。</span><span class="sxs-lookup"><span data-stu-id="3b87e-224">The name of this one ends in `Tools`, unlike the CLI package name which ends in `Tools.DotNet`.</span></span>

<span data-ttu-id="3b87e-225">有关 CLI 命令的详细信息，请参阅 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-225">For more information about the CLI commands, see [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="3b87e-226">有关 PMC 命令的详细信息，请参阅[包管理器控制台 (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-226">For more information about the PMC commands, see [Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3b87e-227">疑难解答</span><span class="sxs-lookup"><span data-stu-id="3b87e-227">Troubleshooting</span></span>

<span data-ttu-id="3b87e-228">请下载[本阶段的已完成应用](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。</span><span class="sxs-lookup"><span data-stu-id="3b87e-228">Download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="3b87e-229">应用会生成以下异常：</span><span class="sxs-lookup"><span data-stu-id="3b87e-229">The app generates the following exception:</span></span>

```text
SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

<span data-ttu-id="3b87e-230">解决方案：运行 `dotnet ef database update`</span><span class="sxs-lookup"><span data-stu-id="3b87e-230">Solution: Run `dotnet ef database update`</span></span>

<span data-ttu-id="3b87e-231">如果 `update` 命令返回“生成失败。”错误：</span><span class="sxs-lookup"><span data-stu-id="3b87e-231">If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="3b87e-232">请再次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="3b87e-232">Run the command again.</span></span>
* <span data-ttu-id="3b87e-233">请在页面底部留言。</span><span class="sxs-lookup"><span data-stu-id="3b87e-233">Leave a message at the bottom of the page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3b87e-234">[上一页](xref:data/ef-rp/sort-filter-page)
> [下一页](xref:data/ef-rp/complex-data-model)</span><span class="sxs-lookup"><span data-stu-id="3b87e-234">[Previous](xref:data/ef-rp/sort-filter-page)
[Next](xref:data/ef-rp/complex-data-model)</span></span>
