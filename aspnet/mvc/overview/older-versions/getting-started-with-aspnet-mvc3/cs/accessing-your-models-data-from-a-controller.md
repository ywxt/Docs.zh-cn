---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: "从控制器 (C#) 访问您的模型的数据 |Microsoft 文档"
author: Rick-Anderson
description: "本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5ee29dbc5b4566273592041d94458104e6e0f65e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="accessing-your-models-data-from-a-controller-c"></a><span data-ttu-id="3ef44-103">访问您的模型的数据从控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="3ef44-103">Accessing your Model's Data from a Controller (C#)</span></span>
====================
<span data-ttu-id="3ef44-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="3ef44-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="3ef44-105">本教程的更新的版本可[此处](../../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="3ef44-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="3ef44-106">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="3ef44-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="3ef44-107">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3ef44-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3ef44-108">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="3ef44-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3ef44-109">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3ef44-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3ef44-110">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="3ef44-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3ef44-111">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="3ef44-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3ef44-112">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="3ef44-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3ef44-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="3ef44-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3ef44-114">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3ef44-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3ef44-115">使用 C# 源代码的 Visual Web Developer 项目是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="3ef44-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="3ef44-116">[下载的 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="3ef44-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3ef44-117">如果你愿意 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="3ef44-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="3ef44-118">在本部分中，将创建一个新`MoviesController`类，并编写代码检索影片数据并将其显示在浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="3ef44-118">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="3ef44-119">请确保生成应用程序然后再继续。</span><span class="sxs-lookup"><span data-stu-id="3ef44-119">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="3ef44-120">右键单击*控制器*文件夹并创建新`MoviesController`控制器。</span><span class="sxs-lookup"><span data-stu-id="3ef44-120">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="3ef44-121">选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="3ef44-121">Select the following options:</span></span>

- <span data-ttu-id="3ef44-122">控制器名称： **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-122">Controller name: **MoviesController**.</span></span> <span data-ttu-id="3ef44-123">（这是默认值。</span><span class="sxs-lookup"><span data-stu-id="3ef44-123">(This is the default.</span></span> <span data-ttu-id="3ef44-124">)</span><span class="sxs-lookup"><span data-stu-id="3ef44-124">)</span></span>
- <span data-ttu-id="3ef44-125">模板：**控制器，具有读/写操作和视图使用 Entity Framework**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-125">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="3ef44-126">模型类：**电影 (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-126">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3ef44-127">数据上下文类： **MovieDBContext (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-127">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3ef44-128">视图： **Razor (CSHTML)**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-128">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="3ef44-129">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="3ef44-129">(The default.)</span></span>

<span data-ttu-id="3ef44-130">[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-130">[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="3ef44-131">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-131">Click **Add**.</span></span> <span data-ttu-id="3ef44-132">Visual Web Developer 会创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="3ef44-132">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="3ef44-133">*MoviesController.cs*文件在项目的*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ef44-133">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="3ef44-134">A*电影*文件夹在项目的*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ef44-134">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="3ef44-135">*Create.cshtml，Delete.cshtml，Details.cshtml，Edit.cshtml*，和*Index.cshtml*在新*Views\Movies*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ef44-135">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="3ef44-136">[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-136">[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="3ef44-137">ASP.NET MVC 3 基架机制自动创建 CRUD （创建、 读取、 更新和删除） 操作方法和为你的视图。</span><span class="sxs-lookup"><span data-stu-id="3ef44-137">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="3ef44-138">你现在具有完全正常运行的 web 应用程序，你可以创建、 列出、 编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="3ef44-138">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="3ef44-139">运行应用程序，并浏览到`Movies`控制器通过追加*/Movies*到你的浏览器的地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="3ef44-139">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="3ef44-140">因为应用程序依赖于默认路由 (在中定义*Global.asax*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认值`Index`操作方法`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="3ef44-140">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="3ef44-141">换而言之，浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="3ef44-141">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="3ef44-142">结果是电影、 一个空列表，因为你尚未添加。</span><span class="sxs-lookup"><span data-stu-id="3ef44-142">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a><span data-ttu-id="3ef44-143">创建电影</span><span class="sxs-lookup"><span data-stu-id="3ef44-143">Creating a Movie</span></span>

<span data-ttu-id="3ef44-144">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="3ef44-144">Select the **Create New** link.</span></span> <span data-ttu-id="3ef44-145">输入一些有关影片详细信息，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="3ef44-145">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="3ef44-146">单击**创建**按钮使窗体发布到服务器，其中的影片信息保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="3ef44-146">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="3ef44-147">然后转向*/Movies* URL，其中你可以看到在列表中新创建的影片。</span><span class="sxs-lookup"><span data-stu-id="3ef44-147">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="3ef44-148">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-148">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="3ef44-149">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="3ef44-149">Create a couple more movie entries.</span></span> <span data-ttu-id="3ef44-150">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="3ef44-150">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="3ef44-151">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="3ef44-151">Examining the Generated Code</span></span>

<span data-ttu-id="3ef44-152">打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="3ef44-152">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="3ef44-153">电影控制器与的一部分`Index`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="3ef44-153">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="3ef44-154">以下行从`MoviesController`类实例化电影数据库上下文，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="3ef44-154">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="3ef44-155">电影数据库上下文可用于查询、 编辑和删除电影。</span><span class="sxs-lookup"><span data-stu-id="3ef44-155">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="3ef44-156">对请求`Movies`控制器将返回中的所有条目`Movies`电影数据库表，然后将传递到结果`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="3ef44-156">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="3ef44-157">强类型模型和@model关键字</span><span class="sxs-lookup"><span data-stu-id="3ef44-157">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="3ef44-158">之前在本教程中，您了解了如何控制器传递数据或对象视图模板使用到`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="3ef44-158">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="3ef44-159">`ViewBag`是一个动态对象，提供了简便的后期绑定方法，将信息传递给视图。</span><span class="sxs-lookup"><span data-stu-id="3ef44-159">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="3ef44-160">ASP.NET MVC 还提供了将强传递的功能类型化数据或查看模板的对象。</span><span class="sxs-lookup"><span data-stu-id="3ef44-160">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="3ef44-161">此强类型方法允许更好地进行编译时检查的代码和在 Visual Web Developer 编辑器中的更丰富智能感知。</span><span class="sxs-lookup"><span data-stu-id="3ef44-161">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="3ef44-162">我们将使用此方法`MoviesController`类和*Index.cshtml*查看模板。</span><span class="sxs-lookup"><span data-stu-id="3ef44-162">We're using this approach with the `MoviesController` class and *Index.cshtml* view template.</span></span>

<span data-ttu-id="3ef44-163">请注意该代码如何创建[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它调用`View`中的帮助器方法`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="3ef44-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="3ef44-164">在代码然后传递此`Movies`从控制器到视图的列表：</span><span class="sxs-lookup"><span data-stu-id="3ef44-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="3ef44-165">通过包括`@model`语句视图模板文件的顶部，你可以指定视图需要的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="3ef44-165">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="3ef44-166">在创建电影控制器时，Visual Web Developer 将自动包括以下`@model`语句的顶部*Index.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="3ef44-166">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="3ef44-167">这`@model`指令允许你访问的控制器传递到视图中使用的影片列表`Model`强类型的对象。</span><span class="sxs-lookup"><span data-stu-id="3ef44-167">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="3ef44-168">例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做，`foreach`通过强类型化的语句`Model`对象：</span><span class="sxs-lookup"><span data-stu-id="3ef44-168">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

<span data-ttu-id="3ef44-169">因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，则每个`item`循环中的对象被类型化为`Movie`。</span><span class="sxs-lookup"><span data-stu-id="3ef44-169">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="3ef44-170">其他优点，这意味着你获取编译时检查的代码，并在代码编辑器中的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="3ef44-170">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="3ef44-171">[![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntellisene")](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-171">[![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntellisene")](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="3ef44-172">使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="3ef44-172">Working with SQL Server Compact</span></span>

<span data-ttu-id="3ef44-173">提供的数据库连接字符串指向 entity Framework Code First 检测到`Movies`不存在，因此 Code First 数据库自动创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="3ef44-173">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="3ef44-174">你可以验证它由查找中已创建*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ef44-174">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="3ef44-175">如果看不到*Movies.sdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏上，单击**刷新**按钮，然后再展开*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ef44-175">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="3ef44-176">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-176">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="3ef44-177">双击*Movies.sdf*以打开**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-177">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="3ef44-178">然后展开**表**文件夹以查看已在数据库中创建的表。</span><span class="sxs-lookup"><span data-stu-id="3ef44-178">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3ef44-179">如果你收到错误，当你双击*Movies.sdf*，请确保已安装[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）。</span><span class="sxs-lookup"><span data-stu-id="3ef44-179">If you get an error when you double-click *Movies.sdf*, make sure you've installed [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support).</span></span> <span data-ttu-id="3ef44-180">（有关软件的链接，请参阅本系列教程的第 1 部分中的先决条件的列表。）如果你现在安装版本，你将需要关闭并重新打开 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="3ef44-180">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>


<span data-ttu-id="3ef44-181">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-181">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="3ef44-182">有两个表，一个用于`Movie`实体集，然后`EdmMetadata`表。</span><span class="sxs-lookup"><span data-stu-id="3ef44-182">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="3ef44-183">`EdmMetadata`实体框架使用表来确定何时模型和数据库同步。</span><span class="sxs-lookup"><span data-stu-id="3ef44-183">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="3ef44-184">右键单击`Movies`表，然后选择**显示表数据**以查看你创建的数据。</span><span class="sxs-lookup"><span data-stu-id="3ef44-184">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="3ef44-185">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-185">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="3ef44-186">右键单击`Movies`表，然后选择**编辑表架构**。</span><span class="sxs-lookup"><span data-stu-id="3ef44-186">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="3ef44-187">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-187">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

<span data-ttu-id="3ef44-188">[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-188">[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)</span></span>

<span data-ttu-id="3ef44-189">请注意如何的架构`Movies`表映射到`Movie`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="3ef44-189">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="3ef44-190">Entity Framework Code First 自动创建此架构根据你`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="3ef44-190">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="3ef44-191">完成后，关闭连接。</span><span class="sxs-lookup"><span data-stu-id="3ef44-191">When you're finished, close the connection.</span></span> <span data-ttu-id="3ef44-192">（如果不关闭连接，你可能会错误在下次运行项目时）。</span><span class="sxs-lookup"><span data-stu-id="3ef44-192">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="3ef44-193">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="3ef44-193">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)</span></span>

<span data-ttu-id="3ef44-194">你现在具有数据库和一个简单列表页，以便显示从它的内容。</span><span class="sxs-lookup"><span data-stu-id="3ef44-194">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="3ef44-195">在下一步的教程中，我们将检查基架的代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`可以搜索此数据库中的电影的视图。</span><span class="sxs-lookup"><span data-stu-id="3ef44-195">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="3ef44-196">[上一页](adding-a-model.md)
[下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="3ef44-196">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
