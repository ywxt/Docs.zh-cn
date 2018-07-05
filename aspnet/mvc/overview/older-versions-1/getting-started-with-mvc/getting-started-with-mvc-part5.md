---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 从控制器访问模型的数据 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: fe5111e2f103e9b20f27385421a1985062acaac1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371608"
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="b200b-104">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="b200b-104">Accessing your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="b200b-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="b200b-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="b200b-106">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="b200b-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="b200b-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="b200b-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="b200b-108">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="b200b-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="b200b-109">在本部分中我们将创建新的 MoviesController 类，并编写一些代码来检索电影数据，并显示返回到浏览器中使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="b200b-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="b200b-110">右键单击 Controllers 文件夹，并使新 MoviesController。</span><span class="sxs-lookup"><span data-stu-id="b200b-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="b200b-111">[![添加控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b200b-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="b200b-112">这将创建我们的项目中我们 \Controllers 文件夹下的新"MoviesController.cs"文件。</span><span class="sxs-lookup"><span data-stu-id="b200b-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="b200b-113">让我们更新 MovieController 从我们的新填充数据库中检索的影片列表。</span><span class="sxs-lookup"><span data-stu-id="b200b-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="b200b-114">我们正在执行 LINQ 查询，以便我们仅检索在 1984 年夏天之后发布的电影。</span><span class="sxs-lookup"><span data-stu-id="b200b-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="b200b-115">我们将需要视图模板能够呈现电影返回此列表，因此在方法中右键单击并选择添加视图来创建它。</span><span class="sxs-lookup"><span data-stu-id="b200b-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="b200b-116">在添加视图对话框将指示我们传递的列表&lt;Movies.Models.Movie&gt;向视图模板。</span><span class="sxs-lookup"><span data-stu-id="b200b-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="b200b-117">与上一次我们使用添加视图对话框中，选择创建一个"空"模板，我们将指示这次我们希望 Visual Studio 自动"搭建基架"视图模板为我们使用一些默认内容。</span><span class="sxs-lookup"><span data-stu-id="b200b-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="b200b-118">我们将执行此操作选择的"列表"项中的"视图内容的下拉列表菜单。</span><span class="sxs-lookup"><span data-stu-id="b200b-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="b200b-119">请记住，您可以创建一个新类，你将需要编译为其显示在添加的视图对话框的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b200b-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![添加视图](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="b200b-121">单击添加，系统将自动生成的代码用于视图为我们显示我们的电影列表。</span><span class="sxs-lookup"><span data-stu-id="b200b-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="b200b-122">这是更改的好时机&lt;h2&gt;标题为"My Movie List"类似，我们之前使用 Hello World 视图。</span><span class="sxs-lookup"><span data-stu-id="b200b-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="b200b-123">[![电影-Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b200b-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="b200b-124">运行应用程序并在地址栏中访问 /Movies。</span><span class="sxs-lookup"><span data-stu-id="b200b-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="b200b-125">现在我们使用基本控制器中的查询从数据库检索数据并将数据返回到了解的有关电影的视图。</span><span class="sxs-lookup"><span data-stu-id="b200b-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="b200b-126">该视图然后旋转的电影列表，并会为我们创建包含数据的表。</span><span class="sxs-lookup"><span data-stu-id="b200b-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="b200b-127">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="b200b-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="b200b-128">因此我们无需为我们创建了基架模板的默认链接，我们不会将实现与此应用程序的编辑、 详细信息和删除功能。</span><span class="sxs-lookup"><span data-stu-id="b200b-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="b200b-129">打开 /Movies/Index.aspx 文件并将其删除。</span><span class="sxs-lookup"><span data-stu-id="b200b-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="b200b-130">下面是什么我们已更新的视图模板应如下所示我们做这些更改后的源代码：</span><span class="sxs-lookup"><span data-stu-id="b200b-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="b200b-131">它创建我们不需要的链接，因此对于此示例将删除它们。</span><span class="sxs-lookup"><span data-stu-id="b200b-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="b200b-132">但是，因为这是下一步，我们将保留我们新创建的链接 ！</span><span class="sxs-lookup"><span data-stu-id="b200b-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="b200b-133">下面是我们的应用程序中删除的列的外观。</span><span class="sxs-lookup"><span data-stu-id="b200b-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="b200b-134">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="b200b-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="b200b-135">我们现在有了我们的电影数据的简单列表。</span><span class="sxs-lookup"><span data-stu-id="b200b-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="b200b-136">但是，如果我们单击"新建"链接时，我们将会出错，因为它不挂起 ！</span><span class="sxs-lookup"><span data-stu-id="b200b-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="b200b-137">让我们实现创建操作方法，并使用户能够在我们的数据库输入新影片。</span><span class="sxs-lookup"><span data-stu-id="b200b-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b200b-138">[上一页](getting-started-with-mvc-part4.md)
> [下一页](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="b200b-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
