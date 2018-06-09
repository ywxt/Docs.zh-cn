---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: 引入的 ASP.NET Web Pages-通过使用 WebMatrix 发布的站点 |Microsoft 文档
author: tfitzmac
description: 本教程是文章中介绍的 ASP.NET Web Pages 和 Microsoft WebMatrix 的教程集最后一部分。 还会讨论如何以发布站点 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 7b9bffac5cc72e1bea3f1b211cc03be2ccb8e499
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "30899585"
---
<a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="69a1e-104">引入了 ASP.NET Web 页-通过使用 WebMatrix 发布站点</span><span class="sxs-lookup"><span data-stu-id="69a1e-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>
====================
<span data-ttu-id="69a1e-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="69a1e-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="69a1e-106">本教程是文章中介绍的 ASP.NET Web Pages 和 Microsoft WebMatrix 的教程集最后一部分。</span><span class="sxs-lookup"><span data-stu-id="69a1e-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="69a1e-107">它讨论如何将你的站点发布到 Internet，以便其他人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="69a1e-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="69a1e-108">它假定你已完成通过系列[为 ASP.NET 网页站点创建一致的查看](https://go.microsoft.com/fwlink/?LinkId=251585)。</span><span class="sxs-lookup"><span data-stu-id="69a1e-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="69a1e-109">你将了解如何以发布你的站点使用：</span><span class="sxs-lookup"><span data-stu-id="69a1e-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="69a1e-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="69a1e-110">Microsoft Azure</span></span>
> - <span data-ttu-id="69a1e-111">Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="69a1e-111">Web Hosting Company</span></span>


## <a name="about-publishing-your-site"></a><span data-ttu-id="69a1e-112">有关发布你的站点</span><span class="sxs-lookup"><span data-stu-id="69a1e-112">About Publishing Your Site</span></span>

<span data-ttu-id="69a1e-113">到目前为止，则你已完成你的本地计算机上，包括测试页面的所有工作。</span><span class="sxs-lookup"><span data-stu-id="69a1e-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="69a1e-114">若要运行你<em>.cshtml</em>页，你已使用内置到 WebMatrix 中，即 IIS Express web 服务器。</span><span class="sxs-lookup"><span data-stu-id="69a1e-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="69a1e-115">但这是当然没有人可以看到已创建不同的站点。</span><span class="sxs-lookup"><span data-stu-id="69a1e-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="69a1e-116">若要让其他人使用你的站点，你必须将其发布到 Internet。</span><span class="sxs-lookup"><span data-stu-id="69a1e-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="69a1e-117">除非你已具有对公共 web 服务器的访问，发布意味着你必须有一个用于帐户*云平台*或*托管提供商*。</span><span class="sxs-lookup"><span data-stu-id="69a1e-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="69a1e-118">云平台，如 Microsoft Azure 为你的应用程序提供按需基础结构。</span><span class="sxs-lookup"><span data-stu-id="69a1e-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="69a1e-119">托管提供程序是的公司拥有可公开访问的 web 服务器和，将出租你空间为您的网站。</span><span class="sxs-lookup"><span data-stu-id="69a1e-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="69a1e-120">托管计划运行从每月只需几美元 （或甚至免费） 对于小型网站到数以百计的大量商业网站的每月的资金。</span><span class="sxs-lookup"><span data-stu-id="69a1e-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="69a1e-121">你可能有权通过 internet 服务提供商 (ISP) 用于获取在家里 internet 服务的公共 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="69a1e-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="69a1e-122">但是，你托管提供商必须支持 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="69a1e-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="69a1e-123">许多 Isp 不这样做，但最好始终检查。</span><span class="sxs-lookup"><span data-stu-id="69a1e-123">Many ISPs don't, but it's always worth checking.</span></span>


<span data-ttu-id="69a1e-124">在本教程中，我们将向你提供如何将发布的概述。</span><span class="sxs-lookup"><span data-stu-id="69a1e-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="69a1e-125">因为流程有点不同于每个宿主提供程序，则它是不可行涵盖所有情况，提供准确的详细信息。</span><span class="sxs-lookup"><span data-stu-id="69a1e-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="69a1e-126">但，你将获取进程的工作原理的一个好主意。</span><span class="sxs-lookup"><span data-stu-id="69a1e-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="69a1e-127">本教程包含四个部分：</span><span class="sxs-lookup"><span data-stu-id="69a1e-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="69a1e-128">设置默认页</span><span class="sxs-lookup"><span data-stu-id="69a1e-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="69a1e-129">发布 （选择以下项之一）</span><span class="sxs-lookup"><span data-stu-id="69a1e-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="69a1e-130">a.</span><span class="sxs-lookup"><span data-stu-id="69a1e-130">a.</span></span> [<span data-ttu-id="69a1e-131">你的站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="69a1e-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="69a1e-132">b.</span><span class="sxs-lookup"><span data-stu-id="69a1e-132">b.</span></span> [<span data-ttu-id="69a1e-133">将你的站点发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="69a1e-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="69a1e-134">更新实时站点： 重新发布</span><span class="sxs-lookup"><span data-stu-id="69a1e-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="69a1e-135">设置默认页</span><span class="sxs-lookup"><span data-stu-id="69a1e-135">Setting up the default page</span></span>

<span data-ttu-id="69a1e-136">当用户导航到您的网站的基址时，向用户显示你的站点的默认页面。</span><span class="sxs-lookup"><span data-stu-id="69a1e-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="69a1e-137">例如，如果在 www.contoso.com 情况下，Default.htm 设为该站点的默认页，然后导航到<strong>www.contoso.com</strong>等同于导航到<strong>www.contoso.com/Default.htm</strong>。</span><span class="sxs-lookup"><span data-stu-id="69a1e-137">For example, when Default.htm is set as the default page for the site at www.contoso.com, then navigating to <strong>www.contoso.com</strong> is the same as navigating to <strong>www.contoso.com/Default.htm</strong>.</span></span>

<span data-ttu-id="69a1e-138">目前，您的网站使用**Default.cshtml**作为默认页。</span><span class="sxs-lookup"><span data-stu-id="69a1e-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="69a1e-139">此页是相当不错的默认页，但在本教程中你未添加任何内容到该页面以便它将显示一个空白页。</span><span class="sxs-lookup"><span data-stu-id="69a1e-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="69a1e-140">打开 Default.cshtml 并将内容替换为下面的代码。</span><span class="sxs-lookup"><span data-stu-id="69a1e-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="69a1e-141">现在你的站点是准备好进行发布。</span><span class="sxs-lookup"><span data-stu-id="69a1e-141">Now your site is ready for publication.</span></span> <span data-ttu-id="69a1e-142">首先，你将看到如何将站点部署到 Azure，然后如何将其部署到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="69a1e-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="69a1e-143">任一选项适用于您的网站，并且你只需遵循的部署选项之一。</span><span class="sxs-lookup"><span data-stu-id="69a1e-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="69a1e-144">你的站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="69a1e-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="69a1e-145">本教程将首先显示您如何将您的网站部署到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="69a1e-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="69a1e-146">通过使用 Microsoft 帐户登录，你可以在 Azure 上创建最多 10 个免费站点。</span><span class="sxs-lookup"><span data-stu-id="69a1e-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="69a1e-147">这些免费站点提供一种简便方式测试你的站点。</span><span class="sxs-lookup"><span data-stu-id="69a1e-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="69a1e-148">你始终可以删除此站点示例更高版本以避免使用所有可用站点。</span><span class="sxs-lookup"><span data-stu-id="69a1e-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="69a1e-149">可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="69a1e-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="69a1e-150">有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="69a1e-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="69a1e-151">在 WebMatrix 功能区中，单击**发布**按钮。</span><span class="sxs-lookup"><span data-stu-id="69a1e-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 功能区中的发布按钮](publishing/_static/image1.png)

<span data-ttu-id="69a1e-153">**发布您网站**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="69a1e-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="69a1e-154">如果你不具有到你的 Microsoft 帐户身份登录的则此对话框将包含**开始使用 Azure**链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="69a1e-155">单击此链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-155">Click this link.</span></span>

![发布你的站点](publishing/_static/image2.png)

<span data-ttu-id="69a1e-157">如果你不具有到 Microsoft 帐户身份登录的则您再次有机会登录。</span><span class="sxs-lookup"><span data-stu-id="69a1e-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="69a1e-158">你必须登录到 Microsoft 帐户来发布站点在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="69a1e-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![登录](publishing/_static/image3.png)

<span data-ttu-id="69a1e-160">在登录到你的 Microsoft 帐户后, 对话框包含指向在 Azure 上创建新站点或连接到你在 Azure 上的现有站点之一的链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![创建新站点](publishing/_static/image4.png)

<span data-ttu-id="69a1e-162">选择**创建新站点**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-162">Select **Create a new site**.</span></span>

<span data-ttu-id="69a1e-163">如果名为你的项目**WebPagesMovies**，你的站点的默认名称将为**webpagesmovies.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="69a1e-164">此默认名称是最有可能不可用，由红色感叹号。</span><span class="sxs-lookup"><span data-stu-id="69a1e-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![默认网站名称](publishing/_static/image5.png)

<span data-ttu-id="69a1e-166">将站点名称更改为可可用，并选择靠近你所在位置的位置。</span><span class="sxs-lookup"><span data-stu-id="69a1e-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![更改的站点名称](publishing/_static/image6.png)

<span data-ttu-id="69a1e-168">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-168">Click **OK**.</span></span>

<span data-ttu-id="69a1e-169">WebMatrix performss 测试，确定是否符合你的站点服务器。</span><span class="sxs-lookup"><span data-stu-id="69a1e-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![兼容性测试](publishing/_static/image7.png)

<span data-ttu-id="69a1e-171">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-171">Select **Continue**.</span></span>

<span data-ttu-id="69a1e-172">显示兼容性测试的结果。</span><span class="sxs-lookup"><span data-stu-id="69a1e-172">The results of the compatibility test are displayed.</span></span>

![兼容性结果](publishing/_static/image8.png)

<span data-ttu-id="69a1e-174">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-174">Select **Continue**.</span></span>

<span data-ttu-id="69a1e-175">WebMatrix 显示的文件和将发布到站点的数据库。</span><span class="sxs-lookup"><span data-stu-id="69a1e-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="69a1e-176">由于这是你要将站点发布的第一个时间，所有文件均已列出。</span><span class="sxs-lookup"><span data-stu-id="69a1e-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="69a1e-177">你可以取消选中未准备好发布的文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="69a1e-178">在后续的发布中，将显示仅将已更改的文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="69a1e-179">请参阅[更新实时站点： 重新发布](#update)。</span><span class="sxs-lookup"><span data-stu-id="69a1e-179">See [Updating the Live Site: Republishing](#update).</span></span>

![发布预览](publishing/_static/image9.png)

<span data-ttu-id="69a1e-181">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-181">Select **Continue**.</span></span>

<span data-ttu-id="69a1e-182">站点部署到 Azure 后，将会显示一条消息，指示部署已完成。</span><span class="sxs-lookup"><span data-stu-id="69a1e-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![发布完成](publishing/_static/image10.png)

<span data-ttu-id="69a1e-184">你的站点和数据库已发布到 Azure，和现在向公众提供。</span><span class="sxs-lookup"><span data-stu-id="69a1e-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="69a1e-185">单击消息，指示发布完成后，并且现在，你将看到你已部署的站点中的链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="69a1e-186">也可以访问 Internet 的任何人都可以添加或修改数据库中的记录。</span><span class="sxs-lookup"><span data-stu-id="69a1e-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="69a1e-187">将你的站点发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="69a1e-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="69a1e-188">如果你决定不将发布到 Azure，你可以改为将站点发布到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="69a1e-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="69a1e-189">单击**查找 web 托管**链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-189">Click the **Find web hosting** link.</span></span>

![在发布设置对话框中的查找 web 宿主按钮](publishing/_static/image12.png)

<span data-ttu-id="69a1e-191">你转到页列出了宿主提供程序支持 ASP.NET 的 Microsoft 站点上。</span><span class="sxs-lookup"><span data-stu-id="69a1e-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![列出托管提供商的 Microsoft 站点上的页](publishing/_static/image13.png)

<span data-ttu-id="69a1e-193">显然，它可能很难知道现在完全长远来看可能需要哪些宿主功能。</span><span class="sxs-lookup"><span data-stu-id="69a1e-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="69a1e-194">下面是几个需要考虑的事项：</span><span class="sxs-lookup"><span data-stu-id="69a1e-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="69a1e-195">对于 WebPagesMovies 站点，你无需具有单独的外接程序对于 SQL Server，通常的额外成本。</span><span class="sxs-lookup"><span data-stu-id="69a1e-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="69a1e-196">在你站点中，你正在使用 SQL Server Compact Edition，这自包含。</span><span class="sxs-lookup"><span data-stu-id="69a1e-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="69a1e-197">但是，你可能需要为你执行一些将来网站工作的 SQL Server 访问。</span><span class="sxs-lookup"><span data-stu-id="69a1e-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="69a1e-198">如果你认为你可能会请确保您可以稍后添加 SQL Server 功能。</span><span class="sxs-lookup"><span data-stu-id="69a1e-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="69a1e-199">检查宿主提供程序是否支持 Web 部署发布协议。</span><span class="sxs-lookup"><span data-stu-id="69a1e-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="69a1e-200">可以通过使用 FTP 协议，发布，但更方便地使用 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="69a1e-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="69a1e-201">某些站点还会提供免费试用期。</span><span class="sxs-lookup"><span data-stu-id="69a1e-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="69a1e-202">免费试用版是一种好的方法尝试发布和承载时你正在仍试验 WebMatrix 和 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="69a1e-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="69a1e-203">选择你喜欢的其中一个。</span><span class="sxs-lookup"><span data-stu-id="69a1e-203">Pick one that you like.</span></span> <span data-ttu-id="69a1e-204">对于本教程中，我们选择 DiscountASP.NET，因为我们已创建本教程，该公司还有使用户可以拥有一个对几个月免费站点的站点升级。</span><span class="sxs-lookup"><span data-stu-id="69a1e-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="69a1e-205">我们选择的用于本教程的宿主提供程序不应被视为认可该公司通过任何其他。</span><span class="sxs-lookup"><span data-stu-id="69a1e-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="69a1e-206">但我们不得不选取一个图中，而 DiscountASP.NET 是一个支持 ASP.NET 网页和 Web 部署协议用于发布的很多公司。</span><span class="sxs-lookup"><span data-stu-id="69a1e-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>


<span data-ttu-id="69a1e-207">通常情况下，使用托管提供商注册完后，公司向你发送包含用户名和密码，为 web 服务器上，依次类推 URL 的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="69a1e-208">如果托管公司支持 Web 部署协议，他们可能发送你的文件，包含发布设置，或允许你在下载一个。</span><span class="sxs-lookup"><span data-stu-id="69a1e-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="69a1e-209">发布设置文件简化了为你的过程。</span><span class="sxs-lookup"><span data-stu-id="69a1e-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="69a1e-210">已注册并已准备好发布，请单击**发布**WebMatrix 功能区中的按钮。</span><span class="sxs-lookup"><span data-stu-id="69a1e-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="69a1e-211">**发布设置**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="69a1e-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="69a1e-212">如果托管提供商发送一个发布设置文件，单击**导入发布设置**链接和导入文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="69a1e-213">如果你没有发布设置文件，填写字段使用托管公司向你发送电子邮件中的值。</span><span class="sxs-lookup"><span data-stu-id="69a1e-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="69a1e-214">下面是什么**发布设置**对话框可能如下所示完成后：</span><span class="sxs-lookup"><span data-stu-id="69a1e-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![在发布设置对话框中填写发布设置](publishing/_static/image14.png)

<span data-ttu-id="69a1e-216">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-216">Click **Validate Connection**.</span></span> <span data-ttu-id="69a1e-217">如果所有内容是确定，对话框中报告**已成功连接**，这意味着它可以与托管提供商的服务器通信。</span><span class="sxs-lookup"><span data-stu-id="69a1e-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![成功消息如果发布设置正确无误](publishing/_static/image15.png)

<span data-ttu-id="69a1e-219">如果没有问题，WebMatrix 将会尽全力告诉你的问题是：</span><span class="sxs-lookup"><span data-stu-id="69a1e-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![如果没有问题的错误消息发布设置](publishing/_static/image16.png)

<span data-ttu-id="69a1e-221">单击**保存**以保存设置。</span><span class="sxs-lookup"><span data-stu-id="69a1e-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="69a1e-222">WebMatrix 提供执行测试以确保，它可以正确与宿主站点通信：</span><span class="sxs-lookup"><span data-stu-id="69a1e-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![产品以执行发布过程的测试的消息](publishing/_static/image17.png)

<span data-ttu-id="69a1e-224">单击 **“是”**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-224">Click **Yes**.</span></span> <span data-ttu-id="69a1e-225">WebMatrix 将某些示例文件上载到托管提供商。</span><span class="sxs-lookup"><span data-stu-id="69a1e-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="69a1e-226">如果兼容性测试已完成，WebMatrix 报告的结果：</span><span class="sxs-lookup"><span data-stu-id="69a1e-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![发布测试结果](publishing/_static/image18.png)

<span data-ttu-id="69a1e-228">如果你已准备就绪，请继续并单击**继续**有关实际启动发布过程。</span><span class="sxs-lookup"><span data-stu-id="69a1e-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="69a1e-229">WebMatrix 计算出什么文件位于你的站点和包已在主机服务器 （现在，无） 上以及为你提供的发布过程预览：</span><span class="sxs-lookup"><span data-stu-id="69a1e-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![发布过程将上载文件的预览](publishing/_static/image19.png)

<span data-ttu-id="69a1e-231">要发布的文件列表包括已创建类似的 web 页*Movies.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="69a1e-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="69a1e-232">列表还包括有关帮助程序，您已安装，为您的数据库，运行 SQL Server Compact Edition 等的文件的文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="69a1e-233">因此，初始发布过程会很大。</span><span class="sxs-lookup"><span data-stu-id="69a1e-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="69a1e-234">单击 **“继续”**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-234">Click **Continue**.</span></span> <span data-ttu-id="69a1e-235">WebMatrix 将你的文件复制到托管提供商的服务器。</span><span class="sxs-lookup"><span data-stu-id="69a1e-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="69a1e-236">完成后，状态栏中报告结果：</span><span class="sxs-lookup"><span data-stu-id="69a1e-236">When it's done, the results are reported in the status bar:</span></span>

![状态栏消息发布过程成功完成](publishing/_static/image20.png)

<span data-ttu-id="69a1e-238">若要查看你的实时网站，单击状态栏中的链接。</span><span class="sxs-lookup"><span data-stu-id="69a1e-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="69a1e-239">添加*电影*到 URL，并且您将看到*Movies.cshtml*你创建的文件：</span><span class="sxs-lookup"><span data-stu-id="69a1e-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![显示电影页实时站点](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="69a1e-241">更新实时站点： 重新发布</span><span class="sxs-lookup"><span data-stu-id="69a1e-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="69a1e-242">一旦你已将站点发布 （到 Azure 或 web 托管公司） 中，有两份&mdash;上您的计算机和服务提供商上的版本的版本。</span><span class="sxs-lookup"><span data-stu-id="69a1e-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="69a1e-243">你可能需要在继续开发站点 (如果没有任何其他，作为下一步教程集的一部分)。</span><span class="sxs-lookup"><span data-stu-id="69a1e-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="69a1e-244">执行操作时，你必须重新发布你的站点，以将更改从您的计算机复制到服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="69a1e-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="69a1e-245">在 WebMatrix 中发布过程可以确定在你的站点上，文件已更改内容并发布仅对这些文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="69a1e-246">若要查看重新发布的工作原理，请打开*Movies.cshtml*站点，进行一些小更改，然后保存该文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="69a1e-247">例如，将标题更改为`Movies - Updated`。</span><span class="sxs-lookup"><span data-stu-id="69a1e-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="69a1e-248">单击**发布**中功能区按钮。</span><span class="sxs-lookup"><span data-stu-id="69a1e-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="69a1e-249">WebMatrix 确定更改的内容，并将发布的文件的位置处显示。</span><span class="sxs-lookup"><span data-stu-id="69a1e-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![发布对话框中显示已更改文件可供重新发布](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="69a1e-251">默认情况下，WebMatrix 发布你的数据库 (*.sdf*文件) 仅你发布站点，第一次。</span><span class="sxs-lookup"><span data-stu-id="69a1e-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="69a1e-252">一旦发布你的站点和人员交互与网站，实时站点上的数据库通常具有站点的真实数据。</span><span class="sxs-lookup"><span data-stu-id="69a1e-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="69a1e-253">您必须非常小心，不要覆盖实时数据库与 *.sdf*体现在你的计算机，这通常只包含测试数据的文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="69a1e-254">这就是为什么你看到警告**发布将覆盖任何远程数据库**，为什么的复选框和*WebPagesMovies.sdf*默认未选中状态。</span><span class="sxs-lookup"><span data-stu-id="69a1e-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>


<span data-ttu-id="69a1e-255">单击 **“继续”**。</span><span class="sxs-lookup"><span data-stu-id="69a1e-255">Click **Continue**.</span></span> <span data-ttu-id="69a1e-256">WebMatrix 发布更改的文件，并显示一条成功消息，像你发布的第一个时间。</span><span class="sxs-lookup"><span data-stu-id="69a1e-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="69a1e-257">转到实时网站 （如果它仍显示可以单击成功消息中的链接），并验证已发布所做的更改。</span><span class="sxs-lookup"><span data-stu-id="69a1e-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="69a1e-258">**远程编辑文件**</span><span class="sxs-lookup"><span data-stu-id="69a1e-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="69a1e-259">作为更改你的站点，然后重新发布的替代方法，你可以编辑直接在 WebMatrix 中的远程文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="69a1e-260">在此方案中，打开文件上的服务提供商和 WebMatrix 下载一份它进行编辑。</span><span class="sxs-lookup"><span data-stu-id="69a1e-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="69a1e-261">每次保存该文件，WebMatrix 将所做的更改发送到站点。</span><span class="sxs-lookup"><span data-stu-id="69a1e-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="69a1e-262">远程编辑是对你的实时网站进行更改的简单办法。</span><span class="sxs-lookup"><span data-stu-id="69a1e-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="69a1e-263">但是，这种方式的更改未同步与您的本地站点中的文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="69a1e-264">若要同步的本地文件与远程站点，你可以下载远程文件。</span><span class="sxs-lookup"><span data-stu-id="69a1e-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="69a1e-265">此过程的工作非常类似于发布，除按相反的顺序。</span><span class="sxs-lookup"><span data-stu-id="69a1e-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="69a1e-266">我们不会更描述有关远程编辑和远程下载设施的 WebMatrix 此处。</span><span class="sxs-lookup"><span data-stu-id="69a1e-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="69a1e-267">它们非常有用，如果多个用户需要在不同的计算机上的相同站点上工作。</span><span class="sxs-lookup"><span data-stu-id="69a1e-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="69a1e-268">有关详细信息，请参阅[发布并编辑远程站点使用 WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591)。</span><span class="sxs-lookup"><span data-stu-id="69a1e-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="69a1e-269">其他资源</span><span class="sxs-lookup"><span data-stu-id="69a1e-269">Additional Resources</span></span>

- <span data-ttu-id="69a1e-270">[ASP.NET WebMatrix 的 ASP.NET Web Pages 论坛](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)、 文章的绝佳问题和 get 解答。</span><span class="sxs-lookup"><span data-stu-id="69a1e-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="69a1e-271">上一篇</span><span class="sxs-lookup"><span data-stu-id="69a1e-271">Previous</span></span>](layouts.md)
