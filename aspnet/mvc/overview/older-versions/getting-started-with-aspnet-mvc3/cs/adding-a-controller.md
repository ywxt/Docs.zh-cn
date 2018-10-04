---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 添加控制器 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express 服务包 1，哪些 i 的 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: bef864829320ae17520adfb4bc49f582013614ce
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576386"
---
<a name="adding-a-controller-c"></a><span data-ttu-id="2490e-103">添加控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="2490e-103">Adding a Controller (C#)</span></span>
====================
<span data-ttu-id="2490e-104">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="2490e-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="2490e-105">本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="2490e-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="2490e-106">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="2490e-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="2490e-107">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="2490e-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="2490e-108">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="2490e-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="2490e-109">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="2490e-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="2490e-110">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="2490e-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="2490e-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="2490e-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="2490e-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="2490e-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="2490e-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="2490e-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="2490e-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="2490e-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="2490e-115">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="2490e-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="2490e-116">[下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="2490e-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="2490e-117">如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="2490e-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="2490e-118">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="2490e-118">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="2490e-119">MVC 是用于开发良好设计且易于维护的应用程序的模式。</span><span class="sxs-lookup"><span data-stu-id="2490e-119">MVC is a pattern for developing applications that are well architected and easy to maintain.</span></span> <span data-ttu-id="2490e-120">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="2490e-120">MVC-based applications contain:</span></span>

- <span data-ttu-id="2490e-121">控制器： 处理应用程序，传入请求的类中检索模型数据，然后指定将响应返回到客户端的视图模板。</span><span class="sxs-lookup"><span data-stu-id="2490e-121">Controllers: Classes that handle incoming requests to the application, retrieve model data, and then specify view templates that return a response to the client.</span></span>
- <span data-ttu-id="2490e-122">模型操作类，表示数据的应用程序和使用验证逻辑以强制实施针对这些数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="2490e-122">Models: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="2490e-123">你的应用程序使用动态生成 HTML 响应的视图： 模板文件。</span><span class="sxs-lookup"><span data-stu-id="2490e-123">Views: Template files that your application uses to dynamically generate HTML responses.</span></span>

<span data-ttu-id="2490e-124">我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="2490e-124">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="2490e-125">让我们首先创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="2490e-125">Let's begin by creating a controller class.</span></span> <span data-ttu-id="2490e-126">在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。</span><span class="sxs-lookup"><span data-stu-id="2490e-126">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

<span data-ttu-id="2490e-127">命名新控制器"HelloWorldController"。</span><span class="sxs-lookup"><span data-stu-id="2490e-127">Name your new controller "HelloWorldController".</span></span> <span data-ttu-id="2490e-128">将保留为默认模板**空控制器**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="2490e-128">Leave the default template as **Empty controller** and click **Add**.</span></span>

<span data-ttu-id="2490e-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2490e-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="2490e-130">请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*。</span><span class="sxs-lookup"><span data-stu-id="2490e-130">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="2490e-131">该文件是在 IDE 中打开。</span><span class="sxs-lookup"><span data-stu-id="2490e-131">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="2490e-132">内部`public class HelloWorldController`块中，创建两个方法，如以下代码所示。</span><span class="sxs-lookup"><span data-stu-id="2490e-132">Inside the `public class HelloWorldController` block, create two methods that look like the following code.</span></span> <span data-ttu-id="2490e-133">控制器将返回 HTML 的字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="2490e-133">The controller will return a string of HTML as an example.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="2490e-134">名为你的控制器`HelloWorldController`和更高版本的第一个方法命名为`Index`。</span><span class="sxs-lookup"><span data-stu-id="2490e-134">Your controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="2490e-135">让我们从浏览器调用它。</span><span class="sxs-lookup"><span data-stu-id="2490e-135">Let's invoke it from a browser.</span></span> <span data-ttu-id="2490e-136">运行应用程序 （按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="2490e-136">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="2490e-137">在浏览器中，将"HelloWorld"追加到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="2490e-137">In the browser, append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="2490e-138">(例如，在图中，其下方的`http://localhost:43246/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2490e-138">(For example, in the illustration below, it's `http://localhost:43246/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="2490e-139">在上述方法中，代码直接返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="2490e-139">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="2490e-140">你告诉系统只返回一些 HTML，并确实执行此操作 ！</span><span class="sxs-lookup"><span data-stu-id="2490e-140">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="2490e-141">ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="2490e-141">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="2490e-142">使用 ASP.NET MVC 的默认映射逻辑使用如下格式来确定哪些代码以调用：</span><span class="sxs-lookup"><span data-stu-id="2490e-142">The default mapping logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="2490e-143">URL 的第一个部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="2490e-143">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="2490e-144">因此 */HelloWorld*映射到`HelloWorldController`类。</span><span class="sxs-lookup"><span data-stu-id="2490e-144">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="2490e-145">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="2490e-145">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="2490e-146">因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。</span><span class="sxs-lookup"><span data-stu-id="2490e-146">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="2490e-147">请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。</span><span class="sxs-lookup"><span data-stu-id="2490e-147">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="2490e-148">这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="2490e-148">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="2490e-149">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="2490e-149">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="2490e-150">`Welcome` 方法运行并返回字符串“这是 Welcome 操作方法...”。</span><span class="sxs-lookup"><span data-stu-id="2490e-150">The `Welcome` method runs and returns the string "This is the Welcome action method...".</span></span> <span data-ttu-id="2490e-151">默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="2490e-151">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="2490e-152">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="2490e-152">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="2490e-153">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="2490e-153">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="2490e-154">让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。</span><span class="sxs-lookup"><span data-stu-id="2490e-154">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="2490e-155">更改你`Welcome`方法以包括两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2490e-155">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="2490e-156">请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。</span><span class="sxs-lookup"><span data-stu-id="2490e-156">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="2490e-157">运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="2490e-157">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="2490e-158">你可以尝试不同的值`name`和`numtimes`在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="2490e-158">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="2490e-159">系统将自动映射到方法中的参数将命名的参数从地址栏中的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="2490e-159">The system automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="2490e-160">在这些示例中这两个控制器始终执行 MVC 的"VC"部分，即，视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="2490e-160">In both these examples the controller has been doing the "VC" portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="2490e-161">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="2490e-161">The controller is returning HTML directly.</span></span> <span data-ttu-id="2490e-162">通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。</span><span class="sxs-lookup"><span data-stu-id="2490e-162">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="2490e-163">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="2490e-163">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="2490e-164">让我们看如何实现这在下一步。</span><span class="sxs-lookup"><span data-stu-id="2490e-164">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2490e-165">[上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="2490e-165">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
