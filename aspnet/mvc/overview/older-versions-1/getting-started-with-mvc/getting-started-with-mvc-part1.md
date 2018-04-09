---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 简介 |Microsoft 文档
author: shanselman
description: 这是初学者本教程介绍 ASP.NET MVC 的基础知识。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 476d832e389b9b5a26fe2d552ca648c79b100056
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="intro-to-aspnet-mvc"></a><span data-ttu-id="47ce8-104">ASP.NET MVC 简介</span><span class="sxs-lookup"><span data-stu-id="47ce8-104">Intro to ASP.NET MVC</span></span>
====================
<span data-ttu-id="47ce8-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="47ce8-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="47ce8-106">本教程中是否可用的更新的版本[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。</span><span class="sxs-lookup"><span data-stu-id="47ce8-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="47ce8-107">新的教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="47ce8-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> 
> <span data-ttu-id="47ce8-108">这是初学者本教程介绍 ASP.NET MVC 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="47ce8-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="47ce8-109">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="47ce8-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="47ce8-110">请访问[ASP.NET MVC 学习中心](../../../index.md)若要查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="47ce8-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="47ce8-111">让我们来制作我们第一个 ASP.NET MVC Web 应用程序使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)。</span><span class="sxs-lookup"><span data-stu-id="47ce8-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="47ce8-112">我们将使少量影片列表应用程序，让我们将创建并列出电影。</span><span class="sxs-lookup"><span data-stu-id="47ce8-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="47ce8-113">你将生成</span><span class="sxs-lookup"><span data-stu-id="47ce8-113">What You'll Build</span></span>

<span data-ttu-id="47ce8-114">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="47ce8-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="47ce8-115">你将有一个简单表的影片的各个列。</span><span class="sxs-lookup"><span data-stu-id="47ce8-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="47ce8-116">[![影片列表-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="47ce8-117">然后就可以创建的窗体以便我们可以将电影添加到列表。</span><span class="sxs-lookup"><span data-stu-id="47ce8-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="47ce8-118">[![创建电影-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="47ce8-119">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="47ce8-119">Skills You'll Learn</span></span>

<span data-ttu-id="47ce8-120">本教程将教您生成使用 Visual Studio ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="47ce8-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="47ce8-121">你将学习：</span><span class="sxs-lookup"><span data-stu-id="47ce8-121">You'll learn:</span></span>

- <span data-ttu-id="47ce8-122">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="47ce8-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="47ce8-123">如何使用 SQL Server 创建新数据库</span><span class="sxs-lookup"><span data-stu-id="47ce8-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="47ce8-124">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="47ce8-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="47ce8-125">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="47ce8-125">How to retrieve and display data</span></span>
- <span data-ttu-id="47ce8-126">如何编辑数据并启用数据验证</span><span class="sxs-lookup"><span data-stu-id="47ce8-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="47ce8-127">如何更新数据库架构</span><span class="sxs-lookup"><span data-stu-id="47ce8-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="47ce8-128">开始操作</span><span class="sxs-lookup"><span data-stu-id="47ce8-128">Get Started</span></span>

<span data-ttu-id="47ce8-129">通过从开始屏幕中运行 Visual Web Developer 2010 Express （我将称它"VWD"从现在起），然后选择新项目启动。</span><span class="sxs-lookup"><span data-stu-id="47ce8-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="47ce8-130">Visual Web Developer 是一个 IDE 或集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="47ce8-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="47ce8-131">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="47ce8-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="47ce8-132">没有到你，以及你也可能使用了到选择的文件的菜单显示各个可用的选项顶部工具栏 |新项目。</span><span class="sxs-lookup"><span data-stu-id="47ce8-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="47ce8-133">[![Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="47ce8-134">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="47ce8-134">Creating Your First Application</span></span>

<span data-ttu-id="47ce8-135">你可以创建使用 Visual Basic 或 Visual C# 应用程序。</span><span class="sxs-lookup"><span data-stu-id="47ce8-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="47ce8-136">现在，选择 Visual C# 在左侧，然后选择"ASP.NET MVC 2 Web 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="47ce8-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="47ce8-137">将你的项目"电影"，然后单击确定。</span><span class="sxs-lookup"><span data-stu-id="47ce8-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="47ce8-138">[![新项目](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="47ce8-139">在右侧是应用程序中显示所有文件和文件夹解决方案资源管理器。</span><span class="sxs-lookup"><span data-stu-id="47ce8-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="47ce8-140">在中间的大窗口是你在其中编辑你的代码并花费大部分时间。</span><span class="sxs-lookup"><span data-stu-id="47ce8-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="47ce8-141">因此，必须运行的应用程序现在不执行任何操作的情况下，visual Studio 刚创建的 ASP.NET MVC 项目使用默认模板 ！</span><span class="sxs-lookup"><span data-stu-id="47ce8-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="47ce8-142">这是简单的"Hello World ！</span><span class="sxs-lookup"><span data-stu-id="47ce8-142">This is a simple "Hello World!</span></span> <span data-ttu-id="47ce8-143">项目，然后它是为我们的应用程序启动的好时机。</span><span class="sxs-lookup"><span data-stu-id="47ce8-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="47ce8-144">[![Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="47ce8-145">选择到工具栏的"播放"按钮。</span><span class="sxs-lookup"><span data-stu-id="47ce8-145">Select the "play" button to the toolbar.</span></span>

![开始调试](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="47ce8-147">它是指向将编译你的程序并在 web 浏览器中启动你的应用程序的权限的绿色箭头。</span><span class="sxs-lookup"><span data-stu-id="47ce8-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="47ce8-148">*注意： 你可以改为按你键盘上的 f5 键或选择调试-&gt;从"调试"菜单开始调试。*</span><span class="sxs-lookup"><span data-stu-id="47ce8-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="47ce8-149">这将导致 Visual Web Developer 启动开发 web 服务器并运行 web 应用程序 （没有任何配置或手动启用此功能所需的步骤）。</span><span class="sxs-lookup"><span data-stu-id="47ce8-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="47ce8-150">然后，它将启动浏览器，并将其配置为浏览应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="47ce8-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="47ce8-151">注意下面，浏览器地址栏将显示为"localhost"，并不类似 example.com。这是因为 localhost 始终指向你自己的本地计算机-在这种情况下运行我们刚生成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="47ce8-151">Notice below that the address bar of the browser says "localhost", and not something like example.com. That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="47ce8-152">[![主页](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="47ce8-152">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="47ce8-153">现成的此默认模板提供了您这两页访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="47ce8-153">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="47ce8-154">让我们更改此应用程序的工作原理，并了解得有点 ASP.NET MVC 在进程中。</span><span class="sxs-lookup"><span data-stu-id="47ce8-154">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="47ce8-155">关闭浏览器，并允许更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="47ce8-155">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="47ce8-156">下一篇</span><span class="sxs-lookup"><span data-stu-id="47ce8-156">Next</span></span>](getting-started-with-mvc-part2.md)
