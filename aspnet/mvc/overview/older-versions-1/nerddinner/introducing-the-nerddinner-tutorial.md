---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: 引入 NerdDinner 教程 |Microsoft 文档
author: shanselman
description: 若要了解新框架的最佳方法是生成一些。 本教程将指导完成如何构建使用 ASP.NE 的较小，但完成后，应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 3d925a7dc89fc0c742468653c5c138a0f1d71231
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="7a121-104">引入 NerdDinner 教程</span><span class="sxs-lookup"><span data-stu-id="7a121-104">Introducing the NerdDinner Tutorial</span></span>
====================
<span data-ttu-id="7a121-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="7a121-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="7a121-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="7a121-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7a121-107">若要了解新框架的最佳方法是生成一些。</span><span class="sxs-lookup"><span data-stu-id="7a121-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="7a121-108">本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 1，应用程序，并介绍了一些背后的核心概念。</span><span class="sxs-lookup"><span data-stu-id="7a121-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="7a121-109">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="7a121-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="7a121-110">NerdDinner 教程</span><span class="sxs-lookup"><span data-stu-id="7a121-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="7a121-111">若要了解新框架的最佳方法是生成一些。</span><span class="sxs-lookup"><span data-stu-id="7a121-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="7a121-112">本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 应用程序，并介绍了一些背后的核心概念。</span><span class="sxs-lookup"><span data-stu-id="7a121-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="7a121-113">我们将生成应用程序称为"NerdDinner"。</span><span class="sxs-lookup"><span data-stu-id="7a121-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="7a121-114">NerdDinner 可以轻松地让人有机会查找和组织晚餐联机：</span><span class="sxs-lookup"><span data-stu-id="7a121-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="7a121-115">NerdDinner 使已注册的用户能够创建、 编辑和删除晚餐。</span><span class="sxs-lookup"><span data-stu-id="7a121-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="7a121-116">它会强制实施跨应用程序的一组一致的验证规则和业务规则：</span><span class="sxs-lookup"><span data-stu-id="7a121-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="7a121-117">访问者可以使用基于 AJAX 的映射来搜索即将到来晚餐正在挂起附近它们：</span><span class="sxs-lookup"><span data-stu-id="7a121-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="7a121-118">单击 dinner 会将他们到详细信息页，以了解更多相关信息：</span><span class="sxs-lookup"><span data-stu-id="7a121-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="7a121-119">如果他们感兴趣参加 dinner 他们可以登录，或在站点上注册：</span><span class="sxs-lookup"><span data-stu-id="7a121-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="7a121-120">然后，他们可以单击基于 AJAX 的回复链接参加会议事件：</span><span class="sxs-lookup"><span data-stu-id="7a121-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="7a121-121">实现 NerdDinner</span><span class="sxs-lookup"><span data-stu-id="7a121-121">Implementing NerdDinner</span></span>

<span data-ttu-id="7a121-122">我们将首先我们 NerdDinner 的应用程序使用的文件-&gt;Visual Studio 中的新项目命令以创建新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="7a121-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="7a121-123">然后，我们将以增量方式添加功能和功能。</span><span class="sxs-lookup"><span data-stu-id="7a121-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="7a121-124">此过程中，我们将介绍：</span><span class="sxs-lookup"><span data-stu-id="7a121-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="7a121-125">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="7a121-125">How to create a new ASP.NET MVC Project</span></span>](# "创建新的 ASP.NET MVC 项目")
2. [<span data-ttu-id="7a121-126">如何创建数据库</span><span class="sxs-lookup"><span data-stu-id="7a121-126">How to create a database</span></span>](# "创建数据库")
3. [<span data-ttu-id="7a121-127">如何生成一个具有业务规则验证模型</span><span class="sxs-lookup"><span data-stu-id="7a121-127">How to build a model with business rule validations</span></span>](# "生成一个具有业务规则验证模型")
4. [<span data-ttu-id="7a121-128">如何使用控制器和视图来实现列表/详细 UI</span><span class="sxs-lookup"><span data-stu-id="7a121-128">How to use controllers and views to implement a listing/details UI</span></span>](# "使用控制器和视图，以实现详细信息列表/用户界面")
5. <span data-ttu-id="7a121-129">[如何提供 CRUD （创建、 读取、 更新、 删除） 数据窗体条目支持](# "提供 CRUD （创建、 读取、 更新、 删除） 数据窗体条目支持")</span><span class="sxs-lookup"><span data-stu-id="7a121-129">[How to provide CRUD (create, read, update, delete) data form entry support](# "Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support")</span></span>
6. [<span data-ttu-id="7a121-130">如何使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="7a121-130">How to use ViewData and implement ViewModel classes</span></span>](# "使用 ViewData 和实现 ViewModel 类")
7. [<span data-ttu-id="7a121-131">如何重新使用 UI 使用母版页和它们</span><span class="sxs-lookup"><span data-stu-id="7a121-131">How to re-use UI using master pages and partials</span></span>](# "重用 UI 使用母版页和它们")
8. [<span data-ttu-id="7a121-132">如何实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="7a121-132">How to implement efficient data paging</span></span>](# "实现高效数据分页")
9. [<span data-ttu-id="7a121-133">如何保护应用程序使用身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="7a121-133">How to secure applications using authentication and authorization</span></span>](# "安全应用程序使用身份验证和授权")
10. [<span data-ttu-id="7a121-134">如何使用 AJAX 提供动态更新</span><span class="sxs-lookup"><span data-stu-id="7a121-134">How to use AJAX to deliver dynamic updates</span></span>](# "到提供动态更新使用 AJAX")
11. [<span data-ttu-id="7a121-135">如何使用 AJAX 实现映射方案</span><span class="sxs-lookup"><span data-stu-id="7a121-135">How to use AJAX to implement mapping scenarios</span></span>](# "到实现映射情况下使用 AJAX")
12. [<span data-ttu-id="7a121-136">如何启用自动的单元测试</span><span class="sxs-lookup"><span data-stu-id="7a121-136">How to enable automated unit testing</span></span>](# "启用自动进行单元测试")

<span data-ttu-id="7a121-137">你可以构建你自己的 NerdDinner 副本从头通过完成每个步骤我们的本章中的演练。</span><span class="sxs-lookup"><span data-stu-id="7a121-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="7a121-138">或者，你可以下载完整的版本的源代码此处： [GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。</span><span class="sxs-lookup"><span data-stu-id="7a121-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="7a121-139">你还可以选择还可以[下载本教程的免费 PDF 版](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)如果你想要阅读本教程脱机。</span><span class="sxs-lookup"><span data-stu-id="7a121-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="7a121-140">可以使用 Visual Studio 2008 或可用 Visual Web Developer 2008 速成版生成该应用程序。</span><span class="sxs-lookup"><span data-stu-id="7a121-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="7a121-141">可以为数据库使用 SQL Server 或可用的 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="7a121-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="7a121-142">你可以安装 ASP.NET MVC、 Visual Web Developer 2008 速成版，和 SQL Server Express （所有免费） 使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="7a121-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="7a121-143">现在让我们开始吧...</span><span class="sxs-lookup"><span data-stu-id="7a121-143">Now let's get started....</span></span>

<span data-ttu-id="7a121-144">现在，我们已介绍了 NerdDinner 是什么，让我们汇总我们袖子并编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="7a121-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="7a121-145">我们将首先通过使用文件-&gt;Visual Studio 来创建 NerdDinner 应用程序中的新项目。</span><span class="sxs-lookup"><span data-stu-id="7a121-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7a121-146">下一篇</span><span class="sxs-lookup"><span data-stu-id="7a121-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
