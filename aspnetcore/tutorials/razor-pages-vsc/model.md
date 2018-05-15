---
title: 使用 Visual Studio Code 将模型添加到 ASP.NET Core Razor 页面应用
author: rick-anderson
description: 了解如何使用 Visual Studio Code 将模型添加到 ASP.NET Core 中的 Razor 页面应用。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: 20282b491162e9f35e40702655532a78edceb89a
ms.sourcegitcommit: 2ab550f8c46e1a8a5d45e58be44d151c676af256
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-code"></a><span data-ttu-id="35a7d-103">使用 Visual Studio Code 将模型添加到 ASP.NET Core Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="35a7d-103">Add a model to an ASP.NET Core Razor Pages app with Visual Studio Code</span></span>

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="35a7d-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="35a7d-104">Add a data model</span></span>

* <span data-ttu-id="35a7d-105">添加名为“Models”的文件夹。</span><span class="sxs-lookup"><span data-stu-id="35a7d-105">Add a folder named *Models*.</span></span>
* <span data-ttu-id="35a7d-106">将类添加到名为“Movie.cs”的“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="35a7d-106">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="35a7d-107">将以下代码添加到“Models/Movie.cs”文件：</span><span class="sxs-lookup"><span data-stu-id="35a7d-107">Add the following code to the *Models/Movie.cs* file:</span></span>

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="35a7d-108">生成项目以确定没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="35a7d-108">Build the project to verify you don't have any errors.</span></span>

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="35a7d-109">用于进行迁移的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="35a7d-109">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="35a7d-110">[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了适用于命令行接口 (CLI) 的 EF 工具。</span><span class="sxs-lookup"><span data-stu-id="35a7d-110">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="35a7d-111">若要安装此包，请将它添加到 .csproj 文件中的 `DotNetCliToolReference` 集合。</span><span class="sxs-lookup"><span data-stu-id="35a7d-111">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="35a7d-112">注意：必须通过编辑 .csproj 文件来安装此包；不能使用 `install-package` 命令或程序包管理器 GUI。</span><span class="sxs-lookup"><span data-stu-id="35a7d-112">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="35a7d-113">编辑 RazorPagesMovie.csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="35a7d-113">Edit the *RazorPagesMovie.csproj* file:</span></span>

* <span data-ttu-id="35a7d-114">选择“文件” > “打开文件”，然后选择 RazorPagesMovie.csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="35a7d-114">Select **File** > **Open File**, and then select the *RazorPagesMovie.csproj* file.</span></span>
* <span data-ttu-id="35a7d-115">将 `Microsoft.EntityFrameworkCore.Tools.DotNet` 的 工具引用添加至第二个 \<ItemGroup>：</span><span class="sxs-lookup"><span data-stu-id="35a7d-115">Add tool reference for `Microsoft.EntityFrameworkCore.Tools.DotNet` to the second **\<ItemGroup>**:</span></span>

[!code-xml[](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj)]

[!INCLUDE [model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="35a7d-116">搭建“电影”模型的基架</span><span class="sxs-lookup"><span data-stu-id="35a7d-116">Scaffold the Movie model</span></span>

* <span data-ttu-id="35a7d-117">打开项目目录（包含 Program.cs、Startup.cs 和 .csproj 文件的目录）中的命令窗口。</span><span class="sxs-lookup"><span data-stu-id="35a7d-117">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="35a7d-118">运行下面的命令：</span><span class="sxs-lookup"><span data-stu-id="35a7d-118">Run the following command:</span></span>

<span data-ttu-id="35a7d-119">**注意：请在 Windows 上运行以下命令。对于 MacOS 和 Linux，请参阅下一个命令**</span><span class="sxs-lookup"><span data-stu-id="35a7d-119">**Note: Run the following command on Windows. For MacOS and Linux, see the next command**</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="35a7d-120">在 MacOS 和 Linux 上，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="35a7d-120">On MacOS and Linux, run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="35a7d-121">如果收到错误：</span><span class="sxs-lookup"><span data-stu-id="35a7d-121">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="35a7d-122">退出 Visual Studio，然后重新运行命令。</span><span class="sxs-lookup"><span data-stu-id="35a7d-122">Exit Visual Studio and run the command again.</span></span>

[!INCLUDE [model 4](../../includes/RP/model4.md)]

<span data-ttu-id="35a7d-123">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="35a7d-123">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35a7d-124">[上一篇：入门](xref:tutorials/razor-pages-vsc/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages-vsc/page)</span><span class="sxs-lookup"><span data-stu-id="35a7d-124">[Previous: Get Started](xref:tutorials/razor-pages-vsc/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages-vsc/page)</span></span>
