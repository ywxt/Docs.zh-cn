---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第 2 部分： 控制器 |Microsoft 文档
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 2 部分介绍控制器。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 680cdea388d9b01961bd626643c0fd91c9205ed7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878693"
---
<a name="part-2-controllers"></a><span data-ttu-id="f6048-104">第 2 部分： 控制器</span><span class="sxs-lookup"><span data-stu-id="f6048-104">Part 2: Controllers</span></span>
====================
<span data-ttu-id="f6048-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="f6048-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f6048-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="f6048-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="f6048-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="f6048-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="f6048-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="f6048-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="f6048-109">第 2 部分介绍控制器。</span><span class="sxs-lookup"><span data-stu-id="f6048-109">Part 2 covers Controllers.</span></span>


<span data-ttu-id="f6048-110">与传统 web 框架传入 Url 通常会映射到磁盘上的文件中。</span><span class="sxs-lookup"><span data-stu-id="f6048-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="f6048-111">例如： 如 URL 的请求"/ Products.aspx"或"/ Products.php"的"Products.aspx"或"Products.php"文件可能处理。</span><span class="sxs-lookup"><span data-stu-id="f6048-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="f6048-112">基于 web 的 MVC 框架将 Url 映射到服务器代码，以略有不同的方式。</span><span class="sxs-lookup"><span data-stu-id="f6048-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="f6048-113">而不是将传入 Url 映射到文件，它们改为映射到类的方法的 Url。</span><span class="sxs-lookup"><span data-stu-id="f6048-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="f6048-114">这些类称为"控制器"并负责处理传入的 HTTP 请求，处理用户输入，检索和保存数据，并确定要发送的响应返回给客户端 （显示 HTML，下载的文件，将重定向到不同URL、 等）。</span><span class="sxs-lookup"><span data-stu-id="f6048-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="f6048-115">添加 HomeController</span><span class="sxs-lookup"><span data-stu-id="f6048-115">Adding a HomeController</span></span>

<span data-ttu-id="f6048-116">通过添加了控制器类将处理到我们的站点的主页的 Url，我们将首先我们 MVC 音乐商店的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f6048-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="f6048-117">我们将遵循的 ASP.NET MVC 的默认命名约定，并调用它 HomeController。</span><span class="sxs-lookup"><span data-stu-id="f6048-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="f6048-118">右键单击解决方案资源管理器中的"控制器"文件夹中，然后选择"添加"，然后"控制器..."</span><span class="sxs-lookup"><span data-stu-id="f6048-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…"</span></span> <span data-ttu-id="f6048-119">命令：</span><span class="sxs-lookup"><span data-stu-id="f6048-119">command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="f6048-120">这将显示"添加控制器"对话框。</span><span class="sxs-lookup"><span data-stu-id="f6048-120">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="f6048-121">将命名控制器"HomeController"并按添加按钮。</span><span class="sxs-lookup"><span data-stu-id="f6048-121">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="f6048-122">这将创建新文件中，命名为 HomeController.cs，替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f6048-122">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="f6048-123">若要启动尽可能简单地，让我们使用简单方法只返回一个字符串替换 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="f6048-123">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="f6048-124">我们将进行两个更改：</span><span class="sxs-lookup"><span data-stu-id="f6048-124">We'll make two changes:</span></span>

- <span data-ttu-id="f6048-125">更改方法以返回而不是 ActionResult 字符串</span><span class="sxs-lookup"><span data-stu-id="f6048-125">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="f6048-126">更改返回语句，以返回"Hello 从主页"</span><span class="sxs-lookup"><span data-stu-id="f6048-126">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="f6048-127">该方法现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6048-127">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="f6048-128">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="f6048-128">Running the Application</span></span>

<span data-ttu-id="f6048-129">现在让我们运行该站点。</span><span class="sxs-lookup"><span data-stu-id="f6048-129">Now let's run the site.</span></span> <span data-ttu-id="f6048-130">我们可以启动我们的 web 服务器，然后尝试登录网站，使用以下任一::</span><span class="sxs-lookup"><span data-stu-id="f6048-130">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="f6048-131">选择调试 ⇨ 启动调试菜单项</span><span class="sxs-lookup"><span data-stu-id="f6048-131">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="f6048-132">单击工具栏中的绿色箭头按钮 ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="f6048-132">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="f6048-133">使用键盘快捷方式，F5。</span><span class="sxs-lookup"><span data-stu-id="f6048-133">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="f6048-134">使用任何上述步骤将编译我们项目中，并导致是内置于 Visual Web Developer 启动 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="f6048-134">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="f6048-135">通知会在以指示 ASP.NET 开发服务器已启动，屏幕的右下角中，将显示的端口号下运行。</span><span class="sxs-lookup"><span data-stu-id="f6048-135">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="f6048-136">Visual Web Developer 将自动打开浏览器窗口，其 URL 指向我们的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f6048-136">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="f6048-137">这将使我们可以快速试用我们的 web 应用程序：</span><span class="sxs-lookup"><span data-stu-id="f6048-137">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="f6048-138">那么，这是相当快速 – 我们创建的新网站，添加三个行函数，而且我们在浏览器中有文本。</span><span class="sxs-lookup"><span data-stu-id="f6048-138">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="f6048-139">不特别复杂，但它是一个开始。</span><span class="sxs-lookup"><span data-stu-id="f6048-139">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="f6048-140">*注意： Visual Web Developer 包括 ASP.NET 开发服务器，这将在一个随机可用"端口"号上运行你的网站。在上面的屏幕截图，该站点运行在`http://localhost:26641/`，因此它正在使用端口 26641。端口号将有所不同。当我们谈 URL 的 like /Store/Browse 在本教程中时，后者将更后的端口号。假设 26641 端口号，浏览到/存储/浏览将意味着浏览到`http://localhost:26641/Store/Browse`。*</span><span class="sxs-lookup"><span data-stu-id="f6048-140">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="f6048-141">添加 StoreController</span><span class="sxs-lookup"><span data-stu-id="f6048-141">Adding a StoreController</span></span>

<span data-ttu-id="f6048-142">我们添加简单 HomeController 实现我们站点的主页。</span><span class="sxs-lookup"><span data-stu-id="f6048-142">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="f6048-143">让我们现在添加我们将使用来实现我们音乐商店浏览功能的另一个控制器。</span><span class="sxs-lookup"><span data-stu-id="f6048-143">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="f6048-144">存储控制器将支持三种方案：</span><span class="sxs-lookup"><span data-stu-id="f6048-144">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="f6048-145">在我们音乐商店音乐风格列表页面</span><span class="sxs-lookup"><span data-stu-id="f6048-145">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="f6048-146">列出所有在特定流派音乐集浏览页</span><span class="sxs-lookup"><span data-stu-id="f6048-146">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="f6048-147">显示有关特定音乐唱片集的信息的详细信息页</span><span class="sxs-lookup"><span data-stu-id="f6048-147">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="f6048-148">我们首先添加一个新的 StoreController 类...</span><span class="sxs-lookup"><span data-stu-id="f6048-148">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="f6048-149">如果你尚未这样做，则停止正在运行的应用程序或者通过关闭浏览器选择调试 ⇨ 停止调试菜单项。</span><span class="sxs-lookup"><span data-stu-id="f6048-149">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="f6048-150">现在，添加新 StoreController。</span><span class="sxs-lookup"><span data-stu-id="f6048-150">Now add a new StoreController.</span></span> <span data-ttu-id="f6048-151">就像我们未与 HomeController，我们需要执行此操作通过右键单击解决方案资源管理器中的"控制器"文件夹，然后选择添加-&gt;控制器菜单项</span><span class="sxs-lookup"><span data-stu-id="f6048-151">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="f6048-152">我们新 StoreController 已具有"Index"的方法。</span><span class="sxs-lookup"><span data-stu-id="f6048-152">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="f6048-153">我们将使用此"索引"方法来实现我们列表页，其中列出我们音乐商店中的所有风格。</span><span class="sxs-lookup"><span data-stu-id="f6048-153">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="f6048-154">我们还将添加两个其他的方法来实现两种情况下我们想要以处理我们 StoreController： 浏览和详细信息。</span><span class="sxs-lookup"><span data-stu-id="f6048-154">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="f6048-155">在我们控制器内的这些方法 （索引、 浏览和详细信息） 称为"控制器操作"，而你已经了解与 HomeController.Index （） 操作方法，如其作业是响应的 URL 请求并 （通常来说） 确定哪些内容应发送回浏览器或调用 URL 的用户。</span><span class="sxs-lookup"><span data-stu-id="f6048-155">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="f6048-156">我们将首先我们 StoreController 实现更改 theIndex() 方法以返回字符串"Hello 从 Store.Index()"和 browse （） 和 Details()，我们将添加类似的方法：</span><span class="sxs-lookup"><span data-stu-id="f6048-156">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="f6048-157">再次运行项目，并浏览以下 Url:</span><span class="sxs-lookup"><span data-stu-id="f6048-157">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="f6048-158">/Store</span><span class="sxs-lookup"><span data-stu-id="f6048-158">/Store</span></span>
- <span data-ttu-id="f6048-159">/ 应用商店/浏览</span><span class="sxs-lookup"><span data-stu-id="f6048-159">/Store/Browse</span></span>
- <span data-ttu-id="f6048-160">/ 存储/详细信息</span><span class="sxs-lookup"><span data-stu-id="f6048-160">/Store/Details</span></span>

<span data-ttu-id="f6048-161">访问以下 Url 将调用我们控制器中的操作方法，并返回字符串的响应：</span><span class="sxs-lookup"><span data-stu-id="f6048-161">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="f6048-162">这很不错，但它们是只是常量字符串。</span><span class="sxs-lookup"><span data-stu-id="f6048-162">That's great, but these are just constant strings.</span></span> <span data-ttu-id="f6048-163">让我们使这些动态的以便它们采用中 URL 的信息并将其显示在页面输出。</span><span class="sxs-lookup"><span data-stu-id="f6048-163">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="f6048-164">首先我们将更改浏览操作方法，以便从 URL 检索查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="f6048-164">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="f6048-165">我们可以将"genre"参数添加到我们的操作方法来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f6048-165">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="f6048-166">在执行此操作时 ASP.NET MVC 会自动传入任何查询字符串或窗体发布参数名为"genre"到我们的操作方法中，当调用它。</span><span class="sxs-lookup"><span data-stu-id="f6048-166">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="f6048-167">*注意： 我们将使用 HttpUtility.HtmlEncode 实用工具方法，整理用户输入。这可以防止用户将 Javascript 注入到我们的视图，如 /Store/Browse 的链接？流派 =&lt;脚本&gt;window.location=http://hackersite.com&lt;/&gt;。*</span><span class="sxs-lookup"><span data-stu-id="f6048-167">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="f6048-168">现在让我们浏览到/存储/浏览？流派 = Disco</span><span class="sxs-lookup"><span data-stu-id="f6048-168">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="f6048-169">让我们下一次更改的详细信息操作读取，并显示输入的参数名为 id。</span><span class="sxs-lookup"><span data-stu-id="f6048-169">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="f6048-170">与不同的是我们前面的方法，我们不会为嵌入的 ID 值作为查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="f6048-170">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="f6048-171">而是我们将嵌入它直接在 URL 本身内。</span><span class="sxs-lookup"><span data-stu-id="f6048-171">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="f6048-172">例如： /Store/Details/5。</span><span class="sxs-lookup"><span data-stu-id="f6048-172">For example: /Store/Details/5.</span></span>

<span data-ttu-id="f6048-173">ASP.NET MVC 允许我们轻松执行此操作而无需进行任何配置。</span><span class="sxs-lookup"><span data-stu-id="f6048-173">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="f6048-174">ASP.NET MVC 的默认路由约定是在操作方法名称后面的 url 段视为一个名为"ID"参数。</span><span class="sxs-lookup"><span data-stu-id="f6048-174">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="f6048-175">如果您操作的方法有一个名为 ID 参数然后 ASP.NET MVC 将自动传递的 URL 段向你作为参数。</span><span class="sxs-lookup"><span data-stu-id="f6048-175">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="f6048-176">运行应用程序，并浏览到 /Store/Details/5:</span><span class="sxs-lookup"><span data-stu-id="f6048-176">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="f6048-177">让我们回顾一下我们到目前为止已完成：</span><span class="sxs-lookup"><span data-stu-id="f6048-177">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="f6048-178">我们已在 Visual Web Developer 中创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="f6048-178">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="f6048-179">我们已讨论了 ASP.NET MVC 应用程序的基本文件夹结构</span><span class="sxs-lookup"><span data-stu-id="f6048-179">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="f6048-180">我们已经学习了如何运行我们的网站使用 ASP.NET 开发服务器</span><span class="sxs-lookup"><span data-stu-id="f6048-180">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="f6048-181">我们已创建了两个控制器类： HomeController 和 StoreController</span><span class="sxs-lookup"><span data-stu-id="f6048-181">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="f6048-182">我们已向我们控制器的响应的 URL 请求并返回到浏览器的文本添加操作方法</span><span class="sxs-lookup"><span data-stu-id="f6048-182">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="f6048-183">[上一页](mvc-music-store-part-1.md)
> [下一页](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="f6048-183">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
