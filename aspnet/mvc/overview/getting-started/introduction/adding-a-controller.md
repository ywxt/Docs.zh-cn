---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: "添加控制器 |Microsoft 文档"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: c8f317b2ac133f560461917af1588b7a1fa51c4f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-controller"></a><span data-ttu-id="a724c-102">添加控制器</span><span class="sxs-lookup"><span data-stu-id="a724c-102">Adding a Controller</span></span>
====================
<span data-ttu-id="a724c-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="a724c-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="a724c-104">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="a724c-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="a724c-105">MVC 是模式，用于开发的应用程序很好地设计、 可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="a724c-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="a724c-106">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="a724c-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="a724c-107">**M** odels： 类： 表示应用程序的数据和使用验证逻辑以强制实施针对这些数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="a724c-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="a724c-108">**V** iews： 应用程序使用动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="a724c-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="a724c-109">**C** ontrollers： 处理传入的浏览器请求，类检索模型数据，然后指定将响应返回到浏览器的视图模板。</span><span class="sxs-lookup"><span data-stu-id="a724c-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="a724c-110">我们将涵盖所有这些概念进行了本系列教程，向您展示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="a724c-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

> [!NOTE]
> <span data-ttu-id="a724c-111">在上一步默认 MVC 模板被选中。</span><span class="sxs-lookup"><span data-stu-id="a724c-111">In the previous step the Default MVC template was selected.</span></span> <span data-ttu-id="a724c-112">这将创建主页，帐户和默认情况下管理控制器。</span><span class="sxs-lookup"><span data-stu-id="a724c-112">This creates Home, Account and Manage Controllers by default.</span></span>

<span data-ttu-id="a724c-113">让我们首先创建了控制器类。</span><span class="sxs-lookup"><span data-stu-id="a724c-113">Let's begin by creating a controller class.</span></span> <span data-ttu-id="a724c-114">在**解决方案资源管理器**，右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。</span><span class="sxs-lookup"><span data-stu-id="a724c-114">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>


![](adding-a-controller/_static/image1.png)

<span data-ttu-id="a724c-115">在**添加基架**对话框中，单击**MVC 5 控制器-空**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a724c-115">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  
 

<span data-ttu-id="a724c-116">将新控制器"HelloWorldController"，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a724c-116">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image3.png)

<span data-ttu-id="a724c-118">请注意，在**解决方案资源管理器**，新的文件具有已创建的名为*HelloWorldController.cs*和一个新文件夹*Views\HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="a724c-118">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="a724c-119">在 IDE 中打开控制器。</span><span class="sxs-lookup"><span data-stu-id="a724c-119">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="a724c-120">文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="a724c-120">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="a724c-121">例如，控制器方法将返回 HTML 的字符串。</span><span class="sxs-lookup"><span data-stu-id="a724c-121">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="a724c-122">控制器命名为`HelloWorldController`和名为第一种方法`Index`。</span><span class="sxs-lookup"><span data-stu-id="a724c-122">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="a724c-123">让我们从浏览器调用它。</span><span class="sxs-lookup"><span data-stu-id="a724c-123">Let's invoke it from a browser.</span></span> <span data-ttu-id="a724c-124">运行应用程序 （按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="a724c-124">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="a724c-125">在浏览器中，追加&quot;HelloWorld&quot;地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="a724c-125">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="a724c-126">(例如，在下面的图`http://localhost:1234/HelloWorld.`) 在浏览器页面将如下所示的以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="a724c-126">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="a724c-127">在上面的方法中，代码直接返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="a724c-127">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="a724c-128">告知系统以仅返回一些 HTML，并且它未 ！</span><span class="sxs-lookup"><span data-stu-id="a724c-128">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="a724c-129">ASP.NET MVC 调用另一个控制器类 （和其中的不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="a724c-129">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="a724c-130">使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码调用：</span><span class="sxs-lookup"><span data-stu-id="a724c-130">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="a724c-131">设置中的路由的格式*应用\_Start/RouteConfig.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="a724c-131">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="a724c-132">当你运行应用程序，并且不提供任何 URL 段时，它默认为"Home"控制器和"索引"操作方法的上面的代码中的默认值部分中指定。</span><span class="sxs-lookup"><span data-stu-id="a724c-132">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="a724c-133">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="a724c-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="a724c-134">因此*/HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="a724c-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="a724c-135">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="a724c-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="a724c-136">因此*/HelloWorld/索引*将导致`Index`方法`HelloWorldController`类执行。</span><span class="sxs-lookup"><span data-stu-id="a724c-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="a724c-137">请注意，我们仅必须浏览到*/HelloWorld*和`Index`时默认情况下使用方法。</span><span class="sxs-lookup"><span data-stu-id="a724c-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="a724c-138">这是因为方法名为`Index`是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="a724c-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="a724c-139">URL 段的第三部分 (`Parameters`) 针对的是路由数据。</span><span class="sxs-lookup"><span data-stu-id="a724c-139">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="a724c-140">在本教程中，我们将更高版本上看到路由数据。</span><span class="sxs-lookup"><span data-stu-id="a724c-140">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="a724c-141">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="a724c-141">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="a724c-142">`Welcome`方法将运行并返回字符串&quot;这是欢迎操作方法...&quot;.</span><span class="sxs-lookup"><span data-stu-id="a724c-142">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="a724c-143">默认 MVC 映射是`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="a724c-143">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="a724c-144">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="a724c-144">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="a724c-145">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="a724c-145">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="a724c-146">让我们修改该示例略有，以便你可以将某些参数信息从 URL 中传递到控制器 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="a724c-146">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="a724c-147">更改你`Welcome`方法以包括两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a724c-147">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="a724c-148">请注意，代码将使用 C# 可选参数的功能，则指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。</span><span class="sxs-lookup"><span data-stu-id="a724c-148">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="a724c-149">安全说明： 使用上面的代码[HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)以防止恶意输入 (即 JavaScript) 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a724c-149">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="a724c-150">有关详细信息请参阅[如何： 保护对脚本利用在 Web 应用程序中进行应用 HTML 编码为字符串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a724c-150">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>


 <span data-ttu-id="a724c-151">运行你的应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`)。</span><span class="sxs-lookup"><span data-stu-id="a724c-151">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="a724c-152">你可以尝试不同的值`name`和`numtimes`在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="a724c-152">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="a724c-153">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将映射到你的方法中的参数的查询字符串中的地址栏中的命名的参数。</span><span class="sxs-lookup"><span data-stu-id="a724c-153">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="a724c-154">在上面的 URL 段的示例 ( `Parameters`) 未使用，`name`和`numTimes`参数作为进行传递[的查询字符串](http://en.wikipedia.org/wiki/Query_string)。</span><span class="sxs-lookup"><span data-stu-id="a724c-154">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="a724c-155">? </span><span class="sxs-lookup"><span data-stu-id="a724c-155">The ?</span></span> <span data-ttu-id="a724c-156">（问号） 在上述 URL 是一个分隔符，并且遵循一定的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="a724c-156">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="a724c-157">&amp; 字符用于分隔查询字符串。</span><span class="sxs-lookup"><span data-stu-id="a724c-157">The &amp; character separates query strings.</span></span>

<span data-ttu-id="a724c-158">欢迎方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a724c-158">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="a724c-159">运行应用程序并输入以下 URL:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="a724c-159">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="a724c-160">这一次的第三个 URL 段匹配的路由参数`ID.``Welcome`操作方法包含的参数 (`ID`) 匹配中的 URL 规范`RegisterRoutes`方法。</span><span class="sxs-lookup"><span data-stu-id="a724c-160">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="a724c-161">在 ASP.NET MVC 应用程序，它是更常见的做法传入作为路由数据 （例如，我们 id 上面所做的那样） 比将它们作为查询字符串中传递的参数。</span><span class="sxs-lookup"><span data-stu-id="a724c-161">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="a724c-162">您也可以添加一个路由，都传递`name`和`numtimes`在参数中为在 URL 中的路由数据。</span><span class="sxs-lookup"><span data-stu-id="a724c-162">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="a724c-163">在*应用\_Start\RouteConfig.cs*文件中，添加"Hello"路由：</span><span class="sxs-lookup"><span data-stu-id="a724c-163">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="a724c-164">运行应用程序，并浏览到`/localhost:XXX/HelloWorld/Welcome/Scott/3`。</span><span class="sxs-lookup"><span data-stu-id="a724c-164">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="a724c-165">对于许多 MVC 应用程序，默认路由工作正常。</span><span class="sxs-lookup"><span data-stu-id="a724c-165">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="a724c-166">你将了解将数据使用模型联编程序，本教程中稍后和无需修改该默认路由。</span><span class="sxs-lookup"><span data-stu-id="a724c-166">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="a724c-167">已在这些示例中执行操作控制器&quot;VC&quot; MVC 部分 — 也就是说，视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="a724c-167">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="a724c-168">控制器直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="a724c-168">The controller is returning HTML directly.</span></span> <span data-ttu-id="a724c-169">通常，你不希望直接返回 HTML，因为该按钮将变为非常麻烦的代码的控制器。</span><span class="sxs-lookup"><span data-stu-id="a724c-169">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="a724c-170">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="a724c-170">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="a724c-171">让我们来看如何我们可以执行此操作在下一步。</span><span class="sxs-lookup"><span data-stu-id="a724c-171">Let's look next at how we can do this.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="a724c-172">[上一页](getting-started.md)
[下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="a724c-172">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
