---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 添加控制器 |Microsoft 文档
author: Rick-Anderson
description: 注意： 本教程的更新的版本此处提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全，请按照和演示要简单得多...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: bb76c0a87d935322406b9d8e18fbdb3e41f327f5
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "30868862"
---
<a name="adding-a-controller"></a><span data-ttu-id="86d2c-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="86d2c-104">Adding a Controller</span></span>
====================
<span data-ttu-id="86d2c-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="86d2c-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="86d2c-106">本教程的更新的版本可[此处](../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="86d2c-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="86d2c-107">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="86d2c-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="86d2c-108">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="86d2c-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="86d2c-109">MVC 是模式，用于开发的应用程序很好地设计、 可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="86d2c-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="86d2c-110">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="86d2c-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="86d2c-111">**M** odels： 类： 表示应用程序的数据和使用验证逻辑以强制实施针对这些数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="86d2c-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="86d2c-112">**V** iews： 应用程序使用动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="86d2c-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="86d2c-113">**C** ontrollers： 处理传入的浏览器请求，类检索模型数据，然后指定将响应返回到浏览器的视图模板。</span><span class="sxs-lookup"><span data-stu-id="86d2c-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="86d2c-114">我们将涵盖所有这些概念进行了本系列教程，向您展示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="86d2c-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="86d2c-115">让我们首先创建了控制器类。</span><span class="sxs-lookup"><span data-stu-id="86d2c-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="86d2c-116">在**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。</span><span class="sxs-lookup"><span data-stu-id="86d2c-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="86d2c-117">新控制器命名&quot;HelloWorldController&quot;。</span><span class="sxs-lookup"><span data-stu-id="86d2c-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="86d2c-118">保留的默认模板**空 MVC 控制器**单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="86d2c-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image2.png)

<span data-ttu-id="86d2c-120">请注意，在**解决方案资源管理器**，新的文件具有已创建的名为*HelloWorldController.cs*。</span><span class="sxs-lookup"><span data-stu-id="86d2c-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="86d2c-121">在 IDE 中打开该文件。</span><span class="sxs-lookup"><span data-stu-id="86d2c-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="86d2c-122">文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="86d2c-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="86d2c-123">例如，控制器方法将返回 HTML 的字符串。</span><span class="sxs-lookup"><span data-stu-id="86d2c-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="86d2c-124">控制器命名为`HelloWorldController`和名为上面的第一个方法`Index`。</span><span class="sxs-lookup"><span data-stu-id="86d2c-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="86d2c-125">让我们从浏览器调用它。</span><span class="sxs-lookup"><span data-stu-id="86d2c-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="86d2c-126">运行应用程序 （按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="86d2c-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="86d2c-127">在浏览器中，追加&quot;HelloWorld&quot;地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="86d2c-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="86d2c-128">(例如，在下面的图`http://localhost:1234/HelloWorld.`) 在浏览器页面将如下所示的以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="86d2c-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="86d2c-129">在上面的方法中，代码直接返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="86d2c-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="86d2c-130">告知系统以仅返回一些 HTML，并且它未 ！</span><span class="sxs-lookup"><span data-stu-id="86d2c-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="86d2c-131">ASP.NET MVC 调用另一个控制器类 （和其中的不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="86d2c-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="86d2c-132">使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码调用：</span><span class="sxs-lookup"><span data-stu-id="86d2c-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="86d2c-133">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="86d2c-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="86d2c-134">因此 */HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="86d2c-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="86d2c-135">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="86d2c-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="86d2c-136">因此 */HelloWorld/索引*将导致`Index`方法`HelloWorldController`类执行。</span><span class="sxs-lookup"><span data-stu-id="86d2c-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="86d2c-137">请注意，我们仅必须浏览到 */HelloWorld*和`Index`时默认情况下使用方法。</span><span class="sxs-lookup"><span data-stu-id="86d2c-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="86d2c-138">这是因为方法名为`Index`是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="86d2c-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="86d2c-139">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="86d2c-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="86d2c-140">`Welcome`方法将运行并返回字符串&quot;这是欢迎操作方法...&quot;.</span><span class="sxs-lookup"><span data-stu-id="86d2c-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="86d2c-141">默认 MVC 映射是`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="86d2c-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="86d2c-142">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="86d2c-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="86d2c-143">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="86d2c-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="86d2c-144">让我们修改该示例略有，以便你可以将某些参数信息从 URL 中传递到控制器 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="86d2c-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="86d2c-145">更改你`Welcome`方法以包括两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="86d2c-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="86d2c-146">请注意，代码将使用 C# 可选参数的功能，则指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。</span><span class="sxs-lookup"><span data-stu-id="86d2c-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="86d2c-147">运行你的应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="86d2c-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="86d2c-148">你可以尝试不同的值`name`和`numtimes`在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="86d2c-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="86d2c-149">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将映射到你的方法中的参数的查询字符串中的地址栏中的命名的参数。</span><span class="sxs-lookup"><span data-stu-id="86d2c-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="86d2c-150">在这些示例中这两个控制器就已开始使用&quot;VC&quot; MVC 部分 — 也就是说，视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="86d2c-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="86d2c-151">控制器直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="86d2c-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="86d2c-152">通常，你不希望直接返回 HTML，因为该按钮将变为非常麻烦的代码的控制器。</span><span class="sxs-lookup"><span data-stu-id="86d2c-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="86d2c-153">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="86d2c-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="86d2c-154">让我们来看如何我们可以执行此操作在下一步。</span><span class="sxs-lookup"><span data-stu-id="86d2c-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86d2c-155">[上一页](intro-to-aspnet-mvc-4.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="86d2c-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
