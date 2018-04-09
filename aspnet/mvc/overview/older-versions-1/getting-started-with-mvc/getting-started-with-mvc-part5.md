---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 从控制器访问您的模型的数据 |Microsoft 文档
author: shanselman
description: 这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 2ba1b73f40a920e27e4a03d9f703e62054d3f25c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="db5bd-104">从控制器访问您的模型的数据</span><span class="sxs-lookup"><span data-stu-id="db5bd-104">Accessing your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="db5bd-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="db5bd-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="db5bd-106">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="db5bd-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="db5bd-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="db5bd-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="db5bd-108">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="db5bd-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="db5bd-109">在本部分中我们将创建新的 MoviesController 类，并编写一些代码来检索我们影片数据并将其显示回浏览器使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="db5bd-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="db5bd-110">右键单击 Controllers 文件夹，并使新 MoviesController。</span><span class="sxs-lookup"><span data-stu-id="db5bd-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="db5bd-111">[![添加控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="db5bd-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="db5bd-112">这将创建我们项目中我们 \Controllers 文件夹下的新"MoviesController.cs"文件。</span><span class="sxs-lookup"><span data-stu-id="db5bd-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="db5bd-113">让我们更新 MovieController 从我们新填充的数据库中检索的影片列表。</span><span class="sxs-lookup"><span data-stu-id="db5bd-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="db5bd-114">我们正在执行 LINQ 查询，以便我们只能检索发布后 1984年夏天的电影。</span><span class="sxs-lookup"><span data-stu-id="db5bd-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="db5bd-115">我们将需要一个视图模板来呈现电影返回此列表，因此在方法中右键单击，然后选择添加视图，以创建它。</span><span class="sxs-lookup"><span data-stu-id="db5bd-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="db5bd-116">在添加视图对话框将指示我们会将一个列表传递&lt;Movies.Models.Movie&gt;到我们查看模板。</span><span class="sxs-lookup"><span data-stu-id="db5bd-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="db5bd-117">与不同的是我们使用添加视图对话框并选择"空"模板创建以前的时间，我们将指示这次我们希望 Visual Studio 自动"搭建基架"视图模板为我们具有一些默认内容。</span><span class="sxs-lookup"><span data-stu-id="db5bd-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="db5bd-118">我们需要执行此操作通过选择"列表"项中的"视图内容的下拉列表菜单。</span><span class="sxs-lookup"><span data-stu-id="db5bd-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="db5bd-119">请记住，你可以创建一个新的类，你将需要编译为其显示在添加的视图对话框的应用程序。</span><span class="sxs-lookup"><span data-stu-id="db5bd-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![添加视图](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="db5bd-121">单击添加和系统将自动生成的代码用于视图为我们显示我们的影片列表。</span><span class="sxs-lookup"><span data-stu-id="db5bd-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="db5bd-122">这是更改的好时机&lt;h2&gt;像我们前面与 Hello World 视图标题为"我的电影列表"类似。</span><span class="sxs-lookup"><span data-stu-id="db5bd-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="db5bd-123">[![电影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="db5bd-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="db5bd-124">运行你的应用程序，并在地址栏中访问 /Movies。</span><span class="sxs-lookup"><span data-stu-id="db5bd-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="db5bd-125">现在我们已使用控制器中的基本查询从数据库检索数据并将数据返回到知道电影的视图。</span><span class="sxs-lookup"><span data-stu-id="db5bd-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="db5bd-126">该视图然后旋转通过影片列表，并为我们创建数据的表。</span><span class="sxs-lookup"><span data-stu-id="db5bd-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="db5bd-127">[![影片列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="db5bd-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="db5bd-128">因此我们不需要基架模板创建为我们的默认链接，我们不会将实现与此应用程序-编辑、 详细信息和删除功能。</span><span class="sxs-lookup"><span data-stu-id="db5bd-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="db5bd-129">打开 /Movies/Index.aspx 文件并将其删除。</span><span class="sxs-lookup"><span data-stu-id="db5bd-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="db5bd-130">下面是什么我们更新的视图模板应如下所示我们进行这些更改后的源代码：</span><span class="sxs-lookup"><span data-stu-id="db5bd-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="db5bd-131">它创建我们不需要的链接，因此我们将此示例删除它们。</span><span class="sxs-lookup"><span data-stu-id="db5bd-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="db5bd-132">不过，根据下一步，我们会保持我们创建新的链接 ！</span><span class="sxs-lookup"><span data-stu-id="db5bd-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="db5bd-133">下面是我们的应用程序与删除此列的外观。</span><span class="sxs-lookup"><span data-stu-id="db5bd-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="db5bd-134">[![影片列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="db5bd-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="db5bd-135">我们现在有了影片数据的简单列表。</span><span class="sxs-lookup"><span data-stu-id="db5bd-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="db5bd-136">但是，如果我们单击"新建"链接，我们将收到错误，因为它未挂钩 ！</span><span class="sxs-lookup"><span data-stu-id="db5bd-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="db5bd-137">让我们实现创建的操作方法，并使用户能够在我们的数据库中输入新影片。</span><span class="sxs-lookup"><span data-stu-id="db5bd-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="db5bd-138">[上一页](getting-started-with-mvc-part4.md)
> [下一页](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="db5bd-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
