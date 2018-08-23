---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 简介 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 3dda4701c9be90bea7c95a330845d601345ac46b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834551"
---
<a name="intro-to-aspnet-mvc"></a><span data-ttu-id="8ca87-104">ASP.NET MVC 简介</span><span class="sxs-lookup"><span data-stu-id="8ca87-104">Intro to ASP.NET MVC</span></span>
====================
<span data-ttu-id="8ca87-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="8ca87-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="8ca87-106">如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。</span><span class="sxs-lookup"><span data-stu-id="8ca87-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="8ca87-107">新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="8ca87-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> 
> <span data-ttu-id="8ca87-108">这是介绍 ASP.NET MVC 的基础知识初学者教程。</span><span class="sxs-lookup"><span data-stu-id="8ca87-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="8ca87-109">将创建一个简单的 web 应用程序读取和写入数据库中。</span><span class="sxs-lookup"><span data-stu-id="8ca87-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="8ca87-110">请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="8ca87-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="8ca87-111">让我们第一个 ASP.NET MVC Web 应用程序使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)。</span><span class="sxs-lookup"><span data-stu-id="8ca87-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="8ca87-112">我们将使一些电影列表应用程序，让我们将创建并列出电影。</span><span class="sxs-lookup"><span data-stu-id="8ca87-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="8ca87-113">你将生成</span><span class="sxs-lookup"><span data-stu-id="8ca87-113">What You'll Build</span></span>

<span data-ttu-id="8ca87-114">以下是你将生成的应用程序的两个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="8ca87-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="8ca87-115">必须将影片的各个列的一个简单的表。</span><span class="sxs-lookup"><span data-stu-id="8ca87-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="8ca87-116">[![电影列表-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="8ca87-117">您将得到创建窗体，因此我们可以向列表添加电影。</span><span class="sxs-lookup"><span data-stu-id="8ca87-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="8ca87-118">[![创建电影的 Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="8ca87-119">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="8ca87-119">Skills You'll Learn</span></span>

<span data-ttu-id="8ca87-120">本教程将讲述构建 ASP.NET MVC Web 应用程序使用 Visual Studio 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="8ca87-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="8ca87-121">你将学习：</span><span class="sxs-lookup"><span data-stu-id="8ca87-121">You'll learn:</span></span>

- <span data-ttu-id="8ca87-122">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="8ca87-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="8ca87-123">如何使用 SQL Server 创建一个新的数据库</span><span class="sxs-lookup"><span data-stu-id="8ca87-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="8ca87-124">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="8ca87-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="8ca87-125">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="8ca87-125">How to retrieve and display data</span></span>
- <span data-ttu-id="8ca87-126">如何编辑数据并启用数据验证</span><span class="sxs-lookup"><span data-stu-id="8ca87-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="8ca87-127">如何更新数据库架构</span><span class="sxs-lookup"><span data-stu-id="8ca87-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="8ca87-128">开始操作</span><span class="sxs-lookup"><span data-stu-id="8ca87-128">Get Started</span></span>

<span data-ttu-id="8ca87-129">通过从开始屏幕中运行 Visual Web Developer 2010 速成版 （我将称它"VWD"从现在起），然后选择新的项目启动。</span><span class="sxs-lookup"><span data-stu-id="8ca87-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="8ca87-130">Visual Web Developer 是一个 IDE 或集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="8ca87-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="8ca87-131">就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ca87-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="8ca87-132">没有显示各种可用选项，以及您还可以使用到选择的文件的菜单顶部的工具栏 |新项目。</span><span class="sxs-lookup"><span data-stu-id="8ca87-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="8ca87-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="8ca87-134">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="8ca87-134">Creating Your First Application</span></span>

<span data-ttu-id="8ca87-135">您可以创建使用 Visual Basic 或 Visual C# 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ca87-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="8ca87-136">现在，选择 Visual C# 在左侧，然后选择"ASP.NET MVC 2 Web 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="8ca87-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="8ca87-137">将项目命名为"Movies"并单击确定。</span><span class="sxs-lookup"><span data-stu-id="8ca87-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="8ca87-138">[![新项目](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="8ca87-139">在右侧是解决方案资源管理器在应用程序中显示所有文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="8ca87-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="8ca87-140">在中间的大窗口是编辑你的代码和花费大部分时间的位置。</span><span class="sxs-lookup"><span data-stu-id="8ca87-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="8ca87-141">Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！</span><span class="sxs-lookup"><span data-stu-id="8ca87-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="8ca87-142">这是简单的"Hello World ！</span><span class="sxs-lookup"><span data-stu-id="8ca87-142">This is a simple "Hello World!</span></span> <span data-ttu-id="8ca87-143">项目中，也是如此开始我们的应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="8ca87-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="8ca87-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="8ca87-145">选择工具栏上的"播放"按钮。</span><span class="sxs-lookup"><span data-stu-id="8ca87-145">Select the "play" button to the toolbar.</span></span>

![开始调试](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="8ca87-147">它是一个绿色箭头向右将要编译你的程序和 web 浏览器中启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ca87-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="8ca87-148">*注意： 您可以改为在键盘上按 F5 或选择调试-&gt;从"调试"菜单启动调试。*</span><span class="sxs-lookup"><span data-stu-id="8ca87-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="8ca87-149">这会导致 Visual Web Developer 启动开发 web 服务器并运行 （没有任何配置或启用此功能所需的手动步骤） 的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ca87-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="8ca87-150">然后，它将启动浏览器并将其配置为浏览应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="8ca87-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="8ca87-151">请注意，下面的浏览器地址栏显示"localhost"而不是像 example.com。</span><span class="sxs-lookup"><span data-stu-id="8ca87-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="8ca87-152">这是因为 localhost 始终指向你自己的本地计算机-在这种情况下运行的是我们刚刚构建了应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ca87-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="8ca87-153">[![主页](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="8ca87-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="8ca87-154">在初始状态下此默认模板提供了在两个页面访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="8ca87-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="8ca87-155">让我们更改此应用程序的工作原理，并了解有点 ASP.NET MVC 中的过程。</span><span class="sxs-lookup"><span data-stu-id="8ca87-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="8ca87-156">关闭浏览器并允许更改一些代码。</span><span class="sxs-lookup"><span data-stu-id="8ca87-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8ca87-157">下一篇</span><span class="sxs-lookup"><span data-stu-id="8ca87-157">Next</span></span>](getting-started-with-mvc-part2.md)
