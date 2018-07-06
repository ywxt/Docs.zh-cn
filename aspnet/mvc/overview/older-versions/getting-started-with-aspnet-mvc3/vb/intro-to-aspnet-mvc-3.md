---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (VB) 简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 66e267642adabac9a4b4c724b06dc2658ff0ea42
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828012"
---
<a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="0c1da-103">ASP.NET MVC 3 (VB) 简介</span><span class="sxs-lookup"><span data-stu-id="0c1da-103">Intro to ASP.NET MVC 3 (VB)</span></span>
====================
<span data-ttu-id="0c1da-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="0c1da-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="0c1da-105">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="0c1da-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="0c1da-106">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="0c1da-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="0c1da-107">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="0c1da-108">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="0c1da-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="0c1da-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="0c1da-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="0c1da-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="0c1da-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="0c1da-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="0c1da-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="0c1da-112">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="0c1da-113">可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="0c1da-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="0c1da-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="0c1da-115">如果您愿意 C#，切换到[C# 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="0c1da-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="0c1da-116">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="0c1da-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="0c1da-117">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="0c1da-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="0c1da-118">可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="0c1da-119">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="0c1da-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="0c1da-120">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="0c1da-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="0c1da-121">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="0c1da-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="0c1da-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="0c1da-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="0c1da-123">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="0c1da-124">可随附于此项目具有 VB 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="0c1da-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="0c1da-125">[下载的 VB 版本](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。</span><span class="sxs-lookup"><span data-stu-id="0c1da-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="0c1da-126">如果您愿意 CSharp，切换到[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="0c1da-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="0c1da-127">你将生成</span><span class="sxs-lookup"><span data-stu-id="0c1da-127">What You'll Build</span></span>

<span data-ttu-id="0c1da-128">将实现一个简单的电影列表应用程序支持创建、 编辑和列出数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="0c1da-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="0c1da-129">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="0c1da-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="0c1da-130">它包括显示的数据库中的电影列表的页面：</span><span class="sxs-lookup"><span data-stu-id="0c1da-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="0c1da-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0c1da-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="0c1da-132">应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="0c1da-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="0c1da-133">所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。</span><span class="sxs-lookup"><span data-stu-id="0c1da-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="0c1da-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0c1da-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="0c1da-135">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="0c1da-135">Skills You'll Learn</span></span>

<span data-ttu-id="0c1da-136">下面是你将了解：</span><span class="sxs-lookup"><span data-stu-id="0c1da-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="0c1da-137">如何创建一个新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="0c1da-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="0c1da-138">如何创建使用 Entity Framework 代码优先的新数据库</span><span class="sxs-lookup"><span data-stu-id="0c1da-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="0c1da-139">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="0c1da-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="0c1da-140">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="0c1da-140">How to retrieve and display data</span></span>
- <span data-ttu-id="0c1da-141">如何编辑数据并启用数据验证</span><span class="sxs-lookup"><span data-stu-id="0c1da-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="0c1da-142">入门</span><span class="sxs-lookup"><span data-stu-id="0c1da-142">Getting Started</span></span>

<span data-ttu-id="0c1da-143">首先运行 Visual Web Developer 2010 速成版 (简称的"VWD")，然后选择**新的项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="0c1da-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="0c1da-144">Visual Web Developer 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="0c1da-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="0c1da-145">就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c1da-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="0c1da-146">在 Visual Web Developer 是向您显示各种可用选项顶部的工具栏。</span><span class="sxs-lookup"><span data-stu-id="0c1da-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="0c1da-147">此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="0c1da-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="0c1da-148">(例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)</span><span class="sxs-lookup"><span data-stu-id="0c1da-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="0c1da-149">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="0c1da-149">Creating Your First Application</span></span>

<span data-ttu-id="0c1da-150">您可以创建使用所选的 Visual Basic 或 Visual C# 作为编程语言的应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c1da-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="0c1da-151">对于本教程中，在左侧，选择 Visual Basic，然后选择**ASP.NET MVC 3 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="0c1da-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="0c1da-152">命名你的项目"MvcMovie"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="0c1da-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="0c1da-154">在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="0c1da-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="0c1da-155">将保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="0c1da-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="0c1da-157">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0c1da-157">Click **OK**.</span></span> <span data-ttu-id="0c1da-158">Visual Web Developer 中刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！</span><span class="sxs-lookup"><span data-stu-id="0c1da-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="0c1da-159">这是简单"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="0c1da-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="0c1da-160">项目和它的启动应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="0c1da-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="0c1da-161">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="0c1da-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="0c1da-162">请注意，若要开始调试的键盘快捷键 F5。</span><span class="sxs-lookup"><span data-stu-id="0c1da-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="0c1da-163">F5 会导致 Visual Web Developer 才能启动开发 web 服务器和运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c1da-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="0c1da-164">VWD 然后启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="0c1da-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="0c1da-165">请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="0c1da-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="0c1da-166">这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="0c1da-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="0c1da-167">VWD 运行时 web 项目，项目使用一个随机端口。</span><span class="sxs-lookup"><span data-stu-id="0c1da-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="0c1da-168">下图中的随机端口号是 43246。</span><span class="sxs-lookup"><span data-stu-id="0c1da-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="0c1da-169">你的项目可能会使用不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="0c1da-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="0c1da-170">在初始状态下此默认模板提供了在两个页面访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="0c1da-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="0c1da-171">让我们更改此应用程序的工作原理，并了解有点 ASP.NET MVC 中的过程。</span><span class="sxs-lookup"><span data-stu-id="0c1da-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="0c1da-172">关闭浏览器并让我们更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="0c1da-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0c1da-173">下一篇</span><span class="sxs-lookup"><span data-stu-id="0c1da-173">Next</span></span>](adding-a-controller.md)
