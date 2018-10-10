---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 添加控制器 |Microsoft Docs
author: shanselman
description: 如果本教程是此处使用 Visual Studio 2013 提供更新的版本。 新教程使用 ASP.NET MVC 5，可获得许多改进通过 t...
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: 9a8ecac5203234c140783bbe3a518d35f6a57675
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910773"
---
<a name="adding-a-controller"></a><span data-ttu-id="4354d-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="4354d-104">Adding a Controller</span></span>
====================
<span data-ttu-id="4354d-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4354d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="4354d-106">如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)。</span><span class="sxs-lookup"><span data-stu-id="4354d-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="4354d-107">新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="4354d-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="4354d-108">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="4354d-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4354d-109">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="4354d-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4354d-110">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="4354d-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="4354d-111">MVC 代表模型、 视图、 控制器。</span><span class="sxs-lookup"><span data-stu-id="4354d-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="4354d-112">MVC 是一种模式用于开发应用程序，从而使每个部分具有不同于另一个是责任。</span><span class="sxs-lookup"><span data-stu-id="4354d-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="4354d-113">数据的应用程序模型：</span><span class="sxs-lookup"><span data-stu-id="4354d-113">Model: The data of your application</span></span>
- <span data-ttu-id="4354d-114">视图： 应用程序将使用动态生成 HTML 响应模板文件。</span><span class="sxs-lookup"><span data-stu-id="4354d-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="4354d-115">控制器： 处理应用程序，传入 URL 请求的类中检索模型数据，然后指定将响应返回给客户端呈现的视图模板</span><span class="sxs-lookup"><span data-stu-id="4354d-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="4354d-116">我们将在本教程中介绍所有这些概念并说明如何使用它们来构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="4354d-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="4354d-117">右键单击解决方案资源管理器中的 controllers 文件夹并选择添加控制器，让我们创建一个新的控制器。</span><span class="sxs-lookup"><span data-stu-id="4354d-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="4354d-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4354d-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="4354d-119">新控制器"HelloWorldController"命名，并单击添加。</span><span class="sxs-lookup"><span data-stu-id="4354d-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="4354d-120">[![添加控制器对话框](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4354d-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="4354d-121">请注意，在解决方案资源管理器中，已为您调用 HelloWorldController.cs 创建一个新文件并在现在打开该文件在右侧**IDE**。</span><span class="sxs-lookup"><span data-stu-id="4354d-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="4354d-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4354d-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="4354d-123">创建在您的新公共类 HelloWorldController 如下所示的两个新方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="4354d-124">作为示例，我们将直接从控制器返回 HTML 的字符串。</span><span class="sxs-lookup"><span data-stu-id="4354d-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="4354d-125">将控制器命名为 HelloWorldController 和新方法调用索引。</span><span class="sxs-lookup"><span data-stu-id="4354d-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="4354d-126">在再次运行应用程序，可以像以前一样 （单击播放按钮或按 f5 键以执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="4354d-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="4354d-127">一旦你的浏览器已启动，更改到的地址栏中的路径`http://localhost:xx/HelloWorld`其中 xx 是任何数字在计算机已选。</span><span class="sxs-lookup"><span data-stu-id="4354d-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="4354d-128">现在你的浏览器应如下面的屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="4354d-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="4354d-129">我们在上面我们方法返回的字符串传递到一个名为"内容"。 方法</span><span class="sxs-lookup"><span data-stu-id="4354d-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="4354d-130">我们告诉过系统只返回一些 HTML，并确实执行此操作 ！</span><span class="sxs-lookup"><span data-stu-id="4354d-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="4354d-131">ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。</span><span class="sxs-lookup"><span data-stu-id="4354d-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="4354d-132">使用 ASP.NET MVC 的默认映射逻辑使用如下格式来控制运行的代码：</span><span class="sxs-lookup"><span data-stu-id="4354d-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="4354d-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="4354d-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="4354d-134">URL 的第一个部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="4354d-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="4354d-135">因此 /HelloWorld 将映射到 HelloWorldController 类。</span><span class="sxs-lookup"><span data-stu-id="4354d-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="4354d-136">URL 的第二部分确定要执行的类上的操作方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="4354d-137">/HelloWorld/Index 时会导致 HelloWorldcontroller 类执行的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldcontroller class to execute.</span></span> <span data-ttu-id="4354d-138">请注意，我们只需要访问上述 /HelloWorld 和表示为索引的方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="4354d-139">这是因为名为"Index"的方法是如果有一个未显式指定调用在控制器的默认方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="4354d-140">[![这是我的默认操作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4354d-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="4354d-141">现在，我们来访问`http://localhost:xx/HelloWorld/Welcome.`现在我们的欢迎使用方法已执行并返回其 HTML 字符串。</span><span class="sxs-lookup"><span data-stu-id="4354d-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="4354d-142">同样，/ [Controller] / [ActionName] / [参数]，因此控制器是 HelloWorld，欢迎在这种情况下是该方法。</span><span class="sxs-lookup"><span data-stu-id="4354d-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="4354d-143">我们还没有这样的参数。</span><span class="sxs-lookup"><span data-stu-id="4354d-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="4354d-144">[![这是 Welcome 操作方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4354d-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="4354d-145">让我们这样我们可以将中的一些信息从 URL 中传递给我们的控制器，例如如下稍微修改一下我们的示例: / HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4。</span><span class="sxs-lookup"><span data-stu-id="4354d-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="4354d-146">更改欢迎使用方法，以包括两个参数和与下面类似的更新。</span><span class="sxs-lookup"><span data-stu-id="4354d-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="4354d-147">请注意，我们已使用 C# 可选参数功能指示是否它未传入参数 numTimes 应默认为 1。</span><span class="sxs-lookup"><span data-stu-id="4354d-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="4354d-148">运行应用程序并访问`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`根据需要更改名称和 numtimes 的值。</span><span class="sxs-lookup"><span data-stu-id="4354d-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="4354d-149">系统会自动映射到方法中的参数将命名的参数从查询字符串的地址栏中。</span><span class="sxs-lookup"><span data-stu-id="4354d-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="4354d-150">在这些示例中这两个控制器已执行所有操作，并具有已直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="4354d-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="4354d-151">通常我们不希望我们控制器直接-返回 HTML，因为结束的代码非常繁琐。</span><span class="sxs-lookup"><span data-stu-id="4354d-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="4354d-152">而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="4354d-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="4354d-153">让我们看看如何我们可以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="4354d-153">Let's look at how we can do this.</span></span> <span data-ttu-id="4354d-154">关闭浏览器并返回到 IDE。</span><span class="sxs-lookup"><span data-stu-id="4354d-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4354d-155">[上一页](getting-started-with-mvc-part1.md)
> [下一页](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="4354d-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
