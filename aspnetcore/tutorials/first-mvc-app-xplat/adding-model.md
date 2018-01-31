---
title: "将模型添加到 ASP.NET Core MVC 应用。"
author: rick-anderson
description: "将模型添加到简单的 ASP.NET Core 应用。"
manager: wpickett
ms.author: riande
ms.date: 09/18/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app-xplat/adding-model
ms.openlocfilehash: 81511b05a3cc11a58b93452d3c6e5305e7ee4357
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
[!INCLUDE[adding-model1](../../includes/mvc-intro/adding-model1.md)]

* <span data-ttu-id="55e4f-103">将类添加到名为“Movie.cs”的“Models”文件夹。</span><span class="sxs-lookup"><span data-stu-id="55e4f-103">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="55e4f-104">将以下代码添加到“Models/Movie.cs”文件：</span><span class="sxs-lookup"><span data-stu-id="55e4f-104">Add the following code to the *Models/Movie.cs* file:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="55e4f-105">数据库需要 `ID` 字段以获取主键。</span><span class="sxs-lookup"><span data-stu-id="55e4f-105">The `ID` field is required by the database for the primary key.</span></span> 

<span data-ttu-id="55e4f-106">生成应用以确认没有任何错误，最后将 Model 添加到你的 MVC 应用。</span><span class="sxs-lookup"><span data-stu-id="55e4f-106">Build the app to verify you don't have any errors, and you've finally added a **M**odel to your **M**VC app.</span></span>

## <a name="prepare-the-project-for-scaffolding"></a><span data-ttu-id="55e4f-107">准备项目以搭建基架</span><span class="sxs-lookup"><span data-stu-id="55e4f-107">Prepare the project for scaffolding</span></span>

- <span data-ttu-id="55e4f-108">将以下突出显示的 NuGet 包添加到 MvcMovie.csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="55e4f-108">Add the following highlighted NuGet packages to the *MvcMovie.csproj* file:</span></span>
             
   [!code-csharp[Main](start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- <span data-ttu-id="55e4f-109">保存该文件，并对信息性消息“存在未解析的依赖项”选择“还原”。</span><span class="sxs-lookup"><span data-stu-id="55e4f-109">Save the file and select **Restore** to the **Info** message "There are unresolved dependencies".</span></span>
- <span data-ttu-id="55e4f-110">创建 Models/MvcMovieContext.cs 文件并添加以下 `MvcMovieContext` 类：</span><span class="sxs-lookup"><span data-stu-id="55e4f-110">Create a *Models/MvcMovieContext.cs* file and add the following `MvcMovieContext` class:</span></span>

   [!code-csharp[Main](start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]
   
- <span data-ttu-id="55e4f-111">打开 Startup.cs 文件并添加两个 using：</span><span class="sxs-lookup"><span data-stu-id="55e4f-111">Open the *Startup.cs* file and add two usings:</span></span>

   [!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]

- <span data-ttu-id="55e4f-112">将数据库上下文添加到 Startup.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="55e4f-112">Add the database context to the *Startup.cs* file:</span></span>

   [!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  <span data-ttu-id="55e4f-113">这会告诉实体框架，数据模型中包含哪些模型类。</span><span class="sxs-lookup"><span data-stu-id="55e4f-113">This tells Entity Framework which model classes are included in the data model.</span></span> <span data-ttu-id="55e4f-114">现在定义一个 Movie 对象实体集，此实体集会表示为数据库中的一个 Movie 表。</span><span class="sxs-lookup"><span data-stu-id="55e4f-114">You're defining one *entity set* of Movie objects, which will be represented in the database as a Movie table.</span></span>

- <span data-ttu-id="55e4f-115">生成项目并确定没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="55e4f-115">Build the project to verify there are no errors.</span></span>

## <a name="scaffold-the-moviecontroller"></a><span data-ttu-id="55e4f-116">为 MovieController 搭建基架</span><span class="sxs-lookup"><span data-stu-id="55e4f-116">Scaffold the MovieController</span></span>

<span data-ttu-id="55e4f-117">在项目文件夹中打开终端窗口，然后运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="55e4f-117">Open a terminal window in the project folder and run the following commands:</span></span>

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
<span data-ttu-id="55e4f-118">基架引擎创建以下组件：</span><span class="sxs-lookup"><span data-stu-id="55e4f-118">The scaffolding engine creates the following:</span></span>

* <span data-ttu-id="55e4f-119">电影控制器 (Controllers/MoviesController.cs)</span><span class="sxs-lookup"><span data-stu-id="55e4f-119">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="55e4f-120">“创建”、“删除”、“详细信息”、“编辑”和“索引”页面的 Razor 视图文件 (Views/Movies/\*.cshtml)</span><span class="sxs-lookup"><span data-stu-id="55e4f-120">Razor view files for Create, Delete, Details, Edit and Index pages (*Views/Movies/\*.cshtml*)</span></span>

<span data-ttu-id="55e4f-121">自动创建 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)（创建、读取、更新和删除）操作方法和视图的过程称为“搭建基架”。</span><span class="sxs-lookup"><span data-stu-id="55e4f-121">The automatic creation of [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="55e4f-122">你很快就会拥有一个功能完备的 Web 应用程序，并且你可以使用它管理电影数据库。</span><span class="sxs-lookup"><span data-stu-id="55e4f-122">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

[!INCLUDE[adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model3.md)]

<span data-ttu-id="55e4f-123">现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。</span><span class="sxs-lookup"><span data-stu-id="55e4f-123">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="55e4f-124">在下一个教程中，我们将使用此数据库。</span><span class="sxs-lookup"><span data-stu-id="55e4f-124">In the next tutorial, we'll work with the database.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="55e4f-125">其他资源</span><span class="sxs-lookup"><span data-stu-id="55e4f-125">Additional resources</span></span>

* [<span data-ttu-id="55e4f-126">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="55e4f-126">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="55e4f-127">全球化和本地化</span><span class="sxs-lookup"><span data-stu-id="55e4f-127">Globalization and localization</span></span>](xref:fundamentals/localization)

>[!div class="step-by-step"]
<span data-ttu-id="55e4f-128">[上一篇 - 添加视图](adding-view.md)
[下一篇 - 使用 SQLite](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="55e4f-128">[Previous - Add a view](adding-view.md)
[Next - Working with SQLite](working-with-sql.md)</span></span>
