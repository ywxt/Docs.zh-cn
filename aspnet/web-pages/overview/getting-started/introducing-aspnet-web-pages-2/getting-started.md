---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: Introducing ASP.NET Web Pages-入门 |Microsoft Docs
author: tfitzmac
description: WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。 使用 Visual Studio 或 Visual Studio Code。 本指南...
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: b4f554d2bf8bf564fd69239fcc7cc605158c83c3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825032"
---
<a name="introducing-aspnet-web-pages---getting-started"></a><span data-ttu-id="6be95-105">ASP.NET 网页简介-入门</span><span class="sxs-lookup"><span data-stu-id="6be95-105">Introducing ASP.NET Web Pages - Getting Started</span></span>
====================
<span data-ttu-id="6be95-106">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6be95-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > 
> > <span data-ttu-id="6be95-107">WebMatrix 是不再建议将其作为一个集成的开发环境为 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="6be95-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="6be95-108">使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="6be95-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="6be95-109">此指南和应用程序提供您的 ASP.NET Web Pages （版本 2 或更高版本） 概述和 Razor 语法，用于创建动态网站一款轻量级框架。</span><span class="sxs-lookup"><span data-stu-id="6be95-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="6be95-110">它还介绍 WebMatrix 中，用于创建网页和网站的工具。</span><span class="sxs-lookup"><span data-stu-id="6be95-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="6be95-111">**级别**： 新的 ASP.NET Web 页面。</span><span class="sxs-lookup"><span data-stu-id="6be95-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="6be95-112">**假定技能**: HTML、 基本的级联样式表 (CSS)。</span><span class="sxs-lookup"><span data-stu-id="6be95-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="6be95-113">学习内容集的第一个教程中：</span><span class="sxs-lookup"><span data-stu-id="6be95-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="6be95-114">ASP.NET Web Pages 何种技术，它为是。</span><span class="sxs-lookup"><span data-stu-id="6be95-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="6be95-115">WebMatrix 是什么。</span><span class="sxs-lookup"><span data-stu-id="6be95-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="6be95-116">如何安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-116">How to install everything.</span></span>
> - <span data-ttu-id="6be95-117">如何使用 WebMatrix 创建网站。</span><span class="sxs-lookup"><span data-stu-id="6be95-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="6be95-118">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="6be95-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="6be95-119">Microsoft Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="6be95-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="6be95-120">WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="6be95-120">WebMatrix.</span></span>
> - <span data-ttu-id="6be95-121">*.cshtml*页</span><span class="sxs-lookup"><span data-stu-id="6be95-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="6be95-122">Mike 教皇最初编写了本教程。</span><span class="sxs-lookup"><span data-stu-id="6be95-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="6be95-123">Tom FitzMacken 针对 Microsoft WebMatrix 3 更新它。</span><span class="sxs-lookup"><span data-stu-id="6be95-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6be95-124">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6be95-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6be95-125">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="6be95-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="6be95-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="6be95-126">WebMatrix 3</span></span>


## <a name="what-should-you-know"></a><span data-ttu-id="6be95-127">您应该知道哪些内容？</span><span class="sxs-lookup"><span data-stu-id="6be95-127">What Should You Know?</span></span>

<span data-ttu-id="6be95-128">我们假定您熟悉：</span><span class="sxs-lookup"><span data-stu-id="6be95-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="6be95-129">**HTML**。</span><span class="sxs-lookup"><span data-stu-id="6be95-129">**HTML**.</span></span> <span data-ttu-id="6be95-130">没有深入专业知识是必需的。</span><span class="sxs-lookup"><span data-stu-id="6be95-130">No in-depth expertise is required.</span></span> <span data-ttu-id="6be95-131">我们将不再对 HTML，但我们也不使用任何复杂。</span><span class="sxs-lookup"><span data-stu-id="6be95-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="6be95-132">我们将提供指向 HTML 教程，我们认为这非常有用。</span><span class="sxs-lookup"><span data-stu-id="6be95-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="6be95-133">**级联样式表 (CSS)**。</span><span class="sxs-lookup"><span data-stu-id="6be95-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="6be95-134">与相同 HTML。</span><span class="sxs-lookup"><span data-stu-id="6be95-134">Same as with HTML.</span></span>
- <span data-ttu-id="6be95-135">**基本数据库的想法**。</span><span class="sxs-lookup"><span data-stu-id="6be95-135">**Basic database ideas**.</span></span> <span data-ttu-id="6be95-136">如果已使用电子表格的数据和排序和筛选的专业技能级别的数据，我们通常假定用于本教程系列。</span><span class="sxs-lookup"><span data-stu-id="6be95-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="6be95-137">我们还假定你感兴趣学习基本编程。</span><span class="sxs-lookup"><span data-stu-id="6be95-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="6be95-138">ASP.NET Web Pages 使用名为 C# 的编程语言。</span><span class="sxs-lookup"><span data-stu-id="6be95-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="6be95-139">您无需具有任何背景中编程，只需在其中的关注。</span><span class="sxs-lookup"><span data-stu-id="6be95-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="6be95-140">如果您曾经编写任何 JavaScript 在网页上之前，您有充足的背景。</span><span class="sxs-lookup"><span data-stu-id="6be95-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="6be95-141">请注意，是否您熟悉编程，你可能会发现我们就将新程序员加快时，最初设置了本教程将缓慢移动。</span><span class="sxs-lookup"><span data-stu-id="6be95-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="6be95-142">随着我们过去的几个的第一个教程，不过，会有不到基本编程来解释，操作会将上，在更快的剪辑。</span><span class="sxs-lookup"><span data-stu-id="6be95-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="6be95-143">你需要什么？</span><span class="sxs-lookup"><span data-stu-id="6be95-143">What Do You Need?</span></span>

<span data-ttu-id="6be95-144">你将需要以下项目：</span><span class="sxs-lookup"><span data-stu-id="6be95-144">Here's what you'll need:</span></span>

- <span data-ttu-id="6be95-145">在运行 Windows 8、 Windows 7、 Windows Server 2008 或 Windows Server 2012 的计算机。</span><span class="sxs-lookup"><span data-stu-id="6be95-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="6be95-146">实时的 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="6be95-146">A live internet connection.</span></span>
- <span data-ttu-id="6be95-147">（需要在安装过程） 具有管理员特权。</span><span class="sxs-lookup"><span data-stu-id="6be95-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="6be95-148">什么是 ASP.NET 网页？</span><span class="sxs-lookup"><span data-stu-id="6be95-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="6be95-149">ASP.NET Web Pages 是一个框架，可用于创建动态网页。</span><span class="sxs-lookup"><span data-stu-id="6be95-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="6be95-150">简单的 HTML web 页面是静态的;其内容取决于固定的页的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="6be95-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="6be95-151">如您创建使用 ASP.NET Web Pages 动态页，您可以使用代码动态创建页面内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="6be95-152">动态页，您可以执行各种操作。</span><span class="sxs-lookup"><span data-stu-id="6be95-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="6be95-153">您可以通过使用窗体输入请求用户，然后更改页上显示的内容或它的外观。</span><span class="sxs-lookup"><span data-stu-id="6be95-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="6be95-154">您可以从用户中获取信息、 将其保存在数据库中，并更高版本列出它。</span><span class="sxs-lookup"><span data-stu-id="6be95-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="6be95-155">你可以从您的网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="6be95-155">You can send email from your site.</span></span> <span data-ttu-id="6be95-156">可以与 web （例如，映射服务） 上的其他服务进行交互，并生成集成来自这些源的信息的页面。</span><span class="sxs-lookup"><span data-stu-id="6be95-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="6be95-157">WebMatrix 是什么？</span><span class="sxs-lookup"><span data-stu-id="6be95-157">What is WebMatrix?</span></span>

<span data-ttu-id="6be95-158">WebMatrix 是一个集成的网页编辑器、 数据库实用程序、 用于测试页面和用于将你的网站发布到 Internet 的功能的 web 服务器的工具。</span><span class="sxs-lookup"><span data-stu-id="6be95-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="6be95-159">WebMatrix 是免费的而且很容易安装且易于使用。</span><span class="sxs-lookup"><span data-stu-id="6be95-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="6be95-160">（它也只是普通的 HTML 页面，以及其他技术，如 PHP。）</span><span class="sxs-lookup"><span data-stu-id="6be95-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="6be95-161">您不会真正*具有*使用 WebMatrix 来处理使用 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="6be95-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="6be95-162">您可以创建页，使用文本编辑器，例如，和测试页使用有权访问的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="6be95-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="6be95-163">但是，WebMatrix 得所有非常简单，因此这些教程将使用在整个的 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="6be95-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="6be95-164">有关这些教程</span><span class="sxs-lookup"><span data-stu-id="6be95-164">About These Tutorials</span></span>

<span data-ttu-id="6be95-165">本教程系列将介绍如何使用 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="6be95-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="6be95-166">在此介绍性教程集中中共有 9 教程。</span><span class="sxs-lookup"><span data-stu-id="6be95-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="6be95-167">它的一系列教程的集，从 ASP.NET Web Pages 初级用户到创建实际的专业外观的网站的一部分。</span><span class="sxs-lookup"><span data-stu-id="6be95-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="6be95-168">第一个教程设置集中向您展示如何使用 ASP.NET Web Pages 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="6be95-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="6be95-169">完成后，可以使用此结束，其中的更深入地浏览网页选取的其他教程集。</span><span class="sxs-lookup"><span data-stu-id="6be95-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="6be95-170">我们有意继续轻松进行深入的解释。</span><span class="sxs-lookup"><span data-stu-id="6be95-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="6be95-171">只要我们显示一些内容，对于本教程系列我们始终选择的方法，我们认为是最易于帮助理解。</span><span class="sxs-lookup"><span data-stu-id="6be95-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="6be95-172">更高版本的教程集转到更多深入分析和显示更高效或更灵活的方法 （也更有趣）。</span><span class="sxs-lookup"><span data-stu-id="6be95-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="6be95-173">但是，这些教程要求您首先了解的基本知识。</span><span class="sxs-lookup"><span data-stu-id="6be95-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="6be95-174">你刚刚启动教程系列介绍了这些功能的 ASP.NET Web Pages:</span><span class="sxs-lookup"><span data-stu-id="6be95-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="6be95-175">简介和获取安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="6be95-176">（这是您在阅读本教程中值。）</span><span class="sxs-lookup"><span data-stu-id="6be95-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="6be95-177">ASP.NET Web Pages 编程的基础知识。</span><span class="sxs-lookup"><span data-stu-id="6be95-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="6be95-178">创建数据库。</span><span class="sxs-lookup"><span data-stu-id="6be95-178">Creating a database.</span></span>
- <span data-ttu-id="6be95-179">创建和处理用户输入窗体。</span><span class="sxs-lookup"><span data-stu-id="6be95-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="6be95-180">添加、 更新和删除数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="6be95-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="6be95-181">您将创建哪些内容？</span><span class="sxs-lookup"><span data-stu-id="6be95-181">What Will You Create?</span></span>

<span data-ttu-id="6be95-182">本教程中设置和后续条件围绕的网站可以在其中列出您喜欢的电影。</span><span class="sxs-lookup"><span data-stu-id="6be95-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="6be95-183">您可以输入电影，编辑它们，然后列出它们。</span><span class="sxs-lookup"><span data-stu-id="6be95-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="6be95-184">下面是一些你将创建在本教程系列中的页。</span><span class="sxs-lookup"><span data-stu-id="6be95-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="6be95-185">第一个显示电影列表，您将创建的页面：</span><span class="sxs-lookup"><span data-stu-id="6be95-185">The first one shows the movie listing page that you'll create:</span></span>

![已完成的影片应用程序显示电影列表](getting-started/_static/image1.png)

<span data-ttu-id="6be95-187">而以下是可将新电影信息添加到你的站点的页面：</span><span class="sxs-lookup"><span data-stu-id="6be95-187">And here's the page that lets you add new movie information to your site:</span></span>

![显示将添加影片页的已完成的电影应用](getting-started/_static/image2.png)

<span data-ttu-id="6be95-189">后续教程集生成对此设置，并添加更多的功能，如将图片上载、 让人们登录、 发送电子邮件和与社交媒体相集成。</span><span class="sxs-lookup"><span data-stu-id="6be95-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="6be95-190">请参阅在 Azure 上运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="6be95-190">See this App Running on Azure</span></span>

<span data-ttu-id="6be95-191">若要查看已完成的站点作为实时 web 应用运行吗？</span><span class="sxs-lookup"><span data-stu-id="6be95-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="6be95-192">只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="6be95-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="6be95-193">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6be95-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="6be95-194">如果你还没有帐户，你具有以下选项：</span><span class="sxs-lookup"><span data-stu-id="6be95-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="6be95-195">[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="6be95-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="6be95-196">[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="6be95-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="6be95-197">安装的所有内容</span><span class="sxs-lookup"><span data-stu-id="6be95-197">Installing Everything</span></span>

<span data-ttu-id="6be95-198">可以使用 microsoft Web 平台安装程序安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="6be95-199">事实上，您安装安装程序，并且然后使用它来安装其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="6be95-200">若要使用 Web 页，必须至少具有 Windows XP SP3 安装或 Windows Server 2008 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6be95-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="6be95-201">上[Web Pages 页](../../../index.md)的 ASP.NET 网站中，单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="6be95-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET Web 站点显示&quot;安装 WebMatrix&quot;按钮](getting-started/_static/image3.png)

<span data-ttu-id="6be95-203">需要接受许可条款和隐私声明，然后安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="6be95-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![接受条款以开始安装](getting-started/_static/image4.png)

<span data-ttu-id="6be95-205">单击**运行**以开始安装。</span><span class="sxs-lookup"><span data-stu-id="6be95-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="6be95-206">(如果你想要保存该安装程序，请单击**保存**，然后从保存位置的文件夹运行安装程序。)</span><span class="sxs-lookup"><span data-stu-id="6be95-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="6be95-207">Web 平台安装程序将显示，您可以随时安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="6be95-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="6be95-208">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="6be95-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="6be95-209">安装过程计算出它具有要在计算机上安装并启动进程。</span><span class="sxs-lookup"><span data-stu-id="6be95-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="6be95-210">具体取决于确切的功能安装，该过程可能需要从几分钟到几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="6be95-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="6be95-211">选择**我接受**以接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="6be95-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="6be95-212">Hello WebMatrix</span><span class="sxs-lookup"><span data-stu-id="6be95-212">Hello, WebMatrix</span></span>

<span data-ttu-id="6be95-213">完成后，安装过程可以自动启动 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="6be95-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="6be95-214">如果没有，Windows，在从**启动**菜单，启动**Microsoft WebMatrix**。</span><span class="sxs-lookup"><span data-stu-id="6be95-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="6be95-215">当首次启动 WebMatrix 时，系统将提供机会与 Microsoft 帐户登录到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="6be95-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="6be95-216">通过登录，系统会通过 Azure 的 10 个免费的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="6be95-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="6be95-217">这些免费的 web 应用程序提供测试您的应用程序的简便方法。</span><span class="sxs-lookup"><span data-stu-id="6be95-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="6be95-218">如果你还没有 Azure 帐户，但有 MSDN 订阅，可以[激活 MSDN 订阅权益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="6be95-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="6be95-219">否则，可以只需几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="6be95-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6be95-220">有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="6be95-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="6be95-221">无需立即登录以继续学习本教程。</span><span class="sxs-lookup"><span data-stu-id="6be95-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="6be95-222">如果您确实不登录现在，你仍将进行更高版本登录的选项。</span><span class="sxs-lookup"><span data-stu-id="6be95-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="6be95-223">上次[主题](publishing.md)在本教程系列介绍了如何将你的网站部署到 Azure; 因此，您将需要登录以完成该主题。</span><span class="sxs-lookup"><span data-stu-id="6be95-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="6be95-224">此时，请登录你的 Microsoft 帐户或选择**不是现在**右下角中。</span><span class="sxs-lookup"><span data-stu-id="6be95-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![登录](getting-started/_static/image7.png)

<span data-ttu-id="6be95-226">若要开始，将创建空白网站，并添加一个页面。</span><span class="sxs-lookup"><span data-stu-id="6be95-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="6be95-227">在此集中的下一个教程将尝试使用某个内置网站模板。</span><span class="sxs-lookup"><span data-stu-id="6be95-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="6be95-228">在开始窗口中，单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="6be95-228">In the start window, click **New**.</span></span>

![WebMatrix 启动屏幕](getting-started/_static/image8.png)

<span data-ttu-id="6be95-230">模板是网站的预生成的文件和页面的不同类型。</span><span class="sxs-lookup"><span data-stu-id="6be95-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="6be95-231">若要查看所有默认提供的模板，请选择模板库选项。</span><span class="sxs-lookup"><span data-stu-id="6be95-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![选择模板库](getting-started/_static/image9.png)

<span data-ttu-id="6be95-233">在中**快速启动**窗口中，选择**空网站**从**ASP.NET**组，并命名新的站点"WebPagesMovies"。</span><span class="sxs-lookup"><span data-stu-id="6be95-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![WebMatrix 快速启动窗口中选择空网站模板](getting-started/_static/image10.png)

<span data-ttu-id="6be95-235">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="6be95-235">Click **Next**.</span></span>

<span data-ttu-id="6be95-236">如果你已登录到你的 Microsoft 帐户，您将有机会在 Azure 上创建站点。</span><span class="sxs-lookup"><span data-stu-id="6be95-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="6be95-237">根据你的站点的默认名称的名称**WebPagesMovies.azurewebsites.net**建议; 但是，感叹号指示此名称不是 Windows Azure 上提供。</span><span class="sxs-lookup"><span data-stu-id="6be95-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="6be95-238">为简单起见，选择**跳过**绕过现在在 Azure 上创建网站。</span><span class="sxs-lookup"><span data-stu-id="6be95-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="6be95-239">更高版本在此系列中，我们将站点发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6be95-239">Later in this series, we will publish the site to Azure.</span></span>

![创建 azure 网站](getting-started/_static/image11.png)

<span data-ttu-id="6be95-241">WebMatrix 创建并打开该站点：</span><span class="sxs-lookup"><span data-stu-id="6be95-241">WebMatrix creates and opens the site:</span></span>

![在 WebMatrix 中打开新 WebPagesMovies 站点](getting-started/_static/image12.png)

<span data-ttu-id="6be95-243">在顶部，没有快速访问工具栏和一个功能区。</span><span class="sxs-lookup"><span data-stu-id="6be95-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="6be95-244">在左下角，你看到工作区选择器，切换任务 (**站点**，**文件**，**数据库**，**报表**)。</span><span class="sxs-lookup"><span data-stu-id="6be95-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="6be95-245">右侧是内容窗格中，用于在编辑器和报表。</span><span class="sxs-lookup"><span data-stu-id="6be95-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="6be95-246">并在底部有时您会看到消息通知栏。</span><span class="sxs-lookup"><span data-stu-id="6be95-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="6be95-247">您将了解有关 WebMatrix 和它的功能在完成这些教程。</span><span class="sxs-lookup"><span data-stu-id="6be95-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="6be95-248">创建 Web 页</span><span class="sxs-lookup"><span data-stu-id="6be95-248">Creating a Web Page</span></span>

<span data-ttu-id="6be95-249">若要熟悉 WebMatrix 和 ASP.NET Web Pages，将创建一个简单的页面。</span><span class="sxs-lookup"><span data-stu-id="6be95-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="6be95-250">在工作区选择器中，选择**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="6be95-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="6be95-251">此工作区允许您使用的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="6be95-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="6be95-252">左的窗格显示您的网站的文件结构。</span><span class="sxs-lookup"><span data-stu-id="6be95-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="6be95-253">此功能区改为显示与文件相关的任务。</span><span class="sxs-lookup"><span data-stu-id="6be95-253">The ribbon changes to show file-related tasks.</span></span>

![在 WebMatrix 中的文件工作区](getting-started/_static/image13.png)

<span data-ttu-id="6be95-255">在功能区中，单击下的箭头**新建**，然后单击**新文件**。</span><span class="sxs-lookup"><span data-stu-id="6be95-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![使用&quot;新建&quot;命令在功能区中创建新文件](getting-started/_static/image14.png)

<span data-ttu-id="6be95-257">WebMatrix 显示文件类型的列表。</span><span class="sxs-lookup"><span data-stu-id="6be95-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="6be95-258">选择**CSHTML**，然后在**名称**框中，键入"HelloWorld"。</span><span class="sxs-lookup"><span data-stu-id="6be95-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="6be95-259">CSHTML 页面是 ASP.NET Web Pages 页。</span><span class="sxs-lookup"><span data-stu-id="6be95-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![创建新的 CSHTML 页面命名 HelloWorld.cshtml](getting-started/_static/image15.png)

<span data-ttu-id="6be95-261">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="6be95-261">Click **OK**.</span></span>

<span data-ttu-id="6be95-262">WebMatrix 创建页，并在编辑器中打开它。</span><span class="sxs-lookup"><span data-stu-id="6be95-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 编辑器中的新 HelloWorld 页](getting-started/_static/image16.png)

<span data-ttu-id="6be95-264">正如您所看到的页面包含主要是普通的 HTML 标记，如下所示顶部块除外：</span><span class="sxs-lookup"><span data-stu-id="6be95-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="6be95-265">这将添加代码，如稍后您将看到。</span><span class="sxs-lookup"><span data-stu-id="6be95-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="6be95-266">请注意，页面的不同部分&mdash;元素名称、 属性和文本，以及在顶部块 — 所有位于不同的颜色。</span><span class="sxs-lookup"><span data-stu-id="6be95-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="6be95-267">这称为*语法突出显示*，使得更容易地将清除所有内容。</span><span class="sxs-lookup"><span data-stu-id="6be95-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="6be95-268">它是可以轻松地处理在 WebMatrix 中的 web 页面的功能之一。</span><span class="sxs-lookup"><span data-stu-id="6be95-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="6be95-269">添加的内容`<head>`和`<body>`元素类似于下面的示例。</span><span class="sxs-lookup"><span data-stu-id="6be95-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="6be95-270">（如果你想，您可以只需将以下块复制和使用以下代码替换整个现有页面。）</span><span class="sxs-lookup"><span data-stu-id="6be95-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="6be95-271">在快速访问工具栏或在**文件**菜单上，单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="6be95-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![在 WebMatrix 快速访问工具栏中保存按钮](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="6be95-273">测试页</span><span class="sxs-lookup"><span data-stu-id="6be95-273">Testing the Page</span></span>

<span data-ttu-id="6be95-274">在中**文件**工作区中，右键单击*HelloWorld.cshtml*页，然后单击**浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="6be95-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![运行在 WebMatrix 功能区中使用运行按钮的页](getting-started/_static/image18.png)

<span data-ttu-id="6be95-276">WebMatrix 启动内置的 web 服务器 (IIS Express)，可用于测试您的计算机上的页面。</span><span class="sxs-lookup"><span data-stu-id="6be95-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="6be95-277">（无需 IIS Express 在 WebMatrix 中，你将需要发布页面的 web 服务器到某个位置之前无法对其进行测试。）在默认浏览器中显示的页。</span><span class="sxs-lookup"><span data-stu-id="6be95-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;Hello World&quot;页在浏览器中运行](getting-started/_static/image19.png)

<span data-ttu-id="6be95-279">请注意，当在 WebMatrix 中测试一个页面，在浏览器中的 URL 是类似`http://localhost:33651/HelloWorld.cshtml.`名称*localhost*指的是本地服务器，这意味着处理页面时由你自己的计算机上的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="6be95-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="6be95-280">如前所述，WebMatrix 将包含名为 IIS Express 运行时启动的页的 web 服务器程序。</span><span class="sxs-lookup"><span data-stu-id="6be95-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="6be95-281">之后的数字*localhost* (例如， *localhost:33651*) 是指*端口号*您的计算机上。</span><span class="sxs-lookup"><span data-stu-id="6be95-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="6be95-282">这是 IIS Express 使用为此特定网站的"通道"号。</span><span class="sxs-lookup"><span data-stu-id="6be95-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="6be95-283">端口号是随机选择的范围 1024 到 65536 中时创建你的站点，并为您创建的每个站点不同。</span><span class="sxs-lookup"><span data-stu-id="6be95-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="6be95-284">（测试自己的网站时，端口号几乎可以肯定将不同数量比 33561。）通过为每个网站使用其他端口，IIS Express 可以让保持连续的你它正在与通信的站点。</span><span class="sxs-lookup"><span data-stu-id="6be95-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="6be95-285">当你发布你的站点到公共 web 服务器，不会再看到时，更高版本*localhost*在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="6be95-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="6be95-286">此时，你将看到更典型的 URL，例如`http://myhostingsite/mywebsite/HelloWorld.cshtml`或任何页。</span><span class="sxs-lookup"><span data-stu-id="6be95-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="6be95-287">您将了解有关稍后在本系列教程中发布站点。</span><span class="sxs-lookup"><span data-stu-id="6be95-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="6be95-288">添加一些服务器端代码</span><span class="sxs-lookup"><span data-stu-id="6be95-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="6be95-289">关闭浏览器并返回到 WebMatrix 中的页。</span><span class="sxs-lookup"><span data-stu-id="6be95-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="6be95-290">将行添加到代码块，以便它看起来像以下代码：</span><span class="sxs-lookup"><span data-stu-id="6be95-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="6be95-291">这是很少的 Razor 代码中。</span><span class="sxs-lookup"><span data-stu-id="6be95-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="6be95-292">获取当前日期和时间，并将放到此值可能明确*变量*名为`currentDateTime`。</span><span class="sxs-lookup"><span data-stu-id="6be95-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="6be95-293">您在阅读更多有关下一教程中的 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="6be95-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="6be95-294">页上，在正文中后`<p>Hello World!</p>`元素中，添加以下：</span><span class="sxs-lookup"><span data-stu-id="6be95-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="6be95-295">此代码获取的值放入`currentDateTime`顶部变量并将其插入到页的标记。</span><span class="sxs-lookup"><span data-stu-id="6be95-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="6be95-296">`@`字符将标记中页面的 ASP.NET Web Pages 代码。</span><span class="sxs-lookup"><span data-stu-id="6be95-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="6be95-297">运行的页再次 （WebMatrix 将保存所做的更改为你之前运行的页）。</span><span class="sxs-lookup"><span data-stu-id="6be95-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="6be95-298">此时会显示的日期和时间的页中。</span><span class="sxs-lookup"><span data-stu-id="6be95-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World&quot;与动态生成的时间显示在浏览器中运行页面](getting-started/_static/image20.png)

<span data-ttu-id="6be95-300">稍等片刻，然后刷新浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="6be95-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="6be95-301">日期和时间显示更新。</span><span class="sxs-lookup"><span data-stu-id="6be95-301">The date and time display is updated.</span></span>

<span data-ttu-id="6be95-302">在浏览器中，查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="6be95-302">In the browser, look at the page source.</span></span> <span data-ttu-id="6be95-303">它类似于以下标记：</span><span class="sxs-lookup"><span data-stu-id="6be95-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="6be95-304">请注意，`@{ }`顶部块不存在。</span><span class="sxs-lookup"><span data-stu-id="6be95-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="6be95-305">另请注意，日期和时间显示会显示实际字符串的字符 (`1/18/2012 2:49:50 PM`或其他任何)，而非`@currentDateTime`像中有 *.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="6be95-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="6be95-306">发生了什么情况下面是当运行页面时，ASP.NET 处理的所有代码 （几乎在此情况下） 标记有`@`。</span><span class="sxs-lookup"><span data-stu-id="6be95-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="6be95-307">此代码生成输出，并且该输出已插入到页。</span><span class="sxs-lookup"><span data-stu-id="6be95-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="6be95-308">这是 ASP.NET Web Pages 的作用</span><span class="sxs-lookup"><span data-stu-id="6be95-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="6be95-309">当您阅读了 ASP.NET Web Pages 生成动态 web 内容时，你已了解了想法。</span><span class="sxs-lookup"><span data-stu-id="6be95-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="6be95-310">你只需创建的页面包含您以前看到的相同 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="6be95-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="6be95-311">它还可以包含可执行各种任务的代码。</span><span class="sxs-lookup"><span data-stu-id="6be95-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="6be95-312">在此示例中，像普通任务，将当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="6be95-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="6be95-313">如您所见，您可以单引号分隔文件，代码与 HTML 以在页面中生成输出。</span><span class="sxs-lookup"><span data-stu-id="6be95-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="6be95-314">当有人请求 *.cshtml*仍在手中的 web 服务器时，在浏览器，ASP.NET 页处理页。</span><span class="sxs-lookup"><span data-stu-id="6be95-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="6be95-315">ASP.NET 插入代码的输出 （如果有） 页以 html 格式。</span><span class="sxs-lookup"><span data-stu-id="6be95-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="6be95-316">完成代码处理后，ASP.NET 将在生成的页面发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="6be95-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="6be95-317">所有浏览器不断获取为 HTML。</span><span class="sxs-lookup"><span data-stu-id="6be95-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="6be95-318">下面是一个关系图：</span><span class="sxs-lookup"><span data-stu-id="6be95-318">Here's a diagram:</span></span>

![ASP.NET 动态生成 HTML 如何的概念流](getting-started/_static/image21.png)

<span data-ttu-id="6be95-320">其原理很简单，但有许多有趣的任务可执行代码，并有许多有趣的方式在其中您可以向动态添加 HTML 内容页。</span><span class="sxs-lookup"><span data-stu-id="6be95-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="6be95-321">和 ASP.NET *.cshtml*页面，例如从任何 HTML 页上，还可以包括在浏览器本身 （JavaScript 和 jQuery 代码） 中运行的代码。</span><span class="sxs-lookup"><span data-stu-id="6be95-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="6be95-322">将介绍所有这些内容在本教程系列和后续条件。</span><span class="sxs-lookup"><span data-stu-id="6be95-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="6be95-323">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="6be95-323">Coming Up Next</span></span>

<span data-ttu-id="6be95-324">在此系列中的下一教程，您了解 ASP.NET Web Pages 编程有点多。</span><span class="sxs-lookup"><span data-stu-id="6be95-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6be95-325">其他资源</span><span class="sxs-lookup"><span data-stu-id="6be95-325">Additional Resources</span></span>

<span data-ttu-id="6be95-326">[从头开始创建一个 ASP.NET 网站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="6be95-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="6be95-327">这是具体而言，是一个教程使用 WebMatrix (不是 ASP.NET Web Pages)。</span><span class="sxs-lookup"><span data-stu-id="6be95-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="6be95-328">它将进入稍有一些我们不会在本教程系列介绍 WebMatrix 的其他功能的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="6be95-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6be95-329">下一篇</span><span class="sxs-lookup"><span data-stu-id="6be95-329">Next</span></span>](intro-to-web-pages-programming.md)
