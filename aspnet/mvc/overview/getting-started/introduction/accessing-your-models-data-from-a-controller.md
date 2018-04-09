---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 从控制器访问您的模型的数据 |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: d3dfa079c334e04f368531456ec2ec4e9728f893
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="58f7a-102">从控制器访问您的模型的数据</span><span class="sxs-lookup"><span data-stu-id="58f7a-102">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="58f7a-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="58f7a-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="58f7a-104">在本部分中，将创建一个新`MoviesController`类，并编写代码检索影片数据并将其显示在浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="58f7a-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="58f7a-105">**生成应用程序**在转到下一步之前。</span><span class="sxs-lookup"><span data-stu-id="58f7a-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="58f7a-106">如果你不生成应用程序，你将收到错误添加控制器。</span><span class="sxs-lookup"><span data-stu-id="58f7a-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="58f7a-107">在解决方案资源管理器，右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。</span><span class="sxs-lookup"><span data-stu-id="58f7a-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="58f7a-108">在**添加基架**对话框中，单击**数据与视图，MVC 5 控制器使用 Entity Framework**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="58f7a-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="58f7a-109">选择**电影 (MvcMovie.Models)**模型类。</span><span class="sxs-lookup"><span data-stu-id="58f7a-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="58f7a-110">选择**MovieDBContext (MvcMovie.Models)**数据上下文类。</span><span class="sxs-lookup"><span data-stu-id="58f7a-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="58f7a-111">作为控制器名称输入**MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="58f7a-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="58f7a-112">下图显示已完成对话框。</span><span class="sxs-lookup"><span data-stu-id="58f7a-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="58f7a-113">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="58f7a-113">Click **Add**.</span></span> <span data-ttu-id="58f7a-114">（如果收到错误，你可能未生成应用程序，然后开始将控制器添加。）Visual Studio 将创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="58f7a-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="58f7a-115">*MoviesController.cs*文件中*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="58f7a-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="58f7a-116">A *Views\Movies*文件夹。</span><span class="sxs-lookup"><span data-stu-id="58f7a-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="58f7a-117">*Create.cshtml，Delete.cshtml，Details.cshtml，Edit.cshtml*，和*Index.cshtml*在新*Views\Movies*文件夹。</span><span class="sxs-lookup"><span data-stu-id="58f7a-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="58f7a-118">Visual Studio 自动创建[CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) （创建、 读取、 更新和删除） 操作方法和为你的视图 （自动创建的 CRUD 操作方法和视图称为基架）。</span><span class="sxs-lookup"><span data-stu-id="58f7a-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="58f7a-119">你现在具有完全正常运行的 web 应用程序，你可以创建、 列出、 编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="58f7a-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="58f7a-120">运行应用程序并单击**MVC 影片**链接 (或浏览到`Movies`控制器通过追加*/Movies*到你的浏览器的地址栏中的 URL)。</span><span class="sxs-lookup"><span data-stu-id="58f7a-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="58f7a-121">因为应用程序依赖于默认路由 (在中定义*应用\_Start\RouteConfig.cs*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认值`Index`操作方法`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="58f7a-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="58f7a-122">换而言之，浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="58f7a-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="58f7a-123">结果是电影、 一个空列表，因为你尚未添加。</span><span class="sxs-lookup"><span data-stu-id="58f7a-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="58f7a-124">创建电影</span><span class="sxs-lookup"><span data-stu-id="58f7a-124">Creating a Movie</span></span>

<span data-ttu-id="58f7a-125">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="58f7a-125">Select the **Create New** link.</span></span> <span data-ttu-id="58f7a-126">输入一些有关影片详细信息，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="58f7a-126">Enter some details about a movie and then click the **Create** button.</span></span>


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="58f7a-127">你不能在 Price 字段中输入小数点或逗号。</span><span class="sxs-lookup"><span data-stu-id="58f7a-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="58f7a-128">若要为使用逗号的非英语区域设置支持 jQuery 验证 (&quot;，&quot;) 对于小数点，和非美国英语的日期格式中，您必须包含*globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。</span><span class="sxs-lookup"><span data-stu-id="58f7a-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="58f7a-129">我将介绍如何执行此操作在下一步的教程。</span><span class="sxs-lookup"><span data-stu-id="58f7a-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="58f7a-130">目前只能输入整数，例如 10。</span><span class="sxs-lookup"><span data-stu-id="58f7a-130">For now, just enter whole numbers like 10.</span></span>


<span data-ttu-id="58f7a-131">单击**创建**按钮使窗体发布到服务器，其中的影片信息保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="58f7a-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="58f7a-132">然后转向*/Movies* URL，其中你可以看到在列表中新创建的影片。</span><span class="sxs-lookup"><span data-stu-id="58f7a-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="58f7a-133">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="58f7a-133">Create a couple more movie entries.</span></span> <span data-ttu-id="58f7a-134">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="58f7a-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="58f7a-135">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="58f7a-135">Examining the Generated Code</span></span>

<span data-ttu-id="58f7a-136">打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="58f7a-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="58f7a-137">电影控制器与的一部分`Index`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="58f7a-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="58f7a-138">对请求`Movies`控制器将返回中的所有条目`Movies`表，然后将传递到结果`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="58f7a-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="58f7a-139">以下行从`MoviesController`类实例化电影数据库上下文，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="58f7a-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="58f7a-140">电影数据库上下文可用于查询、 编辑和删除电影。</span><span class="sxs-lookup"><span data-stu-id="58f7a-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="58f7a-141">强类型模型和@model关键字</span><span class="sxs-lookup"><span data-stu-id="58f7a-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="58f7a-142">之前在本教程中，您了解了如何控制器传递数据或对象视图模板使用到`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="58f7a-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="58f7a-143">`ViewBag`是一个动态对象，提供了简便的后期绑定方法，将信息传递给视图。</span><span class="sxs-lookup"><span data-stu-id="58f7a-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="58f7a-144">MVC 还提供了将传递的功能*强*类型化的对象添加到视图模板。</span><span class="sxs-lookup"><span data-stu-id="58f7a-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="58f7a-145">使用此强类型化的方法，更好编译时检查的代码和更丰富[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx)在 Visual Studio 编辑器中。</span><span class="sxs-lookup"><span data-stu-id="58f7a-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="58f7a-146">Visual Studio 中的基架机制使用这种方法 (即传递*强*类型化的模型) 使用`MoviesController`类和视图模板创建的方法和视图时。</span><span class="sxs-lookup"><span data-stu-id="58f7a-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="58f7a-147">在*Controllers\MoviesController.cs*文件检查生成`Details`方法。</span><span class="sxs-lookup"><span data-stu-id="58f7a-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="58f7a-148">`Details`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="58f7a-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="58f7a-149">`id`参数通常传递作为路由数据，例如`http://localhost:1234/movies/details/1`将设置为电影控制器上，对指定的操作的控制器`details`和`id`为 1。</span><span class="sxs-lookup"><span data-stu-id="58f7a-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="58f7a-150">你可能还传递中使用查询字符串的 id，如下所示：</span><span class="sxs-lookup"><span data-stu-id="58f7a-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="58f7a-151">如果`Movie`找到的实例`Movie`的模型传递给`Details`视图：</span><span class="sxs-lookup"><span data-stu-id="58f7a-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="58f7a-152">检查的内容*Views\Movies\Details.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="58f7a-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="58f7a-153">通过包括`@model`语句视图模板文件的顶部，你可以指定视图需要的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="58f7a-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="58f7a-154">创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：</span><span class="sxs-lookup"><span data-stu-id="58f7a-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="58f7a-155">此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。</span><span class="sxs-lookup"><span data-stu-id="58f7a-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="58f7a-156">例如，在*Details.cshtml*模板，在代码传递到每个电影字段`DisplayNameFor`和[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx)通过强类型化的 HTML 帮助器`Model`对象。</span><span class="sxs-lookup"><span data-stu-id="58f7a-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="58f7a-157">`Create`和`Edit`方法和查看模板还将传递电影模型对象。</span><span class="sxs-lookup"><span data-stu-id="58f7a-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="58f7a-158">检查*Index.cshtml*视图模板和`Index`中的方法*MoviesController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="58f7a-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="58f7a-159">请注意该代码如何创建[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它调用`View`中的帮助器方法`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="58f7a-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="58f7a-160">在代码然后传递此`Movies`列表中按从`Index`到视图的操作方法：</span><span class="sxs-lookup"><span data-stu-id="58f7a-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="58f7a-161">在创建电影控制器时，Visual Studio 将自动包括以下`@model`语句的顶部*Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="58f7a-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="58f7a-162">这`@model`指令允许你访问的控制器传递到视图中使用的影片列表`Model`强类型的对象。</span><span class="sxs-lookup"><span data-stu-id="58f7a-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="58f7a-163">例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做，`foreach`通过强类型化的语句`Model`对象：</span><span class="sxs-lookup"><span data-stu-id="58f7a-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="58f7a-164">因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，则每个`item`循环中的对象被类型化为`Movie`。</span><span class="sxs-lookup"><span data-stu-id="58f7a-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="58f7a-165">其他优点，这意味着你获取编译时检查的代码，并在代码编辑器中的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="58f7a-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="58f7a-167">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="58f7a-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="58f7a-168">提供的数据库连接字符串指向 entity Framework Code First 检测到`Movies`不存在，因此 Code First 数据库自动创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="58f7a-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="58f7a-169">你可以验证它由查找中已创建*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="58f7a-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="58f7a-170">如果看不到*Movies.mdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏上，单击**刷新**按钮，然后再展开*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="58f7a-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="58f7a-171">双击*Movies.mdf*以打开**服务器资源管理器**，然后展开**表**文件夹以查看电影表。</span><span class="sxs-lookup"><span data-stu-id="58f7a-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="58f7a-172">请注意的密钥图标旁边 id。</span><span class="sxs-lookup"><span data-stu-id="58f7a-172">Note the key icon next to ID.</span></span> <span data-ttu-id="58f7a-173">默认情况下，EF 将名为 ID 为主键的属性。</span><span class="sxs-lookup"><span data-stu-id="58f7a-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="58f7a-174">EF 和 MVC 的详细信息，请参阅 Tom Dykstra 的绝佳教程上[MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="58f7a-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="58f7a-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="58f7a-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="58f7a-176">右键单击`Movies`表，然后选择**显示表数据**以查看你创建的数据。</span><span class="sxs-lookup"><span data-stu-id="58f7a-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="58f7a-177">右键单击`Movies`表，然后选择**打开表定义**以查看结构该 Entity Framework Code First 为你创建的表格。</span><span class="sxs-lookup"><span data-stu-id="58f7a-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="58f7a-178">请注意如何的架构`Movies`表映射到`Movie`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="58f7a-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="58f7a-179">Entity Framework Code First 自动创建此架构根据你`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="58f7a-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="58f7a-180">完成后，通过右键单击关闭连接*MovieDBContext*并选择**关闭连接**。</span><span class="sxs-lookup"><span data-stu-id="58f7a-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="58f7a-181">（如果不关闭连接，你可能会错误在下次运行项目时）。</span><span class="sxs-lookup"><span data-stu-id="58f7a-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="58f7a-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="58f7a-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span></span>

<span data-ttu-id="58f7a-183">现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。</span><span class="sxs-lookup"><span data-stu-id="58f7a-183">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="58f7a-184">在下一步的教程中，我们将检查基架的代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`可以搜索此数据库中的电影的视图。</span><span class="sxs-lookup"><span data-stu-id="58f7a-184">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="58f7a-185">在实体框架使用 MVC 的详细信息，请参阅[为 ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="58f7a-185">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58f7a-186">[上一页](creating-a-connection-string.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="58f7a-186">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
