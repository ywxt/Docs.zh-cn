---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 跟踪 ASP.NET 网页 (Razor) 站点访问者信息 （分析） |Microsoft 文档
author: tfitzmac
description: 你已收到将你的网站后，你可能想要分析你的网站流量。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 9a381ebaed30325fdfa5f0f558910d3002c61559
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26528756"
---
<a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="5338e-103">跟踪一个 ASP.NET Web 页 (Razor) 站点的访问者信息 （分析）</span><span class="sxs-lookup"><span data-stu-id="5338e-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="5338e-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5338e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5338e-105">本文介绍如何使用程序的帮助程序将网站分析添加到在 ASP.NET Web 页 (Razor) 网站中的页。</span><span class="sxs-lookup"><span data-stu-id="5338e-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="5338e-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="5338e-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="5338e-107">如何将有关你的网站流量的信息发送到的分析提供程序。</span><span class="sxs-lookup"><span data-stu-id="5338e-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="5338e-108">这些是 ASP.NET 编程文章中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="5338e-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="5338e-109">`Analytics`帮助器。</span><span class="sxs-lookup"><span data-stu-id="5338e-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5338e-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5338e-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5338e-111">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="5338e-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5338e-112">ASP.NET Web 帮助程序库 （NuGet 包）</span><span class="sxs-lookup"><span data-stu-id="5338e-112">ASP.NET Web Helpers Library (NuGet package)</span></span>


<span data-ttu-id="5338e-113">分析是用于测量你的网站上的流量，这样你可以了解人们如何使用站点的技术的常用术语。</span><span class="sxs-lookup"><span data-stu-id="5338e-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="5338e-114">许多分析服务都可用，包括从 Google、 Yahoo、 StatCounter，和其他服务。</span><span class="sxs-lookup"><span data-stu-id="5338e-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="5338e-115">工作原理是，你注册的帐户分析提供程序，你在其中注册站点与你的方式分析想要跟踪。提供程序发送 JavaScript 代码，其中包括 ID 或跟踪你的帐户的代码的段。</span><span class="sxs-lookup"><span data-stu-id="5338e-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="5338e-116">将 JavaScript 代码段添加到您想要跟踪的站点上的网页。（你通常分析将段添加到页脚或布局页或其他站点中每一页显示的 HTML 标记。）当用户请求包含这些 JavaScript 代码段之一的页时，代码段会将有关当前页的信息发送到分析提供商联系，记录页有关的各种详细信息。</span><span class="sxs-lookup"><span data-stu-id="5338e-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="5338e-117">如果你想要看一下你站点的统计信息，你将登录到分析提供程序的网站。</span><span class="sxs-lookup"><span data-stu-id="5338e-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="5338e-118">然后，可以查看各种类型的报表有关您的网站，如上：</span><span class="sxs-lookup"><span data-stu-id="5338e-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="5338e-119">各个页的页视图的数。</span><span class="sxs-lookup"><span data-stu-id="5338e-119">The number of page views for individual pages.</span></span> <span data-ttu-id="5338e-120">这将告知你 （大约） 有多少人访问站点，并且在你的站点上的页都是最常见。</span><span class="sxs-lookup"><span data-stu-id="5338e-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="5338e-121">人员花费的时间上的特定页。</span><span class="sxs-lookup"><span data-stu-id="5338e-121">How long people spend on specific pages.</span></span> <span data-ttu-id="5338e-122">这可以告知您的主页上是否保持人的兴趣等。</span><span class="sxs-lookup"><span data-stu-id="5338e-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="5338e-123">哪些站点人已在之前它们访问您的站点。</span><span class="sxs-lookup"><span data-stu-id="5338e-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="5338e-124">这有助于你了解你的流量来自链接，从搜索中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="5338e-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="5338e-125">当用户访问你的网站并它们保持多长时间。</span><span class="sxs-lookup"><span data-stu-id="5338e-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="5338e-126">哪些国家/地区距离访客都是从。</span><span class="sxs-lookup"><span data-stu-id="5338e-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="5338e-127">哪些浏览器和操作系统距离访客使用。</span><span class="sxs-lookup"><span data-stu-id="5338e-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic 1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="5338e-129">使用程序的帮助程序添加到页面的分析</span><span class="sxs-lookup"><span data-stu-id="5338e-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="5338e-130">ASP.NET Web Pages 包括多个分析帮助器 (`Analytics.GetGoogleHtml`， `Analytics.GetYahooHtml`，和`Analytics.GetStatCounterHtml`)，使其更容易地管理用于分析的 JavaScript 代码段。</span><span class="sxs-lookup"><span data-stu-id="5338e-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="5338e-131">而不是了解如何以及在何处将 JavaScript 代码，放入所要做是添加到页面的帮助器。</span><span class="sxs-lookup"><span data-stu-id="5338e-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="5338e-132">你需要提供的唯一信息是帐户名称、 ID 或跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="5338e-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="5338e-133">（有关 StatCounter，还必须提供了几个其他值。）</span><span class="sxs-lookup"><span data-stu-id="5338e-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="5338e-134">在此过程中，你将创建一个使用的布局页`GetGoogleHtml`帮助器。</span><span class="sxs-lookup"><span data-stu-id="5338e-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="5338e-135">如果您已具有包含其他分析提供程序之一的帐户，你可以改为使用该帐户，并根据需要进行细微调整。</span><span class="sxs-lookup"><span data-stu-id="5338e-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="5338e-136">当你创建的分析帐户时，你注册你想要跟踪的站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="5338e-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="5338e-137">如果你正在本地计算机上测试所有内容，不会跟踪 （仅发送的流量是你） 的实际流量，因此将看不到记录和查看站点统计信息。</span><span class="sxs-lookup"><span data-stu-id="5338e-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="5338e-138">但此过程演示如何向页中添加一个分析帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5338e-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="5338e-139">当你发布你的站点时，实时站点会将信息发送给你的分析提供商。</span><span class="sxs-lookup"><span data-stu-id="5338e-139">When you publish your site, the live site will send information to your analytics provider.</span></span>


1. <span data-ttu-id="5338e-140">将 ASP.NET Web 帮助程序库添加到你的网站中所述[安装 ASP.NET 网页站点中的帮助器](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未添加它。</span><span class="sxs-lookup"><span data-stu-id="5338e-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="5338e-141">创建具有 Google Analytics 帐户，并记录帐户名称。</span><span class="sxs-lookup"><span data-stu-id="5338e-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="5338e-142">创建一个名为的布局页*Analytics.cshtml*并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="5338e-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="5338e-143">你必须将放置到调用`Analytics`网页的正文中的帮助器 (之前`</body>`标记)。</span><span class="sxs-lookup"><span data-stu-id="5338e-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="5338e-144">否则，浏览器将不运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="5338e-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="5338e-145">如果你使用不同的分析提供程序，请改为使用以下帮助器之一：</span><span class="sxs-lookup"><span data-stu-id="5338e-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="5338e-146">(Yahoo)`@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="5338e-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="5338e-147">(StatCounter)`@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="5338e-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="5338e-148">替换`myaccount`同名的帐户、 ID 或你在步骤 1 中创建的跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="5338e-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="5338e-149">在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="5338e-149">Run the page in the browser.</span></span> <span data-ttu-id="5338e-150">(请确保页中选择**文件**工作区之前运行它。)</span><span class="sxs-lookup"><span data-stu-id="5338e-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="5338e-151">在浏览器中查看页面源文件。</span><span class="sxs-lookup"><span data-stu-id="5338e-151">In the browser, view the page source.</span></span> <span data-ttu-id="5338e-152">你将能够查看呈现的分析代码：</span><span class="sxs-lookup"><span data-stu-id="5338e-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="5338e-153">登录到 Google Analytics 站点，并检查你的站点的统计信息。</span><span class="sxs-lookup"><span data-stu-id="5338e-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="5338e-154">如果您在实时站点上运行页上，你会看到日志访问页面的项。</span><span class="sxs-lookup"><span data-stu-id="5338e-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5338e-155">其他资源</span><span class="sxs-lookup"><span data-stu-id="5338e-155">Additional Resources</span></span>

- [<span data-ttu-id="5338e-156">Google Analytics 站点</span><span class="sxs-lookup"><span data-stu-id="5338e-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="5338e-157">Yahoo ！网站分析</span><span class="sxs-lookup"><span data-stu-id="5338e-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="5338e-158">StatCounter 站点</span><span class="sxs-lookup"><span data-stu-id="5338e-158">StatCounter site</span></span>](http://statcounter.com/)
