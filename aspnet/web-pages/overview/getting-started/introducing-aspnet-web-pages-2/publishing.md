---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Introducing ASP.NET 网页-通过使用 WebMatrix 发布站点 |Microsoft Docs
author: Rick-Anderson
description: 本教程是在引入了 ASP.NET Web Pages 和 Microsoft WebMatrix 的教程系列中最后一期。 介绍了如何发布站点 t...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: fe196e5db8fd1cecbe84b2eb970939303f9313d1
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021451"
---
<a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="b8642-104">ASP.NET 网页简介-通过使用 WebMatrix 发布站点</span><span class="sxs-lookup"><span data-stu-id="b8642-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>
====================
<span data-ttu-id="b8642-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b8642-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b8642-106">本教程是在引入了 ASP.NET Web Pages 和 Microsoft WebMatrix 的教程系列中最后一期。</span><span class="sxs-lookup"><span data-stu-id="b8642-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="b8642-107">它讨论了如何将您的网站发布到 Internet，以便其他人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="b8642-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="b8642-108">它假定你已完成通过时序[为 ASP.NET Web Pages 站点创建一致的查看](https://go.microsoft.com/fwlink/?LinkId=251585)。</span><span class="sxs-lookup"><span data-stu-id="b8642-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="b8642-109">您将学习如何发布站点使用：</span><span class="sxs-lookup"><span data-stu-id="b8642-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="b8642-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b8642-110">Microsoft Azure</span></span>
> - <span data-ttu-id="b8642-111">Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="b8642-111">Web Hosting Company</span></span>


## <a name="about-publishing-your-site"></a><span data-ttu-id="b8642-112">有关发布站点</span><span class="sxs-lookup"><span data-stu-id="b8642-112">About Publishing Your Site</span></span>

<span data-ttu-id="b8642-113">到目前为止，已完成您的本地计算机上，包括测试您的页面的所有工作。</span><span class="sxs-lookup"><span data-stu-id="b8642-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="b8642-114">若要运行你<em>.cshtml</em>页中，你已使用内置到 WebMatrix 中，即 IIS Express web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b8642-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="b8642-115">但当然没有人可以看到已创建除您的站点。</span><span class="sxs-lookup"><span data-stu-id="b8642-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="b8642-116">若要让其他人使用你的站点，必须将其发布到 Internet。</span><span class="sxs-lookup"><span data-stu-id="b8642-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="b8642-117">除非已有权访问公共 web 服务器，否则发布意味着，必须有一个帐户*云平台*或*托管提供商*。</span><span class="sxs-lookup"><span data-stu-id="b8642-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="b8642-118">Microsoft Azure 等云平台，为应用程序提供按需基础结构。</span><span class="sxs-lookup"><span data-stu-id="b8642-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="b8642-119">宿主提供程序是一家公司拥有可公开访问的 web 服务器和，将通过您租借空间为您的网站。</span><span class="sxs-lookup"><span data-stu-id="b8642-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="b8642-120">托管计划运行从每个月的几个美元 （或甚至免费） 的小型站点添加到由数以百计的一个月，提供大量商业网站几美元。</span><span class="sxs-lookup"><span data-stu-id="b8642-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="b8642-121">可能有权通过 internet 服务提供商 (ISP) 用来获取在家里 internet 服务的公共 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b8642-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="b8642-122">但是，托管提供商必须支持 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="b8642-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="b8642-123">很多 Isp 不这样做，但最好始终检查。</span><span class="sxs-lookup"><span data-stu-id="b8642-123">Many ISPs don't, but it's always worth checking.</span></span>


<span data-ttu-id="b8642-124">在本教程中，我们将提供如何将发布的概述。</span><span class="sxs-lookup"><span data-stu-id="b8642-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="b8642-125">因为过程稍微不同的每个宿主提供程序，它并不可行的所有内容，提供有关确切详细信息。</span><span class="sxs-lookup"><span data-stu-id="b8642-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="b8642-126">但您仍然可以清楚地了解该过程的工作原理。</span><span class="sxs-lookup"><span data-stu-id="b8642-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="b8642-127">本教程包含四个部分：</span><span class="sxs-lookup"><span data-stu-id="b8642-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="b8642-128">设置默认页</span><span class="sxs-lookup"><span data-stu-id="b8642-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="b8642-129">发布 （选择以下值之一）</span><span class="sxs-lookup"><span data-stu-id="b8642-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="b8642-130">a.</span><span class="sxs-lookup"><span data-stu-id="b8642-130">a.</span></span> [<span data-ttu-id="b8642-131">你的站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b8642-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="b8642-132">b.</span><span class="sxs-lookup"><span data-stu-id="b8642-132">b.</span></span> [<span data-ttu-id="b8642-133">将站点发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="b8642-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="b8642-134">更新实时站点： 重新发布</span><span class="sxs-lookup"><span data-stu-id="b8642-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="b8642-135">设置默认页</span><span class="sxs-lookup"><span data-stu-id="b8642-135">Setting up the default page</span></span>

<span data-ttu-id="b8642-136">当用户导航到你的网站的基址时，向用户显示你的站点的默认页。</span><span class="sxs-lookup"><span data-stu-id="b8642-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="b8642-137">例如，当 Default.htm 作为该站点的默认页设置为 www.contoso.com ，然后导航到<strong>www.contoso.com</strong>导航到相同<strong>www.contoso.com/Default.htm</strong>。</span><span class="sxs-lookup"><span data-stu-id="b8642-137">For example, when Default.htm is set as the default page for the site at www.contoso.com, then navigating to <strong>www.contoso.com</strong> is the same as navigating to <strong>www.contoso.com/Default.htm</strong>.</span></span>

<span data-ttu-id="b8642-138">目前，您的网站使用**Default.cshtml**与默认页面。</span><span class="sxs-lookup"><span data-stu-id="b8642-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="b8642-139">此页是相当不错的默认页面，但在本教程中未添加任何内容到该页面以便它将显示空白页。</span><span class="sxs-lookup"><span data-stu-id="b8642-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="b8642-140">打开 Default.cshtml 并将内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="b8642-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="b8642-141">现在你的站点是准备好进行发布。</span><span class="sxs-lookup"><span data-stu-id="b8642-141">Now your site is ready for publication.</span></span> <span data-ttu-id="b8642-142">首先，您将看到如何将站点部署到 Azure，以及如何将其部署到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="b8642-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="b8642-143">任一选项适用于您的网站，并且您只需遵循的部署选项之一。</span><span class="sxs-lookup"><span data-stu-id="b8642-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="b8642-144">你的站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b8642-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="b8642-145">本教程将首先演示如何将您的网站部署到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="b8642-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="b8642-146">通过使用 Microsoft 帐户登录，可以在 Azure 上创建最多 10 个免费网站。</span><span class="sxs-lookup"><span data-stu-id="b8642-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="b8642-147">这些免费站点提供了方便地测试您的站点。</span><span class="sxs-lookup"><span data-stu-id="b8642-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="b8642-148">您始终可以删除此示例站点更高版本以避免使用所有免费站点。</span><span class="sxs-lookup"><span data-stu-id="b8642-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="b8642-149">只需几分钟，可以创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="b8642-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b8642-150">有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="b8642-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="b8642-151">在 WebMatrix 功能区中，单击**发布**按钮。</span><span class="sxs-lookup"><span data-stu-id="b8642-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 功能区中的发布按钮](publishing/_static/image1.png)

<span data-ttu-id="b8642-153">**发布你的站点**显示对话框。</span><span class="sxs-lookup"><span data-stu-id="b8642-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="b8642-154">如果你有未登录到你的 Microsoft 帐户，将包含对话框**开始使用 Azure**链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="b8642-155">单击此链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-155">Click this link.</span></span>

![发布站点](publishing/_static/image2.png)

<span data-ttu-id="b8642-157">如果你不具有登录 Microsoft 帐户，您再次提供机会进行登录。</span><span class="sxs-lookup"><span data-stu-id="b8642-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="b8642-158">您必须登录到 Microsoft 帐户来发布 azure 网站。</span><span class="sxs-lookup"><span data-stu-id="b8642-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![登录](publishing/_static/image3.png)

<span data-ttu-id="b8642-160">登录到你的 Microsoft 帐户后, 对话框中包含用于在 Azure 上创建新的站点或连接到一个现有的站点在 Azure 上的链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![创建新的站点](publishing/_static/image4.png)

<span data-ttu-id="b8642-162">选择**创建新的站点**。</span><span class="sxs-lookup"><span data-stu-id="b8642-162">Select **Create a new site**.</span></span>

<span data-ttu-id="b8642-163">如果名为你的项目**WebPagesMovies**，将为你的站点的默认名称**webpagesmovies.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="b8642-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="b8642-164">此默认名称是最有可能不可用，红色感叹号标记所示。</span><span class="sxs-lookup"><span data-stu-id="b8642-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![默认 Web 站点名称](publishing/_static/image5.png)

<span data-ttu-id="b8642-166">将该站点的名称更改为可不可用，并选择靠近所在位置的位置。</span><span class="sxs-lookup"><span data-stu-id="b8642-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![已更改的站点名称](publishing/_static/image6.png)

<span data-ttu-id="b8642-168">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="b8642-168">Click **OK**.</span></span>

<span data-ttu-id="b8642-169">WebMatrix performss 测试，确定服务器是否与你的站点兼容。</span><span class="sxs-lookup"><span data-stu-id="b8642-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![兼容性测试](publishing/_static/image7.png)

<span data-ttu-id="b8642-171">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="b8642-171">Select **Continue**.</span></span>

<span data-ttu-id="b8642-172">显示兼容性测试的结果。</span><span class="sxs-lookup"><span data-stu-id="b8642-172">The results of the compatibility test are displayed.</span></span>

![兼容性结果](publishing/_static/image8.png)

<span data-ttu-id="b8642-174">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="b8642-174">Select **Continue**.</span></span>

<span data-ttu-id="b8642-175">WebMatrix 显示文件和将发布到网站的数据库。</span><span class="sxs-lookup"><span data-stu-id="b8642-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="b8642-176">由于这是要将站点发布第一次，会列出所有文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="b8642-177">你可以取消选中未准备好要发布的文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="b8642-178">在后续的发布，将显示已更改的文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="b8642-179">请参阅[更新实时站点： 重新发布](#update)。</span><span class="sxs-lookup"><span data-stu-id="b8642-179">See [Updating the Live Site: Republishing](#update).</span></span>

![发布预览](publishing/_static/image9.png)

<span data-ttu-id="b8642-181">选择**继续**。</span><span class="sxs-lookup"><span data-stu-id="b8642-181">Select **Continue**.</span></span>

<span data-ttu-id="b8642-182">站点部署到 Azure 后，将显示一条消息指示已完成部署。</span><span class="sxs-lookup"><span data-stu-id="b8642-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![发布完成](publishing/_static/image10.png)

<span data-ttu-id="b8642-184">站点和数据库已发布到 Azure，并且现在可供公众。</span><span class="sxs-lookup"><span data-stu-id="b8642-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="b8642-185">单击消息，指示发布完成后，现在，您将看到你已部署的站点中的链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="b8642-186">你或 Internet 访问权限的任何人都可以添加或修改数据库中的记录。</span><span class="sxs-lookup"><span data-stu-id="b8642-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="b8642-187">将站点发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="b8642-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="b8642-188">如果您决定不将发布到 Azure，你可以改为将你的站点发布到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="b8642-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="b8642-189">单击**查找 web 托管**链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-189">Click the **Find web hosting** link.</span></span>

![在发布设置对话框中的查找 web 托管按钮](publishing/_static/image12.png)

<span data-ttu-id="b8642-191">列出了支持 ASP.NET 的托管提供商的 Microsoft 站点上进入一个页面。</span><span class="sxs-lookup"><span data-stu-id="b8642-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![列出了宿主提供程序的 Microsoft 网站上的页](publishing/_static/image13.png)

<span data-ttu-id="b8642-193">显然，可能很难知道现在完全从长远来说可能需要哪些托管功能。</span><span class="sxs-lookup"><span data-stu-id="b8642-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="b8642-194">下面是一些要考虑的事项：</span><span class="sxs-lookup"><span data-stu-id="b8642-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="b8642-195">对于 WebPagesMovies 站点，您无需具有单独的外接程序对于 SQL Server，通常的额外费用。</span><span class="sxs-lookup"><span data-stu-id="b8642-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="b8642-196">在网站中，使用 SQL Server Compact Edition，这自包含。</span><span class="sxs-lookup"><span data-stu-id="b8642-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="b8642-197">但是，您可能需要访问 SQL Server 为你做一些将来的网站工作。</span><span class="sxs-lookup"><span data-stu-id="b8642-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="b8642-198">如果您认为您可能，请确保可以稍后添加 SQL Server 功能。</span><span class="sxs-lookup"><span data-stu-id="b8642-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="b8642-199">检查宿主提供程序是否支持 Web 部署发布协议。</span><span class="sxs-lookup"><span data-stu-id="b8642-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="b8642-200">可以使用 FTP 协议发布但更方便地使用 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="b8642-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="b8642-201">某些站点提供免费试用期。</span><span class="sxs-lookup"><span data-stu-id="b8642-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="b8642-202">免费试用版是尝试进行发布的好办法，承载时仍与 WebMatrix 和 ASP.NET Web Pages 正在试验。</span><span class="sxs-lookup"><span data-stu-id="b8642-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="b8642-203">选择您喜欢的一个。</span><span class="sxs-lookup"><span data-stu-id="b8642-203">Pick one that you like.</span></span> <span data-ttu-id="b8642-204">对于本教程中，我们选择 DiscountASP.NET，因为虽然我们已创建本教程，该公司必须让人们托管站点的几个月免费升级。</span><span class="sxs-lookup"><span data-stu-id="b8642-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="b8642-205">我们选择的本教程中的托管提供程序不应通过任何其他解释为代表该公司的认可。</span><span class="sxs-lookup"><span data-stu-id="b8642-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="b8642-206">但我们需要选择其中一个是为了进行说明，和 DiscountASP.NET 是许多支持 ASP.NET Web Pages 和 Web Deploy 协议用于发布的公司之一。</span><span class="sxs-lookup"><span data-stu-id="b8642-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>


<span data-ttu-id="b8642-207">通常情况下，您已经使用宿主提供程序注册后，公司向你发送一封电子邮件，其中包含用户名和密码，web 服务器和等等的 URL。</span><span class="sxs-lookup"><span data-stu-id="b8642-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="b8642-208">如果托管的公司支持 Web Deploy 协议，它们可能会发送包含的文件发布设置，也可以让您下载一个。</span><span class="sxs-lookup"><span data-stu-id="b8642-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="b8642-209">发布设置文件为您简化过程。</span><span class="sxs-lookup"><span data-stu-id="b8642-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="b8642-210">已注册且已准备好发布，请单击**发布**WebMatrix 功能区中的按钮。</span><span class="sxs-lookup"><span data-stu-id="b8642-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="b8642-211">**发布设置**显示对话框。</span><span class="sxs-lookup"><span data-stu-id="b8642-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="b8642-212">如果托管提供商向你发送了发布设置文件，请单击**导入发布设置**链接，然后导入文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="b8642-213">如果你没有发布设置文件，填写字段通过使用托管公司向你发送电子邮件中的值。</span><span class="sxs-lookup"><span data-stu-id="b8642-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="b8642-214">下面是什么**发布设置**对话框可能如下所示完成后：</span><span class="sxs-lookup"><span data-stu-id="b8642-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![在发布设置对话框中填写发布设置](publishing/_static/image14.png)

<span data-ttu-id="b8642-216">单击**验证连接**。</span><span class="sxs-lookup"><span data-stu-id="b8642-216">Click **Validate Connection**.</span></span> <span data-ttu-id="b8642-217">如果所有内容是确定，对话框的报告**已成功连接**，这意味着它可以与宿主提供程序的服务器进行通信。</span><span class="sxs-lookup"><span data-stu-id="b8642-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![成功消息，如果将发布设置正确无误](publishing/_static/image15.png)

<span data-ttu-id="b8642-219">如果没有问题，WebMatrix 会尽力告诉您的问题是：</span><span class="sxs-lookup"><span data-stu-id="b8642-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![如果没有问题的错误消息将发布设置](publishing/_static/image16.png)

<span data-ttu-id="b8642-221">单击**保存**以保存设置。</span><span class="sxs-lookup"><span data-stu-id="b8642-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="b8642-222">WebMatrix 提供了执行测试以确保，它可以正确地与宿主站点通信：</span><span class="sxs-lookup"><span data-stu-id="b8642-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![产品/服务来执行发布过程的测试消息](publishing/_static/image17.png)

<span data-ttu-id="b8642-224">单击 **“是”**。</span><span class="sxs-lookup"><span data-stu-id="b8642-224">Click **Yes**.</span></span> <span data-ttu-id="b8642-225">WebMatrix 将一些示例文件上传到宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="b8642-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="b8642-226">完成操作后兼容性测试，WebMatrix 将报告结果：</span><span class="sxs-lookup"><span data-stu-id="b8642-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![发布测试结果](publishing/_static/image18.png)

<span data-ttu-id="b8642-228">如果您准备好，请继续并单击**继续**真正开始发布过程。</span><span class="sxs-lookup"><span data-stu-id="b8642-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="b8642-229">WebMatrix 将计算出什么文件位于你的站点和 （稍后再试，无） 的主机服务器上已以及您提供的发布过程预览：</span><span class="sxs-lookup"><span data-stu-id="b8642-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![哪些发布过程将上传的文件的预览](publishing/_static/image19.png)

<span data-ttu-id="b8642-231">要发布的文件列表包括已创建与类似的网页*Movies.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="b8642-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="b8642-232">列表还包括帮助程序的已安装的数据库，运行 SQL Server Compact Edition 等的文件的文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="b8642-233">因此，在初始发布过程可能很高。</span><span class="sxs-lookup"><span data-stu-id="b8642-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="b8642-234">单击 **“继续”**。</span><span class="sxs-lookup"><span data-stu-id="b8642-234">Click **Continue**.</span></span> <span data-ttu-id="b8642-235">WebMatrix 将你的文件复制到托管提供商的服务器。</span><span class="sxs-lookup"><span data-stu-id="b8642-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="b8642-236">完成后，状态栏中报告结果：</span><span class="sxs-lookup"><span data-stu-id="b8642-236">When it's done, the results are reported in the status bar:</span></span>

![状态条消息时已成功完成发布过程](publishing/_static/image20.png)

<span data-ttu-id="b8642-238">若要查看实时站点，请单击状态栏中的链接。</span><span class="sxs-lookup"><span data-stu-id="b8642-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="b8642-239">添加*电影*到的 URL，您将看到*Movies.cshtml*你创建的文件：</span><span class="sxs-lookup"><span data-stu-id="b8642-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![显示电影页面在实时站点](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="b8642-241">更新实时站点： 重新发布</span><span class="sxs-lookup"><span data-stu-id="b8642-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="b8642-242">一旦您已将站点发布 （到 Azure 或 web 托管公司），有两份&mdash;上您的计算机和服务提供程序上的版本的版本。</span><span class="sxs-lookup"><span data-stu-id="b8642-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="b8642-243">您可能需要在继续开发站点 (如果没有其他下, 一步的教程系列的一部分)。</span><span class="sxs-lookup"><span data-stu-id="b8642-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="b8642-244">执行操作时，您必须重新发布才能将更改从您的计算机复制到服务提供商的站点。</span><span class="sxs-lookup"><span data-stu-id="b8642-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="b8642-245">在 WebMatrix 中的发布过程可以确定您的站点上，文件已更改内容和发布的那些文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="b8642-246">若要查看重新发布的工作原理，请打开*Movies.cshtml*站点、 进行一些小更改，并保存该文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="b8642-247">例如，将标题更改为`Movies - Updated`。</span><span class="sxs-lookup"><span data-stu-id="b8642-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="b8642-248">单击**发布**中功能区按钮。</span><span class="sxs-lookup"><span data-stu-id="b8642-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="b8642-249">WebMatrix 确定哪些更改并将发布的文件的位置处显示。</span><span class="sxs-lookup"><span data-stu-id="b8642-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![发布对话框中显示已更改文件可供重新发布](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="b8642-251">默认情况下，WebMatrix 发布你的数据库 (*.sdf*文件) 仅在发布站点的第一次。</span><span class="sxs-lookup"><span data-stu-id="b8642-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="b8642-252">一旦发布你的站点，并与网站交互的人员，实时站点上的数据库通常具有站点的真实数据。</span><span class="sxs-lookup"><span data-stu-id="b8642-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="b8642-253">一定要非常小心，不要覆盖实时数据库与 *.sdf*是您通常只包含测试数据的计算机的文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="b8642-254">这就是为什么您会看到警告**发布将覆盖任何远程数据库**，以及为什么的复选框*WebPagesMovies.sdf*默认情况下清除。</span><span class="sxs-lookup"><span data-stu-id="b8642-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>


<span data-ttu-id="b8642-255">单击 **“继续”**。</span><span class="sxs-lookup"><span data-stu-id="b8642-255">Click **Continue**.</span></span> <span data-ttu-id="b8642-256">WebMatrix 发布已更改的文件，并显示一条成功消息，像第一次发布。</span><span class="sxs-lookup"><span data-stu-id="b8642-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="b8642-257">转到实时网站 （如果仍显示可单击成功消息中的链接），并验证所做的更改已发布。</span><span class="sxs-lookup"><span data-stu-id="b8642-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="b8642-258">**远程编辑文件**</span><span class="sxs-lookup"><span data-stu-id="b8642-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="b8642-259">为更改你的站点，然后重新发布的替代方法，可以编辑直接在 WebMatrix 中的远程文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="b8642-260">在此方案中，打开位于服务提供商，文件和 WebMatrix 下载它为您要编辑的副本。</span><span class="sxs-lookup"><span data-stu-id="b8642-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="b8642-261">每次保存该文件，WebMatrix 会将所做的更改发送到站点。</span><span class="sxs-lookup"><span data-stu-id="b8642-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="b8642-262">远程编辑是轻松地对实时站点进行更改。</span><span class="sxs-lookup"><span data-stu-id="b8642-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="b8642-263">但是，进行这种方式的更改不会与你的本地站点中的文件同步。</span><span class="sxs-lookup"><span data-stu-id="b8642-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="b8642-264">若要同步的本地文件与远程站点，可以下载远程文件。</span><span class="sxs-lookup"><span data-stu-id="b8642-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="b8642-265">此过程工作方式非常类似发布，除非按相反的顺序。</span><span class="sxs-lookup"><span data-stu-id="b8642-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="b8642-266">我们不会详细介绍的远程编辑和远程下载功能的 WebMatrix 此处。</span><span class="sxs-lookup"><span data-stu-id="b8642-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="b8642-267">它们非常有用，如果多个用户必须在不同的计算机上的同一站点上处理。</span><span class="sxs-lookup"><span data-stu-id="b8642-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="b8642-268">有关详细信息，请参阅[发布和编辑远程站点与 WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591)。</span><span class="sxs-lookup"><span data-stu-id="b8642-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b8642-269">其他资源</span><span class="sxs-lookup"><span data-stu-id="b8642-269">Additional Resources</span></span>

- <span data-ttu-id="b8642-270">[ASP.NET WebMatrix ASP.NET Web Pages 论坛](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)，一个很好的发布问题和获取答案。</span><span class="sxs-lookup"><span data-stu-id="b8642-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b8642-271">上一篇</span><span class="sxs-lookup"><span data-stu-id="b8642-271">Previous</span></span>](layouts.md)
