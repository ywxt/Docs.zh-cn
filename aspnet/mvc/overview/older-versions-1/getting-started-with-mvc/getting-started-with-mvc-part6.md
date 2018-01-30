---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: "添加创建方法，并创建视图 |Microsoft 文档"
author: shanselman
description: "这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 36b3d6ef0432292f21ecd8f29ea2d88ee8867436
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
<a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="693bc-104">添加创建方法，并创建视图</span><span class="sxs-lookup"><span data-stu-id="693bc-104">Adding a Create Method and Create View</span></span>
====================
<span data-ttu-id="693bc-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="693bc-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="693bc-106">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="693bc-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="693bc-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="693bc-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="693bc-108">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="693bc-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="693bc-109">在本部分中我们将实现使用户能够在我们的数据库中创建新影片所需的支持。</span><span class="sxs-lookup"><span data-stu-id="693bc-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="693bc-110">我们将实现电影/创建 URL 操作来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="693bc-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="693bc-111">实现电影/创建 URL 是一个两步过程。</span><span class="sxs-lookup"><span data-stu-id="693bc-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="693bc-112">当用户第一次访问电影/创建 URL 我们想要显示这些通道他们可以填写输入新的影片的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="693bc-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="693bc-113">然后，当用户提交窗体和数据回服务器的文章，我们想要检索的已发布的内容并将其保存到我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="693bc-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="693bc-114">我们将在我们 MoviesController 类中实现这两个 create （） 方法内的两个步骤。</span><span class="sxs-lookup"><span data-stu-id="693bc-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="693bc-115">一种方法将显示&lt;窗体&gt;用户应填写创建新的影片。</span><span class="sxs-lookup"><span data-stu-id="693bc-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="693bc-116">第二种方法将处理处理的已发布的数据，当用户提交&lt;窗体&gt;回服务器，并将保存在我们的数据库中新的影片。</span><span class="sxs-lookup"><span data-stu-id="693bc-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="693bc-117">下面是代码我们将添加到我们 MoviesController 类，以实现这一方案：</span><span class="sxs-lookup"><span data-stu-id="693bc-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="693bc-118">上面的代码包含所有我们需要我们控制器中的代码。</span><span class="sxs-lookup"><span data-stu-id="693bc-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="693bc-119">让我们现在实现我们将使用向用户显示的窗体的 Create View 模板。</span><span class="sxs-lookup"><span data-stu-id="693bc-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="693bc-120">我们将在第一种创建方法中右键单击，然后选择"添加视图"，以创建我们电影窗体视图模板。</span><span class="sxs-lookup"><span data-stu-id="693bc-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="693bc-121">我们将选择我们要将视图模板传递"电影"与它视图的数据类，并指示我们想要"搭建基架的"的"创建"模板。</span><span class="sxs-lookup"><span data-stu-id="693bc-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="693bc-122">[![添加视图](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="693bc-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="693bc-123">单击添加按钮后，将为你创建 \Movies\Create.aspx 视图模板。</span><span class="sxs-lookup"><span data-stu-id="693bc-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="693bc-124">由于我们从"查看内容"下拉列表中选择"创建"，添加视图对话框中自动"基架"一些默认内容为我们。</span><span class="sxs-lookup"><span data-stu-id="693bc-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="693bc-125">基架创建 HTML&lt;窗体&gt;、 验证错误的位置消息若要转，和基架知道电影，因为它创建标签和字段我们的类的每个属性。</span><span class="sxs-lookup"><span data-stu-id="693bc-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="693bc-126">由于我们的数据库自动使一部电影 ID，请让我们这些字段删除该引用模型。从我们创建视图的 id。</span><span class="sxs-lookup"><span data-stu-id="693bc-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="693bc-127">删除后的几行 7&lt;图例&gt;字段&lt;/legend&gt;如它们所示的 ID 字段，我们不希望。</span><span class="sxs-lookup"><span data-stu-id="693bc-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="693bc-128">让我们现在创建新的影片，并将其添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="693bc-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="693bc-129">我们执行此操作通过运行一次，应用程序，请访问"/ 电影"URL，然后单击"创建"链接以添加新的影片。</span><span class="sxs-lookup"><span data-stu-id="693bc-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="693bc-130">[![创建的 Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="693bc-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="693bc-131">当我们单击创建按钮时，我们将为回 （通过 HTTP POST) 的数据发布到我们刚刚创建的 /Movies/Create 方法此窗体上。</span><span class="sxs-lookup"><span data-stu-id="693bc-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="693bc-132">一样在系统自动花费了超出 URL 的"numTimes"和"名称"参数，并映射到更早版本的方法上的参数，系统将自动将窗体字段带从文章，并将它们映射到对象。</span><span class="sxs-lookup"><span data-stu-id="693bc-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="693bc-133">在这种情况下，从 HTML 如"ReleaseDate"和"标题"中的字段的值将自动放入一部电影的新实例的正确属性中。</span><span class="sxs-lookup"><span data-stu-id="693bc-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="693bc-134">让我们看一下第二个的 Create 方法从我们 MoviesController 试。</span><span class="sxs-lookup"><span data-stu-id="693bc-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="693bc-135">请注意它采用"电影"对象用作参数的方式：</span><span class="sxs-lookup"><span data-stu-id="693bc-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="693bc-136">此电影对象然后传递给我们创建操作方法中，[HttpPost] 版本和我们将其保存在数据库中，然后被用户重定向回影片列表中将显示已保存的结果 index （） 的操作方法：</span><span class="sxs-lookup"><span data-stu-id="693bc-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="693bc-137">[![影片列表-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="693bc-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="693bc-138">我们不检查是否我们电影是正确的不过，并且数据库不会使我们能够与无标题保存一部电影。</span><span class="sxs-lookup"><span data-stu-id="693bc-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="693bc-139">如果我们无法告知用户的数据库之前引发了错误，则可以很好。</span><span class="sxs-lookup"><span data-stu-id="693bc-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="693bc-140">我们将通过将验证支持添加到我们的应用程序来执行此下一步。</span><span class="sxs-lookup"><span data-stu-id="693bc-140">We'll do this next by adding validation support to our application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="693bc-141">[上一页](getting-started-with-mvc-part5.md)
[下一页](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="693bc-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
