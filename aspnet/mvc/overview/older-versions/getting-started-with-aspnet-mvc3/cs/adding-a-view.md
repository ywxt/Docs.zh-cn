---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 添加的视图 (C#) |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 50ce4a2024ffd9e2bbb5526717052d486689ff38
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "30873165"
---
<a name="adding-a-view-c"></a><span data-ttu-id="932d9-103">添加的视图 (C#)</span><span class="sxs-lookup"><span data-stu-id="932d9-103">Adding a View (C#)</span></span>
====================
<span data-ttu-id="932d9-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="932d9-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="932d9-105">本教程的更新的版本可[此处](../../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="932d9-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="932d9-106">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="932d9-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="932d9-107">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="932d9-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="932d9-108">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="932d9-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="932d9-109">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="932d9-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="932d9-110">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="932d9-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="932d9-111">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="932d9-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="932d9-112">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="932d9-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="932d9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="932d9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="932d9-114">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="932d9-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="932d9-115">使用 C# 源代码的 Visual Web Developer 项目是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="932d9-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="932d9-116">[下载的 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="932d9-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="932d9-117">如果你愿意 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="932d9-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="932d9-118">在本节中你要修改`HelloWorldController`类以使用模板文件复制到完全封装生成 HTML 响应客户端的过程的视图。</span><span class="sxs-lookup"><span data-stu-id="932d9-118">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="932d9-119">你将创建使用新的视图模板文件[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)引入了 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="932d9-119">You'll create a view template file using the new [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="932d9-120">基于 razor 视图模板具有 *.cshtml*文件扩展名，并且提供一种简洁的方式来创建 HTML 输出使用 C#。</span><span class="sxs-lookup"><span data-stu-id="932d9-120">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="932d9-121">Razor 降至最低数量的字符时编写视图模板，所需的击键，并使快，流体编码工作流。</span><span class="sxs-lookup"><span data-stu-id="932d9-121">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="932d9-122">使用具有的视图模板启动`Index`中的方法`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="932d9-122">Start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="932d9-123">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="932d9-123">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="932d9-124">更改`Index`方法以返回`View`对象，如在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="932d9-124">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="932d9-125">此代码使用视图模板以生成对浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="932d9-125">This code uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="932d9-126">在项目中，添加可与一个视图模板`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="932d9-126">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="932d9-127">若要执行此操作，右键单击内`Index`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="932d9-127">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="932d9-128">**添加视图**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="932d9-128">The **Add View** dialog box appears.</span></span> <span data-ttu-id="932d9-129">保留默认值的方式变，并单击**添加**按钮：</span><span class="sxs-lookup"><span data-stu-id="932d9-129">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="932d9-130">*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*创建文件。</span><span class="sxs-lookup"><span data-stu-id="932d9-130">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="932d9-131">你可以看到在**解决方案资源管理器**:</span><span class="sxs-lookup"><span data-stu-id="932d9-131">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="932d9-132">如下所示*Index.cshtml*已创建的文件：</span><span class="sxs-lookup"><span data-stu-id="932d9-132">The following shows the *Index.cshtml* file that was created:</span></span>

<span data-ttu-id="932d9-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="932d9-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span></span>

<span data-ttu-id="932d9-134">添加一些 HTML 下的`<h2>`标记。</span><span class="sxs-lookup"><span data-stu-id="932d9-134">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="932d9-135">已修改*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="932d9-135">The modified *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

<span data-ttu-id="932d9-136">运行应用程序，并浏览到`HelloWorld`控制器 (`http://localhost:xxxx/HelloWorld`)。</span><span class="sxs-lookup"><span data-stu-id="932d9-136">Run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="932d9-137">`Index`方法在你的控制器中未做大量的工作; 它只需运行该语句`return View()`，其指定该方法应使用的视图模板文件来呈现到浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="932d9-137">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="932d9-138">因为你未显式指定要使用的视图模板文件的名称，ASP.NET MVC 将默认为使用*Index.cshtml*视图文件中的*\Views\HelloWorld*文件夹。</span><span class="sxs-lookup"><span data-stu-id="932d9-138">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="932d9-139">下图显示了硬编码在视图中的字符串。</span><span class="sxs-lookup"><span data-stu-id="932d9-139">The image below shows the string hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="932d9-140">看起来一切都非常好。</span><span class="sxs-lookup"><span data-stu-id="932d9-140">Looks pretty good.</span></span> <span data-ttu-id="932d9-141">但是，请注意，浏览器的标题栏将显示为"Index"，并在页上的大标题显示"My MVC Application。"</span><span class="sxs-lookup"><span data-stu-id="932d9-141">However, notice that the browser's title bar says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="932d9-142">让我们更改那些。</span><span class="sxs-lookup"><span data-stu-id="932d9-142">Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="932d9-143">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="932d9-143">Changing Views and Layout Pages</span></span>

<span data-ttu-id="932d9-144">首先，你想要更改页面顶部的"My MVC Application"标题。</span><span class="sxs-lookup"><span data-stu-id="932d9-144">First, you want to change the "My MVC Application" title at the top of the page.</span></span> <span data-ttu-id="932d9-145">该文本是通用的每一页。</span><span class="sxs-lookup"><span data-stu-id="932d9-145">That text is common to every page.</span></span> <span data-ttu-id="932d9-146">它实际上被实现只能在一个位置，在项目中，即使在应用程序中的每一页上显示。</span><span class="sxs-lookup"><span data-stu-id="932d9-146">It actually is implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="932d9-147">转到 */视图/共享*文件夹中的**解决方案资源管理器**并打开 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="932d9-147">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="932d9-148">此文件称为*布局页*且共享的"shell"其他所有页使用。</span><span class="sxs-lookup"><span data-stu-id="932d9-148">This file is called a *layout page* and it's the shared "shell" that all other pages use.</span></span>

<span data-ttu-id="932d9-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="932d9-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="932d9-150">布局模板，可以在一个位置中指定你的站点的 HTML 容器布局，然后将它应用跨站点中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="932d9-150">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="932d9-151">请注意`@RenderBody()`文件底部附近的行。</span><span class="sxs-lookup"><span data-stu-id="932d9-151">Note the `@RenderBody()` line near the bottom of the file.</span></span> <span data-ttu-id="932d9-152">`RenderBody` 是，你创建的所有特定于视图的页面都显示，"包装"在布局页中的占位符。</span><span class="sxs-lookup"><span data-stu-id="932d9-152">`RenderBody` is a placeholder where all the view-specific pages you create show up, "wrapped" in the layout page.</span></span> <span data-ttu-id="932d9-153">更改布局模板从"My MVC Application"到"MVC 影片应用程序"中的标题标头。</span><span class="sxs-lookup"><span data-stu-id="932d9-153">Change the title heading in the layout template from "My MVC Application" to "MVC Movie App".</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

<span data-ttu-id="932d9-154">运行应用程序，并请注意它现在显示"MVC 影片应用程序"。</span><span class="sxs-lookup"><span data-stu-id="932d9-154">Run the application and notice that it now says "MVC Movie App".</span></span> <span data-ttu-id="932d9-155">单击**有关**链接，你会看到如何该页面显示"MVC 影片应用程序，"过。</span><span class="sxs-lookup"><span data-stu-id="932d9-155">Click the **About** link, and you see how that page shows "MVC Movie App", too.</span></span> <span data-ttu-id="932d9-156">我们无法一次中的布局模板进行的更改，并具有站点上的所有页都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="932d9-156">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="932d9-157">完整 *\_Layout.cshtml*文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="932d9-157">The complete *\_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="932d9-158">现在，让我们更改索引页 （视图） 的标题。</span><span class="sxs-lookup"><span data-stu-id="932d9-158">Now, let's change the title of the Index page (view).</span></span>

<span data-ttu-id="932d9-159">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="932d9-159">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="932d9-160">有两个位置进行更改： 首先，文本显示的标题中的浏览器中，然后在辅助标头 (`<h2>`元素)。</span><span class="sxs-lookup"><span data-stu-id="932d9-160">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="932d9-161">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="932d9-161">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="932d9-162">指示要显示，集上面的代码的 HTML 标题`Title`属性`ViewBag`对象 (即在*Index.cshtml*视图模板)。</span><span class="sxs-lookup"><span data-stu-id="932d9-162">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="932d9-163">如果你查看返回的布局模板的源代码，你会注意到，该模板使用中的此值`<title>`作为的一部分的元素`<head>`HTML 的一部分。</span><span class="sxs-lookup"><span data-stu-id="932d9-163">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML.</span></span> <span data-ttu-id="932d9-164">使用此方法，可以查看模板和布局文件之间轻松地传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="932d9-164">Using this approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="932d9-165">运行应用程序，并浏览到`http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="932d9-165">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="932d9-166">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="932d9-166">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="932d9-167">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="932d9-167">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="932d9-168">在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）</span><span class="sxs-lookup"><span data-stu-id="932d9-168">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="932d9-169">另请注意如何在内容*Index.cshtml*视图模板与合并 *\_Layout.cshtml*视图模板和单个 HTML 响应发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="932d9-169">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="932d9-170">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="932d9-170">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="932d9-171">但我们这一点点“数据”（在此示例中为“Hello from our View Template!”</span><span class="sxs-lookup"><span data-stu-id="932d9-171">Our little bit of "data" (in this case the "Hello from our View Template!"</span></span> <span data-ttu-id="932d9-172">消息）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="932d9-172">message) is hard-coded, though.</span></span> <span data-ttu-id="932d9-173">MVC 应用程序有一个“V”（视图），而你已有一个“C”（控制器），但还没有“M”（模型）。</span><span class="sxs-lookup"><span data-stu-id="932d9-173">The MVC application has a "V" (view) and you've got a "C" (controller), but no "M" (model) yet.</span></span> <span data-ttu-id="932d9-174">很快，我们将演练如何创建数据库并从它检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="932d9-174">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="932d9-175">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="932d9-175">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="932d9-176">我们转到数据库，并讨论模型之前，不过，让我们先介绍一下将从控制器的信息传递到一个视图。</span><span class="sxs-lookup"><span data-stu-id="932d9-176">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="932d9-177">在与传入 URL 请求的响应中将会调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="932d9-177">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="932d9-178">控制器类是响应的你在其中编写代码来处理传入的参数、 从数据库检索数据并最终决定哪种类型将发送回浏览器。</span><span class="sxs-lookup"><span data-stu-id="932d9-178">A controller class is where you write the code that handles the incoming parameters, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="932d9-179">查看模板随后可从控制器以生成并设置格式对浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="932d9-179">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="932d9-180">控制器负责提供任何数据或对象所需顺序查看模板，以呈现到浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="932d9-180">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="932d9-181">查看模板应永远不会执行业务逻辑或直接与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="932d9-181">A view template should never perform business logic or interact with a database directly.</span></span> <span data-ttu-id="932d9-182">相反，它应只使用由控制器提供给它的数据。</span><span class="sxs-lookup"><span data-stu-id="932d9-182">Instead, it should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="932d9-183">维护此"分离问题"有助于使代码保持干净且更易于维护。</span><span class="sxs-lookup"><span data-stu-id="932d9-183">Maintaining this "separation of concerns" helps keep your code clean and more maintainable.</span></span>

<span data-ttu-id="932d9-184">目前，`Welcome`中的操作方法`HelloWorldController`类采用`name`和`numTimes`参数，然后输出直接向浏览器的值。</span><span class="sxs-lookup"><span data-stu-id="932d9-184">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="932d9-185">而不是有呈现为一个字符串，此响应的控制器，让我们更改控制器以改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="932d9-185">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="932d9-186">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="932d9-186">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="932d9-187">你可以执行此操作通过让将动态视图模板需要的数据控制器`ViewBag`视图模板然后可以访问的对象。</span><span class="sxs-lookup"><span data-stu-id="932d9-187">You can do this by having the controller put the dynamic data that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="932d9-188">返回到*HelloWorldController.cs*文件并将更改`Welcome`方法将添加`Message`和`NumTimes`值赋给`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="932d9-188">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="932d9-189">`ViewBag` 是动态对象，这意味着你可以放置希望中包括的任何内容`ViewBag`对象具有未定义的属性，直到你输入其内部的一些内容。</span><span class="sxs-lookup"><span data-stu-id="932d9-189">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="932d9-190">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="932d9-190">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

<span data-ttu-id="932d9-191">现在`ViewBag`对象包含将自动传递到视图的数据。</span><span class="sxs-lookup"><span data-stu-id="932d9-191">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="932d9-192">接下来，你需要一个欢迎视图模板 ！</span><span class="sxs-lookup"><span data-stu-id="932d9-192">Next, you need a Welcome view template!</span></span> <span data-ttu-id="932d9-193">在**调试**菜单上，选择**生成 MvcMovie**若要确保编译项目。</span><span class="sxs-lookup"><span data-stu-id="932d9-193">In the **Debug** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="932d9-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="932d9-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="932d9-195">然后右键单击内`Welcome`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="932d9-195">Then right-click inside the `Welcome` method and click **Add View**.</span></span> <span data-ttu-id="932d9-196">下面是什么**添加视图**对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="932d9-196">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image13.png)

<span data-ttu-id="932d9-197">单击**添加**，然后添加以下代码在`<h2>`在新的元素*Welcome.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="932d9-197">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="932d9-198">你将创建让用户说出它应多次显示"Hello"的循环。</span><span class="sxs-lookup"><span data-stu-id="932d9-198">You'll create a loop that says "Hello" as many times as the user says it should.</span></span> <span data-ttu-id="932d9-199">完整*Welcome.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="932d9-199">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

<span data-ttu-id="932d9-200">运行应用程序，并浏览到以下 URL:</span><span class="sxs-lookup"><span data-stu-id="932d9-200">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="932d9-201">现在数据是来自 URL，并自动传递到的控制器。</span><span class="sxs-lookup"><span data-stu-id="932d9-201">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="932d9-202">控制器包数据插入`ViewBag`对象并将该对象传递到视图。</span><span class="sxs-lookup"><span data-stu-id="932d9-202">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="932d9-203">视图然后会以 html 格式的数据向用户显示。</span><span class="sxs-lookup"><span data-stu-id="932d9-203">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image14.png)

<span data-ttu-id="932d9-204">当然，这是模型的一种“M”类型，而不是数据库类。</span><span class="sxs-lookup"><span data-stu-id="932d9-204">Well, that was a kind of an "M" for model, but not the database kind.</span></span> <span data-ttu-id="932d9-205">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="932d9-205">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="932d9-206">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="932d9-206">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
