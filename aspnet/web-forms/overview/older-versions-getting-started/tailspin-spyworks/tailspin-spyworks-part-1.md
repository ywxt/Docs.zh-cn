---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第 1 部分： 文件-> 新建项目 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 1 部分介绍概述和文件 / 新建项目。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: a1b9681516e626b6a0eec420b168a74e05d88afb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892460"
---
<a name="part-1-file--new-project"></a><span data-ttu-id="9dc0c-104">第 1 部分： 文件-> 新建项目</span><span class="sxs-lookup"><span data-stu-id="9dc0c-104">Part 1: File-> New Project</span></span>
====================
<span data-ttu-id="9dc0c-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="9dc0c-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="9dc0c-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="9dc0c-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="9dc0c-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="9dc0c-109">第 1 部分介绍概述和文件 / 新建项目。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-109">Part 1 covers Overview and File/New Project.</span></span>


## <a id="_Toc260221666"></a>  <span data-ttu-id="9dc0c-110">概述</span><span class="sxs-lookup"><span data-stu-id="9dc0c-110">Overview</span></span>

<span data-ttu-id="9dc0c-111">本教程是 ASP.NET WebForms 的简介。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="9dc0c-112">我们将启动速度慢，因此初学者级别 web 开发体验没什么关系。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="9dc0c-113">我们将构建的应用程序是一个简单的在线商店。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)


<span data-ttu-id="9dc0c-114">访问者可以浏览按类别排列产品：</span><span class="sxs-lookup"><span data-stu-id="9dc0c-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="9dc0c-115">它们可以查看单个产品，并将其添加到购物车：</span><span class="sxs-lookup"><span data-stu-id="9dc0c-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="9dc0c-116">它们可以查看其购物车，删除它们不再需要的任何项：</span><span class="sxs-lookup"><span data-stu-id="9dc0c-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="9dc0c-117">在继续结帐将提示他们到</span><span class="sxs-lookup"><span data-stu-id="9dc0c-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="9dc0c-118">排序之后, 他们将看到简单确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="9dc0c-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)


<span data-ttu-id="9dc0c-119">我们将通过在 Visual Studio 2010 中，创建新的 ASP.NET WebForms 项目开始，我们将以增量方式添加功能可以创建一个完整的正常运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="9dc0c-120">与此同时，我们将介绍数据库访问权限、 列表和网格视图、 数据更新页、 数据验证、 使用母版页提供一致的页面布局、 AJAX、 验证、 用户成员身份和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="9dc0c-121">您可以执行步骤，或者你可以下载已完成应用程序 [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="9dc0c-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="9dc0c-122">你可以使用 Visual Studio 2010 或免费的 Visual Web Developer 2010 从[ https://www.microsoft.com/express/Web/ ](https://www.microsoft.com/express/Web/)。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="9dc0c-123">若要生成应用程序，可以使用 SQL Server 或可用 SQL Server Express 到主机数据库。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a>  <span data-ttu-id="9dc0c-124">文件 / 新项目</span><span class="sxs-lookup"><span data-stu-id="9dc0c-124">File / New Project</span></span>

<span data-ttu-id="9dc0c-125">我们将开始通过从 Visual Studio 中的文件菜单中选择新项目。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="9dc0c-126">这将显示新项目对话框。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="9dc0c-127">我们将选择的 Visual C# / Web 模板组在左侧，，然后在中间栏中选择"ASP.NET Web 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="9dc0c-128">将命名你的项目 TailspinSpyworks 并按确定按钮。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="9dc0c-129">这将创建我们的项目。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-129">This will create our project.</span></span> <span data-ttu-id="9dc0c-130">让我们看看我们在右侧的解决方案资源管理器的应用程序中包括的文件夹。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="9dc0c-131">空的解决方案不完全为空 – 它将添加基本的文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="9dc0c-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="9dc0c-132">请注意实现的 ASP.NET 4 默认项目模板的约定。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="9dc0c-133">"帐户"文件夹为 ASP 实现基本用户界面。NET 的成员资格子系统。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="9dc0c-134">"脚本"文件夹用作客户端 JavaScript 文件的存储库并核心 jQuery.js 文件都可用的默认值。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="9dc0c-135">"样式"文件夹用于组织我们网站的视觉对象 （CSS 样式表）</span><span class="sxs-lookup"><span data-stu-id="9dc0c-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="9dc0c-136">当我们按下 F5 以运行我们的应用程序和呈现 default.aspx 页时我们看到以下内容。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="9dc0c-137">我们第一个应用程序增强功能就是使用 CSS 类和关联的图像文件将呈现我们希望我们 Tailspin Spyworks 的应用程序 visual asthetics 替换默认 WebForms 模板中的 Style.css 文件。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="9dc0c-138">这样做之后我们 default.aspx 页上呈现如下。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="9dc0c-139">请注意位于顶部的映像链接页以及已添加到母版页的菜单项的权限。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="9dc0c-140">仅"登录"和"帐户"链接指向的存在 （由默认模板生成） 的页面，但我们将实现构建我们的应用程序的页面的其余部分。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="9dc0c-141">我们还将将母版页重新定位到的样式目录。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="9dc0c-142">虽然这是只是首选项它可能简化操作有点如果我们决定在将来执行我们的应用程序"skinable"。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="9dc0c-143">在执行此我们将需要更改母版页后所有的.aspx 文件中的引用默认生成 ASP.NET WebForms 页。</span><span class="sxs-lookup"><span data-stu-id="9dc0c-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9dc0c-144">下一篇</span><span class="sxs-lookup"><span data-stu-id="9dc0c-144">Next</span></span>](tailspin-spyworks-part-2.md)
