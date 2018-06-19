---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 添加视图 |Microsoft 文档
author: shanselman
description: 这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 978d7980274c072ed559b54ed69ab86245b6c5a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
ms.locfileid: "30869590"
---
<a name="adding-a-view"></a><span data-ttu-id="88c25-104">添加视图</span><span class="sxs-lookup"><span data-stu-id="88c25-104">Adding a View</span></span>
====================
<span data-ttu-id="88c25-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="88c25-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="88c25-106">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="88c25-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="88c25-107">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="88c25-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="88c25-108">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="88c25-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="88c25-109">在本部分中我们将查看如何我们可以使用视图模板文件来完全封装回客户端生成的 HTML 响应我们 HelloWorldController 类。</span><span class="sxs-lookup"><span data-stu-id="88c25-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="88c25-110">让我们开始通过查看模板使用我们 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="88c25-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="88c25-111">我们的方法中调用索引，它位于 HelloWorldController。</span><span class="sxs-lookup"><span data-stu-id="88c25-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="88c25-112">目前我们 index （） 方法返回使用的是控制器类中的硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="88c25-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="88c25-113">让我们现在更改索引方法，以便改用如下所示：</span><span class="sxs-lookup"><span data-stu-id="88c25-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="88c25-114">让我们现在添加到我们的项目，我们可以使用我们的 index （） 方法中的视图模板。</span><span class="sxs-lookup"><span data-stu-id="88c25-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="88c25-115">若要执行此操作，用某个位置的中间索引方法鼠标右键单击，然后单击添加视图...</span><span class="sxs-lookup"><span data-stu-id="88c25-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![图像](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="88c25-117">这将显示为我们提供一些用于我们想要创建可由我们的索引方法中的视图模板选项的"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="88c25-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="88c25-118">现在，不更改任何内容，并只需单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="88c25-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="88c25-119">[![添加视图对话框](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="88c25-120">单击添加后，新的文件夹和一个新文件将显示在解决方案文件夹中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="88c25-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="88c25-121">我现在有在该文件夹的视图和 Index.aspx 文件下的一个 HelloWorld 文件夹。</span><span class="sxs-lookup"><span data-stu-id="88c25-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="88c25-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="88c25-123">新索引文件也是已打开的并且可供编辑。</span><span class="sxs-lookup"><span data-stu-id="88c25-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="88c25-124">添加一些文本下第一个&lt;h2&gt;索引&lt;/h2&gt;喜欢"Hello World"。</span><span class="sxs-lookup"><span data-stu-id="88c25-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="88c25-125">运行你的应用程序并访问[ `http://localhost:xx/HelloWorld` ](http://localhostxx)再次在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="88c25-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="88c25-126">在此示例中我们控制器中的索引方法不执行任何工作，但未调用"返回 View()"，它表示我们想要使用的视图模板文件来呈现响应发回客户端。</span><span class="sxs-lookup"><span data-stu-id="88c25-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="88c25-127">因为我们未显式指定要使用的视图模板文件的名称，ASP.NET MVC 将默认为 \Views\HelloWorld 文件夹中使用 Index.aspx 视图文件中。</span><span class="sxs-lookup"><span data-stu-id="88c25-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="88c25-128">现在我们可以看到我们硬编码在我们的视图中的字符串。</span><span class="sxs-lookup"><span data-stu-id="88c25-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="88c25-129">[![索引的 Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="88c25-130">看起来一切都非常好。</span><span class="sxs-lookup"><span data-stu-id="88c25-130">Looks pretty good.</span></span> <span data-ttu-id="88c25-131">但是，请注意，浏览器的标题显示"Index"，并在页上的大标题显示"My MVC Application。"</span><span class="sxs-lookup"><span data-stu-id="88c25-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="88c25-132">让我们更改那些。</span><span class="sxs-lookup"><span data-stu-id="88c25-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="88c25-133">更改视图和母版页</span><span class="sxs-lookup"><span data-stu-id="88c25-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="88c25-134">首先，让我们更改文本"My MVC Application。"</span><span class="sxs-lookup"><span data-stu-id="88c25-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="88c25-135">该文本共享，并显示在每一页。</span><span class="sxs-lookup"><span data-stu-id="88c25-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="88c25-136">它实际出现在只有一个位置在代码中，即使它位于我们的应用程序的每一页上。</span><span class="sxs-lookup"><span data-stu-id="88c25-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="88c25-137">转到在解决方案资源管理器的 /Views/Shared 文件夹并打开 Site.Master 文件。</span><span class="sxs-lookup"><span data-stu-id="88c25-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="88c25-138">此文件称为母版页，它是共享的"shell"我们其他所有页使用。</span><span class="sxs-lookup"><span data-stu-id="88c25-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="88c25-139">请注意此文件中，某些文本表明 ContentPlaceholder"主内容"。</span><span class="sxs-lookup"><span data-stu-id="88c25-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="88c25-140">该占位符为其中你创建的所有页将都显示，"包装"在母版页中。</span><span class="sxs-lookup"><span data-stu-id="88c25-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="88c25-141">尝试更改的标题，然后运行您的应用程序并访问多个页。</span><span class="sxs-lookup"><span data-stu-id="88c25-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="88c25-142">你会注意到，你一次更改出现在多个页上。</span><span class="sxs-lookup"><span data-stu-id="88c25-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="88c25-143">现在每一页将具有主标题-即 h 1-"我的 MVC 影片应用程序。"</span><span class="sxs-lookup"><span data-stu-id="88c25-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="88c25-144">用于处理在那里共享跨所有的页面顶部的白色文本。</span><span class="sxs-lookup"><span data-stu-id="88c25-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="88c25-145">下面是 Site.Master 我们已更改的标题与整个：</span><span class="sxs-lookup"><span data-stu-id="88c25-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="88c25-146">现在，让我们更改索引页的标题。</span><span class="sxs-lookup"><span data-stu-id="88c25-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="88c25-147">打开 /HelloWorld/Index.aspx。</span><span class="sxs-lookup"><span data-stu-id="88c25-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="88c25-148">没有两个位置更改。</span><span class="sxs-lookup"><span data-stu-id="88c25-148">There's two places to change.</span></span> <span data-ttu-id="88c25-149">首先，标题显示的浏览器中，然后辅助标头的也是 H2-标题中。</span><span class="sxs-lookup"><span data-stu-id="88c25-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="88c25-150">我将它们分别略有不同，以便你可以查看代码的哪些位更改应用程序的哪个部分。</span><span class="sxs-lookup"><span data-stu-id="88c25-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="88c25-151">运行你的应用并访问 /Movies。</span><span class="sxs-lookup"><span data-stu-id="88c25-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="88c25-152">请注意，已更改浏览器标题、 主标题和副标题。</span><span class="sxs-lookup"><span data-stu-id="88c25-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="88c25-153">很容易在使用很小的更改对应用程序中进行大更改，向你的视图。</span><span class="sxs-lookup"><span data-stu-id="88c25-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="88c25-154">[![影片列表-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="88c25-155">我们一小段 （在此情况下"Hello World ！"的"数据"</span><span class="sxs-lookup"><span data-stu-id="88c25-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="88c25-156">消息） 很难通过编码。</span><span class="sxs-lookup"><span data-stu-id="88c25-156">message) was hard coded though.</span></span> <span data-ttu-id="88c25-157">我们已有 V (Views)，并且我们具有 C （控制器），但尚没有的 M （模型）。</span><span class="sxs-lookup"><span data-stu-id="88c25-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="88c25-158">我们很快将演练如何创建数据库并从它检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="88c25-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="88c25-159">传递 ViewModel</span><span class="sxs-lookup"><span data-stu-id="88c25-159">Passing a ViewModel</span></span>

<span data-ttu-id="88c25-160">我们转到数据库，并讨论模型之前，不过，让我们先介绍一下"Viewmodel。"</span><span class="sxs-lookup"><span data-stu-id="88c25-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="88c25-161">这些是表示视图模板所需呈现 HTML 响应回客户端的对象。</span><span class="sxs-lookup"><span data-stu-id="88c25-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="88c25-162">它们通常创建和由了控制器类传递给视图模板，并仅应包含视图模板所需的数据而没有其他。</span><span class="sxs-lookup"><span data-stu-id="88c25-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="88c25-163">以前与我们的 HelloWorld 示例，我们 Welcome() 操作方法采用一个名称和 numTimes 参数，并输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="88c25-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="88c25-164">让我们而不是必须继续直接呈现此响应的控制器，而是使一个小型类来存放该数据，然后将它传递到视图模板返回呈现 HTML 响应使用它。</span><span class="sxs-lookup"><span data-stu-id="88c25-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="88c25-165">这种方式控制器关心一件事和查看模板的另一个 – 使我们能够维护完全"分离关注点"我们的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="88c25-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="88c25-166">返回到 HelloWorldController.cs 文件并添加一个新的"WelcomeViewModel"类并更改控制器内部的欢迎方法。</span><span class="sxs-lookup"><span data-stu-id="88c25-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="88c25-167">下面是完整 HelloWorldController.cs 与相同的文件中的新类。</span><span class="sxs-lookup"><span data-stu-id="88c25-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="88c25-168">即使它是在多行上，我们欢迎方法实际上是仅有两个代码语句。</span><span class="sxs-lookup"><span data-stu-id="88c25-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="88c25-169">第一个语句打包我们两个参数转换的 ViewModel 对象和第二个传递拖放到视图生成的对象。</span><span class="sxs-lookup"><span data-stu-id="88c25-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="88c25-170">现在，我们需要一个欢迎视图模板 ！</span><span class="sxs-lookup"><span data-stu-id="88c25-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="88c25-171">欢迎使用的方法中右键单击并选择添加视图。</span><span class="sxs-lookup"><span data-stu-id="88c25-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="88c25-172">此时，我们将检查"创建强类型视图"，并且从下拉列表中选择我们 WelcomeViewModel 类。</span><span class="sxs-lookup"><span data-stu-id="88c25-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="88c25-173">此新视图将只知道 WelcomeViewModels 和任何其他类型的对象。</span><span class="sxs-lookup"><span data-stu-id="88c25-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="88c25-174">*注意： 你将需要将已编译的添加有关你 WelcomeViewModel 才会显示在下拉列表中后，一次。*</span><span class="sxs-lookup"><span data-stu-id="88c25-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>


<span data-ttu-id="88c25-175">下面是你添加视图的对话框应如下所示。</span><span class="sxs-lookup"><span data-stu-id="88c25-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="88c25-176">单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="88c25-176">Click the Add button.</span></span> ![添加视图带圆圈](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="88c25-178">将在下，此代码添加&lt;h2&gt;新 Welcome.aspx 中。</span><span class="sxs-lookup"><span data-stu-id="88c25-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="88c25-179">我们将进行循环，并让用户说出我们应多次说 Hello ！</span><span class="sxs-lookup"><span data-stu-id="88c25-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="88c25-180">另请注意时你输入这些内容因为我们告知这有关 WelcomeViewModel 视图 （已婚，而记住？），我们可以获得有用的 Intellisense 每次我们引用我们模型对象作为下面的屏幕截图所示：</span><span class="sxs-lookup"><span data-stu-id="88c25-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="88c25-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="88c25-182">运行你的应用程序并访问`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`试。</span><span class="sxs-lookup"><span data-stu-id="88c25-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="88c25-183">现在我们会从该 URL 采用数据，它自动传递到控制器，我们控制器打包数据插入视图模型，并将该对象拖放到我们视图传递。</span><span class="sxs-lookup"><span data-stu-id="88c25-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="88c25-184">不是向用户显示以 html 格式的数据视图。</span><span class="sxs-lookup"><span data-stu-id="88c25-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="88c25-185">[![欢迎-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="88c25-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="88c25-186">嗯，这是一种类型的"M"的模型，但不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="88c25-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="88c25-187">让我们我们已了解和创建数据库的影片。</span><span class="sxs-lookup"><span data-stu-id="88c25-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="88c25-188">[上一页](getting-started-with-mvc-part2.md)
> [下一页](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="88c25-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
