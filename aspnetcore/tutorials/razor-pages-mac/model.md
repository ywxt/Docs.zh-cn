---
title: 使用 Visual Studio for Mac 将模型添加到 ASP.NET Core Razor 页面应用
author: rick-anderson
description: 了解如何使用 Visual Studio for Mac 将模型添加到 ASP.NET Core 中的 Razor 页面应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-mac/model
ms.openlocfilehash: 3ca6c9b9988b8335116b7248c6c4a89997d02b14
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273269"
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-for-mac"></a><span data-ttu-id="c3918-103">使用 Visual Studio for Mac 将模型添加到 ASP.NET Core Razor 页面应用</span><span class="sxs-lookup"><span data-stu-id="c3918-103">Add a model to an ASP.NET Core Razor Pages app with Visual Studio for Mac</span></span>

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="c3918-104">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="c3918-104">Add a data model</span></span>

* <span data-ttu-id="c3918-105">在解决方案资源管理器中，右键单击“RazorPagesMovie”项目，然后选择“添加” > “新建文件夹”。</span><span class="sxs-lookup"><span data-stu-id="c3918-105">In Solution Explorer, right-click the **RazorPagesMovie** project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="c3918-106">将文件夹命名为“Models”。</span><span class="sxs-lookup"><span data-stu-id="c3918-106">Name the folder *Models*.</span></span>
* <span data-ttu-id="c3918-107">右键单击“Models”文件夹，然后选择“添加” > “新建文件”。</span><span class="sxs-lookup"><span data-stu-id="c3918-107">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span>
* <span data-ttu-id="c3918-108">在“新建文件”对话框中：</span><span class="sxs-lookup"><span data-stu-id="c3918-108">In the **New File** dialog:</span></span>

  * <span data-ttu-id="c3918-109">在左侧窗格中，选择“常规”。</span><span class="sxs-lookup"><span data-stu-id="c3918-109">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="c3918-110">在中间窗格中，选择“空类”。</span><span class="sxs-lookup"><span data-stu-id="c3918-110">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="c3918-111">将此类命名为“Movie”，然后选择“新建”。</span><span class="sxs-lookup"><span data-stu-id="c3918-111">Name the class **Movie** and select **New**.</span></span>

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="c3918-112">右键单击红色波浪线，例如，行 `services.AddDbContext<MovieContext>(options =>` 中的 `MovieContext`。</span><span class="sxs-lookup"><span data-stu-id="c3918-112">Right click on a red squiggly line, for example `MovieContext` in the line `services.AddDbContext<MovieContext>(options =>`.</span></span> <span data-ttu-id="c3918-113">选择“快速修复”>“使用RazorPagesMovie.Models;”。</span><span class="sxs-lookup"><span data-stu-id="c3918-113">Select **Quick Fix > using RazorPagesMovie.Models;**.</span></span> <span data-ttu-id="c3918-114">Visual Studio 添加 using 语句。</span><span class="sxs-lookup"><span data-stu-id="c3918-114">Visual studio adds the using statement.</span></span>

<span data-ttu-id="c3918-115">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="c3918-115">Build the project to verify you don't have any errors.</span></span>

![创建页面](model/red.png)

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="c3918-117">用于进行迁移的 Entity Framework Core NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c3918-117">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="c3918-118">[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了适用于命令行接口 (CLI) 的 EF 工具。</span><span class="sxs-lookup"><span data-stu-id="c3918-118">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="c3918-119">单击 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 链接以获取要使用的版本号。</span><span class="sxs-lookup"><span data-stu-id="c3918-119">Click on the [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) link to get the version number to use.</span></span> <span data-ttu-id="c3918-120">若要安装此包，请将它添加到 .csproj 文件中的 `DotNetCliToolReference` 集合。</span><span class="sxs-lookup"><span data-stu-id="c3918-120">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="c3918-121">注意：必须通过编辑 .csproj 文件来安装此包；不能使用 `install-package` 命令或程序包管理器 GUI。</span><span class="sxs-lookup"><span data-stu-id="c3918-121">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="c3918-122">若要编辑“.csproj”文件：</span><span class="sxs-lookup"><span data-stu-id="c3918-122">To edit a *.csproj* file:</span></span>

* <span data-ttu-id="c3918-123">选择“文件” > “打开”，然后选择“.csproj”文件。</span><span class="sxs-lookup"><span data-stu-id="c3918-123">Select **File** > **Open**, and then select the *.csproj* file.</span></span>
* <span data-ttu-id="c3918-124">选择“选项”。</span><span class="sxs-lookup"><span data-stu-id="c3918-124">Select **Options**.</span></span>
* <span data-ttu-id="c3918-125">将“打开方式”更改为“源代码编辑器”。</span><span class="sxs-lookup"><span data-stu-id="c3918-125">Change **Open with** to **Source Code Editor**.</span></span>

![编辑 csproj 文件](model/csproj.png)

<span data-ttu-id="c3918-127">将 `Microsoft.EntityFrameworkCore.Tools.DotNet` 工具引用添加至第二个 \<ItemGroup>：</span><span class="sxs-lookup"><span data-stu-id="c3918-127">Add the `Microsoft.EntityFrameworkCore.Tools.DotNet` tool reference to the second **\<ItemGroup>**.:</span></span>

[!code-xml[](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?highlight=10)]

<span data-ttu-id="c3918-128">以下代码中显示的版本号在编写时是正确的。</span><span class="sxs-lookup"><span data-stu-id="c3918-128">The version numbers shown in the following code were correct at the time of writing.</span></span>

[!INCLUDE [model3](../../includes/RP/model3.md)]

[!INCLUDE [model 4x](../../includes/RP/model4x.md)]

[!INCLUDE [model 4 exit](../../includes/RP/model4exit.md)]

[!INCLUDE [model 4](../../includes/RP/model4.md)]

### <a name="add-the-pagesmovies-files-to-the-project"></a><span data-ttu-id="c3918-129">将页面/电影文件添加到项目</span><span class="sxs-lookup"><span data-stu-id="c3918-129">Add the Pages/Movies files to the project</span></span>

* <span data-ttu-id="c3918-130">在 Visual Studio 中，右键单击“页面”文件夹，然后选择“添加”>“添加现有文件夹”。</span><span class="sxs-lookup"><span data-stu-id="c3918-130">In Visual Studio, Right-click the *Pages* folder and select **Add > Add existing Folder**.</span></span>
* <span data-ttu-id="c3918-131">选择“电影”文件夹。</span><span class="sxs-lookup"><span data-stu-id="c3918-131">Select the *Movies* folder.</span></span>
* <span data-ttu-id="c3918-132">在“选择要包含在项目中的文件”对话框中，选择“包括所有”。</span><span class="sxs-lookup"><span data-stu-id="c3918-132">In the *Choose files to include in the project* dialog, select **Include All**.</span></span>

<span data-ttu-id="c3918-133">下一个教程介绍由基架创建的文件。</span><span class="sxs-lookup"><span data-stu-id="c3918-133">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3918-134">[上一篇：入门](xref:tutorials/razor-pages-mac/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages-mac/page)</span><span class="sxs-lookup"><span data-stu-id="c3918-134">[Previous: Get Started](xref:tutorials/razor-pages-mac/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages-mac/page)</span></span>
