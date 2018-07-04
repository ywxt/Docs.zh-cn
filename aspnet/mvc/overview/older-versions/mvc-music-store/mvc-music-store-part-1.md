---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第 1 部分： 概述和文件-> 新建项目 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 1 部分介绍如何概述和文件-> 新项目。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: c03b62db2227c167c68ca5cf8174e4322658d39d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377884"
---
<a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="bf908-104">第 1 部分： 概述和文件-> 新建项目</span><span class="sxs-lookup"><span data-stu-id="bf908-104">Part 1: Overview and File->New Project</span></span>
====================
<span data-ttu-id="bf908-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="bf908-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="bf908-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf908-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="bf908-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="bf908-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="bf908-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="bf908-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="bf908-109">第 1 部分介绍了概述和文件-&gt;新项目。</span><span class="sxs-lookup"><span data-stu-id="bf908-109">Part 1 covers Overview and File-&gt;New Project.</span></span>


## <a name="overview"></a><span data-ttu-id="bf908-110">概述</span><span class="sxs-lookup"><span data-stu-id="bf908-110">Overview</span></span>

<span data-ttu-id="bf908-111">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Web Developer web 开发的分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf908-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="bf908-112">我们将启动速度慢，因此初学者级别 web 开发体验也没关系。</span><span class="sxs-lookup"><span data-stu-id="bf908-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="bf908-113">我们将构建的应用程序是简单音乐应用商店。</span><span class="sxs-lookup"><span data-stu-id="bf908-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="bf908-114">有向应用程序的三个主要部分： 购物、 结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="bf908-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="bf908-115">访问者可以浏览按流派的唱片集：</span><span class="sxs-lookup"><span data-stu-id="bf908-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="bf908-116">他们可以查看一个唱片集，并将其添加到其购物车：</span><span class="sxs-lookup"><span data-stu-id="bf908-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="bf908-117">他们可以查看其购物车，删除它们不再需要任何的项：</span><span class="sxs-lookup"><span data-stu-id="bf908-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="bf908-118">继续下的一步要签出将提示他们登录或注册一个用户帐户。</span><span class="sxs-lookup"><span data-stu-id="bf908-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="bf908-119">创建帐户后，他们可以通过填写传送和付款信息完成顺序。</span><span class="sxs-lookup"><span data-stu-id="bf908-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="bf908-120">为了简单起见，我们将运行令人惊叹的升级： 所有内容都是免费的如果输入促销代码"免费"！</span><span class="sxs-lookup"><span data-stu-id="bf908-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="bf908-121">排序后，他们将看到简单确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="bf908-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="bf908-122">除了客户 faceing 页，我们还将生成一个管理员部分，其中显示了一系列唱片集从其管理员可以创建、 编辑、 并删除唱片集：</span><span class="sxs-lookup"><span data-stu-id="bf908-122">In addition to customer-faceing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="bf908-123">1.文件-&gt;新项目</span><span class="sxs-lookup"><span data-stu-id="bf908-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="bf908-124">安装软件</span><span class="sxs-lookup"><span data-stu-id="bf908-124">Installing the software</span></span>

<span data-ttu-id="bf908-125">本教程将首先创建一个新的 ASP.NET MVC 3 项目使用免费的 Visual Web Developer 2010 Express （这是免费的），，然后我们将以增量方式添加功能，可创建一个完整的正常运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf908-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="bf908-126">此过程中，我们将介绍数据库访问权限、 窗体发布方案、 数据验证、 使用母版页对于一致的页面布局，使用 AJAX 页面更新和验证、 用户登录名和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bf908-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="bf908-127">您可以照着操作步骤，也可以下载完整的应用程序从[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="bf908-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="bf908-128">可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 速成版 SP1 （Visual Studio 2010 的免费版本） 生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf908-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="bf908-129">我们将使用 SQL Server Compact （同样免费） 来承载数据库。</span><span class="sxs-lookup"><span data-stu-id="bf908-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="bf908-130">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="bf908-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>


- <span data-ttu-id="bf908-131">[Visual Studio Web Developer Express SP1 系统必备组件]</span><span class="sxs-lookup"><span data-stu-id="bf908-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="bf908-132">[ASP.NET MVC 3 工具更新]</span><span class="sxs-lookup"><span data-stu-id="bf908-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="bf908-133">[SQL Server Compact 4.0]-包括运行时和工具支持</span><span class="sxs-lookup"><span data-stu-id="bf908-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>


### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="bf908-134">创建新的 ASP.NET MVC 3 项目</span><span class="sxs-lookup"><span data-stu-id="bf908-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="bf908-135">我们将开始通过 Visual Web Developer 中的文件菜单中选择"新建项目"。</span><span class="sxs-lookup"><span data-stu-id="bf908-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="bf908-136">此时会打开新建项目对话框。</span><span class="sxs-lookup"><span data-stu-id="bf908-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="bf908-137">我们将选择 Visual C#-&gt; Web 模板组在左侧，然后在中间栏中选择"ASP.NET MVC 3 Web 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="bf908-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="bf908-138">为项目 MvcMusicStore 命名并按确定按钮。</span><span class="sxs-lookup"><span data-stu-id="bf908-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="bf908-139">这将显示辅助对话框使我们可以使我们的项目中的某些 MVC 特定设置。</span><span class="sxs-lookup"><span data-stu-id="bf908-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="bf908-140">选择以下项：</span><span class="sxs-lookup"><span data-stu-id="bf908-140">Select the following:</span></span>

<span data-ttu-id="bf908-141">项目模板-选择为空</span><span class="sxs-lookup"><span data-stu-id="bf908-141">Project Template - select Empty</span></span>

<span data-ttu-id="bf908-142">视图引擎-选择 Razor</span><span class="sxs-lookup"><span data-stu-id="bf908-142">View Engine - select Razor</span></span>

<span data-ttu-id="bf908-143">使用 HTML5 语义标记的检查</span><span class="sxs-lookup"><span data-stu-id="bf908-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="bf908-144">请验证你的设置是如下所示，然后按确定按钮。</span><span class="sxs-lookup"><span data-stu-id="bf908-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="bf908-145">这将创建我们的项目。</span><span class="sxs-lookup"><span data-stu-id="bf908-145">This will create our project.</span></span> <span data-ttu-id="bf908-146">让我们看看已添加到我们在右侧的解决方案资源管理器中的应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="bf908-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="bf908-147">空 MVC 3 模板并没有完全为空，它将添加基本的文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="bf908-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="bf908-148">ASP.NET MVC 使用的一些基本的命名约定的文件夹名称：</span><span class="sxs-lookup"><span data-stu-id="bf908-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="bf908-149">**文件夹**</span><span class="sxs-lookup"><span data-stu-id="bf908-149">**Folder**</span></span> | <span data-ttu-id="bf908-150">**目的**</span><span class="sxs-lookup"><span data-stu-id="bf908-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="bf908-151">**/ 控制器**</span><span class="sxs-lookup"><span data-stu-id="bf908-151">**/Controllers**</span></span> | <span data-ttu-id="bf908-152">控制器响应从浏览器输入，决定要处理的问题，并向用户返回响应的内容。</span><span class="sxs-lookup"><span data-stu-id="bf908-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="bf908-153">**/ 视图**</span><span class="sxs-lookup"><span data-stu-id="bf908-153">**/Views**</span></span> | <span data-ttu-id="bf908-154">视图保存我们的 UI 模板</span><span class="sxs-lookup"><span data-stu-id="bf908-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="bf908-155">**/ 模型**</span><span class="sxs-lookup"><span data-stu-id="bf908-155">**/Models**</span></span> | <span data-ttu-id="bf908-156">模型保存和操作数据</span><span class="sxs-lookup"><span data-stu-id="bf908-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="bf908-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="bf908-157">**/Content**</span></span> | <span data-ttu-id="bf908-158">此文件夹包含我们的图像、 CSS 和任何其他静态内容</span><span class="sxs-lookup"><span data-stu-id="bf908-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="bf908-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="bf908-159">**/Scripts**</span></span> | <span data-ttu-id="bf908-160">此文件夹包含我们的 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="bf908-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="bf908-161">这些文件夹包含即使在空的 ASP.NET MVC 应用程序，因为默认情况下的 ASP.NET MVC 框架使用"惯例优先于配置"的方法，并默认做了一些假设基于文件夹命名约定。</span><span class="sxs-lookup"><span data-stu-id="bf908-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="bf908-162">例如，控制器视图文件夹中的视图的默认情况下查找而无需显式指定此设置在代码中。</span><span class="sxs-lookup"><span data-stu-id="bf908-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="bf908-163">坚持使用的默认约定可以减少需要编写的代码量还可使其便于其他开发人员了解您的项目。</span><span class="sxs-lookup"><span data-stu-id="bf908-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="bf908-164">我们将介绍这些约定详细构建我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf908-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bf908-165">下一篇</span><span class="sxs-lookup"><span data-stu-id="bf908-165">Next</span></span>](mvc-music-store-part-2.md)
