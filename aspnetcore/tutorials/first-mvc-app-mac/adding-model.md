---
title: 使用 Visual Studio for Mac 将模型添加到 ASP.NET Core MVC 应用
author: rick-anderson
description: 将模型添加到简单的 ASP.NET Core 应用。
ms.author: riande
ms.date: 09/22/2017
uid: tutorials/first-mvc-app-mac/adding-model
ms.openlocfilehash: 6db079558ccf4515a37a90f7a9e2608333acd7cf
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961381"
---
[!INCLUDE [adding-model](../../includes/mvc-intro/adding-model1.md)]

* <span data-ttu-id="777d9-103">右键单击“Models”文件夹，然后选择“添加” > “新建文件”。</span><span class="sxs-lookup"><span data-stu-id="777d9-103">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span> 
* <span data-ttu-id="777d9-104">在“新建文件”对话框中：</span><span class="sxs-lookup"><span data-stu-id="777d9-104">In the **New File** dialog:</span></span>

  * <span data-ttu-id="777d9-105">在左侧窗格中，选择“常规”。</span><span class="sxs-lookup"><span data-stu-id="777d9-105">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="777d9-106">在中间窗格中，选择“空类”。</span><span class="sxs-lookup"><span data-stu-id="777d9-106">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="777d9-107">将此类命名为“Movie”，然后选择“新建”。</span><span class="sxs-lookup"><span data-stu-id="777d9-107">Name the class **Movie** and select **New**.</span></span>

<span data-ttu-id="777d9-108">向 `Movie` 类添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="777d9-108">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="777d9-109">数据库需要 `ID` 字段以获取主键。</span><span class="sxs-lookup"><span data-stu-id="777d9-109">The `ID` field is required by the database for the primary key.</span></span>

<span data-ttu-id="777d9-110">生成项目以验证有没有任何错误存在。</span><span class="sxs-lookup"><span data-stu-id="777d9-110">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="777d9-111">现在 MVC 应用中已具有模型。</span><span class="sxs-lookup"><span data-stu-id="777d9-111">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="prepare-the-project-for-scaffolding"></a><span data-ttu-id="777d9-112">准备项目以搭建基架</span><span class="sxs-lookup"><span data-stu-id="777d9-112">Prepare the project for scaffolding</span></span>

- <span data-ttu-id="777d9-113">右键单击项目文件，然后选择“工具”>“编辑文件”。</span><span class="sxs-lookup"><span data-stu-id="777d9-113">Right click on the project file, and then select **Tools > Edit File**.</span></span>

  ![上述步骤的视图](adding-model/_static/1.png)

- <span data-ttu-id="777d9-115">将以下突出显示的 NuGet 包添加到 MvcMovie.csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="777d9-115">Add the following highlighted NuGet packages to the *MvcMovie.csproj* file:</span></span>
             
  [!code-csharp[](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- <span data-ttu-id="777d9-116">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="777d9-116">Save the file.</span></span>

- <span data-ttu-id="777d9-117">创建 Models/MvcMovieContext.cs 文件并添加以下 `MvcMovieContext` 类：[!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span><span class="sxs-lookup"><span data-stu-id="777d9-117">Create a *Models/MvcMovieContext.cs* file and add the following `MvcMovieContext` class:  [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span></span>
   
- <span data-ttu-id="777d9-118">打开 Startup.cs 文件并添加两个 using：[!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span><span class="sxs-lookup"><span data-stu-id="777d9-118">Open the *Startup.cs* file and add two usings:  [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span></span>

- <span data-ttu-id="777d9-119">将数据库上下文添加到 Startup.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="777d9-119">Add the database context to the *Startup.cs* file:</span></span>

   [!code-csharp[](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  <span data-ttu-id="777d9-120">这会告诉实体框架，数据模型中包含哪些模型类。</span><span class="sxs-lookup"><span data-stu-id="777d9-120">This tells Entity Framework which model classes are included in the data model.</span></span> <span data-ttu-id="777d9-121">现在定义一个 Movie 对象实体集，此实体集会表示为数据库中的一个 Movie 表。</span><span class="sxs-lookup"><span data-stu-id="777d9-121">You're defining one *entity set* of Movie objects, which will be represented in the database as a Movie table.</span></span>

- <span data-ttu-id="777d9-122">生成项目并确定没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="777d9-122">Build the project to verify there are no errors.</span></span>

## <a name="scaffold-the-moviecontroller"></a><span data-ttu-id="777d9-123">为 MovieController 搭建基架</span><span class="sxs-lookup"><span data-stu-id="777d9-123">Scaffold the MovieController</span></span>

<span data-ttu-id="777d9-124">在项目文件夹中打开终端窗口，然后运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="777d9-124">Open a terminal window in the project folder and run the following commands:</span></span>

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
<span data-ttu-id="777d9-125">如果收到错误 `No executable found matching command "dotnet-aspnet-codegenerator", verify`：</span><span class="sxs-lookup"><span data-stu-id="777d9-125">If you get the error `No executable found matching command "dotnet-aspnet-codegenerator", verify`:</span></span>

 * <span data-ttu-id="777d9-126">你现在位于项目目录中。</span><span class="sxs-lookup"><span data-stu-id="777d9-126">You are in the project directory.</span></span> <span data-ttu-id="777d9-127">项目目录中包含 Program.cs、Startup.cs、和 .csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="777d9-127">The project directory has the *Program.cs*, *Startup.cs* and *.csproj* files.</span></span>
 * <span data-ttu-id="777d9-128">你的 dotnet 版本是 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="777d9-128">Your dotnet version is 1.1 or higher.</span></span> <span data-ttu-id="777d9-129">运行 `dotnet` 获取版本。</span><span class="sxs-lookup"><span data-stu-id="777d9-129">Run `dotnet` to get the version.</span></span>
 * <span data-ttu-id="777d9-130">你已将 `<DotNetCliToolReference>` 元素添加到 [MvcMovie.csproj 文件](#prepare-the-project-for-scaffolding)。</span><span class="sxs-lookup"><span data-stu-id="777d9-130">You have added the `<DotNetCliToolReference>` element to the [MvcMovie.csproj file](#prepare-the-project-for-scaffolding).</span></span>
 
<!--
> [!NOTE]
> If you get an error when the scaffolding command runs, see [issue 444 in the scaffolding repository](https://github.com/aspnet/scaffolding/issues/444) for a workaround.
-->

<span data-ttu-id="777d9-131">基架引擎创建以下组件：</span><span class="sxs-lookup"><span data-stu-id="777d9-131">The scaffolding engine creates the following:</span></span>

* <span data-ttu-id="777d9-132">电影控制器 (Controllers/MoviesController.cs)</span><span class="sxs-lookup"><span data-stu-id="777d9-132">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="777d9-133">“创建”、“删除”、“详细信息”、“编辑”和“索引”页面的 Razor 视图文件 (Views/Movies/\*.cshtml)</span><span class="sxs-lookup"><span data-stu-id="777d9-133">Razor view files for Create, Delete, Details, Edit and Index pages (*Views/Movies/\*.cshtml*)</span></span>

<span data-ttu-id="777d9-134">自动创建 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)（创建、读取、更新和删除）操作方法和视图的过程称为“搭建基架”。</span><span class="sxs-lookup"><span data-stu-id="777d9-134">The automatic creation of [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="777d9-135">你很快将具有功能完整的 Web 应用程序，可使用此应用程序管理电影数据库。</span><span class="sxs-lookup"><span data-stu-id="777d9-135">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

### <a name="add-the-files-to-visual-studio"></a><span data-ttu-id="777d9-136">将文件添加到 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="777d9-136">Add the files to Visual Studio</span></span>

* <span data-ttu-id="777d9-137">将 MovieController.cs 文件添加到 Visual Studio 项目：</span><span class="sxs-lookup"><span data-stu-id="777d9-137">Add the *MovieController.cs* file to the Visual Studio project:</span></span>

  * <span data-ttu-id="777d9-138">右键单击“控制器”文件夹，然后选择“添加”>“添加文件”。</span><span class="sxs-lookup"><span data-stu-id="777d9-138">Right-click on the *Controllers* folder and select **Add > Add Files**.</span></span>
  * <span data-ttu-id="777d9-139">选择 MovieController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="777d9-139">Select the *MovieController.cs* file.</span></span>

* <span data-ttu-id="777d9-140">添加“电影”文件夹和视图：</span><span class="sxs-lookup"><span data-stu-id="777d9-140">Add the *Movies* folder and views:</span></span>

  * <span data-ttu-id="777d9-141">右键单击“视图”文件夹，然后选择“添加”>“添加现有文件夹”。</span><span class="sxs-lookup"><span data-stu-id="777d9-141">Right-click on the *Views* folder and select **Add > Add Existing Folder**.</span></span>
  * <span data-ttu-id="777d9-142">导航到“视图”文件夹，选择“视图\电影”，然后选择“打开”。</span><span class="sxs-lookup"><span data-stu-id="777d9-142">Navigate to the *Views* folder, select *Views\Movies*, and then select **Open**.</span></span>
  * <span data-ttu-id="777d9-143">在“从‘电影’选择要添加的文件”对话框中，选择“包括全部”，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="777d9-143">In the **Select files to add from Movies** dialog, select **Include All**, and then **OK**.</span></span>

[!INCLUDE [adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE [adding-model](../../includes/mvc-intro/adding-model3.md)]

<span data-ttu-id="777d9-144">现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。</span><span class="sxs-lookup"><span data-stu-id="777d9-144">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="777d9-145">在下一个教程中，我们将使用此数据库。</span><span class="sxs-lookup"><span data-stu-id="777d9-145">In the next tutorial, we'll work with the database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="777d9-146">其他资源</span><span class="sxs-lookup"><span data-stu-id="777d9-146">Additional resources</span></span>

* [<span data-ttu-id="777d9-147">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="777d9-147">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="777d9-148">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="777d9-148">Globalization and localization</span></span>](xref:fundamentals/localization)

> [!div class="step-by-step"]
> <span data-ttu-id="777d9-149">[上一篇：添加视图](adding-view.md)
> [下一篇：使用 SQL](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="777d9-149">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  
