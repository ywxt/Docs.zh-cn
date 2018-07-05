---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 添加视图 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: e9496f801024bd2d4a135eefbb79b162017197b7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366211"
---
<a name="adding-a-view-c"></a><span data-ttu-id="f52b7-103">添加视图 (C#)</span><span class="sxs-lookup"><span data-stu-id="f52b7-103">Adding a View (C#)</span></span>
====================
<span data-ttu-id="f52b7-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f52b7-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="f52b7-105">本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="f52b7-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="f52b7-106">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="f52b7-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="f52b7-107">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="f52b7-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="f52b7-108">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="f52b7-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="f52b7-109">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="f52b7-110">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="f52b7-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="f52b7-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="f52b7-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="f52b7-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="f52b7-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="f52b7-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="f52b7-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="f52b7-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="f52b7-115">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="f52b7-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="f52b7-116">[下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="f52b7-117">如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="f52b7-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="f52b7-118">在本部分中想要修改`HelloWorldController`类，以使用视图模板文件来顺利封装生成 HTML 响应向客户端的过程。</span><span class="sxs-lookup"><span data-stu-id="f52b7-118">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="f52b7-119">将创建使用新的视图模板文件[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)使用 ASP.NET MVC 3 引入了。</span><span class="sxs-lookup"><span data-stu-id="f52b7-119">You'll create a view template file using the new [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="f52b7-120">基于 razor 的视图模板具有 *.cshtml*文件扩展名，并提供创建 HTML 输出使用 C# 的简洁方法。</span><span class="sxs-lookup"><span data-stu-id="f52b7-120">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="f52b7-121">Razor 字符和击键时编写视图模板，所需的数量降至最低，并启用编码工作流即快速、 流畅。</span><span class="sxs-lookup"><span data-stu-id="f52b7-121">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="f52b7-122">使用视图模板与启动`Index`中的方法`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="f52b7-122">Start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="f52b7-123">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="f52b7-123">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="f52b7-124">更改`Index`方法以返回`View`对象，如在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f52b7-124">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="f52b7-125">此代码使用视图模板来生成 HTML 响应到浏览器。</span><span class="sxs-lookup"><span data-stu-id="f52b7-125">This code uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="f52b7-126">在项目中，添加可用于查看模板`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="f52b7-126">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="f52b7-127">若要执行此操作，右键单击内`Index`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="f52b7-127">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="f52b7-128">**添加视图**对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="f52b7-128">The **Add View** dialog box appears.</span></span> <span data-ttu-id="f52b7-129">保留默认值的方式变，并单击**添加**按钮：</span><span class="sxs-lookup"><span data-stu-id="f52b7-129">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="f52b7-130">*MvcMovie\Views\HelloWorld*文件夹并*MvcMovie\Views\HelloWorld\Index.cshtml*创建文件。</span><span class="sxs-lookup"><span data-stu-id="f52b7-130">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="f52b7-131">你可以看到它们在**解决方案资源管理器**:</span><span class="sxs-lookup"><span data-stu-id="f52b7-131">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="f52b7-132">如下所示*Index.cshtml*已创建的文件：</span><span class="sxs-lookup"><span data-stu-id="f52b7-132">The following shows the *Index.cshtml* file that was created:</span></span>

<span data-ttu-id="f52b7-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f52b7-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span></span>

<span data-ttu-id="f52b7-134">添加一些 HTML 下的`<h2>`标记。</span><span class="sxs-lookup"><span data-stu-id="f52b7-134">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="f52b7-135">已修改*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="f52b7-135">The modified *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

<span data-ttu-id="f52b7-136">运行应用程序，并浏览到`HelloWorld`控制器 (`http://localhost:xxxx/HelloWorld`)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-136">Run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="f52b7-137">`Index`控制器中的方法未做大量的工作; 它只需运行该语句`return View()`，其指定该方法应使用视图模板文件来呈现到浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="f52b7-137">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="f52b7-138">由于未显式指定要使用的视图模板文件的名称，ASP.NET MVC 的默认设置为使用*Index.cshtml*视图中的文件*\Views\HelloWorld*文件夹。</span><span class="sxs-lookup"><span data-stu-id="f52b7-138">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="f52b7-139">下图显示了字符串硬编码的视图中。</span><span class="sxs-lookup"><span data-stu-id="f52b7-139">The image below shows the string hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="f52b7-140">看起来相当棒。</span><span class="sxs-lookup"><span data-stu-id="f52b7-140">Looks pretty good.</span></span> <span data-ttu-id="f52b7-141">但是，请注意，浏览器的标题栏将显示"Index"，并在页上的大标题显示"我 MVC 应用程序。"</span><span class="sxs-lookup"><span data-stu-id="f52b7-141">However, notice that the browser's title bar says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="f52b7-142">让我们将这些更改。</span><span class="sxs-lookup"><span data-stu-id="f52b7-142">Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="f52b7-143">更改视图和布局页面</span><span class="sxs-lookup"><span data-stu-id="f52b7-143">Changing Views and Layout Pages</span></span>

<span data-ttu-id="f52b7-144">首先，你想要更改页面顶部的"My MVC Application"标题。</span><span class="sxs-lookup"><span data-stu-id="f52b7-144">First, you want to change the "My MVC Application" title at the top of the page.</span></span> <span data-ttu-id="f52b7-145">该文本是通用的每一页。</span><span class="sxs-lookup"><span data-stu-id="f52b7-145">That text is common to every page.</span></span> <span data-ttu-id="f52b7-146">它实际上被实现只能在一个位置，在项目中，即使它在应用程序中每一页显示。</span><span class="sxs-lookup"><span data-stu-id="f52b7-146">It actually is implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="f52b7-147">转到 */视图/共享*中的文件夹**解决方案资源管理器**，然后打开 *\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="f52b7-147">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="f52b7-148">此文件称为*布局页*是共享的"shell"，所有其他页面使用。</span><span class="sxs-lookup"><span data-stu-id="f52b7-148">This file is called a *layout page* and it's the shared "shell" that all other pages use.</span></span>

<span data-ttu-id="f52b7-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f52b7-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="f52b7-150">布局模板可用于在一个位置指定您的网站的 HTML 容器布局，然后将其应用于你的站点中多个页面。</span><span class="sxs-lookup"><span data-stu-id="f52b7-150">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="f52b7-151">请注意`@RenderBody()`文件底部附近的行。</span><span class="sxs-lookup"><span data-stu-id="f52b7-151">Note the `@RenderBody()` line near the bottom of the file.</span></span> <span data-ttu-id="f52b7-152">`RenderBody` 是，您创建的所有特定于视图的页面显示，"包装"在布局页面中的占位符。</span><span class="sxs-lookup"><span data-stu-id="f52b7-152">`RenderBody` is a placeholder where all the view-specific pages you create show up, "wrapped" in the layout page.</span></span> <span data-ttu-id="f52b7-153">更改布局模板从"My MVC Application"到"MVC 电影应用"中的标题标头。</span><span class="sxs-lookup"><span data-stu-id="f52b7-153">Change the title heading in the layout template from "My MVC Application" to "MVC Movie App".</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

<span data-ttu-id="f52b7-154">运行应用程序，请注意它现在显示"MVC 电影应用"。</span><span class="sxs-lookup"><span data-stu-id="f52b7-154">Run the application and notice that it now says "MVC Movie App".</span></span> <span data-ttu-id="f52b7-155">单击**有关**链接，并且您看到如何该页面显示"MVC 电影应用"，过。</span><span class="sxs-lookup"><span data-stu-id="f52b7-155">Click the **About** link, and you see how that page shows "MVC Movie App", too.</span></span> <span data-ttu-id="f52b7-156">我们能够在布局模板中一次进行更改，并具有在站点上的所有页面都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="f52b7-156">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="f52b7-157">完整 *\_Layout.cshtml*文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="f52b7-157">The complete *\_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="f52b7-158">现在，让我们来更改索引页面 （视图） 的标题。</span><span class="sxs-lookup"><span data-stu-id="f52b7-158">Now, let's change the title of the Index page (view).</span></span>

<span data-ttu-id="f52b7-159">打开*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="f52b7-159">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="f52b7-160">有两个位置进行更改： 首先，文本显示的标题中的浏览器中，然后在辅助标头 (`<h2>`元素)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-160">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="f52b7-161">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="f52b7-161">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="f52b7-162">若要指示显示集上面的代码的 HTML 标题`Title`的属性`ViewBag`对象 (后者位于*Index.cshtml*视图模板)。</span><span class="sxs-lookup"><span data-stu-id="f52b7-162">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="f52b7-163">如果回顾一下布局模板的源代码，您会注意到，该模板使用此值在`<title>`元素作为的一部分`<head>`HTML 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f52b7-163">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML.</span></span> <span data-ttu-id="f52b7-164">使用此方法，可以在视图模板和布局文件之间轻松传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="f52b7-164">Using this approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="f52b7-165">运行应用程序，并浏览到`http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="f52b7-165">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="f52b7-166">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="f52b7-166">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="f52b7-167">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="f52b7-167">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="f52b7-168">在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）</span><span class="sxs-lookup"><span data-stu-id="f52b7-168">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="f52b7-169">此外会注意到了中的内容*Index.cshtml*视图的模板已与合并 *\_Layout.cshtml*视图模板和单个 HTML 响应已发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="f52b7-169">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="f52b7-170">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="f52b7-170">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="f52b7-171">但我们这一点点“数据”（在此示例中为“Hello from our View Template!”</span><span class="sxs-lookup"><span data-stu-id="f52b7-171">Our little bit of "data" (in this case the "Hello from our View Template!"</span></span> <span data-ttu-id="f52b7-172">消息）是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="f52b7-172">message) is hard-coded, though.</span></span> <span data-ttu-id="f52b7-173">MVC 应用程序有一个“V”（视图），而你已有一个“C”（控制器），但还没有“M”（模型）。</span><span class="sxs-lookup"><span data-stu-id="f52b7-173">The MVC application has a "V" (view) and you've got a "C" (controller), but no "M" (model) yet.</span></span> <span data-ttu-id="f52b7-174">稍后，我们将演练如何创建数据库并从它检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="f52b7-174">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="f52b7-175">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="f52b7-175">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="f52b7-176">我们转到数据库，并讨论模型之前，不过，我们首先讨论一下将信息从控制器传递给视图。</span><span class="sxs-lookup"><span data-stu-id="f52b7-176">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="f52b7-177">控制器类调用以响应传入的 URL 请求。</span><span class="sxs-lookup"><span data-stu-id="f52b7-177">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="f52b7-178">控制器类是响应的编写代码，用于处理传入的参数，从数据库检索数据并最终决定将哪些类型发送回浏览器的位置。</span><span class="sxs-lookup"><span data-stu-id="f52b7-178">A controller class is where you write the code that handles the incoming parameters, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="f52b7-179">查看模板然后可从控制器来生成并格式化对浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="f52b7-179">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="f52b7-180">控制器负责提供使视图模板能够呈现到浏览器的响应所需的任何数据或对象。</span><span class="sxs-lookup"><span data-stu-id="f52b7-180">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="f52b7-181">视图模板应永远不会执行业务逻辑，或直接与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="f52b7-181">A view template should never perform business logic or interact with a database directly.</span></span> <span data-ttu-id="f52b7-182">相反，它应使用仅由控制器提供给它的数据。</span><span class="sxs-lookup"><span data-stu-id="f52b7-182">Instead, it should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="f52b7-183">维护此"关注点分离"有助于保持代码干净且更易于维护。</span><span class="sxs-lookup"><span data-stu-id="f52b7-183">Maintaining this "separation of concerns" helps keep your code clean and more maintainable.</span></span>

<span data-ttu-id="f52b7-184">目前，`Welcome`操作方法中的`HelloWorldController`类采用`name`和一个`numTimes`参数，然后输出直接向浏览器的值。</span><span class="sxs-lookup"><span data-stu-id="f52b7-184">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="f52b7-185">而不是使控制器将作为一个字符串，此响应呈现，让我们更改控制器以改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="f52b7-185">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="f52b7-186">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="f52b7-186">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="f52b7-187">可以为此，需要查看模板的动态数据放置在控制器`ViewBag`视图模板稍后可以访问的对象。</span><span class="sxs-lookup"><span data-stu-id="f52b7-187">You can do this by having the controller put the dynamic data that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="f52b7-188">返回到*HelloWorldController.cs*文件，并更改`Welcome`方法以添加`Message`并`NumTimes`值设为`ViewBag`对象。</span><span class="sxs-lookup"><span data-stu-id="f52b7-188">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="f52b7-189">`ViewBag` 是一个动态对象，这意味着您可以随意设置其中;`ViewBag`对象具有定义的属性，直到你将内容放在它。</span><span class="sxs-lookup"><span data-stu-id="f52b7-189">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="f52b7-190">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="f52b7-190">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

<span data-ttu-id="f52b7-191">现在`ViewBag`对象包含将自动传递给视图的数据。</span><span class="sxs-lookup"><span data-stu-id="f52b7-191">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="f52b7-192">接下来，需要一个欢迎使用视图模板 ！</span><span class="sxs-lookup"><span data-stu-id="f52b7-192">Next, you need a Welcome view template!</span></span> <span data-ttu-id="f52b7-193">在中**调试**菜单中，选择**生成 MvcMovie**以确保编译项目。</span><span class="sxs-lookup"><span data-stu-id="f52b7-193">In the **Debug** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="f52b7-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f52b7-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="f52b7-195">然后在右键单击`Welcome`方法，并单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="f52b7-195">Then right-click inside the `Welcome` method and click **Add View**.</span></span> <span data-ttu-id="f52b7-196">下面是什么**添加视图**对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="f52b7-196">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image13.png)

<span data-ttu-id="f52b7-197">单击**外**，然后添加以下代码`<h2>`中的新元素*Welcome.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="f52b7-197">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="f52b7-198">你将创建无数次，用户所说它应显示"Hello"的循环。</span><span class="sxs-lookup"><span data-stu-id="f52b7-198">You'll create a loop that says "Hello" as many times as the user says it should.</span></span> <span data-ttu-id="f52b7-199">完整*Welcome.cshtml*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="f52b7-199">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

<span data-ttu-id="f52b7-200">运行应用程序并浏览到以下 URL:</span><span class="sxs-lookup"><span data-stu-id="f52b7-200">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="f52b7-201">现在数据取自 URL 并自动传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="f52b7-201">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="f52b7-202">控制器将数据打包到`ViewBag`对象并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="f52b7-202">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="f52b7-203">该视图然后会以 html 格式的数据向用户显示。</span><span class="sxs-lookup"><span data-stu-id="f52b7-203">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image14.png)

<span data-ttu-id="f52b7-204">当然，这是模型的一种“M”类型，而不是数据库类。</span><span class="sxs-lookup"><span data-stu-id="f52b7-204">Well, that was a kind of an "M" for model, but not the database kind.</span></span> <span data-ttu-id="f52b7-205">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="f52b7-205">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f52b7-206">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="f52b7-206">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
