---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) 简介 |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 9b965df6175051a084de35627160161c116be42d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="a56b4-103">ASP.NET MVC 3 (C#) 简介</span><span class="sxs-lookup"><span data-stu-id="a56b4-103">Intro to ASP.NET MVC 3 (C#)</span></span>
====================
<span data-ttu-id="a56b4-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="a56b4-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="a56b4-105">本教程的更新的版本可[此处](../../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="a56b4-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="a56b4-106">它是更安全，请按照要简单得多，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="a56b4-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="a56b4-107">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="a56b4-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="a56b4-108">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="a56b4-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="a56b4-109">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="a56b4-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="a56b4-110">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="a56b4-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="a56b4-111">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="a56b4-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="a56b4-112">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="a56b4-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="a56b4-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="a56b4-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="a56b4-114">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="a56b4-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="a56b4-115">使用 C# 源代码的 Visual Web Developer 项目是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="a56b4-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="a56b4-116">[下载的 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="a56b4-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="a56b4-117">如果你愿意 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="a56b4-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="a56b4-118">你将生成</span><span class="sxs-lookup"><span data-stu-id="a56b4-118">What You'll Build</span></span>

<span data-ttu-id="a56b4-119">你将实现简单的影片列表应用程序支持创建、 编辑和列出数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="a56b4-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="a56b4-120">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="a56b4-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="a56b4-121">它包括一个显示从数据库的影片列表页：</span><span class="sxs-lookup"><span data-stu-id="a56b4-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="a56b4-123">应用程序还可以添加、 编辑和删除电影，以及有关个别权限，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="a56b4-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="a56b4-124">所有数据输入应用场景都包括验证来确保在数据库中存储的数据正确。</span><span class="sxs-lookup"><span data-stu-id="a56b4-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="a56b4-125">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="a56b4-125">Skills You'll Learn</span></span>

<span data-ttu-id="a56b4-126">下面是你将要掌握的内容：</span><span class="sxs-lookup"><span data-stu-id="a56b4-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="a56b4-127">如何创建新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="a56b4-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="a56b4-128">如何创建 ASP.NET MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="a56b4-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="a56b4-129">如何创建新的数据库使用 Entity Framework Code First 范例。</span><span class="sxs-lookup"><span data-stu-id="a56b4-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="a56b4-130">如何检索和显示数据。</span><span class="sxs-lookup"><span data-stu-id="a56b4-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="a56b4-131">如何编辑数据并启用数据验证。</span><span class="sxs-lookup"><span data-stu-id="a56b4-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a56b4-132">入门</span><span class="sxs-lookup"><span data-stu-id="a56b4-132">Getting Started</span></span>

<span data-ttu-id="a56b4-133">通过运行 Visual Web Developer 2010 Express ("Visual Web Developer"简称) 启动，然后选择**新项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="a56b4-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="a56b4-134">Visual Web Developer 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="a56b4-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="a56b4-135">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56b4-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="a56b4-136">在 Visual Web Developer 是向你显示各个可用的选项顶部的工具栏。</span><span class="sxs-lookup"><span data-stu-id="a56b4-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="a56b4-137">此外还有一个菜单，提供另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="a56b4-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="a56b4-138">(例如，而不是选择**新项目**从**启动**页上，你可以使用菜单并选择**文件** &gt; **新项目**.)</span><span class="sxs-lookup"><span data-stu-id="a56b4-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="a56b4-139">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="a56b4-139">Creating Your First Application</span></span>

<span data-ttu-id="a56b4-140">你可以创建使用 Visual Basic 或 Visual C# 作为编程语言的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56b4-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="a56b4-141">选择 Visual C# 在左侧，然后选择**ASP.NET MVC 3 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a56b4-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="a56b4-142">将你的项目"MvcMovie"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a56b4-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="a56b4-143">(如果你愿意 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。)</span><span class="sxs-lookup"><span data-stu-id="a56b4-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="a56b4-144">在**新建 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a56b4-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="a56b4-145">检查**使用 HTML5 标记**并使**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="a56b4-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="a56b4-146">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="a56b4-146">Click **OK**.</span></span> <span data-ttu-id="a56b4-147">因此，必须运行的应用程序现在不执行任何操作的情况下，visual Web Developer 刚创建的 ASP.NET MVC 项目使用默认模板 ！</span><span class="sxs-lookup"><span data-stu-id="a56b4-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="a56b4-148">这是简单"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="a56b4-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="a56b4-149">项目和它的启动你的应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="a56b4-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="a56b4-150">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="a56b4-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="a56b4-151">请注意，键盘快捷方式启动调试 F5。</span><span class="sxs-lookup"><span data-stu-id="a56b4-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="a56b4-152">F5 会导致 Visual Web Developer 启动开发 web 服务器并运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56b4-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="a56b4-153">然后，visual Web Developer 将启动浏览器，并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="a56b4-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="a56b4-154">请注意，浏览器的地址栏显示`localhost`和不类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="a56b4-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="a56b4-155">这是因为`localhost`始终指向你自己本地的计算机，在这种情况下运行你刚才生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="a56b4-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="a56b4-156">当 Visual Web Developer 运行 web 项目时，随机端口适用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="a56b4-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="a56b4-157">在下图中，随机端口号是 43246。</span><span class="sxs-lookup"><span data-stu-id="a56b4-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="a56b4-158">运行应用程序时，你将可能看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="a56b4-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="a56b4-159">现成此默认模板提供两个页面访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="a56b4-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="a56b4-160">下一步是更改此应用程序的工作原理，并了解得有点 ASP.NET MVC 在进程中。</span><span class="sxs-lookup"><span data-stu-id="a56b4-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="a56b4-161">关闭你的浏览器并让我们更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="a56b4-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a56b4-162">下一篇</span><span class="sxs-lookup"><span data-stu-id="a56b4-162">Next</span></span>](adding-a-controller.md)
