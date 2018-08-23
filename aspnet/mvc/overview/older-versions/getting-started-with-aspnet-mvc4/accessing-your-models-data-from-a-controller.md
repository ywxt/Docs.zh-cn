---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2b5747f49a31a6f3559609bbae765025e43c650b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832488"
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="974df-104">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="974df-104">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="974df-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="974df-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="974df-106">本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="974df-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="974df-107">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="974df-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="974df-108">在本部分中，将创建一个新`MoviesController`类，并编写代码来检索电影数据并将其显示在浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="974df-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="974df-109">**生成应用程序**然后才能转到下一步。</span><span class="sxs-lookup"><span data-stu-id="974df-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="974df-110">右键单击*控制器*文件夹，并创建一个新`MoviesController`控制器。</span><span class="sxs-lookup"><span data-stu-id="974df-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="974df-111">生成应用程序之前，不会显示以下选项。</span><span class="sxs-lookup"><span data-stu-id="974df-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="974df-112">选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="974df-112">Select the following options:</span></span>

- <span data-ttu-id="974df-113">控制器名称： **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="974df-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="974df-114">（这是默认值。</span><span class="sxs-lookup"><span data-stu-id="974df-114">(This is the default.</span></span> <span data-ttu-id="974df-115">)</span><span class="sxs-lookup"><span data-stu-id="974df-115">)</span></span>
- <span data-ttu-id="974df-116">模板：**使用实体框架包含读/写操作和视图的 MVC 控制器**。</span><span class="sxs-lookup"><span data-stu-id="974df-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="974df-117">模型类： **Movie (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="974df-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="974df-118">数据上下文类： **MovieDBContext (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="974df-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="974df-119">视图： **Razor (CSHTML)**。</span><span class="sxs-lookup"><span data-stu-id="974df-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="974df-120">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="974df-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="974df-122">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="974df-122">Click **Add**.</span></span> <span data-ttu-id="974df-123">Visual Studio 速成版创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="974df-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="974df-124">*MoviesController.cs*在项目文件中的*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="974df-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="974df-125">一个*电影*文件夹中项目的*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="974df-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="974df-126">*Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml*，并*Index.cshtml*中的新*视图 \ 电影*文件夹。</span><span class="sxs-lookup"><span data-stu-id="974df-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="974df-127">ASP.NET MVC 4 自动创建 CRUD （创建、 读取、 更新和删除） 操作方法和视图为您 （CRUD 操作方法和视图的自动创建被称为基架）。</span><span class="sxs-lookup"><span data-stu-id="974df-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="974df-128">现可完全正常运行的 web 应用程序，可用于创建、 列出、 编辑和删除的电影条目。</span><span class="sxs-lookup"><span data-stu-id="974df-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="974df-129">运行应用程序，并浏览到`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="974df-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="974df-130">因为应用程序依赖于默认路由 (在中定义*Global.asax*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认`Index`操作方法的`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="974df-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="974df-131">换而言之，将浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="974df-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="974df-132">结果是空列表的电影，因为还未添加任何。</span><span class="sxs-lookup"><span data-stu-id="974df-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="974df-133">创建电影</span><span class="sxs-lookup"><span data-stu-id="974df-133">Creating a Movie</span></span>

<span data-ttu-id="974df-134">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="974df-134">Select the **Create New** link.</span></span> <span data-ttu-id="974df-135">输入有关电影的一些详细信息，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="974df-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="974df-136">单击**创建**按钮后，窗体会发布到服务器，其中电影信息保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="974df-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="974df-137">然后，将重定向到 */Movies* URL，其中显示在列表中新创建的电影。</span><span class="sxs-lookup"><span data-stu-id="974df-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="974df-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="974df-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="974df-139">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="974df-139">Create a couple more movie entries.</span></span> <span data-ttu-id="974df-140">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="974df-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="974df-141">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="974df-141">Examining the Generated Code</span></span>

<span data-ttu-id="974df-142">打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="974df-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="974df-143">与电影控制器的一部分`Index`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="974df-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="974df-144">以下代码行从`MoviesController`类实例化一个电影数据库上下文，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="974df-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="974df-145">电影数据库上下文可用于查询、 编辑和删除电影。</span><span class="sxs-lookup"><span data-stu-id="974df-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="974df-146">对请求`Movies`控制器返回中的所有条目`Movies`电影数据库表，然后将传递到结果`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="974df-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="974df-147">强类型模型和@model关键字</span><span class="sxs-lookup"><span data-stu-id="974df-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="974df-148">前面在本教程中，您已了解如何在控制器可以传入数据或对象视图模板使用`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="974df-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="974df-149">`ViewBag`是一个动态对象，提供了方便的后期绑定方法将信息传递给视图。</span><span class="sxs-lookup"><span data-stu-id="974df-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="974df-150">ASP.NET MVC 还提供了能够传递强类型化数据或视图模板的对象。</span><span class="sxs-lookup"><span data-stu-id="974df-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="974df-151">此强类型化方法允许更好地进行编译时检查的代码和更丰富的 IntelliSense，Visual Studio 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="974df-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="974df-152">在 Visual Studio 中的基架机制使用此方法`MoviesController`类和视图模板时将其创建方法和视图。</span><span class="sxs-lookup"><span data-stu-id="974df-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="974df-153">在中*Controllers\MoviesController.cs*文件检查生成`Details`方法。</span><span class="sxs-lookup"><span data-stu-id="974df-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="974df-154">与电影控制器的一部分`Details`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="974df-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="974df-155">如果`Movie`找到，则实例`Movie`的模型传递到详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="974df-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="974df-156">检查的内容*Views\Movies\Details.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="974df-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="974df-157">通过包括`@model`语句在视图模板文件的顶部，可以指定视图期望的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="974df-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="974df-158">创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：</span><span class="sxs-lookup"><span data-stu-id="974df-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="974df-159">此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。</span><span class="sxs-lookup"><span data-stu-id="974df-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="974df-160">例如，在*Details.cshtml*模板，代码将传递到每个电影字段`DisplayNameFor`并[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型化`Model`对象。</span><span class="sxs-lookup"><span data-stu-id="974df-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="974df-161">创建和编辑方法和视图模板还传递电影模型对象。</span><span class="sxs-lookup"><span data-stu-id="974df-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="974df-162">检查*Index.cshtml*视图模板和`Index`中的方法*MoviesController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="974df-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="974df-163">请注意，该代码会创建如何[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它将调用`View`帮助器方法`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="974df-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="974df-164">该代码，然后将此`Movies`从控制器到视图的列表：</span><span class="sxs-lookup"><span data-stu-id="974df-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="974df-165">创建电影控制器时，Visual Studio Express 自动包括以下`@model`顶部的语句*Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="974df-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="974df-166">这`@model`指令使你能够访问控制器传递给视图使用的电影列表`Model`强类型化的对象。</span><span class="sxs-lookup"><span data-stu-id="974df-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="974df-167">例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做`foreach`语句通过强类型化`Model`对象：</span><span class="sxs-lookup"><span data-stu-id="974df-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="974df-168">因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，每个`item`循环中的对象被类型化为`Movie`。</span><span class="sxs-lookup"><span data-stu-id="974df-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="974df-169">还具有其他优点，这意味着，获取编译时检查的代码，并完全在代码编辑器中的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="974df-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="974df-171">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="974df-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="974df-172">提供数据库连接字符串指向实体框架 Code First 检测到`Movies`未尚未存在，因此 Code First 数据库自动创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="974df-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="974df-173">你可以验证它已创建中查找*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="974df-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="974df-174">如果没有看到*Movies.mdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏中，单击**刷新**按钮，，然后展开*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="974df-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="974df-175">双击*Movies.mdf*以打开**数据库资源管理器**，然后展开**表**文件夹，以查看电影表。</span><span class="sxs-lookup"><span data-stu-id="974df-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="974df-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="974df-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="974df-177">如果未出现数据库资源管理器，从**工具**菜单中，选择**连接到数据库**，然后取消**选择数据源**对话框。</span><span class="sxs-lookup"><span data-stu-id="974df-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="974df-178">这将强制打开数据库资源管理器。</span><span class="sxs-lookup"><span data-stu-id="974df-178">This will force open the database explorer.</span></span>


> [!NOTE]
> <span data-ttu-id="974df-179">如果您正在使用 VWD 或 Visual Studio 2010 并遇到错误类似于以下的以下任何：</span><span class="sxs-lookup"><span data-stu-id="974df-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="974df-180">数据库 C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。MDF 无法打开，因为它是 706 的版本。</span><span class="sxs-lookup"><span data-stu-id="974df-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="974df-181">此服务器支持 655 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="974df-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="974df-182">不支持降级路径。</span><span class="sxs-lookup"><span data-stu-id="974df-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="974df-183">&quot;用户代码未处理 InvalidOperation 异常&quot;提供的 SqlConnection 未指定初始目录。</span><span class="sxs-lookup"><span data-stu-id="974df-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="974df-184">你需要安装[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)并[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。</span><span class="sxs-lookup"><span data-stu-id="974df-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="974df-185">验证`MovieDBContext`前一页上指定的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="974df-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>


<span data-ttu-id="974df-186">右键单击`Movies`表，然后选择**显示表数据**若要查看你创建的数据。</span><span class="sxs-lookup"><span data-stu-id="974df-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="974df-187">右键单击`Movies`表，然后选择**打开表定义**若要查看结构，该实体框架 Code First 为你创建的表。</span><span class="sxs-lookup"><span data-stu-id="974df-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

<span data-ttu-id="974df-188">![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")</span><span class="sxs-lookup"><span data-stu-id="974df-188">![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")</span></span>

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="974df-189">请注意如何的架构`Movies`表映射到`Movie`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="974df-189">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="974df-190">实体框架 Code First 自动创建此架构根据你`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="974df-190">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="974df-191">完成后，通过右键单击关闭连接*MovieDBContext* ，然后选择**关闭连接**。</span><span class="sxs-lookup"><span data-stu-id="974df-191">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="974df-192">（如果不关闭连接，您可能会遇到错误在下次运行项目时）。</span><span class="sxs-lookup"><span data-stu-id="974df-192">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="974df-193">![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="974df-193">![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")</span></span>

<span data-ttu-id="974df-194">现在将具有对数据库和简单列表页，以显示从它的内容。</span><span class="sxs-lookup"><span data-stu-id="974df-194">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="974df-195">在下一步的教程中，我们将检查已搭建基架代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`使您可以搜索电影的此数据库的视图。</span><span class="sxs-lookup"><span data-stu-id="974df-195">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="974df-196">[上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="974df-196">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
