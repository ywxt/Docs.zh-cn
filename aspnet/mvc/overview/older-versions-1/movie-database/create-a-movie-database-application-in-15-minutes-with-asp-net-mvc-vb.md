---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: "创建电影数据库应用程序在 15 分钟内使用 ASP.NET MVC (VB) |Microsoft 文档"
author: StephenWalther
description: "Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。 本教程是人士提供新 t 的极佳介绍..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: b87a69df24a410161dfaf055519eb6137fa76c06
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a><span data-ttu-id="307be-104">创建电影数据库应用程序在 15 分钟内使用 ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="307be-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (VB)</span></span>
====================
<span data-ttu-id="307be-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="307be-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="307be-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="307be-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> <span data-ttu-id="307be-107">Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="307be-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="307be-108">本教程是过程的，新的 ASP.NET MVC framework 并人员想要获取的意义上生成 ASP.NET MVC 应用程序的极佳简介。</span><span class="sxs-lookup"><span data-stu-id="307be-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="307be-109">本教程的目的是为你提供的"在"的意义上生成 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="307be-110">在本教程中，我完全通过生成整个 ASP.NET MVC 应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="307be-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="307be-111">我将向你演示如何构建的简单数据库驱动应用程序演示了如何列出、 创建和编辑数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="307be-112">为了简化生成我们的应用程序的过程，我们将充分利用 Visual Studio 2008 的基架功能。</span><span class="sxs-lookup"><span data-stu-id="307be-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="307be-113">我们将让 Visual Studio 生成的初始代码和我们控制器、 模型和视图的内容。</span><span class="sxs-lookup"><span data-stu-id="307be-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="307be-114">如果你在使用 Active Server Pages 或 ASP.NET，然后应找到 ASP.NET MVC 非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="307be-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="307be-115">ASP.NET MVC 视图非常类似 Active Server Pages 应用程序中的页。</span><span class="sxs-lookup"><span data-stu-id="307be-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="307be-116">和类似于传统的 ASP.NET Web 窗体应用程序，只需 ASP.NET MVC 为您提供完全访问权限组丰富的语言和.NET framework 提供的类。</span><span class="sxs-lookup"><span data-stu-id="307be-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="307be-117">我希望是本教程将为你提供一种方式生成 ASP.NET MVC 应用程序的体验是相似和不同于生成不 Active Server Pages 或 ASP.NET Web 窗体应用程序的体验。</span><span class="sxs-lookup"><span data-stu-id="307be-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="307be-118">电影数据库应用程序的概述</span><span class="sxs-lookup"><span data-stu-id="307be-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="307be-119">由于我们的目标是为简单起见，我们将生成一个非常简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="307be-120">我们简单的电影数据库应用程序将使我们能够做三件事：</span><span class="sxs-lookup"><span data-stu-id="307be-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="307be-121">列出电影数据库记录的集</span><span class="sxs-lookup"><span data-stu-id="307be-121">List a set of movie database records</span></span>
2. <span data-ttu-id="307be-122">创建一个新的影片数据库记录</span><span class="sxs-lookup"><span data-stu-id="307be-122">Create a new movie database record</span></span>
3. <span data-ttu-id="307be-123">编辑现有的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="307be-123">Edit an existing movie database record</span></span>

<span data-ttu-id="307be-124">同样，因为我们想要为简单起见，我们将充分利用 ASP.NET MVC framework 构建我们的应用程序所需的功能的最小数。</span><span class="sxs-lookup"><span data-stu-id="307be-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="307be-125">例如，我们将不会利用 Test-Driven 开发。</span><span class="sxs-lookup"><span data-stu-id="307be-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="307be-126">若要创建我们的应用程序，我们需要完成每个以下步骤：</span><span class="sxs-lookup"><span data-stu-id="307be-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="307be-127">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="307be-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="307be-128">创建数据库</span><span class="sxs-lookup"><span data-stu-id="307be-128">Create the database</span></span>
3. <span data-ttu-id="307be-129">创建数据库模型</span><span class="sxs-lookup"><span data-stu-id="307be-129">Create the database model</span></span>
4. <span data-ttu-id="307be-130">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="307be-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="307be-131">创建 ASP.NET MVC 视图</span><span class="sxs-lookup"><span data-stu-id="307be-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="307be-132">初步操作</span><span class="sxs-lookup"><span data-stu-id="307be-132">Preliminaries</span></span>

<span data-ttu-id="307be-133">你将需要 Visual Studio 2008 或 Visual Web Developer 2008 Express 生成一个 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="307be-134">你还需要下载 ASP.NET MVC framework。</span><span class="sxs-lookup"><span data-stu-id="307be-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="307be-135">如果你拥有 Visual Studio 2008，然后可以从该网站下载 Visual Studio 2008 90 天试用版：</span><span class="sxs-lookup"><span data-stu-id="307be-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[<span data-ttu-id="307be-136">https://msdn.microsoft.com/vs2008/products/cc268305.aspx</span><span class="sxs-lookup"><span data-stu-id="307be-136">https://msdn.microsoft.com/vs2008/products/cc268305.aspx</span></span>](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="307be-137">或者，你可以创建 ASP.NET MVC 应用程序与 Visual Web Developer Express 2008。</span><span class="sxs-lookup"><span data-stu-id="307be-137">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="307be-138">如果你决定使用 Visual Web Developer Express，则你必须拥有安装 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="307be-138">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="307be-139">你可以从此网站中下载 Visual Web Developer 2008 速成版 Service Pack 1:</span><span class="sxs-lookup"><span data-stu-id="307be-139">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="307be-140">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span><span class="sxs-lookup"><span data-stu-id="307be-140">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="307be-141">安装 Visual Studio 2008 或 Visual Web Developer 2008 之后，你需要安装 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="307be-141">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="307be-142">你可以从以下网站下载的 ASP.NET MVC framework:</span><span class="sxs-lookup"><span data-stu-id="307be-142">You can download the ASP.NET MVC framework from the following website:</span></span>

[<span data-ttu-id="307be-143">https://www.asp.net/mvc/</span><span class="sxs-lookup"><span data-stu-id="307be-143">https://www.asp.net/mvc/</span></span>](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="307be-144">而不是单独下载 ASP.NET framework 和 ASP.NET MVC framework，你可以利用 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="307be-144">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="307be-145">Web 平台安装程序是该应用程序，你可以轻松地管理已安装的应用程序是你的计算机：</span><span class="sxs-lookup"><span data-stu-id="307be-145">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [<span data-ttu-id="307be-146">https://www.microsoft.com/web/gallery/Install.aspx</span><span class="sxs-lookup"><span data-stu-id="307be-146">https://www.microsoft.com/web/gallery/Install.aspx</span></span>](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="307be-147">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="307be-147">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="307be-148">让我们开始通过在 Visual Studio 2008 中创建一个新的 ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="307be-148">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="307be-149">选择菜单选项**文件、 新项目**，你将看到图 1 中的新建项目对话框。</span><span class="sxs-lookup"><span data-stu-id="307be-149">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="307be-150">作为编程语言选择 Visual Basic 和选择 ASP.NET MVC Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="307be-150">Select Visual Basic as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="307be-151">为你的项目提供 MovieApp 的名称，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-151">Give your project the name MovieApp and click the OK button.</span></span>


<span data-ttu-id="307be-152">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="307be-152">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span></span>

<span data-ttu-id="307be-153">**图 01**: 新建项目对话框中 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="307be-153">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span></span>


<span data-ttu-id="307be-154">请确保从新项目对话框顶部的下拉列表中选择.NET Framework 3.5 或 ASP.NET MVC Web 应用程序项目模板不会出现。</span><span class="sxs-lookup"><span data-stu-id="307be-154">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="307be-155">每当创建新的 MVC Web 应用程序项目时，Visual Studio 会提示你创建单独的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="307be-155">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="307be-156">在图 2 显示对话框。</span><span class="sxs-lookup"><span data-stu-id="307be-156">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="307be-157">因为我们不会在本教程需要创建测试由于时间约束 （和，是的我们应感觉有关这有点感到） 选择**否**选项，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-157">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="307be-158">Visual Web Developer 不支持测试项目。</span><span class="sxs-lookup"><span data-stu-id="307be-158">Visual Web Developer does not support test projects.</span></span>


<span data-ttu-id="307be-159">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="307be-159">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span></span>

<span data-ttu-id="307be-160">**图 02**: 创建单元测试项目对话框 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="307be-160">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span></span>


<span data-ttu-id="307be-161">ASP.NET MVC 应用程序具有一组标准的文件夹： 模型、 视图和控制器的文件夹。</span><span class="sxs-lookup"><span data-stu-id="307be-161">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="307be-162">你可以看到此组标准的解决方案资源管理器窗口中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="307be-162">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="307be-163">我们将需要将文件添加到每个模型、 视图和控制器文件夹中，以生成电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-163">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="307be-164">当使用 Visual Studio 创建新的 MVC 应用程序时，可以示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-164">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="307be-165">由于我们想要从头开始，我们需要删除此示例应用程序的内容。</span><span class="sxs-lookup"><span data-stu-id="307be-165">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="307be-166">您需要删除以下文件和以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="307be-166">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="307be-167">Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="307be-167">Controllers\HomeController.vb</span></span>
- <span data-ttu-id="307be-168">Views\Home</span><span class="sxs-lookup"><span data-stu-id="307be-168">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="307be-169">创建数据库</span><span class="sxs-lookup"><span data-stu-id="307be-169">Creating the Database</span></span>

<span data-ttu-id="307be-170">我们需要创建一个数据库以包含我们电影的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-170">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="307be-171">幸运的是，Visual Studio 包含一个名为 SQL Server Express 的免费数据库。</span><span class="sxs-lookup"><span data-stu-id="307be-171">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="307be-172">请按照下列步骤来创建数据库：</span><span class="sxs-lookup"><span data-stu-id="307be-172">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="307be-173">右键单击该应用\_在解决方案资源管理器窗口中，然后选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="307be-173">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="307be-174">选择**数据**类别，然后选择**SQL Server 数据库**模板 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="307be-174">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="307be-175">将新数据库命名*MoviesDB.mdf*单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-175">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="307be-176">创建你的数据库后，你可以通过双击位于应用程序中的 MoviesDB.mdf 文件连接到数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="307be-176">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="307be-177">双击 MoviesDB.mdf 文件会打开服务器资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="307be-177">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="307be-178">服务器资源管理器窗口被命名为在 Visual Web Developer 的情况下的数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="307be-178">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


<span data-ttu-id="307be-179">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="307be-179">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span></span>

<span data-ttu-id="307be-180">**图 03**： 创建 Microsoft SQL Server 数据库 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="307be-180">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span></span>


<span data-ttu-id="307be-181">接下来，我们需要创建一个新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="307be-181">Next, we need to create a new database table.</span></span> <span data-ttu-id="307be-182">在服务器资源管理器窗口中，右键单击表文件夹然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="307be-182">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="307be-183">选择此菜单选项将打开数据库表设计器。</span><span class="sxs-lookup"><span data-stu-id="307be-183">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="307be-184">创建以下数据库列：</span><span class="sxs-lookup"><span data-stu-id="307be-184">Create the following database columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="307be-185">**列名称**</span><span class="sxs-lookup"><span data-stu-id="307be-185">**Column Name**</span></span> | <span data-ttu-id="307be-186">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="307be-186">**Data Type**</span></span> | <span data-ttu-id="307be-187">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="307be-187">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="307be-188">Id</span><span class="sxs-lookup"><span data-stu-id="307be-188">Id</span></span> | <span data-ttu-id="307be-189">Int</span><span class="sxs-lookup"><span data-stu-id="307be-189">Int</span></span> | <span data-ttu-id="307be-190">False</span><span class="sxs-lookup"><span data-stu-id="307be-190">False</span></span> |
| <span data-ttu-id="307be-191">标题</span><span class="sxs-lookup"><span data-stu-id="307be-191">Title</span></span> | <span data-ttu-id="307be-192">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="307be-192">Nvarchar(100)</span></span> | <span data-ttu-id="307be-193">False</span><span class="sxs-lookup"><span data-stu-id="307be-193">False</span></span> |
| <span data-ttu-id="307be-194">控制器</span><span class="sxs-lookup"><span data-stu-id="307be-194">Director</span></span> | <span data-ttu-id="307be-195">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="307be-195">Nvarchar(100)</span></span> | <span data-ttu-id="307be-196">False</span><span class="sxs-lookup"><span data-stu-id="307be-196">False</span></span> |
| <span data-ttu-id="307be-197">DateReleased</span><span class="sxs-lookup"><span data-stu-id="307be-197">DateReleased</span></span> | <span data-ttu-id="307be-198">DateTime</span><span class="sxs-lookup"><span data-stu-id="307be-198">DateTime</span></span> | <span data-ttu-id="307be-199">False</span><span class="sxs-lookup"><span data-stu-id="307be-199">False</span></span> |


<span data-ttu-id="307be-200">第一列，Id 列中，具有两个特殊属性。</span><span class="sxs-lookup"><span data-stu-id="307be-200">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="307be-201">首先，你需要将标记为主键列的 Id 列。</span><span class="sxs-lookup"><span data-stu-id="307be-201">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="307be-202">选择 Id 列之后，单击**设置主键**按钮 （它位于图标，看起来类似的键）。</span><span class="sxs-lookup"><span data-stu-id="307be-202">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="307be-203">其次，你需要将标记为标识列的 Id 列。</span><span class="sxs-lookup"><span data-stu-id="307be-203">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="307be-204">在列属性窗口中，向下滚动到标识规范部分，并将其展开。</span><span class="sxs-lookup"><span data-stu-id="307be-204">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="307be-205">更改**是标识**属性值**是**。</span><span class="sxs-lookup"><span data-stu-id="307be-205">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="307be-206">完成后，应如下表所示图 4。</span><span class="sxs-lookup"><span data-stu-id="307be-206">When you are finished, the table should look like Figure 4.</span></span>


<span data-ttu-id="307be-207">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="307be-207">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span></span>

<span data-ttu-id="307be-208">**图 04**: 电影数据库表 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="307be-208">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span></span>


<span data-ttu-id="307be-209">最后一步是以保存新的表。</span><span class="sxs-lookup"><span data-stu-id="307be-209">The final step is to save the new table.</span></span> <span data-ttu-id="307be-210">单击保存按钮 （软盘图标），并且提供名称电影的新表。</span><span class="sxs-lookup"><span data-stu-id="307be-210">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="307be-211">在完成创建表后，向表中添加一些影片记录。</span><span class="sxs-lookup"><span data-stu-id="307be-211">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="307be-212">右键单击服务器资源管理器窗口中的电影表然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="307be-212">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="307be-213">输入您最喜爱的电影 （请参见图 5） 的列表。</span><span class="sxs-lookup"><span data-stu-id="307be-213">Enter a list of your favorite movies (see Figure 5).</span></span>


<span data-ttu-id="307be-214">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="307be-214">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span></span>

<span data-ttu-id="307be-215">**图 05**： 输入电影记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="307be-215">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="307be-216">创建模型</span><span class="sxs-lookup"><span data-stu-id="307be-216">Creating the Model</span></span>

<span data-ttu-id="307be-217">接下来，我们需要创建一组类来表示我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="307be-217">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="307be-218">我们需要创建的数据库模型。</span><span class="sxs-lookup"><span data-stu-id="307be-218">We need to create a database model.</span></span> <span data-ttu-id="307be-219">我们将充分利用 Microsoft 实体框架可以自动生成用于我们的数据库模型的类。</span><span class="sxs-lookup"><span data-stu-id="307be-219">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="307be-220">ASP.NET MVC framework 不依赖于 Microsoft 的实体框架中。</span><span class="sxs-lookup"><span data-stu-id="307be-220">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="307be-221">你也可以利用各种对象关系映射创建你的数据库模型类 (或者 / M) 工具包括 LINQ to SQL、 Subsonic 和 nhibernate 进行。</span><span class="sxs-lookup"><span data-stu-id="307be-221">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="307be-222">请按照下列步骤以启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="307be-222">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="307be-223">右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="307be-223">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="307be-224">选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="307be-224">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="307be-225">将命名的数据模型*MoviesDBModel.edmx*单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-225">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="307be-226">单击添加按钮后，则将显示实体数据模型向导 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="307be-226">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="307be-227">请按照下列步骤以完成向导：</span><span class="sxs-lookup"><span data-stu-id="307be-227">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="307be-228">在**选择模型内容**步骤中，选择**从数据库生成**选项。</span><span class="sxs-lookup"><span data-stu-id="307be-228">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="307be-229">在**选择你的数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*对于连接设置。</span><span class="sxs-lookup"><span data-stu-id="307be-229">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="307be-230">单击**下一步**按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-230">Click the **Next** button.</span></span>
3. <span data-ttu-id="307be-231">在**选择数据库对象**步骤，展开表节点，选择电影表。</span><span class="sxs-lookup"><span data-stu-id="307be-231">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="307be-232">输入的命名空间*MovieApp.Models*单击**完成**按钮。</span><span class="sxs-lookup"><span data-stu-id="307be-232">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


<span data-ttu-id="307be-233">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="307be-233">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span></span>

<span data-ttu-id="307be-234">**图 06**： 生成数据库模型的实体数据模型向导 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="307be-234">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span></span>


<span data-ttu-id="307be-235">完成实体数据模型向导后，将打开实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="307be-235">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="307be-236">设计器应显示电影数据库表 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="307be-236">The Designer should display the Movies database table (see Figure 7).</span></span>


<span data-ttu-id="307be-237">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="307be-237">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span></span>

<span data-ttu-id="307be-238">**图 07**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="307be-238">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span></span>


<span data-ttu-id="307be-239">我们需要进行一次更改，我们继续操作之前。</span><span class="sxs-lookup"><span data-stu-id="307be-239">We need to make one change before we continue.</span></span> <span data-ttu-id="307be-240">实体数据向导将生成一个名为电影模型类，表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="307be-240">The Entity Data Wizard generates a model class named Movies that represents the Movies database table.</span></span> <span data-ttu-id="307be-241">因为我们将使用影片类来表示特定电影，我们需要修改的类的名称*电影*而不是*电影*（单数而复数形式）。</span><span class="sxs-lookup"><span data-stu-id="307be-241">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="307be-242">双击设计器图面上的类的名称，并将影片中的类的名称更改为影片。</span><span class="sxs-lookup"><span data-stu-id="307be-242">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="307be-243">此更改后，单击**保存**按钮 （软盘图标） 生成电影类。</span><span class="sxs-lookup"><span data-stu-id="307be-243">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="307be-244">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="307be-244">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="307be-245">下一步是创建 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="307be-245">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="307be-246">控制器负责控制用户如何与 ASP.NET MVC 应用程序交互。</span><span class="sxs-lookup"><span data-stu-id="307be-246">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="307be-247">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="307be-247">Follow these steps:</span></span>

1. <span data-ttu-id="307be-248">在解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**。</span><span class="sxs-lookup"><span data-stu-id="307be-248">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="307be-249">在添加控制器对话框中，输入名称*HomeController*并选中复选框标记为**添加用于创建、 更新和详细信息的方案的操作方法**（请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="307be-249">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="307be-250">单击**添加**按钮，将新的控制器添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="307be-250">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="307be-251">完成这些步骤后，将创建列表 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="307be-251">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="307be-252">请注意，它包含命名索引，详细信息，创建、 方法和编辑。</span><span class="sxs-lookup"><span data-stu-id="307be-252">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="307be-253">在以下部分中，我们将添加必要的代码来获取这些方法能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="307be-253">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


<span data-ttu-id="307be-254">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="307be-254">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span></span>

<span data-ttu-id="307be-255">**图 08**： 添加新的 ASP.NET MVC 控制器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="307be-255">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span></span>


<span data-ttu-id="307be-256">**列表 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="307be-256">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a><span data-ttu-id="307be-257">列出数据库记录</span><span class="sxs-lookup"><span data-stu-id="307be-257">Listing Database Records</span></span>

<span data-ttu-id="307be-258">Home 控制器的 index （） 方法是 ASP.NET MVC 应用程序的默认方法。</span><span class="sxs-lookup"><span data-stu-id="307be-258">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="307be-259">ASP.NET MVC 应用程序运行时，index （） 方法是调用的第一个控制器方法。</span><span class="sxs-lookup"><span data-stu-id="307be-259">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="307be-260">我们将使用 index （） 方法以显示电影数据库表中的记录的列表。</span><span class="sxs-lookup"><span data-stu-id="307be-260">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="307be-261">我们将充分利用数据库我们之前创建若要检索具有 index （） 方法的电影数据库记录的模型类。</span><span class="sxs-lookup"><span data-stu-id="307be-261">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="307be-262">我已修改中列出的 2 的 HomeController 类，以使其包含名为的新私有字段\_db。</span><span class="sxs-lookup"><span data-stu-id="307be-262">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="307be-263">MoviesDBEntities 类表示我们的数据库模型，并且我们将使用此类与我们的数据库进行通信。</span><span class="sxs-lookup"><span data-stu-id="307be-263">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="307be-264">我已修改中列出的 2 的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="307be-264">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="307be-265">Index （） 方法使用 MoviesDBEntities 类来从电影数据库表中检索的所有影片记录。</span><span class="sxs-lookup"><span data-stu-id="307be-265">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="307be-266">表达式 *\_db。MovieSet.ToList()*返回电影数据库表中的所有影片记录的列表。</span><span class="sxs-lookup"><span data-stu-id="307be-266">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="307be-267">影片列表传递给视图。</span><span class="sxs-lookup"><span data-stu-id="307be-267">The list of movies is passed to the view.</span></span> <span data-ttu-id="307be-268">获取传递给 View() 方法的任何内容获取传递给视图作为视图数据。</span><span class="sxs-lookup"><span data-stu-id="307be-268">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="307be-269">**列出 2 – Controllers/HomeController.vb （修改后的索引方法）**</span><span class="sxs-lookup"><span data-stu-id="307be-269">**Listing 2 – Controllers/HomeController.vb (modified Index method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

<span data-ttu-id="307be-270">Index （） 方法将返回名为索引视图。</span><span class="sxs-lookup"><span data-stu-id="307be-270">The Index() method returns a view named Index.</span></span> <span data-ttu-id="307be-271">我们需要创建此视图以显示的电影数据库记录的列表。</span><span class="sxs-lookup"><span data-stu-id="307be-271">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="307be-272">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="307be-272">Follow these steps:</span></span>


<span data-ttu-id="307be-273">你应该能够生成你的项目 (选择菜单选项**生成，生成解决方案**) 在打开之前**添加视图**对话框或没有类将出现在**查看数据类**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="307be-273">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="307be-274">右键单击在代码编辑器中的 index （） 方法，然后选择菜单选项**添加视图**（请参阅图 9）。</span><span class="sxs-lookup"><span data-stu-id="307be-274">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="307be-275">在添加视图对话框中，验证复选框标记为**创建强类型化视图**已选中。</span><span class="sxs-lookup"><span data-stu-id="307be-275">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="307be-276">从**查看内容**下拉列表中，选择值*列表*。</span><span class="sxs-lookup"><span data-stu-id="307be-276">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="307be-277">从**查看数据类**下拉列表中，选择值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="307be-277">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="307be-278">单击添加按钮以创建新查看 （请参阅图 10）。</span><span class="sxs-lookup"><span data-stu-id="307be-278">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="307be-279">完成这些步骤后，名为 Index.aspx 的新视图添加到 Views\Home 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="307be-279">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="307be-280">索引视图的内容包含在列出 3 中。</span><span class="sxs-lookup"><span data-stu-id="307be-280">The contents of the Index view are included in Listing 3.</span></span>


<span data-ttu-id="307be-281">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="307be-281">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span></span>

<span data-ttu-id="307be-282">**图 09**： 添加视图的控制器操作 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="307be-282">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span></span>


<span data-ttu-id="307be-283">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="307be-283">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span></span>

<span data-ttu-id="307be-284">**图 10**： 使用添加视图对话框创建新视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="307be-284">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span></span>


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

<span data-ttu-id="307be-285">索引视图显示所有从 HTML 表内的电影数据库表的电影记录。</span><span class="sxs-lookup"><span data-stu-id="307be-285">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="307be-286">该视图包含一个 For 循环访问由 ViewData.Model 属性表示每个影片每个循环。</span><span class="sxs-lookup"><span data-stu-id="307be-286">The view contains a For Each loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="307be-287">如果通过点击 F5 键运行应用程序，你将看到图 11 中的 web 页。</span><span class="sxs-lookup"><span data-stu-id="307be-287">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


<span data-ttu-id="307be-288">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="307be-288">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span></span>

<span data-ttu-id="307be-289">**图 11**: 索引视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="307be-289">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="307be-290">创建新的数据库记录</span><span class="sxs-lookup"><span data-stu-id="307be-290">Creating New Database Records</span></span>

<span data-ttu-id="307be-291">我们在上一节中创建的索引视图包括用于创建新的数据库记录的链接。</span><span class="sxs-lookup"><span data-stu-id="307be-291">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="307be-292">让我们继续操作，实现逻辑，并且创建用于创建新的影片数据库记录所必需的视图。</span><span class="sxs-lookup"><span data-stu-id="307be-292">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="307be-293">Home 控制器包含名为 create （） 的两个方法。</span><span class="sxs-lookup"><span data-stu-id="307be-293">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="307be-294">第一种 create （） 方法没有任何参数。</span><span class="sxs-lookup"><span data-stu-id="307be-294">The first Create() method has no parameters.</span></span> <span data-ttu-id="307be-295">Create （） 方法的此重载用于显示用于创建新的影片数据库记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="307be-295">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="307be-296">第二个 create （） 方法有一个 FormCollection 参数。</span><span class="sxs-lookup"><span data-stu-id="307be-296">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="307be-297">创建新的影片的 HTML 窗体发布到服务器时，将调用 create （） 方法的此重载。</span><span class="sxs-lookup"><span data-stu-id="307be-297">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="307be-298">请注意，此第二个 create （） 方法 AcceptVerbs 属性，以防止方法被调用，除非执行 HTTP Post 操作。</span><span class="sxs-lookup"><span data-stu-id="307be-298">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP Post operation is performed.</span></span>

<span data-ttu-id="307be-299">列出 4 中的更新 HomeController 类中修改了此第二个 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="307be-299">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="307be-300">Create （） 方法的新版本接受电影参数，并包含电影数据库表中插入新的影片的逻辑。</span><span class="sxs-lookup"><span data-stu-id="307be-300">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="307be-301">请注意绑定属性。</span><span class="sxs-lookup"><span data-stu-id="307be-301">Notice the Bind attribute.</span></span> <span data-ttu-id="307be-302">因为我们不想更新从 HTML 窗体的电影 Id 属性，我们需要此属性中显式排除。</span><span class="sxs-lookup"><span data-stu-id="307be-302">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


<span data-ttu-id="307be-303">**列出 4 – Controllers\HomeController.vb （修改后的创建方法）**</span><span class="sxs-lookup"><span data-stu-id="307be-303">**Listing 4 – Controllers\HomeController.vb (modified Create method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

<span data-ttu-id="307be-304">Visual Studio 可以轻松地创建用于创建新的影片数据库窗体记录 （请参阅图 12）。</span><span class="sxs-lookup"><span data-stu-id="307be-304">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="307be-305">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="307be-305">Follow these steps:</span></span>

1. <span data-ttu-id="307be-306">右键单击在代码编辑器中的 create （） 方法，然后选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="307be-306">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="307be-307">验证该复选框标记为**创建强类型化视图**已选中。</span><span class="sxs-lookup"><span data-stu-id="307be-307">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="307be-308">从**查看内容**下拉列表中，选择值*创建*。</span><span class="sxs-lookup"><span data-stu-id="307be-308">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="307be-309">从**查看数据类**下拉列表中，选择值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="307be-309">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="307be-310">单击**添加**按钮以创建新视图。</span><span class="sxs-lookup"><span data-stu-id="307be-310">Click the **Add** button to create the new view.</span></span>


<span data-ttu-id="307be-311">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="307be-311">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span></span>

<span data-ttu-id="307be-312">**图 12**： 添加 Create 视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="307be-312">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span></span>


<span data-ttu-id="307be-313">Visual Studio 视图列出 5 中会自动生成。</span><span class="sxs-lookup"><span data-stu-id="307be-313">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="307be-314">此视图包含 HTML 窗体，包括字段对应于每个电影类的属性。</span><span class="sxs-lookup"><span data-stu-id="307be-314">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="307be-315">**列出 5 – Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="307be-315">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="307be-316">生成的添加视图对话框中的 HTML 格式生成 Id 窗体字段。</span><span class="sxs-lookup"><span data-stu-id="307be-316">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="307be-317">Id 列是标识列，因为我们不需要此窗体字段，你可以安全地删除它。</span><span class="sxs-lookup"><span data-stu-id="307be-317">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="307be-318">添加 Create 视图后，你可以向数据库添加新的影片记录。</span><span class="sxs-lookup"><span data-stu-id="307be-318">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="307be-319">通过按 F5 键运行你的应用程序并单击新创建的链接以查看图 13 中的窗体。</span><span class="sxs-lookup"><span data-stu-id="307be-319">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="307be-320">如果完成并提交表单时，会创建新的影片数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-320">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="307be-321">请注意你自动获得窗体验证。</span><span class="sxs-lookup"><span data-stu-id="307be-321">Notice that you get form validation automatically.</span></span> <span data-ttu-id="307be-322">如果你忘记输入发布日期，对于影片，或输入无效的发布日期，然后重新显示窗体，并突出显示发布日期字段。</span><span class="sxs-lookup"><span data-stu-id="307be-322">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


<span data-ttu-id="307be-323">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="307be-323">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span></span>

<span data-ttu-id="307be-324">**图 13**： 创建新的影片数据库记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="307be-324">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="307be-325">编辑现有的数据库记录</span><span class="sxs-lookup"><span data-stu-id="307be-325">Editing Existing Database Records</span></span>

<span data-ttu-id="307be-326">在前面的部分中，我们将讨论如何列表，以及如何创建新的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-326">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="307be-327">在此最后一节，我们将讨论如何可以编辑现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-327">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="307be-328">首先，我们需要生成编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="307be-328">First, we need to generate the Edit form.</span></span> <span data-ttu-id="307be-329">此步骤很容易，因为 Visual Studio 将生成为我们的编辑窗体自动。</span><span class="sxs-lookup"><span data-stu-id="307be-329">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="307be-330">在 Visual Studio 代码编辑器中打开 HomeController.vb 类，并按照以下步骤：</span><span class="sxs-lookup"><span data-stu-id="307be-330">Open the HomeController.vb class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="307be-331">右键单击在代码编辑器中的 edit （） 方法，然后选择菜单选项**添加视图**（请参阅图 14）。</span><span class="sxs-lookup"><span data-stu-id="307be-331">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="307be-332">选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="307be-332">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="307be-333">从**查看内容**下拉列表中，选择值*编辑*。</span><span class="sxs-lookup"><span data-stu-id="307be-333">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="307be-334">从**查看数据类**下拉列表中，选择值*MovieApp.Movie*。</span><span class="sxs-lookup"><span data-stu-id="307be-334">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="307be-335">单击**添加**按钮以创建新视图。</span><span class="sxs-lookup"><span data-stu-id="307be-335">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="307be-336">完成这些步骤将添加名为 Edit.aspx 到 Views\Home 文件夹的新视图。</span><span class="sxs-lookup"><span data-stu-id="307be-336">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="307be-337">此视图包含用于编辑电影记录 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="307be-337">This view contains an HTML form for editing a movie record.</span></span>


<span data-ttu-id="307be-338">[![新项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="307be-338">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span></span>

<span data-ttu-id="307be-339">**图 14**： 添加编辑视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="307be-339">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="307be-340">编辑视图包含一个 HTML 窗体字段，它对应于电影 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="307be-340">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="307be-341">因为你不希望编辑的 Id 属性的值的人员，你应删除此窗体字段。</span><span class="sxs-lookup"><span data-stu-id="307be-341">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="307be-342">最后，我们需要修改主控制器，以便它支持编辑的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-342">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="307be-343">更新的 HomeController 类包含在列出 6。</span><span class="sxs-lookup"><span data-stu-id="307be-343">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="307be-344">**列出 6 – Controllers\HomeController.vb （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="307be-344">**Listing 6 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

<span data-ttu-id="307be-345">在列出 6 中，我已经向 edit （） 方法的两个重载添加其他逻辑。</span><span class="sxs-lookup"><span data-stu-id="307be-345">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="307be-346">第一种 edit （） 方法返回到传递给方法的 Id 参数对应的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="307be-346">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="307be-347">第二个重载执行到影片记录更新，在数据库中。</span><span class="sxs-lookup"><span data-stu-id="307be-347">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="307be-348">请注意，你必须检索原始的电影，，然后调用 ApplyPropertyChanges()，以更新数据库中已有的电影。</span><span class="sxs-lookup"><span data-stu-id="307be-348">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="307be-349">摘要</span><span class="sxs-lookup"><span data-stu-id="307be-349">Summary</span></span>

<span data-ttu-id="307be-350">本教程的目的是体验的为你提供一种生成 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="307be-350">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="307be-351">我希望你发现生成 ASP.NET MVC web 应用程序是非常类似于生成 Active Server Pages 或 ASP.NET 应用程序的体验。</span><span class="sxs-lookup"><span data-stu-id="307be-351">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="307be-352">在本教程中，我们将探讨的 ASP.NET MVC framework 仅最基本的功能。</span><span class="sxs-lookup"><span data-stu-id="307be-352">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="307be-353">在将来的教程中，我们深入了解主题，如控制器、 控制器操作、 视图、 查看数据和 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="307be-353">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="307be-354">上一篇</span><span class="sxs-lookup"><span data-stu-id="307be-354">Previous</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
