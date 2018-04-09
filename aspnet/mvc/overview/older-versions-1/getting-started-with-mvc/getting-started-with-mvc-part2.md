---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 添加控制器 |Microsoft 文档
author: shanselman
description: 如果本教程可在此处使用 Visual Studio 2013 更新的版本。 新的教程使用 ASP.NET MVC 5，基础上 t 提供了许多改进...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: c6ecd1ffdd53a629d0079d57b85c7f6db2f316ce
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-controller"></a><span data-ttu-id="3f12a-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="3f12a-104">Adding a Controller</span></span>
====================
<span data-ttu-id="3f12a-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="3f12a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="3f12a-106">本教程中是否可用的更新的版本[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。</span><span class="sxs-lookup"><span data-stu-id="3f12a-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="3f12a-107">新的教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="3f12a-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> 
> <span data-ttu-id="3f12a-108">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3f12a-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="3f12a-109">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="3f12a-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="3f12a-110">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="3f12a-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="3f12a-111">MVC 代表模型、 视图、 控制器。</span><span class="sxs-lookup"><span data-stu-id="3f12a-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="3f12a-112">MVC 是模式，用于开发应用程序，以便每个部分是不同于其他责任。</span><span class="sxs-lookup"><span data-stu-id="3f12a-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="3f12a-113">模型： 你的应用程序的数据</span><span class="sxs-lookup"><span data-stu-id="3f12a-113">Model: The data of your application</span></span>
- <span data-ttu-id="3f12a-114">视图： 你的应用程序将使用动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="3f12a-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="3f12a-115">控制器： 处理应用程序，传入 URL 请求的类中检索模型数据，，然后指定呈现响应发回客户端的视图模板</span><span class="sxs-lookup"><span data-stu-id="3f12a-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="3f12a-116">我们将涵盖所有这些概念，在本教程中，向您展示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f12a-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="3f12a-117">右键单击解决方案资源管理器中的 controllers 文件夹并选择添加控制器，让我们创建一个新的控制器。</span><span class="sxs-lookup"><span data-stu-id="3f12a-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="3f12a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3f12a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="3f12a-119">将你新控制器"HelloWorldController"，然后单击添加。</span><span class="sxs-lookup"><span data-stu-id="3f12a-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="3f12a-120">[![添加控制器对话框](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3f12a-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="3f12a-121">请注意，在右侧，已为您调用 HelloWorldController.cs 创建了一个新的文件现在在中打开该文件的解决方案资源管理器**IDE**。</span><span class="sxs-lookup"><span data-stu-id="3f12a-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="3f12a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="3f12a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="3f12a-123">创建在您的新公共类 HelloWorldController 内部如下所示的两个新方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="3f12a-124">作为示例，我们将直接从我们控制器返回 HTML 的字符串。</span><span class="sxs-lookup"><span data-stu-id="3f12a-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="3f12a-125">你的控制器名为 HelloWorldController 且新方法调用索引。</span><span class="sxs-lookup"><span data-stu-id="3f12a-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="3f12a-126">你再次运行应用程序，像以前一样 （单击播放按钮或按 f5 键以执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="3f12a-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="3f12a-127">一旦你的浏览器已启动，更改到的地址栏中的路径`http://localhost:xx/HelloWorld`其中，xx 是任何数字你的计算机已选。</span><span class="sxs-lookup"><span data-stu-id="3f12a-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="3f12a-128">现在你的浏览器应类似下面的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3f12a-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="3f12a-129">我们在上面我们方法返回到一种称为"内容"。 方法传递的字符串</span><span class="sxs-lookup"><span data-stu-id="3f12a-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="3f12a-130">系统只返回一些 HTML，并且它未通知我们 ！</span><span class="sxs-lookup"><span data-stu-id="3f12a-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="3f12a-131">ASP.NET MVC 调用不同的控制器类 （和其中的不同操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="3f12a-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="3f12a-132">使用 ASP.NET MVC 的默认映射逻辑使用如下格式来控制运行哪些代码：</span><span class="sxs-lookup"><span data-stu-id="3f12a-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="3f12a-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="3f12a-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="3f12a-134">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="3f12a-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="3f12a-135">因此 /HelloWorld 将映射到 HelloWorldController 类。</span><span class="sxs-lookup"><span data-stu-id="3f12a-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="3f12a-136">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="3f12a-137">因此 /HelloWorld/Index 可能会导致要执行的 HelloWorldcontroller 类的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldcontroller class to execute.</span></span> <span data-ttu-id="3f12a-138">请注意，我们仅必须访问 /HelloWorld 上述和索引已隐式的方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="3f12a-139">这是因为名为"Index"的方法是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="3f12a-140">[![这是我的默认操作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3f12a-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="3f12a-141">现在，让我们访问`http://localhost:xx/HelloWorld/Welcome.`现在我们欢迎方法已执行并返回其 HTML 字符串。</span><span class="sxs-lookup"><span data-stu-id="3f12a-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="3f12a-142">同样，/ [控制器] / [ActionName] / [参数] 因此控制器是 HelloWorld，欢迎在这种情况下是方法。</span><span class="sxs-lookup"><span data-stu-id="3f12a-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="3f12a-143">我们尚未将参数执行操作。</span><span class="sxs-lookup"><span data-stu-id="3f12a-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="3f12a-144">[![这是欢迎操作方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3f12a-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="3f12a-145">让我们，以便我们可以将中的一些信息从 URL 中传递给我们控制器，例如如下所示稍微修改我们的示例: / HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4。</span><span class="sxs-lookup"><span data-stu-id="3f12a-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="3f12a-146">更改欢迎方法，以包括两个参数和与下面类似的更新。</span><span class="sxs-lookup"><span data-stu-id="3f12a-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="3f12a-147">请注意，我们使用了 C# 可选参数功能来指示是否它未传入参数 numTimes 应默认为 1。</span><span class="sxs-lookup"><span data-stu-id="3f12a-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="3f12a-148">运行你的应用程序并访问`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`根据需要更改名称和 numtimes 的值。</span><span class="sxs-lookup"><span data-stu-id="3f12a-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="3f12a-149">系统会自动映射到你的方法中的参数来自你的地址栏中的查询字符串的命名的参数。</span><span class="sxs-lookup"><span data-stu-id="3f12a-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="3f12a-150">在这些示例中这两个控制器已被执行所有工作，并具有已直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="3f12a-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="3f12a-151">通常，我们不希望我们控制器直接-返回 HTML，因为将非常难以代码结束。</span><span class="sxs-lookup"><span data-stu-id="3f12a-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="3f12a-152">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="3f12a-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="3f12a-153">让我们看一下如何我们可以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3f12a-153">Let's look at how we can do this.</span></span> <span data-ttu-id="3f12a-154">关闭你的浏览器并返回到 IDE。</span><span class="sxs-lookup"><span data-stu-id="3f12a-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3f12a-155">[上一页](getting-started-with-mvc-part1.md)
> [下一页](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="3f12a-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
