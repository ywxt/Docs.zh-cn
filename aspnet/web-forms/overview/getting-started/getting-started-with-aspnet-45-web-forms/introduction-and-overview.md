---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: "Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013 |Microsoft 文档"
author: Erikre
description: "此分步教程系列将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio 截止的 ASP.NET Web 窗体应用程序的基础知识..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 6ae398f94c0ac3872601bdc8fd935f6d285793db
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a><span data-ttu-id="8fc5f-103">ASP.NET 4.5 Web 窗体和 Visual Studio 2013 入门</span><span class="sxs-lookup"><span data-stu-id="8fc5f-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013</span></span>
====================
<span data-ttu-id="8fc5f-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="8fc5f-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="8fc5f-106">此分步教程系列将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-106">This step-by-step tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> [<span data-ttu-id="8fc5f-107">ASP.NET Web 窗体测验</span><span class="sxs-lookup"><span data-stu-id="8fc5f-107">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)  
> <span data-ttu-id="8fc5f-108">测试您的知识，并通过采用 ASP.NET Web 窗体 Quiz 强调关键概念。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-108">Test your knowledge and reinforce key concepts by taking the ASP.NET Web Forms Quiz.</span></span> <span data-ttu-id="8fc5f-109">此测验专门从包含在此教程系列中的内容。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-109">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="8fc5f-110">测验中的每个问题提供的附加指导的链接以及解释。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-110">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>


## <a name="introduction"></a><span data-ttu-id="8fc5f-111">介绍</span><span class="sxs-lookup"><span data-stu-id="8fc5f-111">Introduction</span></span>

<span data-ttu-id="8fc5f-112">这一系列的教程将指导您完成创建针对 Web 和 ASP.NET 4.5 使用 Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-112">This series of tutorials guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio Express 2013 for Web and ASP.NET 4.5.</span></span>

<span data-ttu-id="8fc5f-113">应用程序将创建名为**Wingtip Toys**。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-113">The application you'll create is named **Wingtip Toys**.</span></span> <span data-ttu-id="8fc5f-114">它是销售项在线应用商店前端网站的简化的示例。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-114">It's a simplified example of a store front web site that sells items online.</span></span> <span data-ttu-id="8fc5f-115">本系列教程重点介绍 ASP.NET 4.5 中提供的新功能。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-115">This tutorial series highlights new features available in ASP.NET 4.5.</span></span>

<span data-ttu-id="8fc5f-116">注释是欢迎使用和我们将使努力地更新本系列教程基于你的建议。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-116">Comments are welcome, and we'll make every effort to update this tutorial series based on your suggestions.</span></span>

### <a name="download-completed-project"></a><span data-ttu-id="8fc5f-117">已完成的下载项目</span><span class="sxs-lookup"><span data-stu-id="8fc5f-117">Download completed project</span></span>

<span data-ttu-id="8fc5f-118">你可以下载的 C# 项目中包含已完成的教程。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-118">You can download a C# project that contains the completed tutorial.</span></span>

- <span data-ttu-id="8fc5f-119">[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-119">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span>

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a><span data-ttu-id="8fc5f-120">通过执行相关的 ASP.NET Web 窗体测验查看的内容</span><span class="sxs-lookup"><span data-stu-id="8fc5f-120">Review the content by taking the related ASP.NET Web Forms quiz</span></span>

<span data-ttu-id="8fc5f-121">完成本教程后，测试您的知识，并通过采用强调关键概念[ASP.NET Web 窗体 Quiz](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-121">After you complete this tutorial, test your knowledge and reinforce key concepts by taking the [ASP.NET Web Forms Quiz](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001).</span></span> <span data-ttu-id="8fc5f-122">此测验专门从包含在此教程系列中的内容。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-122">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="8fc5f-123">测验中的每个问题提供的附加指导的链接以及解释。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-123">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>

- [<span data-ttu-id="8fc5f-124">ASP.NET Web 窗体测验</span><span class="sxs-lookup"><span data-stu-id="8fc5f-124">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a><span data-ttu-id="8fc5f-125">读者</span><span class="sxs-lookup"><span data-stu-id="8fc5f-125">Audience</span></span>

<span data-ttu-id="8fc5f-126">本系列教程的目标的受众是经验丰富的开发人员不熟悉 ASP.NET Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-126">The intended audience of this tutorial series is experienced developers who are new to ASP.NET Web Forms.</span></span> <span data-ttu-id="8fc5f-127">开发人员感兴趣本系列教程应具有以下几个方面：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-127">A developer interested in this tutorial series should have the following skills:</span></span>

- <span data-ttu-id="8fc5f-128">熟悉对象面向编程 (OOP) 语言</span><span class="sxs-lookup"><span data-stu-id="8fc5f-128">Familiar with an object oriented programming (OOP) language</span></span>
- <span data-ttu-id="8fc5f-129">熟悉 Web 开发概念 (HTML、 CSS、 JavaScript)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-129">Familiar with Web development concepts (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="8fc5f-130">熟悉关系数据库概念</span><span class="sxs-lookup"><span data-stu-id="8fc5f-130">Familiar with relational database concepts</span></span>
- <span data-ttu-id="8fc5f-131">熟悉 n 层体系结构概念</span><span class="sxs-lookup"><span data-stu-id="8fc5f-131">Familiar with n-tier architecture concepts</span></span>

<span data-ttu-id="8fc5f-132">如果你有兴趣查看上面列出的区域，请考虑查看以下内容：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-132">If you are interested in reviewing the areas listed above, consider reviewing the following content:</span></span>

- [<span data-ttu-id="8fc5f-133">Visual C# 入门</span><span class="sxs-lookup"><span data-stu-id="8fc5f-133">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="8fc5f-134">[Web 开发](https://msdn.microsoft.com/beginner/bb308760.aspx)， [HTML、 CSS、 JavaScript、 SQL、 PHP、 JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-134">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="8fc5f-135">关系数据库</span><span class="sxs-lookup"><span data-stu-id="8fc5f-135">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="8fc5f-136">多层体系结构</span><span class="sxs-lookup"><span data-stu-id="8fc5f-136">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="8fc5f-137">应用程序功能</span><span class="sxs-lookup"><span data-stu-id="8fc5f-137">Application Features</span></span>

<span data-ttu-id="8fc5f-138">显示此序列中的 ASP.NET Web 窗体功能包括：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-138">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="8fc5f-139">Web 应用程序项目 （而不是网站项目）</span><span class="sxs-lookup"><span data-stu-id="8fc5f-139">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="8fc5f-140">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="8fc5f-140">Web Forms</span></span>
- <span data-ttu-id="8fc5f-141">主控页配置</span><span class="sxs-lookup"><span data-stu-id="8fc5f-141">Master Pages, Configuration</span></span>
- <span data-ttu-id="8fc5f-142">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="8fc5f-142">Bootstrap</span></span>
- <span data-ttu-id="8fc5f-143">实体框架代码优先，LocalDB</span><span class="sxs-lookup"><span data-stu-id="8fc5f-143">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="8fc5f-144">请求验证</span><span class="sxs-lookup"><span data-stu-id="8fc5f-144">Request Validation</span></span>
- <span data-ttu-id="8fc5f-145">强类型数据控件模型绑定，数据注释，并且值提供程序</span><span class="sxs-lookup"><span data-stu-id="8fc5f-145">Strongly Typed Data Controls, Model Binding, Data Annotations, and Value Providers</span></span>
- <span data-ttu-id="8fc5f-146">SSL 和 OAuth</span><span class="sxs-lookup"><span data-stu-id="8fc5f-146">SSL and OAuth</span></span>
- <span data-ttu-id="8fc5f-147">ASP.NET 标识、 配置和授权</span><span class="sxs-lookup"><span data-stu-id="8fc5f-147">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="8fc5f-148">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="8fc5f-148">Unobtrusive Validation</span></span>
- <span data-ttu-id="8fc5f-149">路由</span><span class="sxs-lookup"><span data-stu-id="8fc5f-149">Routing</span></span>
- <span data-ttu-id="8fc5f-150">ASP.NET 错误处理</span><span class="sxs-lookup"><span data-stu-id="8fc5f-150">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="8fc5f-151">应用程序方案和任务</span><span class="sxs-lookup"><span data-stu-id="8fc5f-151">Application Scenarios and Tasks</span></span>

<span data-ttu-id="8fc5f-152">演示本系列中的任务包括：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-152">Tasks demonstrated in this series include:</span></span>

- <span data-ttu-id="8fc5f-153">创建、 查看和运行新的项目</span><span class="sxs-lookup"><span data-stu-id="8fc5f-153">Creating, reviewing and running the new project</span></span>
- <span data-ttu-id="8fc5f-154">创建数据库结构</span><span class="sxs-lookup"><span data-stu-id="8fc5f-154">Creating the database structure</span></span>
- <span data-ttu-id="8fc5f-155">初始化和数据库进行种子设定</span><span class="sxs-lookup"><span data-stu-id="8fc5f-155">Initializing and seeding the database</span></span>
- <span data-ttu-id="8fc5f-156">自定义 UI 使用样式、 图形和母版页</span><span class="sxs-lookup"><span data-stu-id="8fc5f-156">Customizing the UI using styles, graphics and a master page</span></span>
- <span data-ttu-id="8fc5f-157">添加页面和导航</span><span class="sxs-lookup"><span data-stu-id="8fc5f-157">Adding pages and navigation</span></span>
- <span data-ttu-id="8fc5f-158">显示菜单的详细信息和产品数据</span><span class="sxs-lookup"><span data-stu-id="8fc5f-158">Displaying menu details and product data</span></span>
- <span data-ttu-id="8fc5f-159">创建购物车</span><span class="sxs-lookup"><span data-stu-id="8fc5f-159">Creating a shopping cart</span></span>
- <span data-ttu-id="8fc5f-160">添加 SSL 和 OAuth 支持</span><span class="sxs-lookup"><span data-stu-id="8fc5f-160">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="8fc5f-161">添加付款方式</span><span class="sxs-lookup"><span data-stu-id="8fc5f-161">Adding a payment method</span></span>
- <span data-ttu-id="8fc5f-162">包括的管理员角色和用户访问应用程序</span><span class="sxs-lookup"><span data-stu-id="8fc5f-162">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="8fc5f-163">限制对特定页和文件夹的访问</span><span class="sxs-lookup"><span data-stu-id="8fc5f-163">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="8fc5f-164">将文件上载到 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="8fc5f-164">Uploading a file to the web application</span></span>
- <span data-ttu-id="8fc5f-165">实现输入的验证</span><span class="sxs-lookup"><span data-stu-id="8fc5f-165">Implementing input validation</span></span>
- <span data-ttu-id="8fc5f-166">注册 web 应用程序的路由</span><span class="sxs-lookup"><span data-stu-id="8fc5f-166">Registering routes for the web application</span></span>
- <span data-ttu-id="8fc5f-167">实现错误处理和错误日志记录</span><span class="sxs-lookup"><span data-stu-id="8fc5f-167">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="8fc5f-168">概述</span><span class="sxs-lookup"><span data-stu-id="8fc5f-168">Overview</span></span>

<span data-ttu-id="8fc5f-169">如果你不熟悉 ASP.NET Web 窗体，但同时具备编程概念的熟悉，你可以右教程。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-169">If you are new to ASP.NET Web Forms but have familiarity with programming concepts, you have the right tutorial.</span></span> <span data-ttu-id="8fc5f-170">如果你已熟悉 ASP.NET Web 窗体，可通过 ASP.NET 4.5 中提供的新功能获益从本教程系列。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-170">If you are already familiar with ASP.NET Web Forms, you can benefit from this tutorial series by the new features available in ASP.NET 4.5.</span></span> <span data-ttu-id="8fc5f-171">如果你熟悉编程概念和 ASP.NET Web 窗体，请参阅 Web 窗体中提供的其他教程[入门](../../../index.md)ASP.NET Web 站点上的部分。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-171">If you are unfamiliar with programming concepts and ASP.NET Web Forms, see the additional tutorials provided in the Web Forms [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="8fc5f-172">特定于**最新**ASP.NET 4.5 功能在此 Web 窗体中的系列教程包括以下：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-172">The specific **latest** ASP.NET 4.5 features provided in this Web Forms tutorial series include the following:</span></span>

- <span data-ttu-id="8fc5f-173">用于创建一个简单的 UI 项目提供[支持多个 ASP.NET 框架](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)（Web 窗体、 MVC 和 Web API）。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-173">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="8fc5f-174">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)，布局和主题的框架，可提供响应式设计和主题功能。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-174">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout and theming framework that provides responsive design and theming capabilities.</span></span>
- <span data-ttu-id="8fc5f-175">[ASP.NET 标识](../../../../identity/index.md)，新的 ASP.NET 成员资格系统中所有的 ASP.NET 框架和工作原理相同适用于 web 托管非 IIS 的软件。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-175">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- <span data-ttu-id="8fc5f-176">[实体框架 6](https://msdn.microsoft.com/data/ef.aspx)，更新到实体框架，使你检索和操作数据作为强类型化对象，访问数据以异步方式处理暂时性连接故障，以及记录 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-176">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx), an update to the Entity Framework which allows you retrieve and manipulate data as strongly typed objects, access data asynchronously, handle transient connection faults, and log SQL statements.</span></span>

<span data-ttu-id="8fc5f-177">ASP.NET 4.5 功能的完整列表，请参阅[ASP.NET 和 Web Tools for Visual Studio 2013 发行说明](../../../../visual-studio/overview/2013/release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-177">For a complete list of ASP.NET 4.5 features, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="8fc5f-178">Wingtip Toys 示例应用程序</span><span class="sxs-lookup"><span data-stu-id="8fc5f-178">The Wingtip Toys Sample Application</span></span>

<span data-ttu-id="8fc5f-179">以下屏幕截图提供将在本系列教程中创建 ASP.NET Web 窗体应用程序的快速视图。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-179">The following screen shots provide a quick view of the ASP.NET Web forms application that you will create in this tutorial series.</span></span> <span data-ttu-id="8fc5f-180">从 Visual Studio Express 2013 for Web 中运行应用程序时，你将看到以下 web 主页。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-180">When you run the application from Visual Studio Express 2013 for Web, you will see the following web Home page.</span></span>

![Wingtip Toys 的默认页](introduction-and-overview/_static/image1.png)

<span data-ttu-id="8fc5f-182">你可以注册为新用户，或现有的用户身份登录。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-182">You can register as a new user, or log in as an existing user.</span></span> <span data-ttu-id="8fc5f-183">导航通过从数据库检索可用的产品提供顶部每个产品类别。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-183">Navigation is provided at the top for each product category by retrieving the available products from the database.</span></span>

<span data-ttu-id="8fc5f-184">通过选择的产品链接，你将能够查看所有可用产品的列表。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-184">By selecting the Products link, you will be able to see a list of all available products.</span></span>

![Wingtip Toys-产品](introduction-and-overview/_static/image2.png)

<span data-ttu-id="8fc5f-186">你还可以通过选择列出的产品中的任何查看各个产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-186">You can also see individual product details by selecting any of the listed products.</span></span>

![Wingtip Toys 的产品详细信息](introduction-and-overview/_static/image3.png)

<span data-ttu-id="8fc5f-188">作为用户，可以注册和登录使用 Web 窗体模板的默认功能。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-188">As a user, you can register and log in using the default functionality of the Web Forms template.</span></span> <span data-ttu-id="8fc5f-189">本教程还介绍了如何使用现有 Gmail 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-189">This tutorial also explains how to login using an existing Gmail account.</span></span> <span data-ttu-id="8fc5f-190">此外，你可以登录以管理员身份添加和从数据库中删除产品。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-190">Additionally, you can login as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-登录](introduction-and-overview/_static/image4.png)

<span data-ttu-id="8fc5f-192">以用户身份登录，你可以将产品添加到购物车和与 PayPal 签出。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-192">Once you have logged in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="8fc5f-193">请注意此示例应用程序旨在 PayPal 的开发人员沙盒起作用。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-193">Note that this sample application is designed to function with PayPal's developer sandbox.</span></span> <span data-ttu-id="8fc5f-194">没有实际 money 事务会发生。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-194">No actual money transaction will take place.</span></span>

![Wingtip Toys 的购物车](introduction-and-overview/_static/image5.png)

<span data-ttu-id="8fc5f-196">PayPal 将确认你的帐户、 顺序和付款信息。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-196">PayPal will confirm your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="8fc5f-198">返回从 PayPal 后, 可以查看并完成你的订单。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-198">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-订单审核](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="8fc5f-200">系统必备</span><span class="sxs-lookup"><span data-stu-id="8fc5f-200">Prerequisites</span></span>

<span data-ttu-id="8fc5f-201">在开始之前，请确保你已在计算机上安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-201">Before you start, make sure that you have the following software installed on your computer:</span></span>

- <span data-ttu-id="8fc5f-202">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-202">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="8fc5f-203">自动安装.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-203">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="8fc5f-204">本系列教程使用 Microsoft Visual Studio Express 2013 for Web。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-204">This tutorial series uses Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="8fc5f-205">可以使用 Microsoft Visual Studio Express 2013 for Web，或者 Microsoft Visual Studio 2013 来完成本教程系列。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-205">You can use either Microsoft Visual Studio Express 2013 for Web or Microsoft Visual Studio 2013 to complete this tutorial series.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8fc5f-206">Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 将通常被称为 Visual Studio 在本教程系列整个。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-206">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>


<span data-ttu-id="8fc5f-207">如果你已安装了 Visual Studio 版本，则安装过程将安装 Visual Studio 2013 或 Microsoft Visual Studio Express 2013 for Web 旁边的现有版本。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-207">If you already have a Visual Studio version installed, the installation process will install Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web next to the existing version.</span></span> <span data-ttu-id="8fc5f-208">在早期版本中创建的网站中可以在 Visual Studio 2013 中打开，并继续在以前版本中打开。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-208">Sites that you created in earlier versions can be opened in Visual Studio 2013 and continue to open in previous versions.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8fc5f-209">本演练假定你所选*Web 开发*设置的集合，首次启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-209">This walkthrough assumes that you selected the *Web Development* collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="8fc5f-210">有关详细信息，请参阅[如何： 选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-210">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="download-the-sample-application"></a><span data-ttu-id="8fc5f-211">下载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="8fc5f-211">Download the Sample Application</span></span>

<span data-ttu-id="8fc5f-212">安装必备项之后, 你就可以开始创建新的 Web 项目显示在本教程系列。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-212">After installing the prerequisites, you are ready to begin creating the new Web project that is presented in this tutorial series.</span></span> <span data-ttu-id="8fc5f-213">如果你想要进行**（可选)**运行本系列教程创建示例应用程序，你可以从网站下载它 MSDN 示例。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-213">If you would like to **optionally** run the sample application that this tutorial series creates, you can download it from the MSDN Samples site.</span></span> <span data-ttu-id="8fc5f-214">此下载包含以下项目：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-214">This download contains the following:</span></span>

- <span data-ttu-id="8fc5f-215">中的示例应用程序*WingtipToys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-215">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="8fc5f-216">用于创建示例应用程序中的资源*WingtipToys 资产*文件夹中的*WingtipToys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-216">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

#### <a name="download-the-file-from-msdn-samples-site"></a><span data-ttu-id="8fc5f-217">从 MSDN 示例站点下载文件：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-217">Download the file from MSDN Samples site:</span></span>

<span data-ttu-id="8fc5f-218">[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="8fc5f-218">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

<span data-ttu-id="8fc5f-219">下载*.zip*文件。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-219">The download is a *.zip* file.</span></span> <span data-ttu-id="8fc5f-220">若要查看已完成本教程系列创建的项目中，找到并选择*C#*文件夹中的*.zip*文件。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-220">To see the completed project that this tutorial series creates, find and select the *C#*folder in the *.zip* file.</span></span> <span data-ttu-id="8fc5f-221">保存*C#* folderto 使用以使用 Visual Studio 2013 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-221">Save the *C#* folderto the folder you use to work with Visual Studio 2013 projects.</span></span> <span data-ttu-id="8fc5f-222">默认情况下，Visual Studio 2013 项目文件夹如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fc5f-222">By default, the Visual Studio 2013 projects folder is the following:</span></span>

<span data-ttu-id="8fc5f-223">**C:\Users\*****&lt;username&gt;*****\Documents\Visual Studio 2013\Projects**</span><span class="sxs-lookup"><span data-stu-id="8fc5f-223">**C:\Users\*****&lt;username&gt;*****\Documents\Visual Studio 2013\Projects**</span></span>

<span data-ttu-id="8fc5f-224">重命名***C#***文件夹***WingtipToys***。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-224">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc5f-225">如果你已有一个名为文件夹*WingtipToys*在项目文件夹中，暂时重命名该现有文件夹在重命名之前*C#*文件夹*WingtipToys*。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-225">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>


<span data-ttu-id="8fc5f-226">若要运行已完成的项目，打开*WingtipToys*文件夹并双击*WingtipToys.sln*文件。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-226">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="8fc5f-227">Visual Studio 2013 将打开的项目。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-227">Visual Studio 2013 will open the project.</span></span> <span data-ttu-id="8fc5f-228">接下来，右键单击*Default.aspx*文件位于解决方案资源管理器窗口，并单击右键单击菜单中浏览器中查看。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-228">Next, right-click the *Default.aspx* file in the Solution Explorer window and click View In Browser from the right-click menu.</span></span>

### <a name="tutorial-support-and-comments"></a><span data-ttu-id="8fc5f-229">教程支持和注释</span><span class="sxs-lookup"><span data-stu-id="8fc5f-229">Tutorial Support and Comments</span></span>

<span data-ttu-id="8fc5f-230">使用随附的问题解答部分[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 的任何问题或注释的示例。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-230">Use the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample for any questions or comments.</span></span>

<span data-ttu-id="8fc5f-231">对本系列教程的注释都欢迎，并更新本系列教程时将保持尽一切可能要考虑到帐户更正或建议的教程的注释中提供的改进。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-231">Comments on this tutorial series are welcome, and when this tutorial series is updated every effort will be made to take into account corrections or suggestions for improvements that are provided in the tutorial comments.</span></span>

<span data-ttu-id="8fc5f-232">在开发期间，发生错误时，或者如果网站无法正常运行，错误消息可能的问题来源授予复杂线索，或可能不说明如何修复此错误。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-232">When an error happens during development, or if the Web site does not run correctly, the error messages may give complex clues to the source of the problem or might not explain how to fix it.</span></span> <span data-ttu-id="8fc5f-233">若要帮助你解决问题的一些常见方案，你可以使用[ASP.NET 论坛](https://forums.asp.net/)或附带的问题解答节[Getting Started with ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 示例。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-233">To help you with some common problem scenarios, you can also use the [ASP.NET forums](https://forums.asp.net/) or the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample.</span></span> <span data-ttu-id="8fc5f-234">如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查上述位置。</span><span class="sxs-lookup"><span data-stu-id="8fc5f-234">If you get an error message or something doesn't work as you go through the tutorials, be sure to check the above locations.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="8fc5f-235">下一篇</span><span class="sxs-lookup"><span data-stu-id="8fc5f-235">Next</span></span>](create-the-project.md)
