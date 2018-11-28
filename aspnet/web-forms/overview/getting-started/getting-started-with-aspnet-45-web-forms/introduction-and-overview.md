---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门 |Microsoft Docs
author: Erikre
description: 此分步教程系列将指导您学习生成使用 ASP.NET 4.5 和 Microsoft Visual Studio 截止的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: b9ed6ce4ac13f047f53c56e183433cbd038ea15c
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450679"
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a><span data-ttu-id="dec6c-103">ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门</span><span class="sxs-lookup"><span data-stu-id="dec6c-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013</span></span>
====================
<span data-ttu-id="dec6c-104">通过[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="dec6c-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="dec6c-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="dec6c-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="dec6c-106">此分步教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="dec6c-106">This step-by-step tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> 

## <a name="introduction"></a><span data-ttu-id="dec6c-107">介绍</span><span class="sxs-lookup"><span data-stu-id="dec6c-107">Introduction</span></span>

<span data-ttu-id="dec6c-108">本系列教程将指导您完成创建适用于 Web 和 ASP.NET 4.5 中使用 Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="dec6c-108">This series of tutorials guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio Express 2013 for Web and ASP.NET 4.5.</span></span>

<span data-ttu-id="dec6c-109">应用程序将创建名为**Wingtip Toys**。</span><span class="sxs-lookup"><span data-stu-id="dec6c-109">The application you'll create is named **Wingtip Toys**.</span></span> <span data-ttu-id="dec6c-110">它是销售项在线应用商店前端网站的简化的示例。</span><span class="sxs-lookup"><span data-stu-id="dec6c-110">It's a simplified example of a store front web site that sells items online.</span></span> <span data-ttu-id="dec6c-111">本系列教程重点介绍 ASP.NET 4.5 中提供的新功能。</span><span class="sxs-lookup"><span data-stu-id="dec6c-111">This tutorial series highlights new features available in ASP.NET 4.5.</span></span>

<span data-ttu-id="dec6c-112">注释是欢迎使用，并且我们将采取各种方法来更新本系列教程基于您的建议。</span><span class="sxs-lookup"><span data-stu-id="dec6c-112">Comments are welcome, and we'll make every effort to update this tutorial series based on your suggestions.</span></span>

### <a name="download-completed-project"></a><span data-ttu-id="dec6c-113">下载已完成项目</span><span class="sxs-lookup"><span data-stu-id="dec6c-113">Download completed project</span></span>

<span data-ttu-id="dec6c-114">您可以下载包含已完成本教程的 C# 项目。</span><span class="sxs-lookup"><span data-stu-id="dec6c-114">You can download a C# project that contains the completed tutorial.</span></span>

- <span data-ttu-id="dec6c-115">[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="dec6c-115">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span>

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a><span data-ttu-id="dec6c-116">通过执行相关的 ASP.NET Web 窗体测验查看的内容</span><span class="sxs-lookup"><span data-stu-id="dec6c-116">Review the content by taking the related ASP.NET Web Forms quiz</span></span>

<span data-ttu-id="dec6c-117">完成本教程后，测试你的知识并通过采用加强关键概念[ASP.NET Web 窗体测验](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)。</span><span class="sxs-lookup"><span data-stu-id="dec6c-117">After you complete this tutorial, test your knowledge and reinforce key concepts by taking the [ASP.NET Web Forms Quiz](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001).</span></span> <span data-ttu-id="dec6c-118">此测验专门设计从本教程系列中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="dec6c-118">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="dec6c-119">测验中的每个问题提供的附加指导的链接以及说明。</span><span class="sxs-lookup"><span data-stu-id="dec6c-119">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>

- [<span data-ttu-id="dec6c-120">ASP.NET Web 窗体测验</span><span class="sxs-lookup"><span data-stu-id="dec6c-120">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a><span data-ttu-id="dec6c-121">读者</span><span class="sxs-lookup"><span data-stu-id="dec6c-121">Audience</span></span>

<span data-ttu-id="dec6c-122">本系列教程的目标的读者是经验丰富的开发人员的新 ASP.NET Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="dec6c-122">The intended audience of this tutorial series is experienced developers who are new to ASP.NET Web Forms.</span></span> <span data-ttu-id="dec6c-123">希望本系列教程的开发人员应具备以下技能：</span><span class="sxs-lookup"><span data-stu-id="dec6c-123">A developer interested in this tutorial series should have the following skills:</span></span>

- <span data-ttu-id="dec6c-124">熟悉对象面向编程 (OOP) 语言</span><span class="sxs-lookup"><span data-stu-id="dec6c-124">Familiar with an object oriented programming (OOP) language</span></span>
- <span data-ttu-id="dec6c-125">熟悉 Web 开发概念 (HTML、 CSS、 JavaScript)</span><span class="sxs-lookup"><span data-stu-id="dec6c-125">Familiar with Web development concepts (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="dec6c-126">熟悉关系数据库概念</span><span class="sxs-lookup"><span data-stu-id="dec6c-126">Familiar with relational database concepts</span></span>
- <span data-ttu-id="dec6c-127">熟悉 n 层体系结构概念</span><span class="sxs-lookup"><span data-stu-id="dec6c-127">Familiar with n-tier architecture concepts</span></span>

<span data-ttu-id="dec6c-128">如果您有兴趣查看上面列出的区域，请考虑查看以下内容：</span><span class="sxs-lookup"><span data-stu-id="dec6c-128">If you are interested in reviewing the areas listed above, consider reviewing the following content:</span></span>

- [<span data-ttu-id="dec6c-129">Visual C# 入门</span><span class="sxs-lookup"><span data-stu-id="dec6c-129">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="dec6c-130">[Web 开发](https://msdn.microsoft.com/beginner/bb308760.aspx)， [HTML、 CSS、 JavaScript、 SQL、 PHP、 JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="dec6c-130">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="dec6c-131">关系数据库</span><span class="sxs-lookup"><span data-stu-id="dec6c-131">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="dec6c-132">多层体系结构</span><span class="sxs-lookup"><span data-stu-id="dec6c-132">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="dec6c-133">应用程序功能</span><span class="sxs-lookup"><span data-stu-id="dec6c-133">Application Features</span></span>

<span data-ttu-id="dec6c-134">本系列中显示的 ASP.NET Web 窗体功能包括：</span><span class="sxs-lookup"><span data-stu-id="dec6c-134">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="dec6c-135">Web 应用程序项目 （而不是网站项目）</span><span class="sxs-lookup"><span data-stu-id="dec6c-135">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="dec6c-136">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="dec6c-136">Web Forms</span></span>
- <span data-ttu-id="dec6c-137">母版页配置</span><span class="sxs-lookup"><span data-stu-id="dec6c-137">Master Pages, Configuration</span></span>
- <span data-ttu-id="dec6c-138">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="dec6c-138">Bootstrap</span></span>
- <span data-ttu-id="dec6c-139">实体框架代码优先，LocalDB</span><span class="sxs-lookup"><span data-stu-id="dec6c-139">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="dec6c-140">请求验证</span><span class="sxs-lookup"><span data-stu-id="dec6c-140">Request Validation</span></span>
- <span data-ttu-id="dec6c-141">强类型数据控件模型绑定数据批注和值提供程序</span><span class="sxs-lookup"><span data-stu-id="dec6c-141">Strongly Typed Data Controls, Model Binding, Data Annotations, and Value Providers</span></span>
- <span data-ttu-id="dec6c-142">SSL 和 OAuth</span><span class="sxs-lookup"><span data-stu-id="dec6c-142">SSL and OAuth</span></span>
- <span data-ttu-id="dec6c-143">ASP.NET 标识、 配置和授权</span><span class="sxs-lookup"><span data-stu-id="dec6c-143">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="dec6c-144">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="dec6c-144">Unobtrusive Validation</span></span>
- <span data-ttu-id="dec6c-145">路由</span><span class="sxs-lookup"><span data-stu-id="dec6c-145">Routing</span></span>
- <span data-ttu-id="dec6c-146">ASP.NET 错误处理</span><span class="sxs-lookup"><span data-stu-id="dec6c-146">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="dec6c-147">应用程序方案和任务</span><span class="sxs-lookup"><span data-stu-id="dec6c-147">Application Scenarios and Tasks</span></span>

<span data-ttu-id="dec6c-148">本系列教程中演示的任务包括：</span><span class="sxs-lookup"><span data-stu-id="dec6c-148">Tasks demonstrated in this series include:</span></span>

- <span data-ttu-id="dec6c-149">创建、 查看和运行新的项目</span><span class="sxs-lookup"><span data-stu-id="dec6c-149">Creating, reviewing and running the new project</span></span>
- <span data-ttu-id="dec6c-150">创建的数据库结构</span><span class="sxs-lookup"><span data-stu-id="dec6c-150">Creating the database structure</span></span>
- <span data-ttu-id="dec6c-151">初始化和数据库的种子设定</span><span class="sxs-lookup"><span data-stu-id="dec6c-151">Initializing and seeding the database</span></span>
- <span data-ttu-id="dec6c-152">自定义 UI 使用样式、 图形和母版页</span><span class="sxs-lookup"><span data-stu-id="dec6c-152">Customizing the UI using styles, graphics and a master page</span></span>
- <span data-ttu-id="dec6c-153">添加页面和导航</span><span class="sxs-lookup"><span data-stu-id="dec6c-153">Adding pages and navigation</span></span>
- <span data-ttu-id="dec6c-154">显示菜单的详细信息和产品数据</span><span class="sxs-lookup"><span data-stu-id="dec6c-154">Displaying menu details and product data</span></span>
- <span data-ttu-id="dec6c-155">创建购物车</span><span class="sxs-lookup"><span data-stu-id="dec6c-155">Creating a shopping cart</span></span>
- <span data-ttu-id="dec6c-156">添加 SSL 和 OAuth 支持</span><span class="sxs-lookup"><span data-stu-id="dec6c-156">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="dec6c-157">添加付款方式</span><span class="sxs-lookup"><span data-stu-id="dec6c-157">Adding a payment method</span></span>
- <span data-ttu-id="dec6c-158">包括一个管理员角色和用户访问应用程序</span><span class="sxs-lookup"><span data-stu-id="dec6c-158">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="dec6c-159">限制对特定页面和文件夹的访问</span><span class="sxs-lookup"><span data-stu-id="dec6c-159">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="dec6c-160">将文件上载到 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="dec6c-160">Uploading a file to the web application</span></span>
- <span data-ttu-id="dec6c-161">实施输入的验证</span><span class="sxs-lookup"><span data-stu-id="dec6c-161">Implementing input validation</span></span>
- <span data-ttu-id="dec6c-162">注册 web 应用程序路由</span><span class="sxs-lookup"><span data-stu-id="dec6c-162">Registering routes for the web application</span></span>
- <span data-ttu-id="dec6c-163">实现错误处理和错误日志记录</span><span class="sxs-lookup"><span data-stu-id="dec6c-163">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="dec6c-164">概述</span><span class="sxs-lookup"><span data-stu-id="dec6c-164">Overview</span></span>

<span data-ttu-id="dec6c-165">如果你不熟悉 ASP.NET Web 窗体编程概念的熟悉，但同时具备，则必须正确教程。</span><span class="sxs-lookup"><span data-stu-id="dec6c-165">If you are new to ASP.NET Web Forms but have familiarity with programming concepts, you have the right tutorial.</span></span> <span data-ttu-id="dec6c-166">如果你已熟悉 ASP.NET Web 窗体，您可以受益于本系列教程的 ASP.NET 4.5 中提供的新功能。</span><span class="sxs-lookup"><span data-stu-id="dec6c-166">If you are already familiar with ASP.NET Web Forms, you can benefit from this tutorial series by the new features available in ASP.NET 4.5.</span></span> <span data-ttu-id="dec6c-167">如果您不熟悉编程概念和 ASP.NET Web 窗体，请参阅 Web 窗体中提供的其他教程[Getting Started](../../../index.md) ASP.NET 网站上的部分。</span><span class="sxs-lookup"><span data-stu-id="dec6c-167">If you are unfamiliar with programming concepts and ASP.NET Web Forms, see the additional tutorials provided in the Web Forms [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="dec6c-168">特定于**最新**ASP.NET 4.5 功能在此 Web 窗体中的系列教程包括以下：</span><span class="sxs-lookup"><span data-stu-id="dec6c-168">The specific **latest** ASP.NET 4.5 features provided in this Web Forms tutorial series include the following:</span></span>

- <span data-ttu-id="dec6c-169">用于创建一个简单的 UI 项目的产品/服务[支持多个 ASP.NET 框架](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)（Web 窗体、 MVC 和 Web API）。</span><span class="sxs-lookup"><span data-stu-id="dec6c-169">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="dec6c-170">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)，一个布局和主题的框架，提供响应式设计和主题功能。</span><span class="sxs-lookup"><span data-stu-id="dec6c-170">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout and theming framework that provides responsive design and theming capabilities.</span></span>
- <span data-ttu-id="dec6c-171">[ASP.NET 标识](../../../../identity/index.md)，新的 ASP.NET 成员资格系统的与 web 托管 IIS 之外的软件的工作方式在所有 ASP.NET 框架和工作原理相同。</span><span class="sxs-lookup"><span data-stu-id="dec6c-171">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- <span data-ttu-id="dec6c-172">[实体框架 6](https://msdn.microsoft.com/data/ef.aspx)、 Entity framework，使你检索和操作数据作为强类型化对象、 访问数据以异步方式处理暂时性连接故障和日志的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="dec6c-172">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx), an update to the Entity Framework which allows you retrieve and manipulate data as strongly typed objects, access data asynchronously, handle transient connection faults, and log SQL statements.</span></span>

<span data-ttu-id="dec6c-173">ASP.NET 4.5 功能的完整列表，请参阅[ASP.NET 和 Web Tools for Visual Studio 2013 发行说明](../../../../visual-studio/overview/2013/release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="dec6c-173">For a complete list of ASP.NET 4.5 features, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="dec6c-174">Wingtip Toys 示例应用程序</span><span class="sxs-lookup"><span data-stu-id="dec6c-174">The Wingtip Toys Sample Application</span></span>

<span data-ttu-id="dec6c-175">以下屏幕截图提供将在本系列教程中创建 ASP.NET Web 窗体应用程序的快速视图。</span><span class="sxs-lookup"><span data-stu-id="dec6c-175">The following screen shots provide a quick view of the ASP.NET Web forms application that you will create in this tutorial series.</span></span> <span data-ttu-id="dec6c-176">运行时应用程序从 Visual Studio Express 2013 for Web，您将看到以下 web 主页。</span><span class="sxs-lookup"><span data-stu-id="dec6c-176">When you run the application from Visual Studio Express 2013 for Web, you will see the following web Home page.</span></span>

![Wingtip Toys 的默认页](introduction-and-overview/_static/image1.png)

<span data-ttu-id="dec6c-178">可以将注册为新用户，或现有用户身份登录。</span><span class="sxs-lookup"><span data-stu-id="dec6c-178">You can register as a new user, or log in as an existing user.</span></span> <span data-ttu-id="dec6c-179">导航由从数据库检索可用的产品提供顶部为每个产品类别。</span><span class="sxs-lookup"><span data-stu-id="dec6c-179">Navigation is provided at the top for each product category by retrieving the available products from the database.</span></span>

<span data-ttu-id="dec6c-180">通过选择的产品链接，你将能够查看所有可用产品的列表。</span><span class="sxs-lookup"><span data-stu-id="dec6c-180">By selecting the Products link, you will be able to see a list of all available products.</span></span>

![Wingtip Toys 的产品](introduction-and-overview/_static/image2.png)

<span data-ttu-id="dec6c-182">选择任何列出的产品，还可以查看各个产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="dec6c-182">You can also see individual product details by selecting any of the listed products.</span></span>

![Wingtip Toys 的产品详细信息](introduction-and-overview/_static/image3.png)

<span data-ttu-id="dec6c-184">作为用户，可以注册和登录使用 Web 窗体模板的默认功能。</span><span class="sxs-lookup"><span data-stu-id="dec6c-184">As a user, you can register and log in using the default functionality of the Web Forms template.</span></span> <span data-ttu-id="dec6c-185">本教程还介绍如何使用现有的 Gmail 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="dec6c-185">This tutorial also explains how to login using an existing Gmail account.</span></span> <span data-ttu-id="dec6c-186">此外，你可以登录以管理员身份添加和从数据库中删除产品。</span><span class="sxs-lookup"><span data-stu-id="dec6c-186">Additionally, you can login as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-登录](introduction-and-overview/_static/image4.png)

<span data-ttu-id="dec6c-188">以用户身份登录，你可以将产品添加到购物车并使用 PayPal 结帐。</span><span class="sxs-lookup"><span data-stu-id="dec6c-188">Once you have logged in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="dec6c-189">请注意此示例应用程序旨在 PayPal 的开发人员沙箱起作用。</span><span class="sxs-lookup"><span data-stu-id="dec6c-189">Note that this sample application is designed to function with PayPal's developer sandbox.</span></span> <span data-ttu-id="dec6c-190">没有实际资金事务会发生。</span><span class="sxs-lookup"><span data-stu-id="dec6c-190">No actual money transaction will take place.</span></span>

![Wingtip Toys 的购物车](introduction-and-overview/_static/image5.png)

<span data-ttu-id="dec6c-192">PayPal 将确认你的帐户、 订单和付款信息。</span><span class="sxs-lookup"><span data-stu-id="dec6c-192">PayPal will confirm your account, order, and payment information.</span></span>

![Wingtip Toys 的 PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="dec6c-194">返回从 PayPal 后, 可以查看并完成你的订单。</span><span class="sxs-lookup"><span data-stu-id="dec6c-194">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys 的顺序查看](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="dec6c-196">系统必备</span><span class="sxs-lookup"><span data-stu-id="dec6c-196">Prerequisites</span></span>

<span data-ttu-id="dec6c-197">在开始之前，请确保您已在计算机上安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="dec6c-197">Before you start, make sure that you have the following software installed on your computer:</span></span>

- <span data-ttu-id="dec6c-198">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="dec6c-198">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="dec6c-199">会自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="dec6c-199">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="dec6c-200">本系列教程使用 Microsoft Visual Studio Express 2013 for Web。</span><span class="sxs-lookup"><span data-stu-id="dec6c-200">This tutorial series uses Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="dec6c-201">可以使用 Microsoft Visual Studio Express 2013 for Web，或者 Microsoft Visual Studio 2013 来完成本系列教程。</span><span class="sxs-lookup"><span data-stu-id="dec6c-201">You can use either Microsoft Visual Studio Express 2013 for Web or Microsoft Visual Studio 2013 to complete this tutorial series.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dec6c-202">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常称为 Visual Studio 在整个教程系列中。</span><span class="sxs-lookup"><span data-stu-id="dec6c-202">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>


<span data-ttu-id="dec6c-203">如果已安装了 Visual Studio 版本，安装过程将现有版本旁边安装 Visual Studio 2013 或 Microsoft Visual Studio Express 2013 for Web。</span><span class="sxs-lookup"><span data-stu-id="dec6c-203">If you already have a Visual Studio version installed, the installation process will install Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web next to the existing version.</span></span> <span data-ttu-id="dec6c-204">在早期版本中创建的网站中可以在 Visual Studio 2013 中打开，并继续在以前的版本中打开。</span><span class="sxs-lookup"><span data-stu-id="dec6c-204">Sites that you created in earlier versions can be opened in Visual Studio 2013 and continue to open in previous versions.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dec6c-205">本演练假定你所选*Web 开发*的设置集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="dec6c-205">This walkthrough assumes that you selected the *Web Development* collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="dec6c-206">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dec6c-206">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="download-the-sample-application"></a><span data-ttu-id="dec6c-207">下载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="dec6c-207">Download the Sample Application</span></span>

<span data-ttu-id="dec6c-208">在安装后系统必备组件，已准备好开始本教程系列中创建新的 Web 项目显示。</span><span class="sxs-lookup"><span data-stu-id="dec6c-208">After installing the prerequisites, you are ready to begin creating the new Web project that is presented in this tutorial series.</span></span> <span data-ttu-id="dec6c-209">如果你想要**根据需要**运行本教程系列中创建的示例应用程序，你可以从下载 MSDN 示例网站。</span><span class="sxs-lookup"><span data-stu-id="dec6c-209">If you would like to **optionally** run the sample application that this tutorial series creates, you can download it from the MSDN Samples site.</span></span> <span data-ttu-id="dec6c-210">此下载包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="dec6c-210">This download contains the following:</span></span>

- <span data-ttu-id="dec6c-211">中的示例应用程序*WingtipToys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="dec6c-211">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="dec6c-212">若要创建示例应用程序所使用的资源*WingtipToys 资产*中的文件夹*WingtipToys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="dec6c-212">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

#### <a name="download-the-file-from-msdn-samples-site"></a><span data-ttu-id="dec6c-213">从 MSDN 示例站点下载文件：</span><span class="sxs-lookup"><span data-stu-id="dec6c-213">Download the file from MSDN Samples site:</span></span>

<span data-ttu-id="dec6c-214">[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="dec6c-214">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

<span data-ttu-id="dec6c-215">在下载<em>.zip</em>文件。</span><span class="sxs-lookup"><span data-stu-id="dec6c-215">The download is a <em>.zip</em> file.</span></span> <span data-ttu-id="dec6c-216">若要查看已完成本教程系列中创建的项目，找到并选择<em>C#</em>中的文件夹<em>.zip</em>文件。</span><span class="sxs-lookup"><span data-stu-id="dec6c-216">To see the completed project that this tutorial series creates, find and select the <em>C#</em>folder in the <em>.zip</em> file.</span></span> <span data-ttu-id="dec6c-217">保存<em>C#</em> folderto 使用以使用 Visual Studio 2013 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="dec6c-217">Save the <em>C#</em> folderto the folder you use to work with Visual Studio 2013 projects.</span></span> <span data-ttu-id="dec6c-218">默认情况下，以下是 Visual Studio 2013 项目文件夹：</span><span class="sxs-lookup"><span data-stu-id="dec6c-218">By default, the Visual Studio 2013 projects folder is the following:</span></span>

<span data-ttu-id="dec6c-219"><strong>C:\Users&#92;</strong><strong><em>&lt;用户名&gt;</em></strong><strong>\Documents\Visual Studio 2013\Projects</strong></span><span class="sxs-lookup"><span data-stu-id="dec6c-219"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\Documents\Visual Studio 2013\Projects</strong></span></span>

<span data-ttu-id="dec6c-220">重命名***C#*** 向文件夹***WingtipToys***。</span><span class="sxs-lookup"><span data-stu-id="dec6c-220">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="dec6c-221">如果已有一个名为文件夹*WingtipToys*在项目文件夹中，暂时重命名该现有文件夹重命名前*C#* 文件夹*WingtipToys*。</span><span class="sxs-lookup"><span data-stu-id="dec6c-221">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>


<span data-ttu-id="dec6c-222">若要运行已完成的项目，打开*WingtipToys*文件夹，然后双击*WingtipToys.sln*文件。</span><span class="sxs-lookup"><span data-stu-id="dec6c-222">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="dec6c-223">Visual Studio 2013 将打开的项目。</span><span class="sxs-lookup"><span data-stu-id="dec6c-223">Visual Studio 2013 will open the project.</span></span> <span data-ttu-id="dec6c-224">接下来，右键单击*Default.aspx*文件在解决方案资源管理器窗口中，右键单击菜单中单击视图中浏览器。</span><span class="sxs-lookup"><span data-stu-id="dec6c-224">Next, right-click the *Default.aspx* file in the Solution Explorer window and click View In Browser from the right-click menu.</span></span>

### <a name="tutorial-support-and-comments"></a><span data-ttu-id="dec6c-225">教程支持和提出的意见</span><span class="sxs-lookup"><span data-stu-id="dec6c-225">Tutorial Support and Comments</span></span>

<span data-ttu-id="dec6c-226">使用随附的问题与解答部分[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)示例 (C#) 的任何问题或意见。</span><span class="sxs-lookup"><span data-stu-id="dec6c-226">Use the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample for any questions or comments.</span></span>

<span data-ttu-id="dec6c-227">在本教程系列中的注释是欢迎使用，并更新本系列教程时将进行每项工作要考虑到帐户更正或建议的教程的注释中提供的改进。</span><span class="sxs-lookup"><span data-stu-id="dec6c-227">Comments on this tutorial series are welcome, and when this tutorial series is updated every effort will be made to take into account corrections or suggestions for improvements that are provided in the tutorial comments.</span></span>

<span data-ttu-id="dec6c-228">在开发期间，发生错误，或者如果网站无法正常运行的错误消息可能会给问题的源提供复杂的线索或可能不说明如何修复此错误。</span><span class="sxs-lookup"><span data-stu-id="dec6c-228">When an error happens during development, or if the Web site does not run correctly, the error messages may give complex clues to the source of the problem or might not explain how to fix it.</span></span> <span data-ttu-id="dec6c-229">若要帮助您通过一些常见的问题方案，您可以使用[ASP.NET 论坛](https://forums.asp.net/)或附带的问题与解答部分[开始使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 示例。</span><span class="sxs-lookup"><span data-stu-id="dec6c-229">To help you with some common problem scenarios, you can also use the [ASP.NET forums](https://forums.asp.net/) or the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample.</span></span> <span data-ttu-id="dec6c-230">如果收到错误消息或某些操作无法在完成教程，，请务必检查上述位置。</span><span class="sxs-lookup"><span data-stu-id="dec6c-230">If you get an error message or something doesn't work as you go through the tutorials, be sure to check the above locations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="dec6c-231">下一篇</span><span class="sxs-lookup"><span data-stu-id="dec6c-231">Next</span></span>](create-the-project.md)
