---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '第 1 部分: 概述和文件-> 新建项目 |Microsoft 文档'
author: jongalloway
description: 本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。 第 1 部分介绍如何概述和文件-> 新项目。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 2082927d18c95563893da199d60347fa15952446
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="7cd6a-104">第 1 部分: 概述和文件-> 新建项目</span><span class="sxs-lookup"><span data-stu-id="7cd6a-104">Part 1: Overview and File->New Project</span></span>
====================
<span data-ttu-id="7cd6a-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="7cd6a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="7cd6a-106">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="7cd6a-107">MVC 音乐商店是一个轻型示例存储区实现，该类销售音乐集联机，并实现基本的站点管理、 用户登录，和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="7cd6a-108">本系列教程详细介绍所有生成 ASP.NET MVC 音乐商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="7cd6a-109">第 1 部分介绍概述和文件-&gt;新项目。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-109">Part 1 covers Overview and File-&gt;New Project.</span></span>


## <a name="overview"></a><span data-ttu-id="7cd6a-110">概述</span><span class="sxs-lookup"><span data-stu-id="7cd6a-110">Overview</span></span>

<span data-ttu-id="7cd6a-111">MVC 音乐商店是，从而引入并说明如何使用 ASP.NET MVC 和 Visual Web Developer web 开发的分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="7cd6a-112">我们将启动速度慢，因此初学者级别 web 开发体验没什么关系。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="7cd6a-113">我们将构建的应用程序是简单的音乐商店。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="7cd6a-114">有向应用程序的三个主要部分： 购物、 结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="7cd6a-115">访问者可以浏览按风格的专辑：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="7cd6a-116">它们可以查看单个唱片集并将其添加到购物车：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="7cd6a-117">它们可以查看其购物车，删除它们不再需要的任何项：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="7cd6a-118">在继续结帐将提示他们登录或注册用户帐户。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="7cd6a-119">创建帐户之后，它们可以通过填写传送和付款信息完成顺序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="7cd6a-120">若要为简单起见，我们正在运行了令人惊叹的升级： 所有内容都是免费的如果他们输入促销代码"免费"！</span><span class="sxs-lookup"><span data-stu-id="7cd6a-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="7cd6a-121">排序之后, 他们将看到简单确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="7cd6a-122">除了客户 faceing 页中，我们将生成一个管理员部分，其中显示的专辑，管理员可以从中创建、 编辑、 列表，并删除唱片集：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-122">In addition to customer-faceing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="7cd6a-123">1.文件-&gt;新项目</span><span class="sxs-lookup"><span data-stu-id="7cd6a-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="7cd6a-124">安装软件</span><span class="sxs-lookup"><span data-stu-id="7cd6a-124">Installing the software</span></span>

<span data-ttu-id="7cd6a-125">本教程将会开始通过创建使用免费 Visual Web Developer 2010 Express （这是可用），为新的 ASP.NET MVC 3 项目，然后我们将以增量方式添加功能可以创建一个完整的正常运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="7cd6a-126">与此同时，我们将介绍数据库访问、 窗体发布方案、 数据验证使用母版页提供一致的页面布局使用 AJAX 页更新和验证、 用户登录名和详细信息。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="7cd6a-127">你可以遵循步骤，也可以在下载完成的应用程序从[MVC 音乐商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="7cd6a-128">可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 Express SP1 （免费版本的 Visual Studio 2010） 生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="7cd6a-129">我们将使用 SQL Server Compact （也可用） 来承载数据库。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="7cd6a-130">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>


- <span data-ttu-id="7cd6a-131">[Visual Studio Web Developer Express SP1 系统必备组件]</span><span class="sxs-lookup"><span data-stu-id="7cd6a-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="7cd6a-132">[ASP.NET MVC 3 Tools 更新]</span><span class="sxs-lookup"><span data-stu-id="7cd6a-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="7cd6a-133">[SQL Server Compact 4.0]-包括运行时和工具支持</span><span class="sxs-lookup"><span data-stu-id="7cd6a-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>


### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="7cd6a-134">创建新的 ASP.NET MVC 3 项目</span><span class="sxs-lookup"><span data-stu-id="7cd6a-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="7cd6a-135">我们将开始通过从在 Visual Web Developer 的文件菜单中选择"新建项目"。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="7cd6a-136">这将显示新项目对话框。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="7cd6a-137">我们将选择的 Visual C#&gt; Web 模板组在左侧，然后在中间栏中选择"ASP.NET MVC 3 Web 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="7cd6a-138">将命名你的项目 MvcMusicStore 并按确定按钮。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="7cd6a-139">这将显示辅助对话框，我们使我们的项目中的某些 MVC 特定设置。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="7cd6a-140">选择以下项：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-140">Select the following:</span></span>

<span data-ttu-id="7cd6a-141">项目模板-选择空</span><span class="sxs-lookup"><span data-stu-id="7cd6a-141">Project Template - select Empty</span></span>

<span data-ttu-id="7cd6a-142">查看引擎-选择 Razor</span><span class="sxs-lookup"><span data-stu-id="7cd6a-142">View Engine - select Razor</span></span>

<span data-ttu-id="7cd6a-143">使用 HTML5 语义标记的检查</span><span class="sxs-lookup"><span data-stu-id="7cd6a-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="7cd6a-144">验证你的设置是如下所示，然后按确定按钮。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="7cd6a-145">这将创建我们的项目。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-145">This will create our project.</span></span> <span data-ttu-id="7cd6a-146">让我们看看已添加到我们在右侧的解决方案资源管理器的应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="7cd6a-147">空的 MVC 3 模板并不完全为空 – 它将添加基本的文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="7cd6a-148">ASP.NET MVC 利用的一些基本的命名约定的文件夹名称：</span><span class="sxs-lookup"><span data-stu-id="7cd6a-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="7cd6a-149">**Folder**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-149">**Folder**</span></span> | <span data-ttu-id="7cd6a-150">**目的**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="7cd6a-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-151">**/Controllers**</span></span> | <span data-ttu-id="7cd6a-152">控制器响应输入从浏览器时，决定要处理的问题，并向用户返回响应的内容。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="7cd6a-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-153">**/Views**</span></span> | <span data-ttu-id="7cd6a-154">视图保存我们 UI 模板</span><span class="sxs-lookup"><span data-stu-id="7cd6a-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="7cd6a-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-155">**/Models**</span></span> | <span data-ttu-id="7cd6a-156">模型保存和操作数据</span><span class="sxs-lookup"><span data-stu-id="7cd6a-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="7cd6a-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-157">**/Content**</span></span> | <span data-ttu-id="7cd6a-158">此文件夹包含我们的图像、 CSS 和任何其他静态内容</span><span class="sxs-lookup"><span data-stu-id="7cd6a-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="7cd6a-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="7cd6a-159">**/Scripts**</span></span> | <span data-ttu-id="7cd6a-160">此文件夹包含我们 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="7cd6a-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="7cd6a-161">因为默认情况下的 ASP.NET MVC framework 使用"配置的约定"方法，并使基于文件夹命名约定某些默认假设即使在空的 ASP.NET MVC 应用程序中包含这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="7cd6a-162">例如，控制器看起来的 Views 文件夹中视图的默认情况下您无需显式指定此设置在代码中。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="7cd6a-163">默认约定仍坚持减少的代码需要编写，还可使其便于其他开发人员了解你的项目。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="7cd6a-164">我们将介绍这些约定详细构建我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7cd6a-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7cd6a-165">下一篇</span><span class="sxs-lookup"><span data-stu-id="7cd6a-165">Next</span></span>](mvc-music-store-part-2.md)
