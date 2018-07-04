---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) 简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: d4cda748638a6396750fe2ef7713dd0b2a4555d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379856"
---
<a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="9cc79-103">ASP.NET MVC 3 (C#) 简介</span><span class="sxs-lookup"><span data-stu-id="9cc79-103">Intro to ASP.NET MVC 3 (C#)</span></span>
====================
<span data-ttu-id="9cc79-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="9cc79-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="9cc79-105">本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="9cc79-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="9cc79-106">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="9cc79-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="9cc79-107">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="9cc79-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="9cc79-108">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="9cc79-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="9cc79-109">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="9cc79-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="9cc79-110">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="9cc79-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="9cc79-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="9cc79-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="9cc79-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="9cc79-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="9cc79-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="9cc79-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="9cc79-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="9cc79-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="9cc79-115">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="9cc79-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="9cc79-116">[下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="9cc79-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="9cc79-117">如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="9cc79-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="9cc79-118">你将生成</span><span class="sxs-lookup"><span data-stu-id="9cc79-118">What You'll Build</span></span>

<span data-ttu-id="9cc79-119">将实现一个简单的电影列表应用程序支持创建、 编辑和列出数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="9cc79-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="9cc79-120">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="9cc79-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="9cc79-121">它包括显示的数据库中的电影列表的页面：</span><span class="sxs-lookup"><span data-stu-id="9cc79-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="9cc79-123">应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="9cc79-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="9cc79-124">所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。</span><span class="sxs-lookup"><span data-stu-id="9cc79-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="9cc79-125">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="9cc79-125">Skills You'll Learn</span></span>

<span data-ttu-id="9cc79-126">下面是你将了解：</span><span class="sxs-lookup"><span data-stu-id="9cc79-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="9cc79-127">如何创建一个新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="9cc79-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="9cc79-128">如何创建 ASP.NET MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="9cc79-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="9cc79-129">如何创建新的数据库使用 Entity Framework Code First 范例。</span><span class="sxs-lookup"><span data-stu-id="9cc79-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="9cc79-130">如何检索和显示数据。</span><span class="sxs-lookup"><span data-stu-id="9cc79-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="9cc79-131">了解如何编辑数据并启用数据验证。</span><span class="sxs-lookup"><span data-stu-id="9cc79-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9cc79-132">入门</span><span class="sxs-lookup"><span data-stu-id="9cc79-132">Getting Started</span></span>

<span data-ttu-id="9cc79-133">首先运行 Visual Web Developer 2010 速成版 ("Visual Web Developer"简称)，然后选择**新的项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="9cc79-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="9cc79-134">Visual Web Developer 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="9cc79-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="9cc79-135">就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="9cc79-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="9cc79-136">在 Visual Web Developer 是向您显示各种可用选项顶部的工具栏。</span><span class="sxs-lookup"><span data-stu-id="9cc79-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="9cc79-137">此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="9cc79-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="9cc79-138">(例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)</span><span class="sxs-lookup"><span data-stu-id="9cc79-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="9cc79-139">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="9cc79-139">Creating Your First Application</span></span>

<span data-ttu-id="9cc79-140">您可以创建使用 Visual Basic 或 Visual C# 作为编程语言的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9cc79-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="9cc79-141">选择 Visual C# 在左侧，然后选择**ASP.NET MVC 3 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="9cc79-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="9cc79-142">命名你的项目"MvcMovie"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="9cc79-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="9cc79-143">(如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。)</span><span class="sxs-lookup"><span data-stu-id="9cc79-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="9cc79-144">在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="9cc79-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="9cc79-145">检查**使用 HTML5 标记**并保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9cc79-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="9cc79-146">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="9cc79-146">Click **OK**.</span></span> <span data-ttu-id="9cc79-147">Visual Web Developer 中刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！</span><span class="sxs-lookup"><span data-stu-id="9cc79-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="9cc79-148">这是简单"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="9cc79-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="9cc79-149">项目和它的启动应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="9cc79-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="9cc79-150">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="9cc79-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="9cc79-151">请注意，若要开始调试的键盘快捷键 F5。</span><span class="sxs-lookup"><span data-stu-id="9cc79-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="9cc79-152">F5 会导致 Visual Web Developer 才能启动开发 web 服务器和运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9cc79-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="9cc79-153">然后，visual Web Developer 启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="9cc79-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="9cc79-154">请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="9cc79-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="9cc79-155">这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="9cc79-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="9cc79-156">Visual Web Developer 运行时 web 项目，一个随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9cc79-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="9cc79-157">下图中的随机端口号是 43246。</span><span class="sxs-lookup"><span data-stu-id="9cc79-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="9cc79-158">当您运行该应用程序时，您可能看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="9cc79-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="9cc79-159">即时可用的此默认模板提供两个页面访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="9cc79-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="9cc79-160">下一步是更改此应用程序的工作原理和了解有点 ASP.NET MVC 中的过程。</span><span class="sxs-lookup"><span data-stu-id="9cc79-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="9cc79-161">关闭浏览器并让我们更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="9cc79-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9cc79-162">下一篇</span><span class="sxs-lookup"><span data-stu-id="9cc79-162">Next</span></span>](adding-a-controller.md)
