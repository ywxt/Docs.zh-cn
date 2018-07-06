---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 将列添加到模型 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 5dbda1280c073d5d4f2d71918ca31bc44475f64d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817196"
---
<a name="adding-a-column-to-the-model"></a><span data-ttu-id="a628f-104">向模型添加列</span><span class="sxs-lookup"><span data-stu-id="a628f-104">Adding a Column to the Model</span></span>
====================
<span data-ttu-id="a628f-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="a628f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="a628f-106">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="a628f-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="a628f-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="a628f-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="a628f-108">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="a628f-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="a628f-109">在本部分中我们将引导完成如何对我们的数据库的架构进行更改并处理我们的应用程序中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="a628f-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="a628f-110">让我们将"评级"列添加到的 Movie 表。</span><span class="sxs-lookup"><span data-stu-id="a628f-110">Let's add a "Rating" Colum to the Movie table.</span></span> <span data-ttu-id="a628f-111">返回到 IDE，并单击数据库资源管理器。</span><span class="sxs-lookup"><span data-stu-id="a628f-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="a628f-112">右键单击的 Movie 表并选择打开表定义。</span><span class="sxs-lookup"><span data-stu-id="a628f-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="a628f-113">添加"Rating"列，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a628f-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="a628f-114">我们现在没有任何分级，因为此列可以允许 null 值。</span><span class="sxs-lookup"><span data-stu-id="a628f-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="a628f-115">单击保存。</span><span class="sxs-lookup"><span data-stu-id="a628f-115">Click Save.</span></span>

<span data-ttu-id="a628f-116">[![编辑电影表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a628f-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="a628f-117">接下来，返回到解决方案资源管理器并打开 Movies.edmx 文件 （这是 \Models 文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="a628f-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="a628f-118">右键单击设计图面 （白色区域） 上，然后选择从数据库更新模型。</span><span class="sxs-lookup"><span data-stu-id="a628f-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="a628f-119">[![电影-Microsoft Visual Web Developer 2010 速成版 (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a628f-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="a628f-120">这将启动"更新向导"。</span><span class="sxs-lookup"><span data-stu-id="a628f-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="a628f-121">单击刷新选项卡中的，单击完成。</span><span class="sxs-lookup"><span data-stu-id="a628f-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="a628f-122">然后将新列更新我们的 Movie 模型类。</span><span class="sxs-lookup"><span data-stu-id="a628f-122">Our Movie model class will then be updated with the new column.</span></span>

![更新向导 (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="a628f-124">单击完成后, 可以看到新的评级列已添加到我们的模型中的电影实体。</span><span class="sxs-lookup"><span data-stu-id="a628f-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="a628f-125">[![电影实体](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="a628f-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="a628f-126">我们已在数据库模型中，添加一个列，但视图不知道它。</span><span class="sxs-lookup"><span data-stu-id="a628f-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="a628f-127">使用模型更改更新视图</span><span class="sxs-lookup"><span data-stu-id="a628f-127">Update Views with Model Changes</span></span>

<span data-ttu-id="a628f-128">有几种方法我们无法更新我们的视图模板以反映新的 Rating 列。</span><span class="sxs-lookup"><span data-stu-id="a628f-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="a628f-129">由于我们通过生成它们通过添加视图对话框来创建这些视图，我们可以将其删除并再次重新创建它们。</span><span class="sxs-lookup"><span data-stu-id="a628f-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="a628f-130">但是，通常人们将已进行了修改到其视图模板从初始的基架生成并且将想要添加或删除字段，请手动，只需与使用 ID 字段用于创建。</span><span class="sxs-lookup"><span data-stu-id="a628f-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="a628f-131">打开 \Views\Movies\Index.aspx 模板和添加&lt;th&gt;评级&lt;/th&gt;到开头的 Movie 表。</span><span class="sxs-lookup"><span data-stu-id="a628f-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="a628f-132">我添加我的流派之后。</span><span class="sxs-lookup"><span data-stu-id="a628f-132">I added mine after Genre.</span></span> <span data-ttu-id="a628f-133">然后，在相同的列位置但较低位置添加一个行，以输出我们新的分级。</span><span class="sxs-lookup"><span data-stu-id="a628f-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="a628f-134">我们最终 Index.aspx 模板将如下所示：</span><span class="sxs-lookup"><span data-stu-id="a628f-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="a628f-135">让我们再打开 \Views\Movies\Create.aspx 模板，并为我们的新分级属性添加标签和文本框：</span><span class="sxs-lookup"><span data-stu-id="a628f-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="a628f-136">我们最终 Create.aspx 模板将如下所示，并让我们更改浏览器的标题和辅助数据库&lt;h2&gt;标题为类似于"创建电影"虽然我们在这里 ！</span><span class="sxs-lookup"><span data-stu-id="a628f-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="a628f-137">运行您的应用程序，现在你已生成的数据库的已添加到创建页中的新字段。</span><span class="sxs-lookup"><span data-stu-id="a628f-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="a628f-138">添加新电影-这次使用一个级别的并单击创建。</span><span class="sxs-lookup"><span data-stu-id="a628f-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="a628f-139">[![创建电影的 Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="a628f-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="a628f-140">单击创建后，你将被转到索引页在你新电影列出与数据库中新的评级列</span><span class="sxs-lookup"><span data-stu-id="a628f-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="a628f-141">[![电影列表-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="a628f-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="a628f-142">这一基本教程能满足你的启动使控制器，将它们与视图相关联并传递硬编码数据。</span><span class="sxs-lookup"><span data-stu-id="a628f-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="a628f-143">然后，创建和设计数据库并将一些数据中。</span><span class="sxs-lookup"><span data-stu-id="a628f-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="a628f-144">我们从数据库中检索数据并显示在 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="a628f-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="a628f-145">然后，我们添加了允许用户将数据添加到数据库本身从 Web 应用程序中创建窗体。</span><span class="sxs-lookup"><span data-stu-id="a628f-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="a628f-146">我们添加验证，然后进行客户端上使用 JavaScript 的验证。</span><span class="sxs-lookup"><span data-stu-id="a628f-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="a628f-147">最后，我们更改了数据库，以包括新列的数据，然后更新我们的两个页，以创建并显示此新数据。</span><span class="sxs-lookup"><span data-stu-id="a628f-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="a628f-148">我现在鼓励您转到我们的中级教程"[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"以及许多的视频和资源，请访问[ https://asp.net/mvc ](https://asp.net/mvc)甚至更多地了解 ASP.NET MVC ！</span><span class="sxs-lookup"><span data-stu-id="a628f-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="a628f-149">请尽情体验吧！</span><span class="sxs-lookup"><span data-stu-id="a628f-149">Enjoy!</span></span>

- <span data-ttu-id="a628f-150">Scott Hanselman- [ http://hanselman.com ](http://hanselman.com)并[ @shanselman ](http://twitter.com/shanselman) Twitter 上。</span><span class="sxs-lookup"><span data-stu-id="a628f-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a628f-151">上一篇</span><span class="sxs-lookup"><span data-stu-id="a628f-151">Previous</span></span>](getting-started-with-mvc-part7.md)
