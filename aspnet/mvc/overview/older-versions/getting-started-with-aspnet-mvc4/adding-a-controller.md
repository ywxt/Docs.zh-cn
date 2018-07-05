---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 100f5623bafa33548f9c979e98765c92327eb369
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373284"
---
<a name="adding-a-controller"></a><span data-ttu-id="4b685-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="4b685-104">Adding a Controller</span></span>
====================
<span data-ttu-id="4b685-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="4b685-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="4b685-106">本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="4b685-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="4b685-107">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="4b685-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="4b685-108">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="4b685-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="4b685-109">MVC 是一种模式用于开发应用程序也设计、 可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="4b685-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="4b685-110">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="4b685-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="4b685-111">**M**模式： 类，表示数据的应用程序和使用验证逻辑以强制实施针对这些数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="4b685-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="4b685-112">**V**视图： 应用程序使用动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="4b685-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="4b685-113">**C**控制器： 处理传入的浏览器请求的类中检索模型数据，然后指定将响应返回到浏览器的视图模板。</span><span class="sxs-lookup"><span data-stu-id="4b685-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="4b685-114">我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="4b685-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="4b685-115">让我们首先创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="4b685-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="4b685-116">在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。</span><span class="sxs-lookup"><span data-stu-id="4b685-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="4b685-117">新控制器命名&quot;HelloWorldController&quot;。</span><span class="sxs-lookup"><span data-stu-id="4b685-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="4b685-118">将保留为默认模板**空 MVC 控制器**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="4b685-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image2.png)

<span data-ttu-id="4b685-120">请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*。</span><span class="sxs-lookup"><span data-stu-id="4b685-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="4b685-121">该文件是在 IDE 中打开。</span><span class="sxs-lookup"><span data-stu-id="4b685-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="4b685-122">将以下代码替换为该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="4b685-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="4b685-123">控制器方法将返回 HTML 的字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="4b685-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="4b685-124">控制器被命名为`HelloWorldController`和更高版本的第一个方法命名为`Index`。</span><span class="sxs-lookup"><span data-stu-id="4b685-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="4b685-125">让我们从浏览器调用它。</span><span class="sxs-lookup"><span data-stu-id="4b685-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="4b685-126">运行应用程序 （按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="4b685-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="4b685-127">在浏览器中，追加&quot;HelloWorld&quot;到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="4b685-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="4b685-128">(例如，在图中，其下方的`http://localhost:1234/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4b685-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="4b685-129">在上述方法中，代码直接返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="4b685-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="4b685-130">你告诉系统只返回一些 HTML，并确实执行此操作 ！</span><span class="sxs-lookup"><span data-stu-id="4b685-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="4b685-131">ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="4b685-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="4b685-132">使用 ASP.NET MVC 的默认 URL 路由逻辑使用如下格式来确定哪些代码以调用：</span><span class="sxs-lookup"><span data-stu-id="4b685-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="4b685-133">URL 的第一个部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="4b685-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="4b685-134">因此 */HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="4b685-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="4b685-135">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="4b685-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="4b685-136">因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。</span><span class="sxs-lookup"><span data-stu-id="4b685-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="4b685-137">请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。</span><span class="sxs-lookup"><span data-stu-id="4b685-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="4b685-138">这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="4b685-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="4b685-139">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="4b685-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="4b685-140">`Welcome`方法运行并返回字符串&quot;这是 Welcome 操作方法...&quot;.</span><span class="sxs-lookup"><span data-stu-id="4b685-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="4b685-141">默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="4b685-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="4b685-142">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="4b685-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="4b685-143">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="4b685-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="4b685-144">让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="4b685-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="4b685-145">更改你`Welcome`方法以包括两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4b685-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="4b685-146">请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。</span><span class="sxs-lookup"><span data-stu-id="4b685-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="4b685-147">运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="4b685-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="4b685-148">你可以尝试不同的值`name`和`numtimes`在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="4b685-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="4b685-149">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)会自动将映射到方法中的参数将命名的参数从地址栏中的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="4b685-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="4b685-150">在这些示例中这两个控制器始终执行&quot;VC&quot;的 MVC 部分 — 即，视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="4b685-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="4b685-151">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="4b685-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="4b685-152">通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。</span><span class="sxs-lookup"><span data-stu-id="4b685-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="4b685-153">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="4b685-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="4b685-154">让我们看如何实现这在下一步。</span><span class="sxs-lookup"><span data-stu-id="4b685-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4b685-155">[上一页](intro-to-aspnet-mvc-4.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="4b685-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
