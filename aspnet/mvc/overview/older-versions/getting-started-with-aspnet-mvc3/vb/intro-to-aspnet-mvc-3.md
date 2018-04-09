---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (VB) 简介 |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 3be0de6ea6d49f9c0de659398190b71c36ba222a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="eabce-103">ASP.NET MVC 3 (VB) 简介</span><span class="sxs-lookup"><span data-stu-id="eabce-103">Intro to ASP.NET MVC 3 (VB)</span></span>
====================
<span data-ttu-id="eabce-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="eabce-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="eabce-105">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="eabce-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="eabce-106">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="eabce-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="eabce-107">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="eabce-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="eabce-108">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="eabce-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="eabce-109">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="eabce-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="eabce-110">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="eabce-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="eabce-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="eabce-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="eabce-112">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="eabce-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="eabce-113">Visual Web Developer 项目与 VB.NET 的源代码是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="eabce-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="eabce-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="eabce-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="eabce-115">如果你愿意 C#，切换到[C# 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="eabce-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="eabce-116">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="eabce-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="eabce-117">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="eabce-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="eabce-118">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="eabce-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="eabce-119">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="eabce-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="eabce-120">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="eabce-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="eabce-121">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="eabce-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="eabce-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="eabce-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="eabce-123">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="eabce-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="eabce-124">Visual Web Developer 项目与 VB 的源代码是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="eabce-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="eabce-125">[下载 VB 版本此处](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。</span><span class="sxs-lookup"><span data-stu-id="eabce-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="eabce-126">如果你愿意 CSharp，切换到[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="eabce-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="eabce-127">你将生成</span><span class="sxs-lookup"><span data-stu-id="eabce-127">What You'll Build</span></span>

<span data-ttu-id="eabce-128">你将实现简单的影片列表应用程序支持创建、 编辑和列出数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="eabce-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="eabce-129">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="eabce-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="eabce-130">它包括一个显示从数据库的影片列表页：</span><span class="sxs-lookup"><span data-stu-id="eabce-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="eabce-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="eabce-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="eabce-132">应用程序还可以添加、 编辑和删除电影，以及有关个别权限，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="eabce-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="eabce-133">所有数据输入应用场景都包括验证来确保在数据库中存储的数据正确。</span><span class="sxs-lookup"><span data-stu-id="eabce-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="eabce-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="eabce-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="eabce-135">你将学习的技能</span><span class="sxs-lookup"><span data-stu-id="eabce-135">Skills You'll Learn</span></span>

<span data-ttu-id="eabce-136">下面是你将要掌握的内容：</span><span class="sxs-lookup"><span data-stu-id="eabce-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="eabce-137">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="eabce-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="eabce-138">如何创建新的数据库使用实体框架代码的第一个</span><span class="sxs-lookup"><span data-stu-id="eabce-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="eabce-139">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="eabce-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="eabce-140">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="eabce-140">How to retrieve and display data</span></span>
- <span data-ttu-id="eabce-141">如何编辑数据并启用数据验证</span><span class="sxs-lookup"><span data-stu-id="eabce-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="eabce-142">入门</span><span class="sxs-lookup"><span data-stu-id="eabce-142">Getting Started</span></span>

<span data-ttu-id="eabce-143">通过运行 Visual Web Developer 2010 Express (简称的"VWD") 启动，然后选择**新项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="eabce-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="eabce-144">Visual Web Developer 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="eabce-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="eabce-145">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="eabce-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="eabce-146">在 Visual Web Developer 是向你显示各个可用的选项顶部的工具栏。</span><span class="sxs-lookup"><span data-stu-id="eabce-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="eabce-147">此外还有一个菜单，提供另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="eabce-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="eabce-148">(例如，而不是选择**新项目**从**启动**页上，你可以使用菜单并选择**文件** &gt; **新项目**.)</span><span class="sxs-lookup"><span data-stu-id="eabce-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="eabce-149">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="eabce-149">Creating Your First Application</span></span>

<span data-ttu-id="eabce-150">你可以创建使用你选择的 Visual Basic 或 Visual C# 作为编程语言的应用程序。</span><span class="sxs-lookup"><span data-stu-id="eabce-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="eabce-151">对于本教程中，在左侧，选择 Visual Basic，然后选择**ASP.NET MVC 3 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="eabce-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="eabce-152">将你的项目"MvcMovie"，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="eabce-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="eabce-154">在**新建 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="eabce-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="eabce-155">保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="eabce-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="eabce-157">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="eabce-157">Click **OK**.</span></span> <span data-ttu-id="eabce-158">因此，必须运行的应用程序现在不执行任何操作的情况下，visual Web Developer 刚创建的 ASP.NET MVC 项目使用默认模板 ！</span><span class="sxs-lookup"><span data-stu-id="eabce-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="eabce-159">这是简单"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="eabce-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="eabce-160">项目和它的启动你的应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="eabce-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="eabce-161">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="eabce-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="eabce-162">请注意，键盘快捷方式启动调试 F5。</span><span class="sxs-lookup"><span data-stu-id="eabce-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="eabce-163">F5 会导致 Visual Web Developer 启动开发 web 服务器并运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eabce-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="eabce-164">然后，VWD 启动浏览器，并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="eabce-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="eabce-165">请注意，浏览器的地址栏显示`localhost`和不类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="eabce-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="eabce-166">这是因为`localhost`始终指向你自己本地的计算机，在这种情况下运行你刚才生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="eabce-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="eabce-167">当 VWD 运行 web 项目时，随机端口用于项目。</span><span class="sxs-lookup"><span data-stu-id="eabce-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="eabce-168">在下图中，随机端口号是 43246。</span><span class="sxs-lookup"><span data-stu-id="eabce-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="eabce-169">你的项目将可能使用不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="eabce-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="eabce-170">现成的此默认模板提供了您这两页访问和基本的登录页。</span><span class="sxs-lookup"><span data-stu-id="eabce-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="eabce-171">让我们更改此应用程序的工作原理，并了解得有点 ASP.NET MVC 在进程中。</span><span class="sxs-lookup"><span data-stu-id="eabce-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="eabce-172">关闭你的浏览器并让我们更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="eabce-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="eabce-173">下一篇</span><span class="sxs-lookup"><span data-stu-id="eabce-173">Next</span></span>](adding-a-controller.md)
