---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第 2 部分： 控制器 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 2 部分介绍了控制器。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: a854feff675cae302b9927d209808257b7d087cb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381798"
---
<a name="part-2-controllers"></a><span data-ttu-id="0a602-104">第 2 部分： 控制器</span><span class="sxs-lookup"><span data-stu-id="0a602-104">Part 2: Controllers</span></span>
====================
<span data-ttu-id="0a602-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0a602-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0a602-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="0a602-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0a602-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="0a602-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="0a602-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="0a602-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0a602-109">第 2 部分介绍了控制器。</span><span class="sxs-lookup"><span data-stu-id="0a602-109">Part 2 covers Controllers.</span></span>


<span data-ttu-id="0a602-110">与传统的 web 框架，传入的 Url 通常映射到磁盘上的文件中。</span><span class="sxs-lookup"><span data-stu-id="0a602-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="0a602-111">例如： 所示的请求 url"/ Products.aspx"或"/ Products.php"可能会处理由"Products.aspx"或"Products.php"文件。</span><span class="sxs-lookup"><span data-stu-id="0a602-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="0a602-112">基于 web 的 MVC 框架将 Url 映射到服务器代码中以略有不同的方式。</span><span class="sxs-lookup"><span data-stu-id="0a602-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="0a602-113">而不是将传入 Url 映射到文件，它们而是将 Url 映射到类上的方法。</span><span class="sxs-lookup"><span data-stu-id="0a602-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="0a602-114">这些类称为"控制器"和要负责处理传入的 HTTP 请求，处理用户输入、 检索和保存数据，并确定要发送的响应返回给客户端 （显示 HTML、 下载文件，将重定向到不同URL 等）。</span><span class="sxs-lookup"><span data-stu-id="0a602-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="0a602-115">添加一个 HomeController</span><span class="sxs-lookup"><span data-stu-id="0a602-115">Adding a HomeController</span></span>

<span data-ttu-id="0a602-116">我们将首先我们 MVC Music 商店的应用程序添加到我们的站点的主页将处理 Url 的控制器类。</span><span class="sxs-lookup"><span data-stu-id="0a602-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="0a602-117">我们将遵循 ASP.NET MVC 的默认命名约定，并调用其 HomeController。</span><span class="sxs-lookup"><span data-stu-id="0a602-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="0a602-118">右键单击解决方案资源管理器中的"控制器"文件夹，然后选择"添加"，然后单击"控制器..."命令：</span><span class="sxs-lookup"><span data-stu-id="0a602-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="0a602-119">这将显示"添加控制器"对话框。</span><span class="sxs-lookup"><span data-stu-id="0a602-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="0a602-120">控制器"HomeController"命名，然后按添加按钮。</span><span class="sxs-lookup"><span data-stu-id="0a602-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="0a602-121">这将创建一个新文件，HomeController.cs 中，使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="0a602-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="0a602-122">若要启动尽可能简单地，让我们来替换 Index 方法仅返回字符串的简单方法。</span><span class="sxs-lookup"><span data-stu-id="0a602-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="0a602-123">我们将执行两项更改：</span><span class="sxs-lookup"><span data-stu-id="0a602-123">We'll make two changes:</span></span>

- <span data-ttu-id="0a602-124">更改此方法返回一个字符串而不是 ActionResult</span><span class="sxs-lookup"><span data-stu-id="0a602-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="0a602-125">更改要返回"Hello 从主页"的返回语句</span><span class="sxs-lookup"><span data-stu-id="0a602-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="0a602-126">该方法现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="0a602-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="0a602-127">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="0a602-127">Running the Application</span></span>

<span data-ttu-id="0a602-128">现在让我们运行该站点。</span><span class="sxs-lookup"><span data-stu-id="0a602-128">Now let's run the site.</span></span> <span data-ttu-id="0a602-129">我们可以开始我们的 web 服务器并尝试使用任何以下站点::</span><span class="sxs-lookup"><span data-stu-id="0a602-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="0a602-130">选择调试 ⇨ 启动调试菜单项</span><span class="sxs-lookup"><span data-stu-id="0a602-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="0a602-131">单击工具栏中的绿色箭头按钮 ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="0a602-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="0a602-132">使用键盘快捷方式，F5。</span><span class="sxs-lookup"><span data-stu-id="0a602-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="0a602-133">使用任何上述步骤将编译我们的项目，并引起是内置于 Visual Web Developer 启动 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="0a602-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="0a602-134">通知会在以指示 ASP.NET Development Server 已启动，屏幕的底部角中，将显示的端口号下运行。</span><span class="sxs-lookup"><span data-stu-id="0a602-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="0a602-135">Visual Web Developer 会自动打开浏览器窗口中的 URL 指向我们的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="0a602-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="0a602-136">这将使我们可以快速试用我们的 web 应用程序：</span><span class="sxs-lookup"><span data-stu-id="0a602-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="0a602-137">嗯，这是很快捷 – 我们创建一个新网站，添加三个行函数，并且我们在浏览器中有文本。</span><span class="sxs-lookup"><span data-stu-id="0a602-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="0a602-138">不特别复杂，但它是一个开始。</span><span class="sxs-lookup"><span data-stu-id="0a602-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="0a602-139">*注意： Visual Web Developer 包括 ASP.NET 开发服务器，这将在一个随机免费"端口"号上运行你的网站。在上面的屏幕截图中的网站运行在`http://localhost:26641/`，因此它正在使用端口 26641。端口号将不同。当我们谈及 URL 的 like /Store/Browse 本教程中时，，将投入的端口号。假设 26641 端口号，浏览到/Store/浏览将意味着浏览到`http://localhost:26641/Store/Browse`。*</span><span class="sxs-lookup"><span data-stu-id="0a602-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="0a602-140">添加 StoreController</span><span class="sxs-lookup"><span data-stu-id="0a602-140">Adding a StoreController</span></span>

<span data-ttu-id="0a602-141">我们添加了一个简单的 HomeController 实现我们的站点的主页。</span><span class="sxs-lookup"><span data-stu-id="0a602-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="0a602-142">现在让我们添加另一个控制器，我们将使用实现我们音乐应用商店的浏览功能。</span><span class="sxs-lookup"><span data-stu-id="0a602-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="0a602-143">存储控制器将支持三种方案：</span><span class="sxs-lookup"><span data-stu-id="0a602-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="0a602-144">在我们的音乐应用商店音乐流派列表页</span><span class="sxs-lookup"><span data-stu-id="0a602-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="0a602-145">列出所有特定流派音乐 album 的浏览页面</span><span class="sxs-lookup"><span data-stu-id="0a602-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="0a602-146">显示有关特定音乐唱片集信息的详细信息页</span><span class="sxs-lookup"><span data-stu-id="0a602-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="0a602-147">我们将首先添加一个新的 StoreController 类...</span><span class="sxs-lookup"><span data-stu-id="0a602-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="0a602-148">如果尚未安装，请停止正在运行的应用程序或者通过关闭浏览器选择调试 ⇨ 停止调试菜单项。</span><span class="sxs-lookup"><span data-stu-id="0a602-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="0a602-149">现在，添加新 StoreController。</span><span class="sxs-lookup"><span data-stu-id="0a602-149">Now add a new StoreController.</span></span> <span data-ttu-id="0a602-150">就像我们一样 HomeController，我们将执行此操作通过右键单击解决方案资源管理器中的"控制器"文件夹，然后选择添加-&gt;控制器菜单项</span><span class="sxs-lookup"><span data-stu-id="0a602-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="0a602-151">我们新 StoreController 已具有一个"索引"方法。</span><span class="sxs-lookup"><span data-stu-id="0a602-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="0a602-152">我们将使用此"Index"方法来实现我们列出了我们在音乐应用商店中的所有类型的列表页面。</span><span class="sxs-lookup"><span data-stu-id="0a602-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="0a602-153">我们还将添加两个其他的方法来实现两种情况下我们想要以处理我们 StoreController： 浏览和详细信息。</span><span class="sxs-lookup"><span data-stu-id="0a602-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="0a602-154">我们的控制器中的这些方法 （索引、 浏览和详细信息） 称为"控制器操作"，如您所见与 HomeController.Index （） 操作方法，它们的作用是响应 URL 请求，并 （通常情况下） 确定哪些内容应发送回浏览器或调用 URL 的用户。</span><span class="sxs-lookup"><span data-stu-id="0a602-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="0a602-155">我们通过更改 theIndex() 方法以返回字符串"Hello 从 Store.Index()"启动我们 StoreController 的实现，并且我们将为 browse （） 和 Details() 添加类似的方法：</span><span class="sxs-lookup"><span data-stu-id="0a602-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="0a602-156">再次运行该项目，并浏览以下 Url:</span><span class="sxs-lookup"><span data-stu-id="0a602-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="0a602-157">/ 存储</span><span class="sxs-lookup"><span data-stu-id="0a602-157">/Store</span></span>
- <span data-ttu-id="0a602-158">/ Store/浏览</span><span class="sxs-lookup"><span data-stu-id="0a602-158">/Store/Browse</span></span>
- <span data-ttu-id="0a602-159">/ 存储/详细信息</span><span class="sxs-lookup"><span data-stu-id="0a602-159">/Store/Details</span></span>

<span data-ttu-id="0a602-160">访问这些 Url 将调用我们的控制器内的操作方法并返回字符串响应：</span><span class="sxs-lookup"><span data-stu-id="0a602-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="0a602-161">那太好了，但它们是只是常量字符串。</span><span class="sxs-lookup"><span data-stu-id="0a602-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="0a602-162">让我们来使这些动态的因此它们从 URL 中获取信息并将其显示在页面输出中。</span><span class="sxs-lookup"><span data-stu-id="0a602-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="0a602-163">首先，我们将更改浏览操作方法来检索该 URL 的查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="0a602-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="0a602-164">我们可以通过将"genre"参数添加到我们的操作方法来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0a602-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="0a602-165">当我们执行此操作 ASP.NET MVC 将自动传递名为"genre"到我们的操作方法，在调用时任何查询字符串或窗体 post 参数。</span><span class="sxs-lookup"><span data-stu-id="0a602-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="0a602-166">*注意： 我们使用 HttpUtility.HtmlEncode 实用程序方法来清理用户输入。这可以防止用户与 /Store/Browse 形式的链接将 Javascript 注入到视图？Genre =&lt;脚本&gt;window.location = 'http://hackersite.com'&lt;/script&gt;。*</span><span class="sxs-lookup"><span data-stu-id="0a602-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="0a602-167">现在让我们浏览到/Store/浏览？Genre = Disco</span><span class="sxs-lookup"><span data-stu-id="0a602-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="0a602-168">让我们下一次更改要读取并显示输入的参数的详细信息操作名为 id。</span><span class="sxs-lookup"><span data-stu-id="0a602-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="0a602-169">与我们前面的方法，我们不会为嵌入的 ID 值作为查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="0a602-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="0a602-170">而是我们会将其嵌入直接在 URL 本身中。</span><span class="sxs-lookup"><span data-stu-id="0a602-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="0a602-171">例如： /Store/Details/5。</span><span class="sxs-lookup"><span data-stu-id="0a602-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="0a602-172">ASP.NET MVC 可以让我们轻松执行此操作而无需进行任何配置。</span><span class="sxs-lookup"><span data-stu-id="0a602-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="0a602-173">ASP.NET MVC 的默认路由约定是操作方法名称后的 URL 的段视为名为"ID"的参数。</span><span class="sxs-lookup"><span data-stu-id="0a602-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="0a602-174">如果你操作的方法有一个名为 ID 参数则 ASP.NET MVC 将自动传递 URL 段向你作为参数。</span><span class="sxs-lookup"><span data-stu-id="0a602-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="0a602-175">运行应用程序并浏览到 /Store/Details/5:</span><span class="sxs-lookup"><span data-stu-id="0a602-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="0a602-176">让我们回顾一下到目前为止我们所做:</span><span class="sxs-lookup"><span data-stu-id="0a602-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="0a602-177">我们已在 Visual Web Developer 中创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="0a602-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="0a602-178">我们已经讨论了 ASP.NET MVC 应用程序的基本文件夹结构</span><span class="sxs-lookup"><span data-stu-id="0a602-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="0a602-179">我们已了解如何运行我们的网站使用 ASP.NET 开发服务器</span><span class="sxs-lookup"><span data-stu-id="0a602-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="0a602-180">我们已经创建了两个控制器类： 一个 HomeController 和 StoreController</span><span class="sxs-lookup"><span data-stu-id="0a602-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="0a602-181">我们为我们控制器的响应 URL 请求并返回到浏览器的文本添加了操作方法</span><span class="sxs-lookup"><span data-stu-id="0a602-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="0a602-182">[上一页](mvc-music-store-part-1.md)
> [下一页](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="0a602-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
