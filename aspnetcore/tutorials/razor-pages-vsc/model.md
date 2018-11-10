---
title: 使用 Visual Studio Code 将模型添加到 ASP.NET Core Razor 页面应用
author: rick-anderson
description: 了解如何使用 Visual Studio Code 将模型添加到 ASP.NET Core 中的 Razor 页面应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: c4aef369bb3965b70d1b461cf63e6f5a26a00628
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244718"
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-code"></a><span data-ttu-id="047da-103">使用 Visual Studio Code 将模型添加到 ASP.NET Core Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="047da-103">Add a model to an ASP.NET Core Razor Pages app with Visual Studio Code</span></span>

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="047da-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="047da-104">Add a data model</span></span>

* <span data-ttu-id="047da-105">添加名为“Models”的文件夹。</span><span class="sxs-lookup"><span data-stu-id="047da-105">Add a folder named *Models*.</span></span>
* <span data-ttu-id="047da-106">将类添加到名为“Movie.cs”的“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="047da-106">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="047da-107">将以下代码添加到“Models/Movie.cs”文件：</span><span class="sxs-lookup"><span data-stu-id="047da-107">Add the following code to the *Models/Movie.cs* file:</span></span>

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

### <a name="entity-framework-core-nuget-package-for-sqlite"></a><span data-ttu-id="047da-108">适用于 SQLite 的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="047da-108">Entity Framework Core NuGet package for SQLite</span></span>

<span data-ttu-id="047da-109">从命令行运行以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="047da-109">From the command line, run the following .NET Core CLI command:</span></span>

```console
dotnet add package Microsoft.EntityFrameworkCore.SQLite
```

<a name="reg"></a>

### <a name="register-the-database-context"></a><span data-ttu-id="047da-110">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="047da-110">Register the database context</span></span>

<span data-ttu-id="047da-111">使用 Startup.cs 文件中的[依存关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="047da-111">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the *Startup.cs* file.</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=10-11)]

<span data-ttu-id="047da-112">将以下 `using` 语句添加到 Startup.cs 顶部：</span><span class="sxs-lookup"><span data-stu-id="047da-112">Add the following `using` statements at the top of *Startup.cs*:</span></span>

```csharp
using RazorPagesMovie.Models;
using Microsoft.EntityFrameworkCore;
```

<span data-ttu-id="047da-113">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="047da-113">Build the project to verify you don't have any errors.</span></span>

[!INCLUDE [model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>

### <a name="scaffold-the-movie-model"></a><span data-ttu-id="047da-114">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="047da-114">Scaffold the Movie model</span></span>

* <span data-ttu-id="047da-115">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="047da-115">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="047da-116">**对于 Windows**：运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="047da-116">**For Windows**: Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="047da-117">**对于 macOS 和 Linux**：运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="047da-117">**For macOS and Linux**: Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

[!INCLUDE [model 4](../../includes/RP/model4.md)]

<span data-ttu-id="047da-118">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="047da-118">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="047da-119">[上一篇：入门](xref:tutorials/razor-pages-vsc/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages-vsc/page)</span><span class="sxs-lookup"><span data-stu-id="047da-119">[Previous: Get Started](xref:tutorials/razor-pages-vsc/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages-vsc/page)</span></span>
