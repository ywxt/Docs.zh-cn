---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 简介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教程是此处使用 Visual Studio 2013 提供更新的版本。 新教程使用 ASP.NET MVC 5，可获得许多改进通过 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51e469e131b083325bc565530d91173887769ab0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395809"
---
<a name="intro-to-aspnet-mvc-4"></a><span data-ttu-id="99068-104">ASP.NET MVC 4 简介</span><span class="sxs-lookup"><span data-stu-id="99068-104">Intro to ASP.NET MVC 4</span></span>
====================
<span data-ttu-id="99068-105">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="99068-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="99068-106">如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。</span><span class="sxs-lookup"><span data-stu-id="99068-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="99068-107">新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="99068-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> <span data-ttu-id="99068-108">本教程将教您构建使用 Microsoft 的 ASP.NET MVC 4 Web 应用程序的基础知识[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="99068-108">This tutorial will teach you the basics of building an ASP.NET MVC 4 Web application using Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1.</span></span> <span data-ttu-id="99068-109">建议使用 visual Studio 2012，无需安装任何要完成本教程的内容。</span><span class="sxs-lookup"><span data-stu-id="99068-109">Visual Studio 2012 is recommended, you won't need to install anything to complete the tutorial.</span></span> <span data-ttu-id="99068-110">如果您使用的 Visual Studio 2010，则必须安装以下组件。</span><span class="sxs-lookup"><span data-stu-id="99068-110">If you are using Visual Studio 2010 you must install the components below.</span></span> <span data-ttu-id="99068-111">可以通过单击以下链接安装所有这些：</span><span class="sxs-lookup"><span data-stu-id="99068-111">You can install all of them by clicking the following links:</span></span>
> 
> - [<span data-ttu-id="99068-112">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="99068-112">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="99068-113">为 ASP.NET MVC 4 WPI 安装程序</span><span class="sxs-lookup"><span data-stu-id="99068-113">WPI installer for ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [<span data-ttu-id="99068-114">LocalDB</span><span class="sxs-lookup"><span data-stu-id="99068-114">LocalDB</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [<span data-ttu-id="99068-115">SSDT</span><span class="sxs-lookup"><span data-stu-id="99068-115">SSDT</span></span>](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
> 
> <span data-ttu-id="99068-116">如果您正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，安装[WPI 安装程序为 ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)和: [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span><span class="sxs-lookup"><span data-stu-id="99068-116">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the [WPI installer for ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) and the: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span></span>
> 
> <span data-ttu-id="99068-117">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="99068-117">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="99068-118">[下载 C# 版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。</span><span class="sxs-lookup"><span data-stu-id="99068-118">[Download the C# version](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).</span></span>
> 
> <span data-ttu-id="99068-119">在本教程在 Visual Studio 中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="99068-119">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="99068-120">您还可以让应用程序访问 Internet 上通过将其部署到托管提供商。</span><span class="sxs-lookup"><span data-stu-id="99068-120">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="99068-121">Microsoft 提供了免费的 web 托管最多 10 个网站中有关[免费 Windows Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="99068-121">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="99068-122">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的信息，请参阅[创建和部署 ASP.NET 网站和 SQL 数据库使用 Visual Studio](https://docs.microsoft.com/dotnet/azure/)。</span><span class="sxs-lookup"><span data-stu-id="99068-122">For information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create and deploy an ASP.NET web site and SQL Database with Visual Studio](https://docs.microsoft.com/dotnet/azure/).</span></span> <span data-ttu-id="99068-123">该教程还演示如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Windows Azure SQL 数据库 (以前称为 SQL Azure)。</span><span class="sxs-lookup"><span data-stu-id="99068-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Windows Azure SQL Database (formerly SQL Azure).</span></span>
> 
> <span data-ttu-id="99068-124">本教程由 Rick Anderson 编写 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )。</span><span class="sxs-lookup"><span data-stu-id="99068-124">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="99068-125">你将生成</span><span class="sxs-lookup"><span data-stu-id="99068-125">What You'll Build</span></span>

> [!NOTE]
> <span data-ttu-id="99068-126">如果本教程中可用的更新的版本[这里](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)。</span><span class="sxs-lookup"><span data-stu-id="99068-126">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="99068-127">新教程使用 ASP.NET MVC 5，通过本教程提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="99068-127">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>


<span data-ttu-id="99068-128">将实现一个简单的电影列表应用程序支持创建、 编辑、 搜索和列出数据库中的电影。</span><span class="sxs-lookup"><span data-stu-id="99068-128">You'll implement a simple movie-listing application that supports creating, editing, searching and listing movies from a database.</span></span> <span data-ttu-id="99068-129">以下是你将生成的应用程序的两个屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="99068-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="99068-130">它包括显示的数据库中的电影列表的页面：</span><span class="sxs-lookup"><span data-stu-id="99068-130">It includes a page that displays a list of movies from a database:</span></span>

![](intro-to-aspnet-mvc-4/_static/image1.png)

<span data-ttu-id="99068-131">应用程序还可以添加、 编辑和删除电影，以及有关各个权限，请参阅详细信息。</span><span class="sxs-lookup"><span data-stu-id="99068-131">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="99068-132">所有数据输入应用场景都包括验证，以确保在数据库中存储的数据正确。</span><span class="sxs-lookup"><span data-stu-id="99068-132">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a><span data-ttu-id="99068-133">入门</span><span class="sxs-lookup"><span data-stu-id="99068-133">Getting Started</span></span>

<span data-ttu-id="99068-134">首先运行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="99068-134">Start by running Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="99068-135">大部分屏幕快照中本系列，请使用 Visual Studio Express 2012 中，但你可以完成本教程使用 Visual Studio 2010 SP1、 Visual Studio 2012，Visual Studio Express 2012 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="99068-135">Most of the screen shots in this series use Visual Studio Express 2012, but you can complete this tutorial with Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="99068-136">选择**新的项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="99068-136">Select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="99068-137">Visual Studio 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="99068-137">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="99068-138">就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="99068-138">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="99068-139">在 Visual Studio 中没有向您显示各种可用选项顶部的工具栏。</span><span class="sxs-lookup"><span data-stu-id="99068-139">In Visual Studio there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="99068-140">此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="99068-140">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="99068-141">(例如，而不是选择**新的项目**从**启动**页上，您可以使用菜单并选择**文件** &gt; **的新项目**.)</span><span class="sxs-lookup"><span data-stu-id="99068-141">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="99068-142">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="99068-142">Creating Your First Application</span></span>

<span data-ttu-id="99068-143">您可以创建使用 Visual Basic 或 Visual C# 作为编程语言的应用程序。</span><span class="sxs-lookup"><span data-stu-id="99068-143">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="99068-144">选择 Visual C# 在左侧，然后选择**ASP.NET MVC 4 Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="99068-144">Select Visual C# on the left and then select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="99068-145">将项目命名&quot;MvcMovie&quot; ，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="99068-145">Name your project &quot;MvcMovie&quot; and then click **OK**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image4.png)

<span data-ttu-id="99068-146">在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="99068-146">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="99068-147">将保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="99068-147">Leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-4/_static/image5.png)

<span data-ttu-id="99068-148">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="99068-148">Click **OK**.</span></span> <span data-ttu-id="99068-149">Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！</span><span class="sxs-lookup"><span data-stu-id="99068-149">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="99068-150">这是一个简单&quot;Hello World ！&quot;项目中，和它的启动应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="99068-150">This is a simple &quot;Hello World!&quot; project, and it's a good place to start your application.</span></span>

![](intro-to-aspnet-mvc-4/_static/image6.png)

<span data-ttu-id="99068-151">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="99068-151">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image7.png)

<span data-ttu-id="99068-152">请注意，若要开始调试的键盘快捷键 F5。</span><span class="sxs-lookup"><span data-stu-id="99068-152">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="99068-153">F5 导致 Visual Studio 启动 IIS Express 和运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="99068-153">F5 causes Visual Studio to start IIS Express and run your web application.</span></span> <span data-ttu-id="99068-154">然后，visual Studio 启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="99068-154">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="99068-155">请注意，在浏览器地址栏将显示`localhost`并不是类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="99068-155">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="99068-156">这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="99068-156">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="99068-157">Visual Studio 运行时 web 项目，一个随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="99068-157">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="99068-158">下图中的端口号是 41788。</span><span class="sxs-lookup"><span data-stu-id="99068-158">In the image below, the port number is 41788.</span></span> <span data-ttu-id="99068-159">当您运行该应用程序时，您可能看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="99068-159">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-4/_static/image8.png)

<span data-ttu-id="99068-160">即时可用的此默认模板也提供家庭、 联系人以及有关页面。</span><span class="sxs-lookup"><span data-stu-id="99068-160">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="99068-161">它还提供支持，以注册和登录，并链接到 Facebook 和 Twitter。</span><span class="sxs-lookup"><span data-stu-id="99068-161">It also provides support to register and log in, and links to Facebook and Twitter.</span></span> <span data-ttu-id="99068-162">下一步是要更改此应用程序的工作方式有点了解 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="99068-162">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="99068-163">关闭浏览器并让我们更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="99068-163">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="99068-164">下一篇</span><span class="sxs-lookup"><span data-stu-id="99068-164">Next</span></span>](adding-a-controller.md)
