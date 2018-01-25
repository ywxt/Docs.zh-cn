---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: "添加视图 |Microsoft 文档"
author: Rick-Anderson
description: "注意： 本教程的更新的版本此处提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全，请按照和演示要简单得多..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 60374ddc6754f7e312ad08b420268308a9935bb4
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-view"></a><span data-ttu-id="33f5b-104">添加视图</span><span class="sxs-lookup"><span data-stu-id="33f5b-104">Adding a View</span></span>
====================
<span data-ttu-id="33f5b-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="33f5b-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="33f5b-106">本教程的更新的版本可[此处](../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="33f5b-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="33f5b-107">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="33f5b-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="33f5b-108">在本节中你要修改`HelloWorldController`类以使用模板文件复制到完全封装生成 HTML 响应客户端的过程的视图。</span><span class="sxs-lookup"><span data-stu-id="33f5b-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="33f5b-109">你将创建视图模板文件使用[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)引入了 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="33f5b-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="33f5b-110">基于 razor 视图模板具有*.cshtml*文件扩展名，并且提供一种简洁的方式来创建 HTML 输出使用 C#。</span><span class="sxs-lookup"><span data-stu-id="33f5b-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="33f5b-111">Razor 降至最低数量的字符时编写视图模板，所需的击键，并使快，流体编码工作流。</span><span class="sxs-lookup"><span data-stu-id="33f5b-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="33f5b-112">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="33f5b-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="33f5b-113">更改`Index`方法以返回`View`对象，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="33f5b-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="33f5b-114">`Index`上面方法使用视图模板来生成对浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="33f5b-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="33f5b-115">控制器方法 (也称为[操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained))，如`Index`上面，方法通常返回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (或从派生的类[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx))，不基元类型喜欢字符串。</span><span class="sxs-lookup"><span data-stu-id="33f5b-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="33f5b-116">在项目中，添加可与一个视图模板`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="33f5b-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="33f5b-117">若要执行此操作，右键单击内`Index`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="33f5b-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="33f5b-118">**添加视图**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="33f5b-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="33f5b-119">保留默认值的方式变，并单击**添加**按钮：</span><span class="sxs-lookup"><span data-stu-id="33f5b-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="33f5b-120">*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*创建文件。</span><span class="sxs-lookup"><span data-stu-id="33f5b-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="33f5b-121">你可以看到在**解决方案资源管理器**:</span><span class="sxs-lookup"><span data-stu-id="33f5b-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="33f5b-122">如下所示*Index.cshtml*已创建的文件：</span><span class="sxs-lookup"><span data-stu-id="33f5b-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="33f5b-124">添加下的以下 HTML`<h2>`标记。</span><span class="sxs-lookup"><span data-stu-id="33f5b-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="33f5b-125">完整*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="33f5b-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="33f5b-126">如果使用的 Visual Studio 2012 中，在解决方案资源管理器中，右键单击*Index.cshtml*文件，然后选择**在 Page Inspector 中的查看**。</span><span class="sxs-lookup"><span data-stu-id="33f5b-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="33f5b-128">[Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md)提供了有关此新工具的详细信息。</span><span class="sxs-lookup"><span data-stu-id="33f5b-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="33f5b-129">或者，运行该应用程序，并浏览到`HelloWorld`控制器 (`http://localhost:xxxx/HelloWorld`)。</span><span class="sxs-lookup"><span data-stu-id="33f5b-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="33f5b-130">`Index`方法在你的控制器中未做大量的工作; 它只需运行该语句`return View()`，其指定该方法应使用的视图模板文件来呈现到浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="33f5b-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="33f5b-131">因为你未显式指定要使用的视图模板文件的名称，ASP.NET MVC 将默认为使用*Index.cshtml*视图文件中的*\Views\HelloWorld*文件夹。</span><span class="sxs-lookup"><span data-stu-id="33f5b-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="33f5b-132">下图显示字符串&quot;从我们的视图模板 Hello ！&quot;硬编码在视图中。</span><span class="sxs-lookup"><span data-stu-id="33f5b-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="33f5b-133">看起来一切都非常好。</span><span class="sxs-lookup"><span data-stu-id="33f5b-133">Looks pretty good.</span></span> <span data-ttu-id="33f5b-134">但是，请注意，浏览器的标题栏显示&quot;索引我 ASP.NET A&quot; ，并在页面顶部的大链接显示&quot;此处你的徽标。&quot;下面&quot;你徽标此处。&quot;链接大约的注册和日志中的链接，或其下链接到主页，并向页。</span><span class="sxs-lookup"><span data-stu-id="33f5b-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="33f5b-135">让我们更改其中的某些类。</span><span class="sxs-lookup"><span data-stu-id="33f5b-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="33f5b-136">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="33f5b-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="33f5b-137">首先，你想要更改&quot;你徽标此处。&quot;页顶部的标题。</span><span class="sxs-lookup"><span data-stu-id="33f5b-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="33f5b-138">该文本是通用的每一页。</span><span class="sxs-lookup"><span data-stu-id="33f5b-138">That text is common to every page.</span></span> <span data-ttu-id="33f5b-139">它是实际实现只能在一个位置，在项目中，即使在应用程序中的每一页上显示。</span><span class="sxs-lookup"><span data-stu-id="33f5b-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="33f5b-140">转到*/视图/共享*文件夹中的**解决方案资源管理器**并打开 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="33f5b-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="33f5b-141">此文件称为*布局页*共享它并且&quot;shell&quot;其他所有页使用。</span><span class="sxs-lookup"><span data-stu-id="33f5b-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="33f5b-143">布局模板，可以在一个位置中指定你的站点的 HTML 容器布局，然后将它应用跨站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="33f5b-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="33f5b-144">查找 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="33f5b-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="33f5b-145">`RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="33f5b-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="33f5b-146">例如，如果选择关于链接， *Views\Home\About.cshtml*内呈现视图`RenderBody`方法。</span><span class="sxs-lookup"><span data-stu-id="33f5b-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="33f5b-147">更改从布局模板中的站点-标题标头&quot;此处你的徽标&quot;到&quot;MVC 影片&quot;。</span><span class="sxs-lookup"><span data-stu-id="33f5b-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="33f5b-148">标题元素的内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="33f5b-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="33f5b-149">运行应用程序，并请注意，它现在显示&quot;MVC 影片&quot;。</span><span class="sxs-lookup"><span data-stu-id="33f5b-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="33f5b-150">单击**有关**链接，你会看到该页面将显示如何&quot;MVC 影片&quot;也。</span><span class="sxs-lookup"><span data-stu-id="33f5b-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="33f5b-151">我们无法一次中的布局模板进行的更改，并具有站点上的所有页都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="33f5b-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="33f5b-152">现在，让我们更改索引视图的标题。</span><span class="sxs-lookup"><span data-stu-id="33f5b-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="33f5b-153">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="33f5b-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="33f5b-154">有两个位置进行更改： 首先，文本显示的标题中的浏览器中，然后在辅助标头 (`<h2>`元素)。</span><span class="sxs-lookup"><span data-stu-id="33f5b-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="33f5b-155">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="33f5b-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="33f5b-156">指示要显示，集上面的代码的 HTML 标题`Title`属性`ViewBag`对象 (即在*Index.cshtml*视图模板)。</span><span class="sxs-lookup"><span data-stu-id="33f5b-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="33f5b-157">如果你查看返回的布局模板的源代码，你会注意到，该模板使用中的此值`<title>`作为的一部分的元素`<head>`一部分我们之前修改的 HTML。</span><span class="sxs-lookup"><span data-stu-id="33f5b-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="33f5b-158">使用此`ViewBag`方法中，你可以轻松地将传递其他参数视图模板与布局文件之间。</span><span class="sxs-lookup"><span data-stu-id="33f5b-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="33f5b-159">运行应用程序，并浏览到`http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="33f5b-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="33f5b-160">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="33f5b-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="33f5b-161">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="33f5b-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="33f5b-162">在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）使用创建浏览器标题`ViewBag.Title`我们在中设置*Index.cshtml*查看模板和其他&quot;的电影应用&quot;在布局文件中添加。</span><span class="sxs-lookup"><span data-stu-id="33f5b-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="33f5b-163">另请注意如何在内容*Index.cshtml*视图模板与合并 *\_Layout.cshtml*视图模板和单个 HTML 响应发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="33f5b-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="33f5b-164">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="33f5b-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="33f5b-165">我们一小段&quot;数据&quot;(在这种情况下&quot;从我们的视图模板 Hello ！&quot;消息) 但是硬编码。</span><span class="sxs-lookup"><span data-stu-id="33f5b-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="33f5b-166">MVC 应用程序具有&quot;V&quot; （视图） 并已获得了&quot;C&quot; （控制器），但不&quot;M&quot; （模型），尚未。</span><span class="sxs-lookup"><span data-stu-id="33f5b-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="33f5b-167">很快，我们将演练如何创建数据库并从它检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="33f5b-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="33f5b-168">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="33f5b-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="33f5b-169">我们转到数据库，并讨论模型之前，不过，让我们先介绍一下将从控制器的信息传递到一个视图。</span><span class="sxs-lookup"><span data-stu-id="33f5b-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="33f5b-170">在与传入 URL 请求的响应中将会调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="33f5b-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="33f5b-171">控制器类是响应的在其中编写代码来处理传入的浏览器请求，从数据库检索数据并最终决定哪种类型将发送回浏览器。</span><span class="sxs-lookup"><span data-stu-id="33f5b-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="33f5b-172">查看模板随后可从控制器以生成并设置格式对浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="33f5b-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="33f5b-173">控制器负责提供任何数据或对象所需顺序查看模板，以呈现到浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="33f5b-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="33f5b-174">一种最佳做法：**视图模板应永远不会执行业务逻辑或直接与数据库交互**。</span><span class="sxs-lookup"><span data-stu-id="33f5b-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="33f5b-175">相反，一个视图模板应只使用由控制器提供给它的数据。</span><span class="sxs-lookup"><span data-stu-id="33f5b-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="33f5b-176">维护这&quot;关注点分离&quot;干净、 可测试并且更易于维护，有助于保持你的代码。</span><span class="sxs-lookup"><span data-stu-id="33f5b-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="33f5b-177">目前，`Welcome`中的操作方法`HelloWorldController`类采用`name`和`numTimes`参数，然后输出直接向浏览器的值。</span><span class="sxs-lookup"><span data-stu-id="33f5b-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="33f5b-178">而不是有呈现为一个字符串，此响应的控制器，让我们更改控制器以改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="33f5b-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="33f5b-179">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="33f5b-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="33f5b-180">你可以执行此操作通过让放在需要查看模板的动态数据 （参数） 的控制器`ViewBag`视图模板然后可以访问的对象。</span><span class="sxs-lookup"><span data-stu-id="33f5b-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="33f5b-181">返回到*HelloWorldController.cs*文件并将更改`Welcome`方法将添加`Message`和`NumTimes`值赋给`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="33f5b-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="33f5b-182">`ViewBag`是动态对象，这意味着你可以放置希望中包括的任何内容`ViewBag`对象具有未定义的属性，直到你输入其内部的一些内容。</span><span class="sxs-lookup"><span data-stu-id="33f5b-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="33f5b-183">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将映射的命名的参数 (`name`和`numTimes`) 从到你的方法中的参数的地址栏中的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="33f5b-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="33f5b-184">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="33f5b-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="33f5b-185">现在`ViewBag`对象包含将自动传递到视图的数据。</span><span class="sxs-lookup"><span data-stu-id="33f5b-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="33f5b-186">接下来，你需要一个欢迎视图模板 ！</span><span class="sxs-lookup"><span data-stu-id="33f5b-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="33f5b-187">在**生成**菜单上，选择**生成 MvcMovie**若要确保编译项目。</span><span class="sxs-lookup"><span data-stu-id="33f5b-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="33f5b-188">然后右键单击内`Welcome`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="33f5b-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="33f5b-189">下面是什么**添加视图**对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="33f5b-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="33f5b-190">单击**添加**，然后添加以下代码在`<h2>`在新的元素*Welcome.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="33f5b-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="33f5b-191">你将创建循环表明&quot;Hello&quot;让用户说出它应多次。</span><span class="sxs-lookup"><span data-stu-id="33f5b-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="33f5b-192">完整*Welcome.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="33f5b-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="33f5b-193">运行应用程序，并浏览到以下 URL:</span><span class="sxs-lookup"><span data-stu-id="33f5b-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="33f5b-194">现在是从 URL 中获取数据并将其传递给控制器使用[模型联编程序](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)。</span><span class="sxs-lookup"><span data-stu-id="33f5b-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="33f5b-195">控制器包数据插入`ViewBag`对象并将该对象传递到视图。</span><span class="sxs-lookup"><span data-stu-id="33f5b-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="33f5b-196">视图然后会以 html 格式的数据向用户显示。</span><span class="sxs-lookup"><span data-stu-id="33f5b-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="33f5b-197">在上面的示例中，我们使用`ViewBag`要将数据从控制器传递到视图对象。</span><span class="sxs-lookup"><span data-stu-id="33f5b-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="33f5b-198">后者在本教程中，我们将视图模型以将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="33f5b-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="33f5b-199">视图模型种方法可以将数据传递是好得相比于视图包方法。</span><span class="sxs-lookup"><span data-stu-id="33f5b-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="33f5b-200">请参阅博客文章[动态 V 强类型化的视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="33f5b-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="33f5b-201">当然，这是一种类型的&quot;M&quot;模型，但不数据库类型。</span><span class="sxs-lookup"><span data-stu-id="33f5b-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="33f5b-202">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="33f5b-202">Let's take what we've learned and create a database of movies.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="33f5b-203">[上一页](adding-a-controller.md)
[下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="33f5b-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
