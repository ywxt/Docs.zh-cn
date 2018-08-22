---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: 使用 ASP.NET MVC (VB) 创建电影数据库应用程序在 15 分钟 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。 本教程是很棒的介绍的人员将新 t...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: f0a060bffc2e45f54d03571b6609a30876202e32
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830070"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a><span data-ttu-id="7ad1e-104">创建电影数据库应用程序在 15 分钟内使用 ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (VB)</span></span>
====================
<span data-ttu-id="7ad1e-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="7ad1e-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="7ad1e-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> <span data-ttu-id="7ad1e-107">Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="7ad1e-108">本教程是过程的谁不熟悉 ASP.NET MVC Framework 和想要了解的构建 ASP.NET MVC 应用程序的人员很棒的介绍。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="7ad1e-109">本教程的目的是为您提供的"什么就像"的意义上构建的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="7ad1e-110">在本教程中，我冲击生成整个 ASP.NET MVC 应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="7ad1e-111">我向您展示如何构建的简单数据库驱动应用程序说明了如何列出、 创建和编辑数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="7ad1e-112">若要简化构建我们的应用程序的过程，我们将利用 Visual Studio 2008 的基架功能。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="7ad1e-113">我们将让 Visual Studio 生成的初始代码和我们的控制器、 模型和视图的内容。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="7ad1e-114">如果您曾经使用 Active Server Pages 或 ASP.NET，然后应发现 ASP.NET MVC 非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="7ad1e-115">ASP.NET MVC 视图是非常类似于 Active Server Pages 应用程序中的页。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="7ad1e-116">并且，就像传统的 ASP.NET Web 窗体应用程序，ASP.NET MVC 提供具有丰富的语言和.NET framework 提供的类的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="7ad1e-117">我希望是本教程将为您提供一种构建的 ASP.NET MVC 应用程序体验的方式相似和不同于生成 Active Server Pages 或 ASP.NET Web 窗体应用程序的体验。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="7ad1e-118">电影数据库应用程序的概述</span><span class="sxs-lookup"><span data-stu-id="7ad1e-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="7ad1e-119">由于我们的目标是为了简单起见，我们将构建一个非常简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="7ad1e-120">我们简单的电影数据库应用程序将使我们可以做三件事：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="7ad1e-121">列出一组的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-121">List a set of movie database records</span></span>
2. <span data-ttu-id="7ad1e-122">创建一个新的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-122">Create a new movie database record</span></span>
3. <span data-ttu-id="7ad1e-123">编辑现有的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-123">Edit an existing movie database record</span></span>

<span data-ttu-id="7ad1e-124">同样，因为我们想要为简单起见，我们将充分利用 ASP.NET MVC framework 构建我们的应用程序所需的功能的最小数目。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="7ad1e-125">例如，我们将不会利用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="7ad1e-126">若要创建我们的应用程序，我们需要完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="7ad1e-127">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="7ad1e-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="7ad1e-128">创建数据库</span><span class="sxs-lookup"><span data-stu-id="7ad1e-128">Create the database</span></span>
3. <span data-ttu-id="7ad1e-129">创建数据库模型</span><span class="sxs-lookup"><span data-stu-id="7ad1e-129">Create the database model</span></span>
4. <span data-ttu-id="7ad1e-130">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="7ad1e-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="7ad1e-131">创建 ASP.NET MVC 视图</span><span class="sxs-lookup"><span data-stu-id="7ad1e-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="7ad1e-132">初步操作</span><span class="sxs-lookup"><span data-stu-id="7ad1e-132">Preliminaries</span></span>

<span data-ttu-id="7ad1e-133">你将需要 Visual Studio 2008 或 Visual Web Developer 2008 Express 构建的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="7ad1e-134">此外需要下载 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="7ad1e-135">如果你拥有 Visual Studio 2008，然后可以从该网站下载 Visual Studio 2008 的 90 天试用版：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="7ad1e-136">或者，您可以创建 ASP.NET MVC 应用程序与 Visual Web Developer Express 2008。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="7ad1e-137">如果您决定使用 Visual Web Developer 速成版，然后必须具有安装 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="7ad1e-138">您可以从此网站中下载 Visual Web Developer 2008 速成版 Service Pack 1:</span><span class="sxs-lookup"><span data-stu-id="7ad1e-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="7ad1e-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&ampdisplaylang = en</span><span class="sxs-lookup"><span data-stu-id="7ad1e-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="7ad1e-140">安装 Visual Studio 2008 或 Visual Web Developer 2008 后，你需要安装 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="7ad1e-141">您可以从以下网站下载 ASP.NET MVC framework:</span><span class="sxs-lookup"><span data-stu-id="7ad1e-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-142">而无需单独下载 ASP.NET framework 和 ASP.NET MVC 框架，可以充分利用 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="7ad1e-143">Web 平台安装程序是使你能够轻松地管理已安装的应用程序的应用程序是您的计算机：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="7ad1e-144">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="7ad1e-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="7ad1e-145">让我们首先在 Visual Studio 2008 中创建新的 ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="7ad1e-146">选择菜单选项**文件，新的项目**，你将看到在图 1 中的新项目对话框。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="7ad1e-147">选择作为编程语言的 Visual Basic，并选择 ASP.NET MVC Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-147">Select Visual Basic as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="7ad1e-148">为项目名称 MovieApp，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-148">Give your project the name MovieApp and click the OK button.</span></span>


<span data-ttu-id="7ad1e-149">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-149">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span></span>

<span data-ttu-id="7ad1e-150">**图 01**: 新建项目对话框 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span></span>


<span data-ttu-id="7ad1e-151">请确保从新项目对话框顶部的下拉列表中选择.NET Framework 3.5 或 ASP.NET MVC Web 应用程序项目模板不会显示。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="7ad1e-152">每当创建新的 MVC Web 应用程序项目时，Visual Studio 会提示您创建一个单独的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="7ad1e-153">图 2 中的对话框会显示。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="7ad1e-154">由于我们不会在本教程中需要创建测试由于时间约束 （并且，是的我们应认为这有点歉疚） 选择**否**选项，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-155">Visual Web Developer 不支持测试项目。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-155">Visual Web Developer does not support test projects.</span></span>


<span data-ttu-id="7ad1e-156">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-156">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span></span>

<span data-ttu-id="7ad1e-157">**图 02**: 创建单元测试项目对话框 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span></span>


<span data-ttu-id="7ad1e-158">ASP.NET MVC 应用程序具有一组标准的文件夹： 模型、 视图和控制器的文件夹。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="7ad1e-159">您可以看到此组标准的解决方案资源管理器窗口中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="7ad1e-160">我们需要将文件添加到的每个模型、 视图和控制器文件夹中，以生成我们的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="7ad1e-161">使用 Visual Studio 创建新的 MVC 应用程序，可以获取示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="7ad1e-162">因为我们想要从头开始，我们需要删除此示例应用程序的内容。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="7ad1e-163">您需要删除以下文件和以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="7ad1e-164">Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="7ad1e-164">Controllers\HomeController.vb</span></span>
- <span data-ttu-id="7ad1e-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="7ad1e-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="7ad1e-166">创建数据库</span><span class="sxs-lookup"><span data-stu-id="7ad1e-166">Creating the Database</span></span>

<span data-ttu-id="7ad1e-167">我们需要创建一个数据库以包含我们的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="7ad1e-168">幸运的是，Visual Studio 包含一个名为 SQL Server Express 的免费数据库。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="7ad1e-169">请按照下列步骤来创建数据库：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="7ad1e-170">右键单击该应用\_在解决方案资源管理器窗口中，选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="7ad1e-171">选择**数据**类别，然后选择**SQL Server 数据库**模板 （参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="7ad1e-172">新数据库命名*MoviesDB.mdf*然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="7ad1e-173">创建数据库后，您可以通过双击 MoviesDB.mdf 文件应用中连接到数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="7ad1e-174">双击 MoviesDB.mdf 文件会打开服务器资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-175">服务器资源管理器窗口是名为在 Visual Web Developer 的情况下的数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


<span data-ttu-id="7ad1e-176">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-176">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span></span>

<span data-ttu-id="7ad1e-177">**图 03**： 创建 Microsoft SQL Server 数据库 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span></span>


<span data-ttu-id="7ad1e-178">接下来，我们需要创建一个新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="7ad1e-179">在服务器资源管理器窗口中，右键单击表文件夹并选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="7ad1e-180">选择此菜单选项打开的数据库表设计器。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="7ad1e-181">创建数据库以下列：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-181">Create the following database columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="7ad1e-182">**列名称**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-182">**Column Name**</span></span> | <span data-ttu-id="7ad1e-183">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-183">**Data Type**</span></span> | <span data-ttu-id="7ad1e-184">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-184">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ad1e-185">Id</span><span class="sxs-lookup"><span data-stu-id="7ad1e-185">Id</span></span> | <span data-ttu-id="7ad1e-186">Int</span><span class="sxs-lookup"><span data-stu-id="7ad1e-186">Int</span></span> | <span data-ttu-id="7ad1e-187">False</span><span class="sxs-lookup"><span data-stu-id="7ad1e-187">False</span></span> |
| <span data-ttu-id="7ad1e-188">标题</span><span class="sxs-lookup"><span data-stu-id="7ad1e-188">Title</span></span> | <span data-ttu-id="7ad1e-189">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-189">Nvarchar(100)</span></span> | <span data-ttu-id="7ad1e-190">False</span><span class="sxs-lookup"><span data-stu-id="7ad1e-190">False</span></span> |
| <span data-ttu-id="7ad1e-191">主管</span><span class="sxs-lookup"><span data-stu-id="7ad1e-191">Director</span></span> | <span data-ttu-id="7ad1e-192">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-192">Nvarchar(100)</span></span> | <span data-ttu-id="7ad1e-193">False</span><span class="sxs-lookup"><span data-stu-id="7ad1e-193">False</span></span> |
| <span data-ttu-id="7ad1e-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="7ad1e-194">DateReleased</span></span> | <span data-ttu-id="7ad1e-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="7ad1e-195">DateTime</span></span> | <span data-ttu-id="7ad1e-196">False</span><span class="sxs-lookup"><span data-stu-id="7ad1e-196">False</span></span> |


<span data-ttu-id="7ad1e-197">第一列，Id 列中，有两个特殊属性。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="7ad1e-198">首先，需要将 Id 列作为主键列标记。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="7ad1e-199">选择 Id 列之后，单击**设置主键**（它是看起来像一个键的图标） 按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="7ad1e-200">其次，您需要将标记为标识列的 Id 列。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="7ad1e-201">在列属性窗口中向下滚动到标识规范部分并展开它。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="7ad1e-202">更改**是标识**属性设置为值**是**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="7ad1e-203">完成后，表应如图 4 所示。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-203">When you are finished, the table should look like Figure 4.</span></span>


<span data-ttu-id="7ad1e-204">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-204">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span></span>

<span data-ttu-id="7ad1e-205">**图 04**: 电影数据库表 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span></span>


<span data-ttu-id="7ad1e-206">最后一步是将保存新表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-206">The final step is to save the new table.</span></span> <span data-ttu-id="7ad1e-207">单击保存按钮 （软盘图标） 并为新的表名称电影。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="7ad1e-208">完成创建表后，向表中添加某些电影记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="7ad1e-209">右键单击服务器资源管理器窗口中的电影表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="7ad1e-210">输入你最喜爱的电影 （请参见图 5） 的列表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-210">Enter a list of your favorite movies (see Figure 5).</span></span>


<span data-ttu-id="7ad1e-211">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-211">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span></span>

<span data-ttu-id="7ad1e-212">**图 05**： 输入电影记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="7ad1e-213">创建模型</span><span class="sxs-lookup"><span data-stu-id="7ad1e-213">Creating the Model</span></span>

<span data-ttu-id="7ad1e-214">接下来，我们需要创建一组类来表示我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="7ad1e-215">我们需要创建数据库模型。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-215">We need to create a database model.</span></span> <span data-ttu-id="7ad1e-216">我们将充分利用 Microsoft Entity Framework 自动生成数据库模型的类。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-217">ASP.NET MVC 框架不依赖于 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="7ad1e-218">您也可以利用的各种对象关系映射创建你的数据库模型类 (或者 / M) 工具，包括 LINQ to SQL，Subsonic 和 NHibernate。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="7ad1e-219">请按照下列步骤以启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="7ad1e-220">右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="7ad1e-221">选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="7ad1e-222">为你的数据模型提供名称*MoviesDBModel.edmx*然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="7ad1e-223">单击添加按钮后，会显示实体数据模型向导 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="7ad1e-224">请按照下列步骤以完成向导：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="7ad1e-225">在中**选择模型内容**步骤中，选择**从数据库生成**选项。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="7ad1e-226">在中**选择数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*的连接设置。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="7ad1e-227">单击**下一步**按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="7ad1e-228">在中**选择数据库对象**步骤中，展开表节点中，选择电影表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="7ad1e-229">输入的命名空间*MovieApp.Models*然后单击**完成**按钮。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


<span data-ttu-id="7ad1e-230">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-230">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span></span>

<span data-ttu-id="7ad1e-231">**图 06**： 生成具有实体数据模型向导的数据库模型 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span></span>


<span data-ttu-id="7ad1e-232">完成实体数据模型向导后，会打开实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="7ad1e-233">在设计器应显示电影数据库表 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-233">The Designer should display the Movies database table (see Figure 7).</span></span>


<span data-ttu-id="7ad1e-234">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-234">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span></span>

<span data-ttu-id="7ad1e-235">**图 07**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span></span>


<span data-ttu-id="7ad1e-236">我们需要做出一项更改，然后我们继续。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-236">We need to make one change before we continue.</span></span> <span data-ttu-id="7ad1e-237">实体数据向导生成一个名为电影模型类，表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-237">The Entity Data Wizard generates a model class named Movies that represents the Movies database table.</span></span> <span data-ttu-id="7ad1e-238">由于我们将使用电影类来表示特定电影，我们需要修改这个类为名称*电影*而不是*电影*（单数而非复数形式）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="7ad1e-239">双击设计器图面上的类的名称并将影片中的类的名称更改为电影。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="7ad1e-240">此更改后，单击**保存**按钮 （软盘图标） 以生成电影类。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="7ad1e-241">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="7ad1e-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="7ad1e-242">下一步是创建 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="7ad1e-243">控制器负责控制用户如何与 ASP.NET MVC 应用程序交互。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="7ad1e-244">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-244">Follow these steps:</span></span>

1. <span data-ttu-id="7ad1e-245">在解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="7ad1e-246">在添加控制器对话框中，输入名称*HomeController* ，并检查标记为复选框**添加操作方法用于创建、 更新和的详细信息方案**（请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="7ad1e-247">单击**添加**按钮将新控制器添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="7ad1e-248">完成这些步骤后，将创建在列表 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="7ad1e-249">请注意，它包含名为 Index，详细信息，创建、 方法和编辑。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="7ad1e-250">在以下部分中，我们将添加必要的代码来获取这些方法才能起作用。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


<span data-ttu-id="7ad1e-251">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-251">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span></span>

<span data-ttu-id="7ad1e-252">**图 08**： 添加新的 ASP.NET MVC 控制器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span></span>


<span data-ttu-id="7ad1e-253">**代码清单 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-253">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a><span data-ttu-id="7ad1e-254">列出数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-254">Listing Database Records</span></span>

<span data-ttu-id="7ad1e-255">主控制器的 index （） 方法是 ASP.NET MVC 应用程序的默认方法。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="7ad1e-256">当您运行的 ASP.NET MVC 应用程序时，index （） 方法是调用的第一个控制器方法。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="7ad1e-257">我们将使用 index （） 方法以显示电影数据库表中的记录的列表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="7ad1e-258">我们将充分利用数据库模型类我们之前创建的电影数据库记录检索使用 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="7ad1e-259">我已修改 HomeController 类在代码清单 2 中的，使其包含名为的新私有字段\_db。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="7ad1e-260">MoviesDBEntities 类表示我们的数据库模型，我们将使用此类与我们的数据库进行通信。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="7ad1e-261">我已修改代码清单 2 中的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="7ad1e-262">Index （） 方法使用 MoviesDBEntities 类从电影数据库表中检索的所有电影记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="7ad1e-263">表达式 *\_db。MovieSet.ToList()* 从电影数据库表中返回所有电影记录的列表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="7ad1e-264">电影列表传递给视图。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="7ad1e-265">获取传递给 View() 方法的任何内容获取传递给视图作为视图数据。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="7ad1e-266">**代码清单 2 – Controllers/HomeController.vb （已修改索引方法）**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-266">**Listing 2 – Controllers/HomeController.vb (modified Index method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

<span data-ttu-id="7ad1e-267">Index （） 方法返回名为 Index 的视图。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="7ad1e-268">我们需要创建此视图以显示电影数据库记录的列表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="7ad1e-269">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-269">Follow these steps:</span></span>


<span data-ttu-id="7ad1e-270">应生成项目 (选择菜单选项**生成，生成解决方案**) 打开之前**添加视图**中将出现对话框或没有类**查看数据类**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="7ad1e-271">右键单击代码编辑器中的 index （） 方法，然后选择菜单选项**添加视图**（请参阅图 9）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="7ad1e-272">在添加视图对话框中，验证相应的复选框标记为**创建强类型化视图**检查。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="7ad1e-273">从**查看内容**下拉列表中，选择的值*列表*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="7ad1e-274">从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-274">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="7ad1e-275">单击添加按钮以创建新查看 （请参阅图 10）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="7ad1e-276">完成这些步骤后，名为 Index.aspx 的新视图添加到 views/home 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="7ad1e-277">索引视图的内容包含在列表 3 中。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-277">The contents of the Index view are included in Listing 3.</span></span>


<span data-ttu-id="7ad1e-278">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-278">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span></span>

<span data-ttu-id="7ad1e-279">**图 09**： 添加的视图的控制器操作 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span></span>


<span data-ttu-id="7ad1e-280">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-280">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span></span>

<span data-ttu-id="7ad1e-281">**图 10**： 使用添加视图对话框中创建新视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span></span>


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

<span data-ttu-id="7ad1e-282">索引视图显示的所有电影记录从 HTML 表内的电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-282">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="7ad1e-283">该视图包含一个 For Each 循环，循环访问由 ViewData.Model 属性表示每个电影。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-283">The view contains a For Each loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="7ad1e-284">如果按 F5 键运行应用程序，您将看到在图 11 网页。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-284">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


<span data-ttu-id="7ad1e-285">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-285">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span></span>

<span data-ttu-id="7ad1e-286">**图 11**： 该索引视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-286">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="7ad1e-287">创建新的数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-287">Creating New Database Records</span></span>

<span data-ttu-id="7ad1e-288">我们在上一节中创建的索引视图包含用于创建新的数据库记录的链接。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-288">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="7ad1e-289">让我们继续并实现的逻辑和创建视图所需创建新的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-289">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="7ad1e-290">主控制器包含名为 create （） 的两个方法。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-290">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="7ad1e-291">第一个 create （） 方法没有任何参数。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-291">The first Create() method has no parameters.</span></span> <span data-ttu-id="7ad1e-292">Create （） 方法的此重载用于显示用于创建新的电影数据库记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-292">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="7ad1e-293">第二个 create （） 方法有一个 FormCollection 参数。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-293">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="7ad1e-294">用于创建新的电影的 HTML 窗体发布到服务器时，调用 create （） 方法的此重载。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-294">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="7ad1e-295">请注意，此第二个 create （） 方法具有 AcceptVerbs 属性，以防止方法被调用，除非执行 HTTP Post 操作。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-295">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP Post operation is performed.</span></span>

<span data-ttu-id="7ad1e-296">此第二个 create （） 方法已在列表 4 中更新 HomeController 类中被修改。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-296">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="7ad1e-297">Create （） 方法的新版本接受电影参数，并包含用于电影数据库表中插入新电影的逻辑。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-297">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-298">请注意，绑定属性。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-298">Notice the Bind attribute.</span></span> <span data-ttu-id="7ad1e-299">因为我们不想要更新从 HTML 窗体的电影 Id 属性，我们需要此属性中显式排除。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-299">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


<span data-ttu-id="7ad1e-300">**列表 4 – Controllers\HomeController.vb （已修改 Create 方法）**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-300">**Listing 4 – Controllers\HomeController.vb (modified Create method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

<span data-ttu-id="7ad1e-301">Visual Studio，可以轻松地创建用于创建新的电影数据库窗体记录 （请参阅图 12）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-301">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="7ad1e-302">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-302">Follow these steps:</span></span>

1. <span data-ttu-id="7ad1e-303">右键单击代码编辑器中的 create （） 方法，然后选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-303">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="7ad1e-304">验证相应的复选框标记为**创建强类型化视图**检查。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-304">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="7ad1e-305">从**查看内容**下拉列表中，选择的值*创建*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-305">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="7ad1e-306">从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-306">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="7ad1e-307">单击**添加**按钮以创建新视图。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-307">Click the **Add** button to create the new view.</span></span>


<span data-ttu-id="7ad1e-308">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-308">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span></span>

<span data-ttu-id="7ad1e-309">**图 12**： 添加创建视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-309">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span></span>


<span data-ttu-id="7ad1e-310">Visual Studio 查看在列表 5 中会自动生成。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-310">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="7ad1e-311">此视图包含 HTML 窗体包括的字段对应于每个电影类的属性。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-311">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="7ad1e-312">**列表 5 – Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-312">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-313">生成的添加视图对话框中的 HTML 窗体生成 Id 窗体字段。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-313">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="7ad1e-314">Id 列是标识列，因为我们不需要此窗体字段，并且可以放心删除它。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-314">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="7ad1e-315">添加 Create 视图后，您可以向数据库添加新电影记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-315">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="7ad1e-316">通过按 F5 键运行应用程序，并单击新创建的链接以查看图 13 中的窗体。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-316">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="7ad1e-317">如果完成并提交表单时，会创建新的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-317">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="7ad1e-318">请注意，自动获取窗体验证。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-318">Notice that you get form validation automatically.</span></span> <span data-ttu-id="7ad1e-319">如果没有输入一个 movie，发布日期，或者输入无效的发布日期，然后重新显示该窗体，并突出显示发布日期字段。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-319">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


<span data-ttu-id="7ad1e-320">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-320">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span></span>

<span data-ttu-id="7ad1e-321">**图 13**： 创建新的电影数据库记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-321">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="7ad1e-322">编辑现有的数据库记录</span><span class="sxs-lookup"><span data-stu-id="7ad1e-322">Editing Existing Database Records</span></span>

<span data-ttu-id="7ad1e-323">在前面部分中，我们讨论了如何列出和创建新的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-323">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="7ad1e-324">在此最后一节中，我们将讨论如何可以编辑现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-324">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="7ad1e-325">首先，我们需要生成编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-325">First, we need to generate the Edit form.</span></span> <span data-ttu-id="7ad1e-326">此步骤很容易，因为 Visual Studio 将生成为我们的编辑窗体自动。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-326">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="7ad1e-327">在 Visual Studio 代码编辑器中打开 HomeController.vb 类，并按照以下步骤：</span><span class="sxs-lookup"><span data-stu-id="7ad1e-327">Open the HomeController.vb class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="7ad1e-328">右键单击代码编辑器中的 edit （） 方法，然后选择菜单选项**添加视图**（请参阅图 14）。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-328">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="7ad1e-329">选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-329">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="7ad1e-330">从**查看内容**下拉列表中，选择的值*编辑*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-330">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="7ad1e-331">从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-331">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="7ad1e-332">单击**添加**按钮以创建新视图。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-332">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="7ad1e-333">完成这些步骤将添加到 views/home 文件夹中名为 Edit.aspx 的新视图。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-333">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="7ad1e-334">此视图包含 HTML 窗体以编辑电影记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-334">This view contains an HTML form for editing a movie record.</span></span>


<span data-ttu-id="7ad1e-335">[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="7ad1e-335">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span></span>

<span data-ttu-id="7ad1e-336">**图 14**： 添加编辑视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="7ad1e-336">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="7ad1e-337">编辑视图包含电影 Id 属性与对应的 HTML 窗体字段。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-337">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="7ad1e-338">由于您不希望人们编辑 Id 属性的值，则应删除此窗体字段。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-338">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="7ad1e-339">最后，我们需要修改主控制器，以便它也支持编辑的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-339">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="7ad1e-340">更新的 HomeController 类都包含在列表 6。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-340">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="7ad1e-341">**代码清单 6 – Controllers\HomeController.vb （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="7ad1e-341">**Listing 6 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

<span data-ttu-id="7ad1e-342">列表 6 中我到 edit （） 方法的这两个重载添加其他逻辑。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-342">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="7ad1e-343">第一种 edit （） 方法返回给传递给方法的 Id 参数相对应的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-343">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="7ad1e-344">第二个重载在数据库中执行到电影记录的更新。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-344">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="7ad1e-345">请注意，您必须检索原始电影，然后调用 ApplyPropertyChanges()，以更新数据库中已有的电影。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-345">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="7ad1e-346">总结</span><span class="sxs-lookup"><span data-stu-id="7ad1e-346">Summary</span></span>

<span data-ttu-id="7ad1e-347">本教程的目的是让您构建的 ASP.NET MVC 应用程序体验的了解。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-347">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="7ad1e-348">我希望您发现构建 ASP.NET MVC web 应用程序是非常类似于生成 Active Server Pages 或 ASP.NET 应用程序的体验。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-348">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="7ad1e-349">在本教程中，我们检查只 ASP.NET MVC 框架的最基本功能。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-349">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="7ad1e-350">在将来的教程中，我们深入控制器、 控制器操作、 视图、 视图数据，以及 HTML 帮助程序等主题。</span><span class="sxs-lookup"><span data-stu-id="7ad1e-350">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7ad1e-351">上一篇</span><span class="sxs-lookup"><span data-stu-id="7ad1e-351">Previous</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
