---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: "从控制器 (VB) 访问您的模型的数据 |Microsoft 文档"
author: Rick-Anderson
description: "本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f1a1db907aa1d0a62af9b363fabfc74ac11acc68
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="3bcb2-103">从控制器 (VB) 访问您的模型的数据</span><span class="sxs-lookup"><span data-stu-id="3bcb2-103">Accessing your Model's Data from a Controller (VB)</span></span>
====================
<span data-ttu-id="3bcb2-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="3bcb2-105">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3bcb2-106">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3bcb2-107">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3bcb2-108">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3bcb2-109">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="3bcb2-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3bcb2-110">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="3bcb2-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3bcb2-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="3bcb2-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3bcb2-112">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3bcb2-113">Visual Web Developer 项目与 VB.NET 的源代码是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3bcb2-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3bcb2-115">如果你愿意 C#，切换到[C# 版本](../cs/accessing-your-models-data-from-a-controller.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>


<span data-ttu-id="3bcb2-116">在本部分中，将创建一个新`MoviesController`类，并编写代码检索影片数据并将其显示在浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="3bcb2-117">请确保生成应用程序然后再继续。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="3bcb2-118">右键单击*控制器*文件夹并创建新`MoviesController`控制器。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="3bcb2-119">选择以下选项：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-119">Select the following options:</span></span>

- <span data-ttu-id="3bcb2-120">控制器名称： **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="3bcb2-121">（这是默认值）。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-121">(This is the default.)</span></span>
- <span data-ttu-id="3bcb2-122">模板：**控制器，具有读/写操作和视图使用 Entity Framework**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="3bcb2-123">模型类：**电影 (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3bcb2-124">数据上下文类： **MovieDBContext (MvcMovie.Models)**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3bcb2-125">视图： **Razor (CSHTML)**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="3bcb2-126">（默认值。）</span><span class="sxs-lookup"><span data-stu-id="3bcb2-126">(The default.)</span></span>

<span data-ttu-id="3bcb2-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="3bcb2-128">单击 **“添加”**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-128">Click **Add**.</span></span> <span data-ttu-id="3bcb2-129">Visual Web Developer 会创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="3bcb2-130">*MoviesController.vb*文件在项目的*控制器*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="3bcb2-131">A*电影*文件夹在项目的*视图*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="3bcb2-132">*Create.vbhtml，Delete.vbhtml，Details.vbhtml，Edit.vbhtml*，和*Index.vbhtml*在新*Views\Movies*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="3bcb2-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="3bcb2-134">ASP.NET MVC 3 基架机制自动创建 CRUD （创建、 读取、 更新和删除） 操作方法和为你的视图。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="3bcb2-135">你现在具有完全正常运行的 web 应用程序，你可以创建、 列出、 编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="3bcb2-136">运行应用程序，并浏览到`Movies`控制器通过追加*/Movies*到你的浏览器的地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="3bcb2-137">因为应用程序依赖于默认路由 (在中定义*Global.asax*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认值`Index`操作方法`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="3bcb2-138">换而言之，浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="3bcb2-139">结果是电影、 一个空列表，因为你尚未添加。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="3bcb2-140">创建电影</span><span class="sxs-lookup"><span data-stu-id="3bcb2-140">Creating a Movie</span></span>

<span data-ttu-id="3bcb2-141">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-141">Select the **Create New** link.</span></span> <span data-ttu-id="3bcb2-142">输入一些有关影片详细信息，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="3bcb2-143">单击**创建**按钮使窗体发布到服务器，其中的影片信息保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="3bcb2-144">然后转向*/Movies* URL，其中你可以看到在列表中新创建的影片。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="3bcb2-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="3bcb2-146">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-146">Create a couple more movie entries.</span></span> <span data-ttu-id="3bcb2-147">试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="3bcb2-148">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="3bcb2-148">Examining the Generated Code</span></span>

<span data-ttu-id="3bcb2-149">打开*Controllers\MoviesController.vb*文件并检查生成`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="3bcb2-150">电影控制器与的一部分`Index`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="3bcb2-151">以下行从`MoviesController`类实例化电影数据库上下文，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="3bcb2-152">电影数据库上下文可用于查询、 编辑和删除电影。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="3bcb2-153">对请求`Movies`控制器将返回中的所有条目`Movies`电影数据库表，然后将传递到结果`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="3bcb2-154">强类型模型和@model关键字</span><span class="sxs-lookup"><span data-stu-id="3bcb2-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="3bcb2-155">之前在本教程中，您了解了如何控制器传递数据或对象视图模板使用到`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="3bcb2-156">`ViewBag`是一个动态对象，提供了简便的后期绑定方法，将信息传递给视图。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="3bcb2-157">ASP.NET MVC 还提供了将强传递的功能类型化数据或查看模板的对象。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="3bcb2-158">此强类型方法允许更好地进行编译时检查的代码和在 Visual Web Developer 编辑器中的更丰富智能感知。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="3bcb2-159">我们将使用此方法`MoviesController`类和*Index.vbhtml*查看模板。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="3bcb2-160">请注意该代码如何创建[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它调用`View`中的帮助器方法`Index`操作方法。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="3bcb2-161">在代码然后传递此`Movies`从控制器到视图的列表：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="3bcb2-162">通过包括`@ModelType`语句视图模板文件的顶部，你可以指定视图需要的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="3bcb2-163">在创建电影控制器时，Visual Web Developer 将自动包括以下`@model`语句的顶部*Index.vbhtml*文件：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="3bcb2-164">这`@ModelType`指令允许你访问的控制器传递到视图中使用的影片列表`Model`强类型的对象。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="3bcb2-165">例如，在*Index.vbhtml*模板，该代码循环访问电影通过这样做，`foreach`通过强类型化的语句`Model`对象：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="3bcb2-166">因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，则每个`item`循环中的对象被类型化为`Movie`。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="3bcb2-167">其他优点，这意味着你获取编译时检查的代码，并在代码编辑器中的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="3bcb2-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="3bcb2-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="3bcb2-169">使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="3bcb2-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="3bcb2-170">提供的数据库连接字符串指向 entity Framework Code First 检测到`Movies`不存在，因此 Code First 数据库自动创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="3bcb2-171">你可以验证它由查找中已创建*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="3bcb2-172">如果看不到*Movies.sdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏上，单击**刷新**按钮，然后再展开*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="3bcb2-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="3bcb2-174">双击*Movies.sdf*以打开**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="3bcb2-175">然后展开**表**文件夹以查看已在数据库中创建的表。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3bcb2-176">如果你收到错误，当你双击*Movies.sdf*，请确保已安装**Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="3bcb2-177">（有关软件的链接，请参阅本系列教程的第 1 部分中的先决条件的列表。）如果你现在安装版本，你将需要关闭并重新打开 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>


<span data-ttu-id="3bcb2-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="3bcb2-179">有两个表，一个用于`Movie`实体集，然后`EdmMetadata`表。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="3bcb2-180">`EdmMetadata`实体框架使用表来确定何时模型和数据库同步。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="3bcb2-181">右键单击`Movies`表，然后选择**显示表数据**以查看你创建的数据。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="3bcb2-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="3bcb2-183">右键单击`Movies`表，然后选择**编辑表架构**。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="3bcb2-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="3bcb2-186">请注意如何的架构`Movies`表映射到`Movie`前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="3bcb2-187">Entity Framework Code First 自动创建此架构根据你`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="3bcb2-188">完成后，关闭连接。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-188">When you're finished, close the connection.</span></span> <span data-ttu-id="3bcb2-189">（如果不关闭连接，你可能会错误在下次运行项目时）。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="3bcb2-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="3bcb2-191">你现在具有数据库和一个简单列表页，以便显示从它的内容。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="3bcb2-192">在下一步的教程中，我们将检查基架的代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`可以搜索此数据库中的电影的视图。</span><span class="sxs-lookup"><span data-stu-id="3bcb2-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="3bcb2-193">[上一页](adding-a-model.md)
[下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="3bcb2-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
