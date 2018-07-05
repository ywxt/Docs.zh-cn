---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 添加创建方法，并创建视图 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 976df78ea22c30c094f70a57792d287f15d2c62d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400903"
---
<a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="72b47-104">添加创建方法，并创建视图</span><span class="sxs-lookup"><span data-stu-id="72b47-104">Adding a Create Method and Create View</span></span>
====================
<span data-ttu-id="72b47-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="72b47-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="72b47-106">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="72b47-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="72b47-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="72b47-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="72b47-108">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="72b47-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="72b47-109">在本部分中我们要实现使用户能够在我们的数据库中创建新电影所需的支持。</span><span class="sxs-lookup"><span data-stu-id="72b47-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="72b47-110">我们将通过实现电影/创建 URL 操作来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="72b47-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="72b47-111">实现电影/创建 URL 是一个两步过程。</span><span class="sxs-lookup"><span data-stu-id="72b47-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="72b47-112">当用户首次访问电影/创建 URL 我们需要向他们展示他们可以填写输入新电影的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="72b47-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="72b47-113">然后，当用户提交窗体和数据返回到服务器的文章，我们想要检索已发布的内容并将其保存到我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="72b47-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="72b47-114">我们为 MoviesController 类中，我们将实现两个 create （） 方法中的这两个步骤。</span><span class="sxs-lookup"><span data-stu-id="72b47-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="72b47-115">一种方法将显示&lt;窗体&gt;用户应填写创建新的电影。</span><span class="sxs-lookup"><span data-stu-id="72b47-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="72b47-116">第二种方法将处理处理已发布的数据，当用户提交&lt;窗体&gt;回服务器，并保存新电影中我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="72b47-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="72b47-117">下面是代码我们将添加到我们为 MoviesController 类，以实现这一点：</span><span class="sxs-lookup"><span data-stu-id="72b47-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="72b47-118">上面的代码中包含的所有控制器中，我们需要代码。</span><span class="sxs-lookup"><span data-stu-id="72b47-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="72b47-119">现在让我们来实现，我们将使用向用户显示窗体创建视图模板。</span><span class="sxs-lookup"><span data-stu-id="72b47-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="72b47-120">我们将第一个 Create 方法中右键单击并选择"添加视图"，以创建电影窗体的视图模板。</span><span class="sxs-lookup"><span data-stu-id="72b47-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="72b47-121">我们将选择，我们要为其视图数据类，通过查看模板"电影"，并指出我们希望"搭建基架的"的"创建"模板。</span><span class="sxs-lookup"><span data-stu-id="72b47-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="72b47-122">[![添加视图](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="72b47-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="72b47-123">单击添加按钮后，将为您创建 \Movies\Create.aspx 视图模板。</span><span class="sxs-lookup"><span data-stu-id="72b47-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="72b47-124">由于我们从"视图内容"下拉列表中选择"创建"，添加视图对话框中自动"基架"一些默认内容为我们。</span><span class="sxs-lookup"><span data-stu-id="72b47-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="72b47-125">基架创建对应的 HTML&lt;窗体&gt;、 使验证错误消息，随时随地和基架了解的有关电影，因为它创建标签和字段我们的类的每个属性。</span><span class="sxs-lookup"><span data-stu-id="72b47-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="72b47-126">由于我们的数据库自动提供电影的 ID，让我们这些字段删除该引用模型。从我们创建视图的 id。</span><span class="sxs-lookup"><span data-stu-id="72b47-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="72b47-127">删除后的 7 几&lt;图例&gt;字段&lt;/legend&gt;如他们所示的 ID 字段，我们不希望。</span><span class="sxs-lookup"><span data-stu-id="72b47-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="72b47-128">现在让我们来创建新电影并将其添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="72b47-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="72b47-129">我们将运行一次应用程序执行此操作，请访问"/ 电影"URL，然后单击"创建"链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="72b47-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="72b47-130">[![创建的 Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="72b47-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="72b47-131">当我们单击创建按钮时，我们将进行回 （通过 HTTP POST) 的数据发布到我们刚刚创建的 /Movies/Create 方法此窗体上。</span><span class="sxs-lookup"><span data-stu-id="72b47-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="72b47-132">就像在系统自动执行在 url 的"numTimes"和"name"参数，并映射到在前面的方法的参数，系统将自动从帖子采取窗体字段，并将它们映射到一个对象。</span><span class="sxs-lookup"><span data-stu-id="72b47-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="72b47-133">在这种情况下，从"ReleaseDate"和"Title"等的 HTML 中的字段的值都将自动放入电影的新实例的正确属性。</span><span class="sxs-lookup"><span data-stu-id="72b47-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="72b47-134">让我们看一下第二个 Create 方法从我们为 MoviesController 试。</span><span class="sxs-lookup"><span data-stu-id="72b47-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="72b47-135">请注意如何需要"电影"对象作为参数：</span><span class="sxs-lookup"><span data-stu-id="72b47-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="72b47-136">然后此电影对象传递给我们创建的操作方法，[HttpPost] 版本和我们在数据库中保存和重定向回到 index （） 操作方法，它将在已保存的结果显示电影列表中的用户：</span><span class="sxs-lookup"><span data-stu-id="72b47-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="72b47-137">[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="72b47-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="72b47-138">我们不会检查是否我们的电影是正确的不过，并且数据库不会使我们能够将电影保存与没有标题。</span><span class="sxs-lookup"><span data-stu-id="72b47-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="72b47-139">如果我们可以告诉用户的数据库之前引发了错误，它很好。</span><span class="sxs-lookup"><span data-stu-id="72b47-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="72b47-140">我们通过将验证支持添加到我们的应用程序执行此下一步。</span><span class="sxs-lookup"><span data-stu-id="72b47-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="72b47-141">[上一页](getting-started-with-mvc-part5.md)
> [下一页](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="72b47-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
