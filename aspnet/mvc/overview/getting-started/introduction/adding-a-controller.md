---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: d5cc9db7b1eec139a37afb6427fd761342fcc1f5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824724"
---
<a name="adding-a-controller"></a><span data-ttu-id="1772d-102">添加控制器</span><span class="sxs-lookup"><span data-stu-id="1772d-102">Adding a Controller</span></span>
====================
<span data-ttu-id="1772d-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="1772d-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="1772d-104">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="1772d-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="1772d-105">MVC 是一种模式用于开发应用程序也设计、 可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="1772d-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="1772d-106">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="1772d-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="1772d-107">**M**模式： 类，表示数据的应用程序和使用验证逻辑以强制实施针对这些数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="1772d-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="1772d-108">**V**视图： 应用程序使用动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="1772d-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="1772d-109">**C**控制器： 处理传入的浏览器请求的类中检索模型数据，然后指定将响应返回到浏览器的视图模板。</span><span class="sxs-lookup"><span data-stu-id="1772d-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="1772d-110">我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="1772d-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

> [!NOTE]
> <span data-ttu-id="1772d-111">在上一步默认 MVC 模板被选中。</span><span class="sxs-lookup"><span data-stu-id="1772d-111">In the previous step the Default MVC template was selected.</span></span> <span data-ttu-id="1772d-112">这将创建主文件夹、 帐户和默认情况下管理控制器。</span><span class="sxs-lookup"><span data-stu-id="1772d-112">This creates Home, Account and Manage Controllers by default.</span></span>

<span data-ttu-id="1772d-113">让我们首先创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="1772d-113">Let's begin by creating a controller class.</span></span> <span data-ttu-id="1772d-114">在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。</span><span class="sxs-lookup"><span data-stu-id="1772d-114">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>


![](adding-a-controller/_static/image1.png)

<span data-ttu-id="1772d-115">在中**添加基架**对话框中，单击**MVC 5 控制器-空**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="1772d-115">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  
 

<span data-ttu-id="1772d-116">新控制器命名为"HelloWorldController"，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="1772d-116">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image3.png)

<span data-ttu-id="1772d-118">请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*和 new folder *Views\HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="1772d-118">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="1772d-119">控制器已在 IDE 中打开。</span><span class="sxs-lookup"><span data-stu-id="1772d-119">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="1772d-120">将以下代码替换为该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="1772d-120">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="1772d-121">控制器方法将返回 HTML 的字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="1772d-121">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="1772d-122">控制器被命名为`HelloWorldController`和第一种方法名为`Index`。</span><span class="sxs-lookup"><span data-stu-id="1772d-122">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="1772d-123">让我们从浏览器调用它。</span><span class="sxs-lookup"><span data-stu-id="1772d-123">Let's invoke it from a browser.</span></span> <span data-ttu-id="1772d-124">运行应用程序 （按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="1772d-124">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="1772d-125">在浏览器中，追加&quot;HelloWorld&quot;到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="1772d-125">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="1772d-126">(例如，在图中，其下方的`http://localhost:1234/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="1772d-126">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="1772d-127">在上述方法中，代码直接返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="1772d-127">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="1772d-128">你告诉系统只返回一些 HTML，并确实执行此操作 ！</span><span class="sxs-lookup"><span data-stu-id="1772d-128">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="1772d-129">ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="1772d-129">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="1772d-130">使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码以调用：</span><span class="sxs-lookup"><span data-stu-id="1772d-130">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="1772d-131">设置中的路由的格式*应用程序\_Start/RouteConfig.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="1772d-131">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="1772d-132">运行应用程序并不提供任何 URL 段，则默认为"Home"控制器，并在上面的代码的 defaults 节中指定"的索引"操作方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-132">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="1772d-133">URL 的第一个部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="1772d-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="1772d-134">因此 */HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="1772d-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="1772d-135">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="1772d-136">因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。</span><span class="sxs-lookup"><span data-stu-id="1772d-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="1772d-137">请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="1772d-138">这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="1772d-139">URL 段的第三部分 (`Parameters`) 针对的是路由数据。</span><span class="sxs-lookup"><span data-stu-id="1772d-139">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="1772d-140">在本教程中，我们将更高版本上看到路由数据。</span><span class="sxs-lookup"><span data-stu-id="1772d-140">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="1772d-141">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="1772d-141">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="1772d-142">`Welcome`方法运行并返回字符串&quot;这是 Welcome 操作方法...&quot;.</span><span class="sxs-lookup"><span data-stu-id="1772d-142">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="1772d-143">默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="1772d-143">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="1772d-144">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-144">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="1772d-145">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="1772d-145">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="1772d-146">让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="1772d-146">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="1772d-147">更改你`Welcome`方法以包括两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1772d-147">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="1772d-148">请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。</span><span class="sxs-lookup"><span data-stu-id="1772d-148">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="1772d-149">安全说明： 使用上面的代码[HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)以防止恶意输入 (即 JavaScript) 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1772d-149">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="1772d-150">有关详细信息请参阅[如何： 保护对脚本攻击在 Web 应用程序通过应用 HTML 编码为字符串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1772d-150">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>


 <span data-ttu-id="1772d-151">运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`)。</span><span class="sxs-lookup"><span data-stu-id="1772d-151">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="1772d-152">你可以尝试不同的值`name`和`numtimes`在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="1772d-152">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="1772d-153">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)会自动将映射到方法中的参数将命名的参数从地址栏中的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="1772d-153">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="1772d-154">在上面的 URL 段示例 ( `Parameters`) 未使用，则`name`并`numTimes`作为参数传递[查询字符串](http://en.wikipedia.org/wiki/Query_string)。</span><span class="sxs-lookup"><span data-stu-id="1772d-154">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="1772d-155">? </span><span class="sxs-lookup"><span data-stu-id="1772d-155">The ?</span></span> <span data-ttu-id="1772d-156">（问号） 在上述 URL 中为分隔符，并后接查询字符串。</span><span class="sxs-lookup"><span data-stu-id="1772d-156">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="1772d-157">&amp; 字符用于分隔查询字符串。</span><span class="sxs-lookup"><span data-stu-id="1772d-157">The &amp; character separates query strings.</span></span>

<span data-ttu-id="1772d-158">欢迎使用方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1772d-158">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="1772d-159">运行应用程序并输入以下 URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="1772d-159">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="1772d-160">这一次第三个 URL 段匹配路由参数`ID.``Welcome`操作方法包含一个参数 (`ID`) 的匹配中的 URL 规范`RegisterRoutes`方法。</span><span class="sxs-lookup"><span data-stu-id="1772d-160">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="1772d-161">在 ASP.NET MVC 应用程序，它是更常见的做法在作为路由数据 （例如，我们使用上述 ID 所做的那样） 比将其作为查询字符串中传递的参数中传递。</span><span class="sxs-lookup"><span data-stu-id="1772d-161">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="1772d-162">您还可以添加一个路由，同时传递`name`和`numtimes`参数作为 URL 中的路由数据中。</span><span class="sxs-lookup"><span data-stu-id="1772d-162">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="1772d-163">在中*应用程序\_Start\RouteConfig.cs*文件中，添加"Hello"路由：</span><span class="sxs-lookup"><span data-stu-id="1772d-163">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="1772d-164">运行应用程序，并浏览到`/localhost:XXX/HelloWorld/Welcome/Scott/3`。</span><span class="sxs-lookup"><span data-stu-id="1772d-164">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="1772d-165">对于许多 MVC 应用程序的默认路由工作正常。</span><span class="sxs-lookup"><span data-stu-id="1772d-165">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="1772d-166">你将了解在本教程中使用模型联编程序，数据传递更高版本，无需为此，修改默认路由。</span><span class="sxs-lookup"><span data-stu-id="1772d-166">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="1772d-167">在这些示例控制器始终执行&quot;VC&quot;的 MVC 部分 — 即，视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="1772d-167">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="1772d-168">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="1772d-168">The controller is returning HTML directly.</span></span> <span data-ttu-id="1772d-169">通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。</span><span class="sxs-lookup"><span data-stu-id="1772d-169">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="1772d-170">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="1772d-170">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="1772d-171">让我们看如何实现这在下一步。</span><span class="sxs-lookup"><span data-stu-id="1772d-171">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1772d-172">[上一页](getting-started.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="1772d-172">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
