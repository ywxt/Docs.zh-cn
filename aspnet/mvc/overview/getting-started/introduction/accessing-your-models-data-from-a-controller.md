---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 8d359de17bc35d0e14047ccd0589f080e0f949fc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396105"
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="fd49c-102">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="fd49c-102">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="fd49c-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="fd49c-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="fd49c-104">在本部分中，将创建一个新`MoviesController`类，并编写代码来检索电影数据并将其显示在浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="fd49c-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="fd49c-105">**生成应用程序**然后才能转到下一步。</span><span class="sxs-lookup"><span data-stu-id="fd49c-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="fd49c-106">如果不生成应用程序，您会添加一个控制器发生错误。</span><span class="sxs-lookup"><span data-stu-id="fd49c-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="fd49c-107">在解决方案资源管理器中右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。</span><span class="sxs-lookup"><span data-stu-id="fd49c-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="fd49c-108">在中**添加基架**对话框中，单击**包含的 MVC 5 控制器视图，使用实体框架**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="fd49c-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="fd49c-109">选择**Movie (MvcMovie.Models)** 模型类。</span><span class="sxs-lookup"><span data-stu-id="fd49c-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="fd49c-110">选择**MovieDBContext (MvcMovie.Models)** 为数据上下文类。</span><span class="sxs-lookup"><span data-stu-id="fd49c-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="fd49c-111">对于控制器名称输入**MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="fd49c-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="fd49c-112">下图显示了已完成的对话框。</span><span class="sxs-lookup"><span data-stu-id="fd49c-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="fd49c-113">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="fd49c-113">Click **Add**.</span></span> <span data-ttu-id="fd49c-114">（如果遇到错误，您可能不生成应用程序开始将控制器添加之前。）Visual Studio 将创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="fd49c-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="fd49c-115">*MoviesController.cs*文件中*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="fd49c-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="fd49c-116">一个*视图 \ 电影*文件夹。</span><span class="sxs-lookup"><span data-stu-id="fd49c-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="fd49c-117">*Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml*，并*Index.cshtml*中的新*视图 \ 电影*文件夹。</span><span class="sxs-lookup"><span data-stu-id="fd49c-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="fd49c-118">自动创建 visual Studio [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) （创建、 读取、 更新和删除） 操作方法和视图为您 （CRUD 操作方法和视图的自动创建被称为基架）。</span><span class="sxs-lookup"><span data-stu-id="fd49c-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="fd49c-119">现可完全正常运行的 web 应用程序，可用于创建、 列出、 编辑和删除的电影条目。</span><span class="sxs-lookup"><span data-stu-id="fd49c-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="fd49c-120">运行应用程序并单击**MVC 电影**链接 (或浏览至`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL)。</span><span class="sxs-lookup"><span data-stu-id="fd49c-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="fd49c-121">因为应用程序依赖于默认路由 (中定义*应用程序\_Start\RouteConfig.cs*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认`Index`的操作方法`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="fd49c-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="fd49c-122">换而言之，将浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="fd49c-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="fd49c-123">结果是空列表的电影，因为还未添加任何。</span><span class="sxs-lookup"><span data-stu-id="fd49c-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="fd49c-124">创建电影</span><span class="sxs-lookup"><span data-stu-id="fd49c-124">Creating a Movie</span></span>

<span data-ttu-id="fd49c-125">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="fd49c-125">Select the **Create New** link.</span></span> <span data-ttu-id="fd49c-126">输入有关电影的一些详细信息，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="fd49c-126">Enter some details about a movie and then click the **Create** button.</span></span>


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="fd49c-127">您不能在价格字段中输入小数点或逗号。</span><span class="sxs-lookup"><span data-stu-id="fd49c-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="fd49c-128">若要支持 jQuery 验证的非英语区域设置，请使用逗号 (&quot;，&quot;) 必须包含小数点，和非美国英语日期格式， *globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。</span><span class="sxs-lookup"><span data-stu-id="fd49c-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="fd49c-129">我将介绍如何执行此操作在下一步的教程。</span><span class="sxs-lookup"><span data-stu-id="fd49c-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="fd49c-130">目前只能输入整数，例如 10。</span><span class="sxs-lookup"><span data-stu-id="fd49c-130">For now, just enter whole numbers like 10.</span></span>


<span data-ttu-id="fd49c-131">单击**创建**按钮后，窗体会发布到服务器，其中电影信息保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="fd49c-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="fd49c-132">然后，将重定向到 */Movies* URL，其中显示在列表中新创建的电影。</span><span class="sxs-lookup"><span data-stu-id="fd49c-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="fd49c-133">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="fd49c-133">Create a couple more movie entries.</span></span> <span data-ttu-id="fd49c-134">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="fd49c-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="fd49c-135">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="fd49c-135">Examining the Generated Code</span></span>

<span data-ttu-id="fd49c-136">打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="fd49c-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="fd49c-137">与电影控制器的一部分`Index`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd49c-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="fd49c-138">对请求`Movies`控制器返回中的所有条目`Movies`表，然后将传递到结果`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="fd49c-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="fd49c-139">以下代码行从`MoviesController`类实例化一个电影数据库上下文，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="fd49c-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="fd49c-140">电影数据库上下文可用于查询、 编辑和删除电影。</span><span class="sxs-lookup"><span data-stu-id="fd49c-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="fd49c-141">强类型模型和@model关键字</span><span class="sxs-lookup"><span data-stu-id="fd49c-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="fd49c-142">前面在本教程中，您已了解如何在控制器可以传入数据或对象视图模板使用`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="fd49c-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="fd49c-143">`ViewBag`是一个动态对象，提供了方便的后期绑定方法将信息传递给视图。</span><span class="sxs-lookup"><span data-stu-id="fd49c-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="fd49c-144">MVC 还提供了将传递的功能*强*类型化视图模板的对象。</span><span class="sxs-lookup"><span data-stu-id="fd49c-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="fd49c-145">使用此强类型化的方法，更好地编译时检查的代码和更丰富[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) Visual Studio 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="fd49c-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="fd49c-146">在 Visual Studio 中的基架机制使用这种方法 (即传递*强*类型化的模型) 与`MoviesController`类和视图模板时将其创建方法和视图。</span><span class="sxs-lookup"><span data-stu-id="fd49c-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="fd49c-147">在中*Controllers\MoviesController.cs*文件检查生成`Details`方法。</span><span class="sxs-lookup"><span data-stu-id="fd49c-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="fd49c-148">`Details`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd49c-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="fd49c-149">`id`参数通常作为路由数据传递，例如`http://localhost:1234/movies/details/1`将设置为电影控制器，对指定的操作的控制器`details`和`id`为 1。</span><span class="sxs-lookup"><span data-stu-id="fd49c-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="fd49c-150">您还可以传入查询字符串的 id，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd49c-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="fd49c-151">如果`Movie`找到的实例`Movie`的模型传递给`Details`视图：</span><span class="sxs-lookup"><span data-stu-id="fd49c-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="fd49c-152">检查的内容*Views\Movies\Details.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="fd49c-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="fd49c-153">通过包括`@model`语句在视图模板文件的顶部，可以指定视图期望的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="fd49c-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="fd49c-154">创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：</span><span class="sxs-lookup"><span data-stu-id="fd49c-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="fd49c-155">此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。</span><span class="sxs-lookup"><span data-stu-id="fd49c-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="fd49c-156">例如，在*Details.cshtml*模板，代码将传递到每个电影字段`DisplayNameFor`并[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型化`Model`对象。</span><span class="sxs-lookup"><span data-stu-id="fd49c-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="fd49c-157">`Create`和`Edit`方法和视图模板还将传递电影模型对象。</span><span class="sxs-lookup"><span data-stu-id="fd49c-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="fd49c-158">检查*Index.cshtml*视图模板和`Index`中的方法*MoviesController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="fd49c-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="fd49c-159">请注意，该代码会创建如何[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它将调用`View`帮助器方法`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="fd49c-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="fd49c-160">该代码，然后将这`Movies`列表从`Index`到视图的操作方法：</span><span class="sxs-lookup"><span data-stu-id="fd49c-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="fd49c-161">创建电影控制器时，Visual Studio 自动包括以下`@model`顶部的语句*Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="fd49c-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="fd49c-162">这`@model`指令使你能够访问控制器传递给视图使用的电影列表`Model`强类型化的对象。</span><span class="sxs-lookup"><span data-stu-id="fd49c-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="fd49c-163">例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做`foreach`语句通过强类型化`Model`对象：</span><span class="sxs-lookup"><span data-stu-id="fd49c-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="fd49c-164">因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，每个`item`循环中的对象被类型化为`Movie`。</span><span class="sxs-lookup"><span data-stu-id="fd49c-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="fd49c-165">还具有其他优点，这意味着，获取编译时检查的代码，并完全在代码编辑器中的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="fd49c-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="fd49c-167">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="fd49c-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="fd49c-168">提供数据库连接字符串指向实体框架 Code First 检测到`Movies`未尚未存在，因此 Code First 数据库自动创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="fd49c-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="fd49c-169">你可以验证它已创建中查找*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="fd49c-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="fd49c-170">如果没有看到*Movies.mdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏中，单击**刷新**按钮，，然后展开*应用程序\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="fd49c-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="fd49c-171">双击*Movies.mdf*以打开**服务器资源管理器**，然后展开**表**文件夹，以查看电影表。</span><span class="sxs-lookup"><span data-stu-id="fd49c-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="fd49c-172">请注意旁密钥的 id。</span><span class="sxs-lookup"><span data-stu-id="fd49c-172">Note the key icon next to ID.</span></span> <span data-ttu-id="fd49c-173">默认情况下，EF 将名为 ID 的主键的属性。</span><span class="sxs-lookup"><span data-stu-id="fd49c-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="fd49c-174">EF 和 MVC 的详细信息，请参阅 Tom Dykstra 的绝佳教程上[MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="fd49c-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="fd49c-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="fd49c-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="fd49c-176">右键单击`Movies`表，然后选择**显示表数据**若要查看你创建的数据。</span><span class="sxs-lookup"><span data-stu-id="fd49c-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="fd49c-177">右键单击`Movies`表，然后选择**打开表定义**若要查看结构，该实体框架 Code First 为你创建的表。</span><span class="sxs-lookup"><span data-stu-id="fd49c-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="fd49c-178">请注意如何的架构`Movies`表映射到`Movie`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="fd49c-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="fd49c-179">实体框架 Code First 自动创建此架构根据你`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="fd49c-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="fd49c-180">完成后，通过右键单击关闭连接*MovieDBContext* ，然后选择**关闭连接**。</span><span class="sxs-lookup"><span data-stu-id="fd49c-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="fd49c-181">（如果不关闭连接，您可能会遇到错误在下次运行项目时）。</span><span class="sxs-lookup"><span data-stu-id="fd49c-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="fd49c-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="fd49c-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span></span>

<span data-ttu-id="fd49c-183">现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。</span><span class="sxs-lookup"><span data-stu-id="fd49c-183">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="fd49c-184">在下一步的教程中，我们将检查已搭建基架代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`使您可以搜索电影的此数据库的视图。</span><span class="sxs-lookup"><span data-stu-id="fd49c-184">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="fd49c-185">与 MVC 结合使用实体框架的详细信息，请参阅[为 ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="fd49c-185">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fd49c-186">[上一页](creating-a-connection-string.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="fd49c-186">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
