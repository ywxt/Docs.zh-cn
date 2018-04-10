---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 将列添加到模型 |Microsoft 文档
author: shanselman
description: 这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 7a0b64ce00fc5ee6d49990f1d4d93a154c467bf5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="adding-a-column-to-the-model"></a><span data-ttu-id="da2bf-104">向模型添加列</span><span class="sxs-lookup"><span data-stu-id="da2bf-104">Adding a Column to the Model</span></span>
====================
<span data-ttu-id="da2bf-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="da2bf-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="da2bf-106">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="da2bf-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="da2bf-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="da2bf-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="da2bf-108">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="da2bf-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="da2bf-109">在本部分中我们将演练如何我们可以对我们的数据库的架构进行更改，并在我们的应用程序内处理所做的更改。</span><span class="sxs-lookup"><span data-stu-id="da2bf-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="da2bf-110">让我们将"级别"的列添加到影片表。</span><span class="sxs-lookup"><span data-stu-id="da2bf-110">Let's add a "Rating" Colum to the Movie table.</span></span> <span data-ttu-id="da2bf-111">返回到 IDE，并单击数据库资源管理器。</span><span class="sxs-lookup"><span data-stu-id="da2bf-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="da2bf-112">右键单击电影表并选择打开表定义。</span><span class="sxs-lookup"><span data-stu-id="da2bf-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="da2bf-113">添加"分级"列，如下所示。</span><span class="sxs-lookup"><span data-stu-id="da2bf-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="da2bf-114">我们现在没有任何级别，因为此列可以允许 null 值。</span><span class="sxs-lookup"><span data-stu-id="da2bf-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="da2bf-115">单击保存。</span><span class="sxs-lookup"><span data-stu-id="da2bf-115">Click Save.</span></span>

<span data-ttu-id="da2bf-116">[![编辑电影表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="da2bf-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="da2bf-117">接下来，返回到解决方案资源管理器并打开 Movies.edmx 文件 （这是 \Models 文件夹中）。</span><span class="sxs-lookup"><span data-stu-id="da2bf-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="da2bf-118">右键单击设计图面 （白色区域） 上并从数据库中选择更新模型。</span><span class="sxs-lookup"><span data-stu-id="da2bf-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="da2bf-119">[![电影-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="da2bf-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="da2bf-120">这将启动"更新向导"。</span><span class="sxs-lookup"><span data-stu-id="da2bf-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="da2bf-121">单击刷新选项卡中的，单击完成。</span><span class="sxs-lookup"><span data-stu-id="da2bf-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="da2bf-122">然后将新列更新我们电影模型的类。</span><span class="sxs-lookup"><span data-stu-id="da2bf-122">Our Movie model class will then be updated with the new column.</span></span>

![更新向导 (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="da2bf-124">单击完成，后，你可以看到新的分级列已添加到我们的模型中的电影实体。</span><span class="sxs-lookup"><span data-stu-id="da2bf-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="da2bf-125">[![电影实体](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="da2bf-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="da2bf-126">我们在数据库模型中，添加了列，但是视图不知道有关它。</span><span class="sxs-lookup"><span data-stu-id="da2bf-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="da2bf-127">使用模型更改更新视图</span><span class="sxs-lookup"><span data-stu-id="da2bf-127">Update Views with Model Changes</span></span>

<span data-ttu-id="da2bf-128">有几种方法，我们无法更新我们的视图模板，以反映新的分级列。</span><span class="sxs-lookup"><span data-stu-id="da2bf-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="da2bf-129">由于我们创建这些视图通过添加视图对话框通过生成它们，我们无法将其删除并再次重新创建它们。</span><span class="sxs-lookup"><span data-stu-id="da2bf-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="da2bf-130">但是，通常的人员将具有已进行了修改对其视图模板从初始的基架生成并且将想要添加或删除字段，手动，只需与我们创建相同的 ID 字段。</span><span class="sxs-lookup"><span data-stu-id="da2bf-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="da2bf-131">打开 \Views\Movies\Index.aspx 模板并添加&lt;th&gt;评级&lt;/th&gt;到影片表的开头。</span><span class="sxs-lookup"><span data-stu-id="da2bf-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="da2bf-132">我添加挖掘之后风格。</span><span class="sxs-lookup"><span data-stu-id="da2bf-132">I added mine after Genre.</span></span> <span data-ttu-id="da2bf-133">然后，在相同的列位置但较低位置添加行以便输出我们新级别。</span><span class="sxs-lookup"><span data-stu-id="da2bf-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="da2bf-134">我们最终 Index.aspx 模板将如下所示：</span><span class="sxs-lookup"><span data-stu-id="da2bf-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="da2bf-135">让我们然后打开 \Views\Movies\Create.aspx 模板，然后添加标签和文本框中为我们新分级属性：</span><span class="sxs-lookup"><span data-stu-id="da2bf-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="da2bf-136">我们最终 Create.aspx 模板将如下所示，并让我们更改我们浏览器的标题和辅助&lt;h2&gt;标题为类似于"创建电影"当我们在此处解决 ！</span><span class="sxs-lookup"><span data-stu-id="da2bf-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="da2bf-137">运行你的应用，现在你已生成已添加到创建页面数据库中的新字段。</span><span class="sxs-lookup"><span data-stu-id="da2bf-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="da2bf-138">添加新的影片的分级-此时间，并单击创建。</span><span class="sxs-lookup"><span data-stu-id="da2bf-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="da2bf-139">[![创建电影-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="da2bf-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="da2bf-140">单击创建后，你要发送到索引页在你新影片列出与数据库中的新级别列</span><span class="sxs-lookup"><span data-stu-id="da2bf-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="da2bf-141">[![影片列表-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="da2bf-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="da2bf-142">这一基本教程了你可以开始进行控制器，将其与视图关联并传递关于硬编码数据。</span><span class="sxs-lookup"><span data-stu-id="da2bf-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="da2bf-143">则我们创建和设计数据库，并将一些数据放在。</span><span class="sxs-lookup"><span data-stu-id="da2bf-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="da2bf-144">我们从数据库中检索数据，并显示在 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="da2bf-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="da2bf-145">然后，我们添加创建窗体，让用户将数据添加到数据库本身从 Web 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="da2bf-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="da2bf-146">我们添加验证，则进行客户端上使用 JavaScript 的验证。</span><span class="sxs-lookup"><span data-stu-id="da2bf-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="da2bf-147">最后，我们更改了数据库，以包括新列的数据，然后更新我们的两个页来创建和显示此新数据。</span><span class="sxs-lookup"><span data-stu-id="da2bf-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="da2bf-148">我现在鼓励你转到我们中级教程"[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"以及许多视频和资源在[ https://asp.net/mvc ](https://asp.net/mvc)若要了解更多有关 ASP.NET MVC ！</span><span class="sxs-lookup"><span data-stu-id="da2bf-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="da2bf-149">请尽情体验吧！</span><span class="sxs-lookup"><span data-stu-id="da2bf-149">Enjoy!</span></span>

- <span data-ttu-id="da2bf-150">Scott Hanselman- [ http://hanselman.com ](http://hanselman.com)和[ @shanselman ](http://twitter.com/shanselman)在 Twitter 上。</span><span class="sxs-lookup"><span data-stu-id="da2bf-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="da2bf-151">上一篇</span><span class="sxs-lookup"><span data-stu-id="da2bf-151">Previous</span></span>](getting-started-with-mvc-part7.md)
