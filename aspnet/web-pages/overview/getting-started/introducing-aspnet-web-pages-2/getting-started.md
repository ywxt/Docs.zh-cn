---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 引入了 ASP.NET Web Pages-入门教程 |Microsoft 文档
author: tfitzmac
description: WebMatrix 是不再建议将其作为集成的开发环境的 ASP.NET Web 页。 使用 Visual Studio 或 Visual Studio 代码。 本指南...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 5fd67a230f76774e102094f42426b8bb126c0cc6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30898094"
---
<a name="introducing-aspnet-web-pages---getting-started"></a><span data-ttu-id="90590-105">引入了 ASP.NET Web 页-入门</span><span class="sxs-lookup"><span data-stu-id="90590-105">Introducing ASP.NET Web Pages - Getting Started</span></span>
====================
<span data-ttu-id="90590-106">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="90590-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > 
> > <span data-ttu-id="90590-107">WebMatrix 是不再建议将其作为集成的开发环境的 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="90590-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="90590-108">使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="90590-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="90590-109">此指南并应用程序使您的概览的 ASP.NET Web Pages （2 或更高版本） 和 Razor 语法，一个轻型框架，用于创建动态网站。</span><span class="sxs-lookup"><span data-stu-id="90590-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="90590-110">它还引入了 WebMatrix 中，一个用于创建网页和网站工具。</span><span class="sxs-lookup"><span data-stu-id="90590-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="90590-111">**级别**： 新的 ASP.NET Web 页面。</span><span class="sxs-lookup"><span data-stu-id="90590-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="90590-112">**假定的技能**: HTML，基本的级联样式表 (CSS)。</span><span class="sxs-lookup"><span data-stu-id="90590-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="90590-113">你将要掌握的内容集的第一个教程中：</span><span class="sxs-lookup"><span data-stu-id="90590-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="90590-114">哪种 ASP.NET Web Pages 技术和它的适用。</span><span class="sxs-lookup"><span data-stu-id="90590-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="90590-115">WebMatrix 是什么。</span><span class="sxs-lookup"><span data-stu-id="90590-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="90590-116">如何安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="90590-116">How to install everything.</span></span>
> - <span data-ttu-id="90590-117">如何使用 WebMatrix 创建网站。</span><span class="sxs-lookup"><span data-stu-id="90590-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="90590-118">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="90590-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="90590-119">Microsoft Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="90590-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="90590-120">WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="90590-120">WebMatrix.</span></span>
> - <span data-ttu-id="90590-121">*.cshtml*页</span><span class="sxs-lookup"><span data-stu-id="90590-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="90590-122">Mike Pope 最初已写入本教程。</span><span class="sxs-lookup"><span data-stu-id="90590-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="90590-123">Tom FitzMacken 为 Microsoft WebMatrix 3 更新它。</span><span class="sxs-lookup"><span data-stu-id="90590-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="90590-124">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="90590-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="90590-125">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="90590-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="90590-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="90590-126">WebMatrix 3</span></span>


## <a name="what-should-you-know"></a><span data-ttu-id="90590-127">你应该知道哪些内容？</span><span class="sxs-lookup"><span data-stu-id="90590-127">What Should You Know?</span></span>

<span data-ttu-id="90590-128">我们假定你熟悉：</span><span class="sxs-lookup"><span data-stu-id="90590-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="90590-129">**HTML**。</span><span class="sxs-lookup"><span data-stu-id="90590-129">**HTML**.</span></span> <span data-ttu-id="90590-130">没有深入专业知识是必需的。</span><span class="sxs-lookup"><span data-stu-id="90590-130">No in-depth expertise is required.</span></span> <span data-ttu-id="90590-131">我们不会介绍 HTML，但我们也不使用任何复杂。</span><span class="sxs-lookup"><span data-stu-id="90590-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="90590-132">我们将提供到 HTML 教程，我们认为它们是有用的链接。</span><span class="sxs-lookup"><span data-stu-id="90590-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="90590-133">**级联样式表 (CSS)**。</span><span class="sxs-lookup"><span data-stu-id="90590-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="90590-134">与相同 HTML。</span><span class="sxs-lookup"><span data-stu-id="90590-134">Same as with HTML.</span></span>
- <span data-ttu-id="90590-135">**基本数据库想法**。</span><span class="sxs-lookup"><span data-stu-id="90590-135">**Basic database ideas**.</span></span> <span data-ttu-id="90590-136">如果你已对数据使用电子表格和排序和筛选的数据，是专业技术级别我们通常假定此教程的集。</span><span class="sxs-lookup"><span data-stu-id="90590-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="90590-137">我们还假定你感兴趣学习基本编程。</span><span class="sxs-lookup"><span data-stu-id="90590-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="90590-138">ASP.NET 网页使用名为 C# 的编程语言。</span><span class="sxs-lookup"><span data-stu-id="90590-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="90590-139">你无需具有在编程中，只需有兴趣了解它的任何背景。</span><span class="sxs-lookup"><span data-stu-id="90590-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="90590-140">如果您曾经编写了任何 JavaScript 网页中之前，你具有充足的背景。</span><span class="sxs-lookup"><span data-stu-id="90590-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="90590-141">请注意，是否你熟悉编程，你可能会发现时我们将新程序员掌握，最初设置了本教程将慢慢地移动。</span><span class="sxs-lookup"><span data-stu-id="90590-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="90590-142">我们共同点的第一个的几个教程，不过，将会不太基本的编程，以解释和操作将移动更快的剪辑。</span><span class="sxs-lookup"><span data-stu-id="90590-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="90590-143">你需要做什么？</span><span class="sxs-lookup"><span data-stu-id="90590-143">What Do You Need?</span></span>

<span data-ttu-id="90590-144">你将需要以下项目：</span><span class="sxs-lookup"><span data-stu-id="90590-144">Here's what you'll need:</span></span>

- <span data-ttu-id="90590-145">运行 Windows 8、 Windows 7、 Windows Server 2008 或 Windows Server 2012 的计算机。</span><span class="sxs-lookup"><span data-stu-id="90590-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="90590-146">实时的 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="90590-146">A live internet connection.</span></span>
- <span data-ttu-id="90590-147">（安装过程所需） 具有管理员特权。</span><span class="sxs-lookup"><span data-stu-id="90590-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="90590-148">什么是 ASP.NET Web 页？</span><span class="sxs-lookup"><span data-stu-id="90590-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="90590-149">ASP.NET Web 页是一个框架，可用于创建动态网页。</span><span class="sxs-lookup"><span data-stu-id="90590-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="90590-150">简单的 HTML 网页是静态的;位于页中的固定 HTML 标记取决于其内容。</span><span class="sxs-lookup"><span data-stu-id="90590-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="90590-151">如你创建的 ASP.NET Web Pages 使用的动态页面，您可以动态，通过使用代码创建的页面内容。</span><span class="sxs-lookup"><span data-stu-id="90590-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="90590-152">动态页面，您可以执行所有类型的操作。</span><span class="sxs-lookup"><span data-stu-id="90590-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="90590-153">你可以要求用户进行输入使用窗体，，然后更改页的显示或它的外观。</span><span class="sxs-lookup"><span data-stu-id="90590-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="90590-154">你可以从用户获取信息，将其保存在数据库中，然后将其列更高版本。</span><span class="sxs-lookup"><span data-stu-id="90590-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="90590-155">你可以从您的网站发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="90590-155">You can send email from your site.</span></span> <span data-ttu-id="90590-156">你可以与 web （例如，映射服务） 上的其他服务进行交互，并生成集成来自这些源的信息的页。</span><span class="sxs-lookup"><span data-stu-id="90590-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="90590-157">WebMatrix 是什么？</span><span class="sxs-lookup"><span data-stu-id="90590-157">What is WebMatrix?</span></span>

<span data-ttu-id="90590-158">WebMatrix 是集成的网页编辑器、 一个数据库实用程序、 用于测试页面和用于将你的网站发布到 Internet 的功能的 web 服务器的工具。</span><span class="sxs-lookup"><span data-stu-id="90590-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="90590-159">WebMatrix 是免费的而且很容易安装且易于使用。</span><span class="sxs-lookup"><span data-stu-id="90590-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="90590-160">（它还适用仅纯 HTML 页面，以及其他技术，如 PHP。）</span><span class="sxs-lookup"><span data-stu-id="90590-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="90590-161">实际不*具有*要 WebMatrix 用于工作与 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="90590-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="90590-162">你可以创建页面，通过使用文本编辑器中，例如，使用和测试页有权访问的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="90590-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="90590-163">但是，WebMatrix 更加所有非常方便，因此这些教程将使用在整个 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="90590-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="90590-164">有关这些教程</span><span class="sxs-lookup"><span data-stu-id="90590-164">About These Tutorials</span></span>

<span data-ttu-id="90590-165">此教程集是如何使用 ASP.NET Web 页的简介。</span><span class="sxs-lookup"><span data-stu-id="90590-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="90590-166">在此介绍性教程集中共有 9 教程。</span><span class="sxs-lookup"><span data-stu-id="90590-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="90590-167">它的一系列教程的集，使您从 ASP.NET Web Pages 初级用户转至创建真实的专业的网站的一部分。</span><span class="sxs-lookup"><span data-stu-id="90590-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="90590-168">此第一个教程设置侧重点向您展示如何处理与 ASP.NET Web 页的基础知识。</span><span class="sxs-lookup"><span data-stu-id="90590-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="90590-169">完成后，你可以使用选取此结束，其中，更深入探索 Web 页的其他教程集。</span><span class="sxs-lookup"><span data-stu-id="90590-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="90590-170">我们有意继续轻松深入说明。</span><span class="sxs-lookup"><span data-stu-id="90590-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="90590-171">然后我们显示内容，只要此教程集我们始终选择我们认为的方法是最简单的方法了解。</span><span class="sxs-lookup"><span data-stu-id="90590-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="90590-172">更高版本的教程集进入详细深度，并显示效率更高或更灵活方法 （也更有趣）。</span><span class="sxs-lookup"><span data-stu-id="90590-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="90590-173">但这些教程要求你首先了解基础知识。</span><span class="sxs-lookup"><span data-stu-id="90590-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="90590-174">您刚才已启动的教程集涵盖这些功能的 ASP.NET Web 页：</span><span class="sxs-lookup"><span data-stu-id="90590-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="90590-175">简介和获取安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="90590-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="90590-176">（这是你正在阅读本教程中值。）</span><span class="sxs-lookup"><span data-stu-id="90590-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="90590-177">ASP.NET Web Pages 编程基础知识。</span><span class="sxs-lookup"><span data-stu-id="90590-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="90590-178">创建数据库。</span><span class="sxs-lookup"><span data-stu-id="90590-178">Creating a database.</span></span>
- <span data-ttu-id="90590-179">创建和处理用户输入窗体。</span><span class="sxs-lookup"><span data-stu-id="90590-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="90590-180">添加、 更新和删除数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="90590-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="90590-181">你将创建什么？</span><span class="sxs-lookup"><span data-stu-id="90590-181">What Will You Create?</span></span>

<span data-ttu-id="90590-182">本教程设置和后续的围绕的网站，你可以在其中列出您喜欢的电影。</span><span class="sxs-lookup"><span data-stu-id="90590-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="90590-183">你将能够输入电影、 编辑它们，并将其列。</span><span class="sxs-lookup"><span data-stu-id="90590-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="90590-184">以下是几个你将创建此教程集中的页。</span><span class="sxs-lookup"><span data-stu-id="90590-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="90590-185">第一个显示影片列出你将创建的页：</span><span class="sxs-lookup"><span data-stu-id="90590-185">The first one shows the movie listing page that you'll create:</span></span>

![创建显示的影片列表完成影片应用程序](getting-started/_static/image1.png)

<span data-ttu-id="90590-187">而且，此处是可将新的影片信息添加到您的网站的页面：</span><span class="sxs-lookup"><span data-stu-id="90590-187">And here's the page that lets you add new movie information to your site:</span></span>

![创建显示将添加影片页完成的影片应用程序](getting-started/_static/image2.png)

<span data-ttu-id="90590-189">后续教程集生成对此设置，并添加更多的功能，如上载图片、 允许登录的人员、 发送电子邮件和与社交媒体集成。</span><span class="sxs-lookup"><span data-stu-id="90590-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="90590-190">请参阅在 Azure 上运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="90590-190">See this App Running on Azure</span></span>

<span data-ttu-id="90590-191">若要查看与实时 web 应用运行的已完成的站点吗？</span><span class="sxs-lookup"><span data-stu-id="90590-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="90590-192">只需单击下面的按钮，可以将应用程序的完整版本部署到你的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="90590-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="90590-193">你需要将此解决方案部署到 Azure 的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="90590-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="90590-194">如果你还没有帐户，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="90590-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="90590-195">[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度来试用付费版 Azure 服务，你可以使用和甚至在用完后，最多可以保留帐户和使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="90590-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="90590-196">[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅为你的信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="90590-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="90590-197">安装的所有内容</span><span class="sxs-lookup"><span data-stu-id="90590-197">Installing Everything</span></span>

<span data-ttu-id="90590-198">你可以通过从 Microsoft Web 平台安装程序安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="90590-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="90590-199">实际上，你安装安装程序，然后使用它来安装其他任何内容。</span><span class="sxs-lookup"><span data-stu-id="90590-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="90590-200">若要使用 Web 页，你必须至少具有 sp3 安装，Windows XP 或 Windows Server 2008 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="90590-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="90590-201">上[网页页](../../../index.md)ASP.NET 网站中，单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="90590-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET Web 站点显示&quot;安装 WebMatrix&quot;按钮](getting-started/_static/image3.png)

<span data-ttu-id="90590-203">系统会要求你接受许可条款和隐私声明，然后安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="90590-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![接受条款以开始安装](getting-started/_static/image4.png)

<span data-ttu-id="90590-205">单击**运行**开始安装。</span><span class="sxs-lookup"><span data-stu-id="90590-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="90590-206">(如果你想要保存安装程序，请单击**保存**，然后从保存位置的文件夹运行安装程序。)</span><span class="sxs-lookup"><span data-stu-id="90590-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="90590-207">Web 平台安装程序中出现，请准备好安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="90590-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="90590-208">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="90590-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="90590-209">安装过程指出它已在你的计算机上安装并启动该过程。</span><span class="sxs-lookup"><span data-stu-id="90590-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="90590-210">具体取决于完全什么已安装，过程可能需要任何位置从几分钟到几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="90590-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="90590-211">选择**我接受**以接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="90590-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="90590-212">Hello WebMatrix</span><span class="sxs-lookup"><span data-stu-id="90590-212">Hello, WebMatrix</span></span>

<span data-ttu-id="90590-213">完成后，安装过程可以自动启动 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="90590-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="90590-214">如果它不存在，在 Windows 中，从**启动**菜单，启动**Microsoft WebMatrix**。</span><span class="sxs-lookup"><span data-stu-id="90590-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="90590-215">首次启动 WebMatrix，你可以在有机会使用你的 Microsoft 帐户登录到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="90590-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="90590-216">登录，你将收到 10 个免费的 web 应用的整个 Azure。</span><span class="sxs-lookup"><span data-stu-id="90590-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="90590-217">这些免费的 web 应用程序提供一种简便方式测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="90590-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="90590-218">如果你还没有 Azure 帐户，但你有 MSDN 订阅，你可以[激活 MSDN 订阅权益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="90590-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="90590-219">否则，可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="90590-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="90590-220">有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="90590-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="90590-221">无需立即登录以继续本教程。</span><span class="sxs-lookup"><span data-stu-id="90590-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="90590-222">如果你执行不登录现在，你仍将进行更高版本登录的选项。</span><span class="sxs-lookup"><span data-stu-id="90590-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="90590-223">最后一个[主题](publishing.md)系列在本教程介绍如何将你的网站部署到 Azure; 因此，你将需要登录以完成该主题。</span><span class="sxs-lookup"><span data-stu-id="90590-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="90590-224">此时，请登录你的 Microsoft 帐户或选择**现在不**右下角中。</span><span class="sxs-lookup"><span data-stu-id="90590-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![登录](getting-started/_static/image7.png)

<span data-ttu-id="90590-226">若要开始，将创建空网站，并添加页。</span><span class="sxs-lookup"><span data-stu-id="90590-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="90590-227">在这一组后面的教程中你将播放的某个内置网站模板。</span><span class="sxs-lookup"><span data-stu-id="90590-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="90590-228">在开始窗口中，单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="90590-228">In the start window, click **New**.</span></span>

![WebMatrix 启动屏幕](getting-started/_static/image8.png)

<span data-ttu-id="90590-230">模板是网站的预构建的文件和不同类型的页。</span><span class="sxs-lookup"><span data-stu-id="90590-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="90590-231">若要查看所有默认为可用的模板，请选择模板库选项。</span><span class="sxs-lookup"><span data-stu-id="90590-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![选择模板库](getting-started/_static/image9.png)

<span data-ttu-id="90590-233">在**快速启动**窗口中，选择**空网站**从**ASP.NET**组并命名新站点"WebPagesMovies"。</span><span class="sxs-lookup"><span data-stu-id="90590-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![WebMatrix 快速启动窗口中与选择的空网站模板](getting-started/_static/image10.png)

<span data-ttu-id="90590-235">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="90590-235">Click **Next**.</span></span>

<span data-ttu-id="90590-236">如果你已登录到你的 Microsoft 帐户，你将有机会在 Azure 上创建站点。</span><span class="sxs-lookup"><span data-stu-id="90590-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="90590-237">根据你的站点的默认名称的名称**WebPagesMovies.azurewebsites.net**建议; 但是，感叹号指示此名称不是 Windows Azure 上提供。</span><span class="sxs-lookup"><span data-stu-id="90590-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="90590-238">为简单起见，选择**跳过**跳过立即在 Azure 上创建网站。</span><span class="sxs-lookup"><span data-stu-id="90590-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="90590-239">稍后在此系列中，我们将站点发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="90590-239">Later in this series, we will publish the site to Azure.</span></span>

![创建 azure 网站](getting-started/_static/image11.png)

<span data-ttu-id="90590-241">WebMatrix 创建和打开站点：</span><span class="sxs-lookup"><span data-stu-id="90590-241">WebMatrix creates and opens the site:</span></span>

![在 WebMatrix 中打开新 WebPagesMovies 站点](getting-started/_static/image12.png)

<span data-ttu-id="90590-243">在顶部，有了快速访问工具栏和功能区。</span><span class="sxs-lookup"><span data-stu-id="90590-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="90590-244">在左下角，你看到工作区中选择器其中切换任务 (**站点**，**文件**，**数据库**，**报表**)。</span><span class="sxs-lookup"><span data-stu-id="90590-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="90590-245">在右侧是内容窗格中，为编辑器和报表。</span><span class="sxs-lookup"><span data-stu-id="90590-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="90590-246">和跨底部有时您会看到消息通知栏。</span><span class="sxs-lookup"><span data-stu-id="90590-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="90590-247">你将了解有关 WebMatrix 和其功能在学习这些教程。</span><span class="sxs-lookup"><span data-stu-id="90590-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="90590-248">创建 Web 页</span><span class="sxs-lookup"><span data-stu-id="90590-248">Creating a Web Page</span></span>

<span data-ttu-id="90590-249">要熟悉 WebMatrix 和 ASP.NET 网页，你将创建一个简单的页面。</span><span class="sxs-lookup"><span data-stu-id="90590-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="90590-250">在工作区中选择器中，选择**文件**工作区。</span><span class="sxs-lookup"><span data-stu-id="90590-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="90590-251">此工作区，可以使用文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="90590-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="90590-252">左窗格中显示你的站点的文件结构。</span><span class="sxs-lookup"><span data-stu-id="90590-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="90590-253">功能区更改为显示与文件相关的任务。</span><span class="sxs-lookup"><span data-stu-id="90590-253">The ribbon changes to show file-related tasks.</span></span>

![在 WebMatrix 的文件工作区](getting-started/_static/image13.png)

<span data-ttu-id="90590-255">在功能区中，单击下的箭头**新建**，然后单击**新文件**。</span><span class="sxs-lookup"><span data-stu-id="90590-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![使用&quot;新建&quot;命令在功能区中创建新的文件](getting-started/_static/image14.png)

<span data-ttu-id="90590-257">WebMatrix 显示的文件类型的列表。</span><span class="sxs-lookup"><span data-stu-id="90590-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="90590-258">选择**CSHTML**，然后在**名称**框中，键入"HelloWorld"。</span><span class="sxs-lookup"><span data-stu-id="90590-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="90590-259">CSHTML 页是一个 ASP.NET Web Pages 页。</span><span class="sxs-lookup"><span data-stu-id="90590-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![创建一个新的 CSHTML 页命名 HelloWorld.cshtml](getting-started/_static/image15.png)

<span data-ttu-id="90590-261">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="90590-261">Click **OK**.</span></span>

<span data-ttu-id="90590-262">WebMatrix 创建页面，并在编辑器中打开它。</span><span class="sxs-lookup"><span data-stu-id="90590-262">WebMatrix creates the page and opens it in the editor.</span></span>

![在 WebMatrix 编辑器中新的 HelloWorld 页](getting-started/_static/image16.png)

<span data-ttu-id="90590-264">如你所见，页面将包含主要普通 HTML 标记中的，如下所示顶部块除外：</span><span class="sxs-lookup"><span data-stu-id="90590-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="90590-265">添加代码，如很快就会看到的。</span><span class="sxs-lookup"><span data-stu-id="90590-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="90590-266">请注意，页面的不同部分&mdash;元素名称、 属性和文本，以及顶部块 — 所有正在不同的颜色。</span><span class="sxs-lookup"><span data-stu-id="90590-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="90590-267">这称为*语法突出显示*，并可更轻松地将清除所有内容保持。</span><span class="sxs-lookup"><span data-stu-id="90590-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="90590-268">它是可以轻松地处理在 WebMatrix 的 web 页面的功能之一。</span><span class="sxs-lookup"><span data-stu-id="90590-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="90590-269">添加的内容`<head>`和`<body>`在下面的示例之类的元素。</span><span class="sxs-lookup"><span data-stu-id="90590-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="90590-270">（如果你想，你可以只需复制下面的块然后使用以下代码替换整个现有页面。）</span><span class="sxs-lookup"><span data-stu-id="90590-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="90590-271">在快速访问工具栏或在**文件**菜单上，单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="90590-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![在 WebMatrix 快速访问工具栏保存按钮](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="90590-273">测试的页</span><span class="sxs-lookup"><span data-stu-id="90590-273">Testing the Page</span></span>

<span data-ttu-id="90590-274">在**文件**工作区中，右键单击*HelloWorld.cshtml*页，然后单击**在浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="90590-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![运行页面 WebMatrix 功能区中使用运行按钮](getting-started/_static/image18.png)

<span data-ttu-id="90590-276">WebMatrix 启动可用于测试你的计算机上的页面的内置 web 服务器 (IIS Express)。</span><span class="sxs-lookup"><span data-stu-id="90590-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="90590-277">（而无需 IIS Express 在 WebMatrix 中，你将必须发布页的 web 服务器到某个位置之前无法对其进行测试。）在默认浏览器中将显示的页。</span><span class="sxs-lookup"><span data-stu-id="90590-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;Hello World&quot;页在浏览器中运行](getting-started/_static/image19.png)

<span data-ttu-id="90590-279">请注意，当你在 WebMatrix 中测试页面，浏览器中的 URL 是类似`http://localhost:33651/HelloWorld.cshtml.`名称*localhost*指的是本地服务器，这意味着，通过在你自己的计算机上的 web 服务器提供的页面。</span><span class="sxs-lookup"><span data-stu-id="90590-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="90590-280">如前所述，WebMatrix 将包含名为 IIS Express 启动页时运行的 web 服务器程序。</span><span class="sxs-lookup"><span data-stu-id="90590-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="90590-281">之后的数字*localhost* (例如， *localhost:33651*) 是指*端口号*你计算机上。</span><span class="sxs-lookup"><span data-stu-id="90590-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="90590-282">这是 IIS Express 用于此特定网站的"通道"的数目。</span><span class="sxs-lookup"><span data-stu-id="90590-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="90590-283">当你创建你的站点，并为你创建的每个站点不同，端口号是从范围 1024 到 65536 随机进行选择。</span><span class="sxs-lookup"><span data-stu-id="90590-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="90590-284">（测试自己的网站时，端口号几乎可以肯定将不同数量比 33561。）通过为每个网站使用不同的端口，IIS Express 可以保留直这你对通信的站点。</span><span class="sxs-lookup"><span data-stu-id="90590-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="90590-285">在发布你的站点到一个公共 web 服务器，不会再看到时，更高版本*localhost*在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="90590-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="90590-286">此时，你将看到更为典型的 URL，如`http://myhostingsite/mywebsite/HelloWorld.cshtml`或任何页。</span><span class="sxs-lookup"><span data-stu-id="90590-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="90590-287">你将了解有关稍后在本教程系列中发布站点的详细信息。</span><span class="sxs-lookup"><span data-stu-id="90590-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="90590-288">添加一些服务器端代码</span><span class="sxs-lookup"><span data-stu-id="90590-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="90590-289">关闭浏览器，然后返回到 WebMatrix 中的页。</span><span class="sxs-lookup"><span data-stu-id="90590-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="90590-290">将行添加到代码块，以便其类似下列代码所示：</span><span class="sxs-lookup"><span data-stu-id="90590-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="90590-291">这是很少的 Razor 代码。</span><span class="sxs-lookup"><span data-stu-id="90590-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="90590-292">获取当前日期和时间，并将该值转换为可能清楚*变量*名为`currentDateTime`。</span><span class="sxs-lookup"><span data-stu-id="90590-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="90590-293">你将在读取更多有关下一教程中的 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="90590-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="90590-294">在页上，正文中后`<p>Hello World!</p>`元素中，添加以下：</span><span class="sxs-lookup"><span data-stu-id="90590-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="90590-295">此代码获取的值放入`currentDateTime`顶部变量并将它插入到页的标记。</span><span class="sxs-lookup"><span data-stu-id="90590-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="90590-296">`@`字符将标记中页的 ASP.NET 网页代码。</span><span class="sxs-lookup"><span data-stu-id="90590-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="90590-297">运行的页面再次 （WebMatrix 将保存所做的更改为你之前它运行页面）。</span><span class="sxs-lookup"><span data-stu-id="90590-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="90590-298">此时会显示的日期和时间在页中。</span><span class="sxs-lookup"><span data-stu-id="90590-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World&quot;页具有动态生成的时间显示浏览器中运行](getting-started/_static/image20.png)

<span data-ttu-id="90590-300">请稍等片刻，然后刷新浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="90590-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="90590-301">日期和时间显示会更新。</span><span class="sxs-lookup"><span data-stu-id="90590-301">The date and time display is updated.</span></span>

<span data-ttu-id="90590-302">在浏览器中，查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="90590-302">In the browser, look at the page source.</span></span> <span data-ttu-id="90590-303">它类似于以下标记：</span><span class="sxs-lookup"><span data-stu-id="90590-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="90590-304">请注意，`@{ }`顶部块不存在。</span><span class="sxs-lookup"><span data-stu-id="90590-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="90590-305">另请注意，日期和时间屏幕将显示实际字符串的字符 (`1/18/2012 2:49:50 PM`或任何)，而不`@currentDateTime`像中有 *.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="90590-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="90590-306">发生了什么情况下面是运行时页上，ASP.NET 将处理所有的代码 （几乎在此情况下），标记有`@`。</span><span class="sxs-lookup"><span data-stu-id="90590-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="90590-307">此代码生成输出，然后该输出已插入到页。</span><span class="sxs-lookup"><span data-stu-id="90590-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="90590-308">这是 ASP.NET Web 页即将</span><span class="sxs-lookup"><span data-stu-id="90590-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="90590-309">当你读取的 ASP.NET Web Pages 生成动态 web 内容时，你已了解是主意。</span><span class="sxs-lookup"><span data-stu-id="90590-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="90590-310">你刚刚创建的页面包含如上所示的相同的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="90590-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="90590-311">它还可以包含可以执行各种任务的代码。</span><span class="sxs-lookup"><span data-stu-id="90590-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="90590-312">在此示例中，它未获取当前日期和时间的重要任务。</span><span class="sxs-lookup"><span data-stu-id="90590-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="90590-313">如你所看到的你可以使用 HTML 中以生成在页中的输出点缀代码。</span><span class="sxs-lookup"><span data-stu-id="90590-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="90590-314">当有人请求 *.cshtml*中浏览器中，ASP.NET 页处理页，同时仍在手中的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="90590-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="90590-315">ASP.NET 将插入代码的输出 （如果有） 到页以 HTML 的形式。</span><span class="sxs-lookup"><span data-stu-id="90590-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="90590-316">完成的代码处理后，ASP.NET 将发送到浏览器所生成的页面。</span><span class="sxs-lookup"><span data-stu-id="90590-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="90590-317">所有浏览器曾获取为 HTML。</span><span class="sxs-lookup"><span data-stu-id="90590-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="90590-318">下面是一个关系图：</span><span class="sxs-lookup"><span data-stu-id="90590-318">Here's a diagram:</span></span>

![如何 ASP.NET 动态生成 HTML 时的概念流](getting-started/_static/image21.png)

<span data-ttu-id="90590-320">其原理很简单，但有许多有趣的任务的代码可以执行，并且有在其中你可以动态 HTML 内容添加到页面的多种有趣方法。</span><span class="sxs-lookup"><span data-stu-id="90590-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="90590-321">和 ASP.NET *.cshtml*页面，例如从任何 HTML 页中，还可以包括在浏览器本身 （JavaScript 和 jQuery 代码） 中运行的代码。</span><span class="sxs-lookup"><span data-stu-id="90590-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="90590-322">您将了解所有这些操作在此教程集和后续条件。</span><span class="sxs-lookup"><span data-stu-id="90590-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="90590-323">接下来</span><span class="sxs-lookup"><span data-stu-id="90590-323">Coming Up Next</span></span>

<span data-ttu-id="90590-324">在本系列中下一步教程中，您了解 ASP.NET Web Pages 稍微编程。</span><span class="sxs-lookup"><span data-stu-id="90590-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90590-325">其他资源</span><span class="sxs-lookup"><span data-stu-id="90590-325">Additional Resources</span></span>

<span data-ttu-id="90590-326">[从头开始创建 ASP.NET 网站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="90590-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="90590-327">这是一个教程，具体而言，是有关使用 WebMatrix （不是 ASP.NET Web 页）。</span><span class="sxs-lookup"><span data-stu-id="90590-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="90590-328">它将进入稍有一些我们将不在此教程集中涉及的 WebMatrix 的其他功能的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="90590-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="90590-329">下一篇</span><span class="sxs-lookup"><span data-stu-id="90590-329">Next</span></span>](intro-to-web-pages-programming.md)
