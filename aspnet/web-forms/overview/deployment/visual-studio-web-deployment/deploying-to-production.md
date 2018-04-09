---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio 的 ASP.NET Web 部署： 将部署到生产 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: f3b3898bd003ace100ba05619f2c45ca808462df
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a><span data-ttu-id="1a092-103">使用 Visual Studio 的 ASP.NET Web 部署： 将部署到生产</span><span class="sxs-lookup"><span data-stu-id="1a092-103">ASP.NET Web Deployment using Visual Studio: Deploying to Production</span></span>
====================
<span data-ttu-id="1a092-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1a092-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="1a092-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="1a092-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="1a092-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="1a092-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1a092-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1a092-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="1a092-108">概述</span><span class="sxs-lookup"><span data-stu-id="1a092-108">Overview</span></span>

<span data-ttu-id="1a092-109">在本教程中，设置 Microsoft Azure 帐户、 创建过渡和生产环境和部署 ASP.NET web 应用程序到过渡环境和生产环境中的通过使用 Visual Studio 一键式发布功能。</span><span class="sxs-lookup"><span data-stu-id="1a092-109">In this tutorial, you set up a Microsoft Azure account, create staging and production environments, and deploy your ASP.NET web application to the staging and production environments by using the Visual Studio one-click publish feature.</span></span>

<span data-ttu-id="1a092-110">如果你愿意，你可以将其部署到第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="1a092-110">If you prefer, you can deploy to a third-party hosting provider.</span></span> <span data-ttu-id="1a092-111">在本教程中所述的过程的大部分都是相同的宿主提供程序或 azure，只不过每个提供程序具有其自己的帐户和 web 站点管理的用户界面。</span><span class="sxs-lookup"><span data-stu-id="1a092-111">Most of the procedures described in this tutorial are the same for a hosting provider or for Azure, except that each provider has its own user interface for account and web site management.</span></span> <span data-ttu-id="1a092-112">你可以查找中的宿主提供程序[的提供程序库](https://www.microsoft.com/web/hosting)Microsoft.com web 站点上。</span><span class="sxs-lookup"><span data-stu-id="1a092-112">You can find a hosting provider in the [gallery of providers](https://www.microsoft.com/web/hosting) on the Microsoft.com web site.</span></span>

<span data-ttu-id="1a092-113">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查本系列教程中的疑难解答页。</span><span class="sxs-lookup"><span data-stu-id="1a092-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the Troubleshooting page in this tutorial series.</span></span>

## <a name="get-a-microsoft-azure-account"></a><span data-ttu-id="1a092-114">获取一个 Microsoft Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="1a092-114">Get a Microsoft Azure account</span></span>

<span data-ttu-id="1a092-115">如果你还没有 Azure 帐户，可以在几分钟内创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="1a092-115">If you don't already have an Azure account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1a092-116">有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="1a092-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

## <a name="create-a-staging-environment"></a><span data-ttu-id="1a092-117">创建过渡环境</span><span class="sxs-lookup"><span data-stu-id="1a092-117">Create a staging environment</span></span>

> [!NOTE]
> <span data-ttu-id="1a092-118">由于在撰写本教程时，Azure App Service 添加了新功能来自动执行许多创建过渡和生产环境的过程。</span><span class="sxs-lookup"><span data-stu-id="1a092-118">Since this tutorial was written, Azure App Service added a new feature to automate many of the processes for creating staging and production environments.</span></span> <span data-ttu-id="1a092-119">请参阅[设置过渡环境在 Azure App Service 的 web 应用的](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。</span><span class="sxs-lookup"><span data-stu-id="1a092-119">See [Set up staging environments for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).</span></span>


<span data-ttu-id="1a092-120">中所述[部署到测试环境教程](deploying-to-iis.md)、 最可靠的测试环境是在具有就像生产网站托管提供商的网站。</span><span class="sxs-lookup"><span data-stu-id="1a092-120">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), the most reliable test environment is a web site at the hosting provider that's just like the production web site.</span></span> <span data-ttu-id="1a092-121">许多托管服务提供商，您将不得不重量此功能的优势与重要的其他成本，但在 Azure 中，你可以创建其他的免费 web 应用程序作为你的过渡应用。</span><span class="sxs-lookup"><span data-stu-id="1a092-121">At many hosting providers you would have to weigh the benefits of this against significant additional cost, but in Azure you can create an additional free web app as your staging app.</span></span> <span data-ttu-id="1a092-122">你还需要一个数据库，并为该通过生产数据库的费用的额外费用将为无或最小。</span><span class="sxs-lookup"><span data-stu-id="1a092-122">You also need a database, and the additional expense for that over the expense of your production database will be either none or minimal.</span></span> <span data-ttu-id="1a092-123">在 Azure 中您支付你使用的数据库存储量而不是每个数据库，并将过渡环境中使用的其他存储量将最小。</span><span class="sxs-lookup"><span data-stu-id="1a092-123">In Azure you pay for the amount of database storage you use rather than for each database, and the amount of additional storage you'll use in staging will be minimal.</span></span>

<span data-ttu-id="1a092-124">中所述[部署到测试环境教程](deploying-to-iis.md)、 过渡和生产你要将两个数据库部署到一个数据库中。</span><span class="sxs-lookup"><span data-stu-id="1a092-124">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), in staging and production you're going to deploy your two databases into one database.</span></span> <span data-ttu-id="1a092-125">如果你想要将它们分开，过程将相同，只不过将会产生的每个环境的其他数据库并在创建发布配置文件时，将选择每个数据库的正确的目标字符串。</span><span class="sxs-lookup"><span data-stu-id="1a092-125">If you wanted to keep them separate, the process would be the same except that you'd create an additional database for each environment and you would select the correct destination string for each database when you create the publish profile.</span></span>

<span data-ttu-id="1a092-126">在本教程的本部分中，你将要创建一个 web 应用和数据库要用于过渡环境，并将部署到过渡环境，还可以创建和部署到生产环境之前，那里测试。</span><span class="sxs-lookup"><span data-stu-id="1a092-126">In this section of the tutorial you'll create a web app and database to use for the staging environment, and you'll deploy to staging and test there before creating and deploying to the production environment.</span></span>

> [!NOTE]
> <span data-ttu-id="1a092-127">以下步骤演示如何使用 Azure 管理门户在 Azure App Service 中创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1a092-127">The following steps show how to create a web app in Azure App Service by using the Azure management portal.</span></span> <span data-ttu-id="1a092-128">在 Azure SDK 的最新版本，你也可以这样做无需离开 Visual Studio 中，通过使用服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="1a092-128">In the latest version of the Azure SDK, you can also do this without leaving Visual Studio, by using Server Explorer.</span></span> <span data-ttu-id="1a092-129">在 Visual Studio 2013 中，还可以直接从发布对话框创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1a092-129">In Visual Studio 2013, you can also create a web app directly from the Publish dialog.</span></span> <span data-ttu-id="1a092-130">有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span><span class="sxs-lookup"><span data-stu-id="1a092-130">For more information, see [Create an ASP.NET web app in Azure App Service.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span></span>


1. <span data-ttu-id="1a092-131">在[Azure 管理门户](https://manage.windowsazure.com/)，单击**网站**，然后单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="1a092-131">In the [Azure Management Portal](https://manage.windowsazure.com/), click **Websites**, and then click **New**.</span></span>
2. <span data-ttu-id="1a092-132">单击**网站**，然后单击**自定义创建**。</span><span class="sxs-lookup"><span data-stu-id="1a092-132">Click **Website**, and then click **Custom Create**.</span></span>

    <span data-ttu-id="1a092-133">**新建网站-自定义创建**向导随即打开。</span><span class="sxs-lookup"><span data-stu-id="1a092-133">The **New Website - Custom Create** wizard opens.</span></span> <span data-ttu-id="1a092-134">**自定义创建**向导可以同时创建网站和数据库。</span><span class="sxs-lookup"><span data-stu-id="1a092-134">The **Custom Create** wizard enables you to create a web site and a database at the same time.</span></span>
3. <span data-ttu-id="1a092-135">在**创建网站**步骤的向导中，输入中的字符串**URL**框，以用作你的应用程序的唯一 URL 的过渡环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-135">In the **Create Website** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application's staging environment.</span></span> <span data-ttu-id="1a092-136">例如，输入 ContosoUniversity staging123 （包括结尾的随机数字，以确保其唯一性，以防执行 ContosoUniversity 过渡）。</span><span class="sxs-lookup"><span data-stu-id="1a092-136">For example, enter ContosoUniversity-staging123 (including random numbers at the end to make it unique in case ContosoUniversity-staging is taken).</span></span>

    <span data-ttu-id="1a092-137">完整的 URL 将包含的你在此处输入和文本框旁边看到的后缀。</span><span class="sxs-lookup"><span data-stu-id="1a092-137">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span>
4. <span data-ttu-id="1a092-138">在**区域**下拉列表中，选择离你的区域。</span><span class="sxs-lookup"><span data-stu-id="1a092-138">In the **Region** drop-down list, choose the region that is closest to you.</span></span>

    <span data-ttu-id="1a092-139">此设置指定你的 web 应用将在中运行哪个数据中心。</span><span class="sxs-lookup"><span data-stu-id="1a092-139">This setting specifies which data center your web app will run in.</span></span>
5. <span data-ttu-id="1a092-140">在**数据库**下拉列表中，选择**创建新的 SQL 数据库**。</span><span class="sxs-lookup"><span data-stu-id="1a092-140">In the **Database** drop-down list, choose **Create a new SQL database**.</span></span>
6. <span data-ttu-id="1a092-141">在**数据库连接字符串名称**框中，保留默认值， *DefaultConnection*。</span><span class="sxs-lookup"><span data-stu-id="1a092-141">In the **DB Connection String Name** box, leave the default value, *DefaultConnection*.</span></span>
7. <span data-ttu-id="1a092-142">单击框底部右侧箭头。</span><span class="sxs-lookup"><span data-stu-id="1a092-142">Click the arrow that points to the right at the bottom of the box.</span></span>

    <span data-ttu-id="1a092-143">下图显示**创建网站**与示例中它的值的对话框。</span><span class="sxs-lookup"><span data-stu-id="1a092-143">The following illustration shows the **Create Website** dialog with sample values in it.</span></span> <span data-ttu-id="1a092-144">将不同的 URL 和您输入的区域。</span><span class="sxs-lookup"><span data-stu-id="1a092-144">The URL and Region that you have entered will be different.</span></span>

    ![创建网站的步骤](deploying-to-production/_static/image1.png)

    <span data-ttu-id="1a092-146">向导将前进到**指定数据库设置**步骤。</span><span class="sxs-lookup"><span data-stu-id="1a092-146">The wizard advances to the **Specify database settings** step.</span></span>
8. <span data-ttu-id="1a092-147">在**名称**框中，输入*ContosoUniversity*加上随机的编号，以使之成为唯一的例如*ContosoUniversity123*。</span><span class="sxs-lookup"><span data-stu-id="1a092-147">In the **Name** box, enter *ContosoUniversity* plus a random number to make it unique, for example *ContosoUniversity123*.</span></span>
9. <span data-ttu-id="1a092-148">在**服务器**框中，选择**新建 SQL 数据库服务器**。</span><span class="sxs-lookup"><span data-stu-id="1a092-148">In the **Server** box, select **New SQL Database Server**.</span></span>
10. <span data-ttu-id="1a092-149">输入管理员名称和密码。</span><span class="sxs-lookup"><span data-stu-id="1a092-149">Enter an administrator name and password.</span></span>

    <span data-ttu-id="1a092-150">不要输入现有名称和密码。</span><span class="sxs-lookup"><span data-stu-id="1a092-150">You aren't entering an existing name and password here.</span></span> <span data-ttu-id="1a092-151">要输入新名称和你定义现在要以后访问数据库时使用的密码。</span><span class="sxs-lookup"><span data-stu-id="1a092-151">You're entering a new name and password that you're defining now to use later when you access the database.</span></span>
11. <span data-ttu-id="1a092-152">在**区域**框中，选择为 web 应用所选的同一区域。</span><span class="sxs-lookup"><span data-stu-id="1a092-152">In the **Region** box, choose the same region that you chose for the web app.</span></span>

    <span data-ttu-id="1a092-153">将 web 服务器和数据库服务器放置在同一区域提供最佳性能并最大程度减少费用。</span><span class="sxs-lookup"><span data-stu-id="1a092-153">Keeping the web server and the database server in the same region gives you the best performance and minimizes expenses.</span></span>
12. <span data-ttu-id="1a092-154">单击底部的框以指示你已完成的复选标记。</span><span class="sxs-lookup"><span data-stu-id="1a092-154">Click the check mark at the bottom of the box to indicate that you're finished.</span></span>

    <span data-ttu-id="1a092-155">下图显示**指定数据库设置**与示例中它的值的对话框。</span><span class="sxs-lookup"><span data-stu-id="1a092-155">The following illustration shows the **Specify database settings** dialog with sample values in it.</span></span> <span data-ttu-id="1a092-156">你输入的值可能不同。</span><span class="sxs-lookup"><span data-stu-id="1a092-156">The values you have entered may be different.</span></span>

    ![数据库设置步骤使用数据库向导创建的新的网站的](deploying-to-production/_static/image2.png)

    <span data-ttu-id="1a092-158">管理门户返回到网站页面中，与**状态**列显示正在创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1a092-158">The Management Portal returns to the Websites page, and the **Status** column shows that the web app is being created.</span></span> <span data-ttu-id="1a092-159">（通常小于一分钟），一段时间后**状态**列显示已成功创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1a092-159">After a while (typically less than a minute), the **Status** column shows that the web app was successfully created.</span></span> <span data-ttu-id="1a092-160">在左侧导航栏中，在你的帐户拥有的 web 应用数旁边将出现**网站**旁边显示图标和数据库的数目**SQL 数据库**图标。</span><span class="sxs-lookup"><span data-stu-id="1a092-160">In the navigation bar at the left, the number of web apps you have in your account appears next to the **Websites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

    ![管理门户中，创建网站的网站页面](deploying-to-production/_static/image3.png)

    <span data-ttu-id="1a092-162">您的 web 应用名称将不同于在图中的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a092-162">Your web app name will be different from the example app in the illustration.</span></span>

## <a name="deploy-the-application-to-staging"></a><span data-ttu-id="1a092-163">部署到过渡环境应用程序</span><span class="sxs-lookup"><span data-stu-id="1a092-163">Deploy the application to staging</span></span>

<span data-ttu-id="1a092-164">既然你已经创建 web 应用和过渡环境的数据库，你可以将项目部署到它。</span><span class="sxs-lookup"><span data-stu-id="1a092-164">Now that you have created a web app and database for the staging environment, you can deploy the project to it.</span></span>

> [!NOTE]
> <span data-ttu-id="1a092-165">这些说明演示如何创建通过下载发布配置文件*.publishsettings*文件，其工作方式不只供 Azure 也为第三方宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="1a092-165">These instructions show how to create a publish profile by downloading a *.publishsettings* file, which works not only for Azure but also for third-party hosting providers.</span></span> <span data-ttu-id="1a092-166">最新 Azure SDK 还可以直接连接到 Azure 从 Visual Studio 中，并从具有 Azure 帐户中的 web 应用的列表中选择。</span><span class="sxs-lookup"><span data-stu-id="1a092-166">The latest Azure SDK also enables you to connect directly to Azure from Visual Studio, and choose from a list of web apps that you have in your Azure account.</span></span> <span data-ttu-id="1a092-167">在 Visual Studio 2013 中，你可以登录到 Azure 从**Web 发布**对话框或从**服务器资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="1a092-167">In Visual Studio 2013, you can sign in to Azure from the **Web Publish** dialog or from the **Server Explorer** window.</span></span> <span data-ttu-id="1a092-168">有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="1a092-168">For more information, see [Create an ASP.NET web app in Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>


### <a name="download-the-publishsettings-file"></a><span data-ttu-id="1a092-169">下载.publishsettings 文件</span><span class="sxs-lookup"><span data-stu-id="1a092-169">Download the .publishsettings file</span></span>

1. <span data-ttu-id="1a092-170">单击你刚刚创建的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="1a092-170">Click the name of the web app that you just created.</span></span>

    ![单击要转到仪表板的站点](deploying-to-production/_static/image4.png)
2. <span data-ttu-id="1a092-172">下**速览**中**仪表板**选项卡上，单击**下载发布配置文件**。</span><span class="sxs-lookup"><span data-stu-id="1a092-172">Under **Quick glance** in the **Dashboard** tab, click **Download publish profile**.</span></span>

    ![下载发布配置文件链接](deploying-to-production/_static/image5.png)

    <span data-ttu-id="1a092-174">此步骤将下载包含所有所需应用程序部署到你的 web 应用的设置的文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-174">This step downloads a file that contains all of the settings that you need in order to deploy an application to your web app.</span></span> <span data-ttu-id="1a092-175">因此你不必手动输入此信息，将导入 Visual Studio 的此文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-175">You'll import this file into Visual Studio so you don't have to enter this information manually.</span></span>
3. <span data-ttu-id="1a092-176">保存*.publishsettings*可以从 Visual Studio 访问的文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-176">Save the *.publishsettings* file in a folder that you can access from Visual Studio.</span></span>

    ![保存.publishsettings 文件](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > <span data-ttu-id="1a092-178">安全- *.publishsettings*文件包含你用于管理你的 Azure 订阅和服务的凭据 （未编码）。</span><span class="sxs-lookup"><span data-stu-id="1a092-178">Security - The *.publishsettings* file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="1a092-179">此文件的最佳安全方案是将其临时存储 （例如在 Libraries\Documents 文件夹中），源目录以外，然后在导入完毕后删除它。</span><span class="sxs-lookup"><span data-stu-id="1a092-179">The security best practice for this file is to store it temporarily outside your source directories (for example in the Libraries\Documents folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="1a092-180">恶意用户获得访问权*.publishsettings*文件可以编辑、 创建和删除你的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="1a092-180">A malicious user who gains access to the *.publishsettings* file can edit, create, and delete your Azure services.</span></span>

### <a name="create-a-publish-profile"></a><span data-ttu-id="1a092-181">创建发布配置文件</span><span class="sxs-lookup"><span data-stu-id="1a092-181">Create a publish profile</span></span>

1. <span data-ttu-id="1a092-182">在 Visual Studio 中，右键单击中的 ContosoUniversity 项目**解决方案资源管理器**和选择**发布**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="1a092-182">In Visual Studio, right-click the ContosoUniversity project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

    <span data-ttu-id="1a092-183">**发布 Web**向导随即打开。</span><span class="sxs-lookup"><span data-stu-id="1a092-183">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="1a092-184">单击**配置文件**选项卡。</span><span class="sxs-lookup"><span data-stu-id="1a092-184">Click the **Profile** tab.</span></span>
3. <span data-ttu-id="1a092-185">单击“导入” 。</span><span class="sxs-lookup"><span data-stu-id="1a092-185">Click **Import**.</span></span>
4. <span data-ttu-id="1a092-186">导航到*.publishsettings*更早版本，下载文件，然后单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="1a092-186">Navigate to the *.publishsettings* file you downloaded earlier, and then click **Open**.</span></span>

    ![导入发布设置对话框](deploying-to-production/_static/image7.png)
5. <span data-ttu-id="1a092-188">在**连接**选项卡上，单击**验证连接**若要确保设置正确无误。</span><span class="sxs-lookup"><span data-stu-id="1a092-188">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>

    <span data-ttu-id="1a092-189">在验证连接后，旁边出现一个绿色的复选标记**验证连接**按钮。</span><span class="sxs-lookup"><span data-stu-id="1a092-189">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span>

    <span data-ttu-id="1a092-190">对于某些宿主提供程序，当你单击**验证连接**，你可能会看到**证书错误**对话框。</span><span class="sxs-lookup"><span data-stu-id="1a092-190">For some hosting providers, when you click **Validate Connection**, you might see a **Certificate Error** dialog box.</span></span> <span data-ttu-id="1a092-191">如果执行操作时，请验证服务器名称是否符合你的预期。</span><span class="sxs-lookup"><span data-stu-id="1a092-191">If you do, verify that the server name is what you expect.</span></span> <span data-ttu-id="1a092-192">如果服务器名称正确，请选择**Visual Studio 的将来会话保存此证书**单击**接受**。</span><span class="sxs-lookup"><span data-stu-id="1a092-192">If the server name is correct, select **Save this certificate for future sessions of Visual Studio** and click **Accept**.</span></span> <span data-ttu-id="1a092-193">（此错误表明，托管提供商已选择免去为您要部署到的 URL 中购买的 SSL 证书的开支。</span><span class="sxs-lookup"><span data-stu-id="1a092-193">(This error means that the hosting provider has chosen to avoid the expense of purchasing an SSL certificate for the URL that you are deploying to.</span></span> <span data-ttu-id="1a092-194">如果想要通过使用有效的证书建立安全连接，请与你托管提供商。）</span><span class="sxs-lookup"><span data-stu-id="1a092-194">If you prefer to establish a secure connection by using a valid certificate, contact your hosting provider.)</span></span>
6. <span data-ttu-id="1a092-195">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="1a092-195">Click **Next**.</span></span>

    ![连接成功图标和连接选项卡中的下一步按钮](deploying-to-production/_static/image8.png)
7. <span data-ttu-id="1a092-197">在**设置**选项卡上，展开**文件发布选项**，然后选择**将应用程序中排除文件\_数据文件夹**。</span><span class="sxs-lookup"><span data-stu-id="1a092-197">In the **Settings** tab, expand **File Publish Options**, and then select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="1a092-198">璝惠下的其他选项**文件发布选项**，请参阅[部署到 IIS](deploying-to-iis.md)教程。</span><span class="sxs-lookup"><span data-stu-id="1a092-198">For information about the other options under **File Publish Options**, see the [deploying to IIS](deploying-to-iis.md) tutorial.</span></span> <span data-ttu-id="1a092-199">此步骤和以下的数据库配置步骤的结果是在数据库配置步骤末尾用于显示的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="1a092-199">The screen shot that shows the result of this step and the following database configuration steps is at the end of the database configuration steps.</span></span>
8. <span data-ttu-id="1a092-200">下**DefaultConnection**中**数据库**部分中，配置成员资格数据库的数据库部署。</span><span class="sxs-lookup"><span data-stu-id="1a092-200">Under **DefaultConnection** in the **Databases** section, configure database deployment for the membership database.</span></span>
9. 1. <span data-ttu-id="1a092-201">选择**更新数据库**。</span><span class="sxs-lookup"><span data-stu-id="1a092-201">Select **Update database**.</span></span>

        <span data-ttu-id="1a092-202">**远程连接字符串**直接下面框**DefaultConnection**使用.publishsettings 文件中的连接字符串填充。连接字符串包含纯文本中存储的 SQL Server 凭据*.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-202">The **Remote connection string** box directly below **DefaultConnection** is filled in with the connection string from the .publishsettings file.The connection string includes SQL Server credentials, which are stored in plain text in the *.pubxml* file.</span></span> <span data-ttu-id="1a092-203">如果你不想将其存储在永久，可以部署数据库后，则会删除它们从发布配置文件，并将它们存储在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="1a092-203">If you prefer not to store them permanently there, you can remove them from the publish profile after the database is deployed and store them in Azure instead.</span></span> <span data-ttu-id="1a092-204">有关详细信息，请参阅[如何保护你的 ASP.NET 数据库连接字符串从源部署到 Azure 时](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx)Scott Hanselman 的博客上。</span><span class="sxs-lookup"><span data-stu-id="1a092-204">For more information, see [How to keep your ASP.NET database connection strings secure when deploying to Azure from Source](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) on Scott Hanselman's blog.</span></span>
      2. <span data-ttu-id="1a092-205">单击**配置数据库更新**。</span><span class="sxs-lookup"><span data-stu-id="1a092-205">Click **Configure database updates**.</span></span>
      3. <span data-ttu-id="1a092-206">在**配置数据库更新**对话框中，单击**添加 SQL 脚本**。</span><span class="sxs-lookup"><span data-stu-id="1a092-206">In the **Configure Database Updates** dialog box, click **Add SQL Script**.</span></span>
      4. <span data-ttu-id="1a092-207">在**添加 SQL 脚本**框中，导航到*aspnet 数据 prod.sql*脚本，你前面保存在解决方案文件夹中，然后单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="1a092-207">In the **Add SQL Script** box, navigate to the *aspnet-data-prod.sql* script that you saved earlier in the solution folder, and then click **Open**.</span></span>
      5. <span data-ttu-id="1a092-208">关闭**配置数据库更新**对话框。</span><span class="sxs-lookup"><span data-stu-id="1a092-208">Close the **Configure Database Updates** dialog box.</span></span>
10. <span data-ttu-id="1a092-209">下**SchoolContext**中**数据库**部分中，选择**执行 Code First 迁移 （应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="1a092-209">Under **SchoolContext** in the **Databases** section, select **Execute Code First Migrations (runs on application start)**.</span></span>

    <span data-ttu-id="1a092-210">Visual Studio 将显示**执行 Code First 迁移**而不是**更新数据库**为`DbContext`类。</span><span class="sxs-lookup"><span data-stu-id="1a092-210">Visual Studio displays **Execute Code First Migrations** instead of **Update Database** for `DbContext` classes.</span></span> <span data-ttu-id="1a092-211">如果你想要使用 dbDacFx 提供程序而不是迁移部署的数据库，你通过使用访问`DbContext`类，请参阅[如何部署没有迁移的 Code First 数据库？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) Visual Studio Web 部署常见问题中和 MSDN 上的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="1a092-211">If you want to use the dbDacFx provider instead of Migrations to deploy a database that you access by using a `DbContext` class, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the Web Deployment FAQ for Visual Studio and ASP.NET on MSDN.</span></span>

    <span data-ttu-id="1a092-212">**设置**选项卡现在看起来像下面的示例：</span><span class="sxs-lookup"><span data-stu-id="1a092-212">The **Settings** tab now looks like the following example:</span></span>

    ![用于过渡的设置选项卡](deploying-to-production/_static/image9.png)
11. <span data-ttu-id="1a092-214">执行以下步骤以保存配置文件并将其命名为*过渡*:</span><span class="sxs-lookup"><span data-stu-id="1a092-214">Perform the following steps to save the profile and rename it to *Staging*:</span></span>

    1. <span data-ttu-id="1a092-215">单击**配置文件**选项卡上，并依次**管理配置文件**。</span><span class="sxs-lookup"><span data-stu-id="1a092-215">Click the **Profile** tab, and then click **Manage Profiles**.</span></span>
    2. <span data-ttu-id="1a092-216">导入创建两个新的配置文件，一个用于 FTP，一个用于 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="1a092-216">The import created two new profiles, one for FTP and one for Web Deploy.</span></span> <span data-ttu-id="1a092-217">配置 Web 部署配置文件： 重命名此配置文件以*过渡*。</span><span class="sxs-lookup"><span data-stu-id="1a092-217">You configured the Web Deploy profile: rename this profile to *Staging*.</span></span>

        ![将配置文件重命名为临时](deploying-to-production/_static/image10.png)
    3. <span data-ttu-id="1a092-219">关闭**编辑 Web 发布配置文件**对话框。</span><span class="sxs-lookup"><span data-stu-id="1a092-219">Close the **Edit Web Publish Profiles** dialog box.</span></span>
    4. <span data-ttu-id="1a092-220">关闭**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="1a092-220">Close the **Publish Web** wizard.</span></span>

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a><span data-ttu-id="1a092-221">配置发布配置文件转换为环境的指示符</span><span class="sxs-lookup"><span data-stu-id="1a092-221">Configure a publish profile transform for the environment indicator</span></span>

> [!NOTE]
> <span data-ttu-id="1a092-222">本部分演示如何设置 Web.config 转换为环境的指示符。</span><span class="sxs-lookup"><span data-stu-id="1a092-222">This section shows how to set up a Web.config transform for the environment indicator.</span></span> <span data-ttu-id="1a092-223">因为指示器位于`<appSettings>`元素，必须在要部署到 Azure App Service 时指定转换所需的另一种可选。</span><span class="sxs-lookup"><span data-stu-id="1a092-223">Because the indicator is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Azure App Service.</span></span> <span data-ttu-id="1a092-224">有关详细信息，请参阅[在 Azure 中的指定 Web.config 设置](web-config-transformations.md#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="1a092-224">For more information, see [Specifying Web.config settings in Azure](web-config-transformations.md#watransforms).</span></span>


1. <span data-ttu-id="1a092-225">在**解决方案资源管理器**，展开**属性**，然后展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="1a092-225">In **Solution Explorer**, expand **Properties**, and then expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="1a092-226">右键单击*Staging.pubxml*，然后单击**添加配置转换**。</span><span class="sxs-lookup"><span data-stu-id="1a092-226">Right-click *Staging.pubxml*, and then click **Add Config Transform**.</span></span>

    ![为临时添加配置转换](deploying-to-production/_static/image11.png)

    <span data-ttu-id="1a092-228">Visual Studio 将创建*Web.Staging.config*转换文件并将其打开。</span><span class="sxs-lookup"><span data-stu-id="1a092-228">Visual Studio creates the *Web.Staging.config* transform file and opens it.</span></span>
3. <span data-ttu-id="1a092-229">在*Web.Staging.config*转换文件中，插入以下代码打开后立即`configuration`标记。</span><span class="sxs-lookup"><span data-stu-id="1a092-229">In the *Web.Staging.config* transform file, insert the following code immediately after the opening `configuration` tag.</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    <span data-ttu-id="1a092-230">当使用过渡发布配置文件时，此转换将设置到"Prod"的环境指示器。</span><span class="sxs-lookup"><span data-stu-id="1a092-230">When you use the Staging publish profile, this transform sets the environment indicator to "Prod".</span></span> <span data-ttu-id="1a092-231">在已部署的 web 应用中，不会在"Contoso 大学"H1 标题后看到任何后缀，例如"（开发）"（测试）"。</span><span class="sxs-lookup"><span data-stu-id="1a092-231">In the deployed web app, you won't see any suffix such as "(Dev)" or "(Test)" after the "Contoso University" H1 heading.</span></span>
4. <span data-ttu-id="1a092-232">右键单击*Web.Staging.config*文件并单击**预览转换**以确保的转换编码时产生预期的更改。</span><span class="sxs-lookup"><span data-stu-id="1a092-232">Right-click the *Web.Staging.config* file and click **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="1a092-233">**Web.config 预览**窗口中显示的应用同时结果*Web.Release.config*转换和*Web.Staging.config*转换。</span><span class="sxs-lookup"><span data-stu-id="1a092-233">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Staging.config* transforms.</span></span>

### <a name="prevent-public-use-of-the-test-app"></a><span data-ttu-id="1a092-234">防止公共使用的测试应用程序</span><span class="sxs-lookup"><span data-stu-id="1a092-234">Prevent public use of the test app</span></span>

<span data-ttu-id="1a092-235">过渡应用的重要考虑事项是： 将实时在 Internet 上，但你不希望使用它的公共。</span><span class="sxs-lookup"><span data-stu-id="1a092-235">An important consideration for the staging app is that it will be live on the Internet, but you don't want the public to use it.</span></span> <span data-ttu-id="1a092-236">若要尽量减少人将查找并使用它的可能性越小，可以使用一个或多个以下方法：</span><span class="sxs-lookup"><span data-stu-id="1a092-236">To minimize the likelihood that people will find and use it, you can use one or more of the following methods:</span></span>

- <span data-ttu-id="1a092-237">设置允许对访问过渡应用仅用于测试过渡的 IP 地址的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="1a092-237">Set firewall rules that allow access to the staging app only from IP addresses that you use to test staging.</span></span>
- <span data-ttu-id="1a092-238">使用是不可能猜到的经过模糊处理的 URL。</span><span class="sxs-lookup"><span data-stu-id="1a092-238">Use an obfuscated URL that would be impossible to guess.</span></span>
- <span data-ttu-id="1a092-239">创建*robots.txt*文件以确保，搜索引擎将不爬网测试应用程序和报表链接到它在搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="1a092-239">Create a *robots.txt* file to ensure that search engines will not crawl the test app and report links to it in search results.</span></span>

<span data-ttu-id="1a092-240">第一种方法最有效，但因为它将需要你将部署到 Azure 云服务而不是 Azure App Service 中本教程未涉及。</span><span class="sxs-lookup"><span data-stu-id="1a092-240">The first of these methods is the most effective but is not covered in this tutorial because it would require that you deploy to an Azure Cloud Service instead of Azure App Service.</span></span> <span data-ttu-id="1a092-241">有关云服务的详细信息和在 Azure 中的 IP 限制，请参阅[选项提供的计算托管 Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)和[阻止特定 IP 地址访问 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a092-241">For more information about Cloud Services and IP restrictions in Azure, see [Compute Hosting Options Provided by Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) and [Block Specific IP Addresses from Accessing a Web Role](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx).</span></span> <span data-ttu-id="1a092-242">如果将部署到第三方托管提供程序，请与联系提供商联系以了解如何实施 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="1a092-242">If you are deploying to a third-party hosting provider, contact the provider to find out how to implement IP restrictions.</span></span>

<span data-ttu-id="1a092-243">对于本教程中，将创建*robots.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-243">For this tutorial, you'll create a *robots.txt* file.</span></span>

1. <span data-ttu-id="1a092-244">在**解决方案资源管理器**，右键单击 ContosoUniversity 项目，然后单击**添加新项**。</span><span class="sxs-lookup"><span data-stu-id="1a092-244">In **Solution Explorer**, right-click the ContosoUniversity project and click **Add New Item**.</span></span>
2. <span data-ttu-id="1a092-245">创建一个新**文本文件**名为*robots.txt*，并向其中放置以下文本：</span><span class="sxs-lookup"><span data-stu-id="1a092-245">Create a new **Text File** named *robots.txt*, and put the following text in it:</span></span>

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    <span data-ttu-id="1a092-246">`User-agent`一行通知文件中的规则应用于所有搜索引擎 web 爬网程序 （机器人） 的搜索引擎和`Disallow`行指定应在站点上的没有页已爬网。</span><span class="sxs-lookup"><span data-stu-id="1a092-246">The `User-agent` line tells search engines that the rules in the file apply to all search engine web crawlers (robots), and the `Disallow` line specifies that no pages on the site should be crawled.</span></span>

    <span data-ttu-id="1a092-247">您希望搜索引擎以目录生产应用程序，因此你需要从生产部署中排除此文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-247">You do want search engines to catalog your production app, so you need to exclude this file from production deployment.</span></span> <span data-ttu-id="1a092-248">为此，你将配置在生产环境中的设置发布配置文件时创建它。</span><span class="sxs-lookup"><span data-stu-id="1a092-248">To do that, you'll configure a setting in the Production publish profile when you create it.</span></span>

### <a name="deploy-to-staging"></a><span data-ttu-id="1a092-249">部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="1a092-249">Deploy to staging</span></span>

1. <span data-ttu-id="1a092-250">打开**发布 Web**向导通过右键单击 Contoso 大学项目并单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="1a092-250">Open the **Publish Web** wizard by right-clicking the Contoso University project and clicking **Publish**.</span></span>
2. <span data-ttu-id="1a092-251">请确保**过渡**选择配置文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-251">Make sure that the **Staging** profile is selected.</span></span>
3. <span data-ttu-id="1a092-252">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="1a092-252">Click **Publish**.</span></span>

    <span data-ttu-id="1a092-253">**输出**窗口将显示已执行的部署操作并报告已成功完成的部署。</span><span class="sxs-lookup"><span data-stu-id="1a092-253">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span> <span data-ttu-id="1a092-254">默认浏览器将自动打开到已部署的 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="1a092-254">The default browser automatically opens to the URL of the deployed web app.</span></span>

## <a name="test-in-the-staging-environment"></a><span data-ttu-id="1a092-255">在过渡环境中测试</span><span class="sxs-lookup"><span data-stu-id="1a092-255">Test in the staging environment</span></span>

<span data-ttu-id="1a092-256">请注意环境指示器不存在 (没有任何"（测试）"或"（开发）"后的 H1 标题，用于显示*Web.config*环境指示器的转换是否成功。</span><span class="sxs-lookup"><span data-stu-id="1a092-256">Notice that the environment indicator is absent (there is no "(Test)" or "(Dev)" after the H1 heading, which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

![主页过渡](deploying-to-production/_static/image12.png)

<span data-ttu-id="1a092-258">运行**学生**页后，可以验证是否已部署的数据库具有任何学生。</span><span class="sxs-lookup"><span data-stu-id="1a092-258">Run the **Students** page to verify that the deployed database has no students.</span></span>

<span data-ttu-id="1a092-259">运行**教师**页以验证 Code First 种子教师数据的数据库：</span><span class="sxs-lookup"><span data-stu-id="1a092-259">Run the **Instructors** page to verify that Code First seeded the database with instructor data:</span></span>

<span data-ttu-id="1a092-260">选择**添加学生**从**学生**菜单上，添加一名学生，，然后查看在新的学生**学生**页以验证是否可以成功写入到数据库.</span><span class="sxs-lookup"><span data-stu-id="1a092-260">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database.</span></span>

<span data-ttu-id="1a092-261">从**课程**页上，单击**更新信用额度**。</span><span class="sxs-lookup"><span data-stu-id="1a092-261">From the **Courses** page, click **Update Credits**.</span></span> <span data-ttu-id="1a092-262">**更新信用额度**页需要管理员权限，因此**Log In**显示页。</span><span class="sxs-lookup"><span data-stu-id="1a092-262">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="1a092-263">输入你创建更早版本 （"admin"和"prodpwd"） 的管理员帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="1a092-263">Enter the administrator account credentials that you created earlier ("admin" and "prodpwd").</span></span> <span data-ttu-id="1a092-264">**更新信用额度**页面显示时，该验证你在前面的教程中创建的管理员帐户已正确部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-264">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="1a092-265">请求无效的 URL，将引发错误 ELMAH 将跟踪，然后请求 ELMAH 错误报告。</span><span class="sxs-lookup"><span data-stu-id="1a092-265">Request an invalid URL to cause an error that ELMAH will track, and then request the ELMAH error report.</span></span> <span data-ttu-id="1a092-266">如果将部署到第三方托管提供商，您可能会发现该报告的相同的原因，它为空以前一教程中为空。</span><span class="sxs-lookup"><span data-stu-id="1a092-266">If you are deploying to a third-party hosting provider, you will probably find that the report is empty for the same reason that it was empty in the previous tutorial.</span></span> <span data-ttu-id="1a092-267">你将需要使用托管提供商的帐户管理工具来配置文件夹的权限以启用 ELMAH 要写入的日志文件夹。</span><span class="sxs-lookup"><span data-stu-id="1a092-267">You will have to use the hosting provider's account management tools to configure folder permissions to enable ELMAH to write to the log folder.</span></span>

<span data-ttu-id="1a092-268">你创建的应用程序现在运行在云中就如同将用于生产的 web 应用中。</span><span class="sxs-lookup"><span data-stu-id="1a092-268">The application that you created is now running in the cloud in a web app that is just like what you will use for production.</span></span> <span data-ttu-id="1a092-269">由于一切正常运行下, 一步是部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-269">Since everything is working correctly, the next step is to deploy to production.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="1a092-270">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="1a092-270">Deploy to production</span></span>

<span data-ttu-id="1a092-271">创建生产 web 应用程序和部署到生产环境的过程是临时，与相同，只不过你需要排除*robots.txt*从部署。</span><span class="sxs-lookup"><span data-stu-id="1a092-271">The process for creating a production web app and deploying to production is the same as for staging, except that you need to exclude the *robots.txt* from deployment.</span></span> <span data-ttu-id="1a092-272">若要执行此操作将编辑发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-272">To do that you'll edit the publish profile file.</span></span>

### <a name="create-the-production-environment-and-the-production-publish-profile"></a><span data-ttu-id="1a092-273">创建生产环境和生产发布配置文件</span><span class="sxs-lookup"><span data-stu-id="1a092-273">Create the production environment and the production publish profile</span></span>

1. <span data-ttu-id="1a092-274">在 Azure 中，执行用于过渡的同一过程中创建的生产 web 应用和数据库。</span><span class="sxs-lookup"><span data-stu-id="1a092-274">Create the production web app and database in Azure, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="1a092-275">在创建数据库时，你可以选择将其放在同一台服务器更早版本，创建或创建新的服务器。</span><span class="sxs-lookup"><span data-stu-id="1a092-275">When you create the database, you can choose to put it on the same server you created earlier, or create a new server.</span></span>
2. <span data-ttu-id="1a092-276">下载*.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-276">Download the *.publishsettings* file.</span></span>
3. <span data-ttu-id="1a092-277">通过导入生产环境中创建的发布配置文件*.publishsettings*文件，用于过渡执行同一过程。</span><span class="sxs-lookup"><span data-stu-id="1a092-277">Create the publish profile by importing the production *.publishsettings* file, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="1a092-278">不要忘记将配置数据部署脚本在**DefaultConnection**中**数据库**部分**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="1a092-278">Don't forget to configure the data deployment script under **DefaultConnection** in the **Databases** section of the **Settings** tab.</span></span>
4. <span data-ttu-id="1a092-279">重命名为发布配置文件*生产*。</span><span class="sxs-lookup"><span data-stu-id="1a092-279">Rename the publish profile to *Production*.</span></span>
5. <span data-ttu-id="1a092-280">配置发布配置文件转换为环境的指示符，用于过渡执行同一过程...</span><span class="sxs-lookup"><span data-stu-id="1a092-280">Configure a publish profile transform for the environment indicator, following the same procedure that you used for staging..</span></span>

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a><span data-ttu-id="1a092-281">编辑要排除 robots.txt 的.pubxml 文件</span><span class="sxs-lookup"><span data-stu-id="1a092-281">Edit the .pubxml file to exclude robots.txt</span></span>

<span data-ttu-id="1a092-282">发布配置文件文件被命名为&lt;profilename&gt;*.pubxml*并位于*PublishProfiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="1a092-282">Publish profile files are named &lt;profilename&gt;*.pubxml* and are located in the *PublishProfiles* folder.</span></span> <span data-ttu-id="1a092-283">*PublishProfiles*文件夹低于*属性*文件夹中的 C# web 应用程序项目，在*我的项目*中 VB web 应用程序项目中，或以下的文件夹*应用\_数据*文件夹中的 web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="1a092-283">The *PublishProfiles* folder is under the *Properties* folder in a C# web application project, under the *My Project* folder in a VB web application project, or under the *App\_Data* folder in a web app project.</span></span> <span data-ttu-id="1a092-284">每个*.pubxml*文件包含将应用于某个设置发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-284">Each *.pubxml* file contains settings that apply to one publish profile.</span></span> <span data-ttu-id="1a092-285">在发布 Web 向导中输入的值存储在这些文件，并可以编辑它们以便创建或更改不会在 Visual Studio UI 中提供的设置。</span><span class="sxs-lookup"><span data-stu-id="1a092-285">The values you enter in the Publish Web wizard are stored in these files, and you can edit them to create or change settings that aren't made available in the Visual Studio UI.</span></span>

<span data-ttu-id="1a092-286">默认情况下， *.pubxml*文件包括在项目中，在你创建的发布配置文件中，但你可以从项目中排除它们和 Visual Studio 仍将使用它们。</span><span class="sxs-lookup"><span data-stu-id="1a092-286">By default, *.pubxml* files are included in the project when you create a publish profile, but you can exclude them from the project and Visual Studio will still use them.</span></span> <span data-ttu-id="1a092-287">Visual Studio 将查找*PublishProfiles*文件夹*.pubxml*文件，无论它们是否包括在项目中。</span><span class="sxs-lookup"><span data-stu-id="1a092-287">Visual Studio looks in the *PublishProfiles* folder for *.pubxml* files, regardless of whether they are included in the project.</span></span>

<span data-ttu-id="1a092-288">每个*.pubxml*文件没有*。 pubxml.user*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-288">For each *.pubxml* file there is a *.pubxml.user* file.</span></span> <span data-ttu-id="1a092-289">*。 Pubxml.user*文件包含加密的密码，如果你选择**保存密码**选项，并且默认情况下会从项目中排除。</span><span class="sxs-lookup"><span data-stu-id="1a092-289">The *.pubxml.user* file contains the encrypted password if you selected the **Save password** option, and by default it is excluded from the project.</span></span>

<span data-ttu-id="1a092-290">A *.pubxml*文件包含适用于特定的发布配置文件的设置。</span><span class="sxs-lookup"><span data-stu-id="1a092-290">A *.pubxml* file contains the settings that pertain to a specific publish profile.</span></span> <span data-ttu-id="1a092-291">如果你想要配置应用于所有配置文件的设置，则可以创建*。 wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-291">If you want to configure settings that apply to all profiles, you can create a *.wpp.targets* file.</span></span> <span data-ttu-id="1a092-292">生成过程中导入到这些文件*.csproj*或*.vbproj*项目文件中，因此可以在这些文件中配置大多数设置都可以在项目文件中配置。</span><span class="sxs-lookup"><span data-stu-id="1a092-292">The build process imports these files into the *.csproj* or *.vbproj* project file, so most settings that you can configure in the project file can be configured in these files.</span></span> <span data-ttu-id="1a092-293">有关详细信息*.pubxml*文件和*。 wpp.targets*文件，请参阅[如何： 编辑发布配置文件 (.pubxml) 文件中的部署设置与。 wpp.targets Visual Studio 中的文件Web 项目发布](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a092-293">For more information about *.pubxml* files and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

1. <span data-ttu-id="1a092-294">在**解决方案资源管理器**，展开**属性**展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="1a092-294">In **Solution Explorer**, expand **Properties** and expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="1a092-295">右键单击*Production.pubxml*单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="1a092-295">Right-click *Production.pubxml* and click **Open**.</span></span>

    ![打开.pubxml 文件](deploying-to-production/_static/image13.png)
3. <span data-ttu-id="1a092-297">右键单击*Production.pubxml*单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="1a092-297">Right-click *Production.pubxml* and click **Open**.</span></span>
4. <span data-ttu-id="1a092-298">添加以下行在关闭之前立即`PropertyGroup`元素：</span><span class="sxs-lookup"><span data-stu-id="1a092-298">Add the following lines immediately before the closing `PropertyGroup` element:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    <span data-ttu-id="1a092-299">.Pubxml 文件现在看起来像下面的示例：</span><span class="sxs-lookup"><span data-stu-id="1a092-299">The .pubxml file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    <span data-ttu-id="1a092-300">有关如何排除文件和文件夹的详细信息，请参阅[可以我排除特定文件或文件夹从部署？](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)中**for Visual Studio 和 ASP.NET 的 Web 部署常见问题**MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="1a092-300">For more information about how to exclude files and folders, see [Can I exclude specific files or folders from deployment?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) in the **Web Deployment FAQ for Visual Studio and ASP.NET** on MSDN.</span></span>

### <a name="deploy-to-production"></a><span data-ttu-id="1a092-301">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="1a092-301">Deploy to production</span></span>

1. <span data-ttu-id="1a092-302">打开**发布 Web**向导确保**生产**发布配置文件已选择，然后单击**开始预览**上**预览**选项卡以确认*robots.txt*文件都不会复制到生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a092-302">Open the **Publish Web** wizard make sure that the **Production** publish profile is selected, and then click **Start Preview** on the **Preview** tab to verify that the *robots.txt* file will not be copied to the production app.</span></span>

    ![要发布到生产环境的文件的预览](deploying-to-production/_static/image14.png)

    <span data-ttu-id="1a092-304">查看将复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="1a092-304">Review the list of files that will be copied.</span></span> <span data-ttu-id="1a092-305">你会看到所有的*.cs*文件，包括*。 aspx.cs*， *。 aspx.designer.cs*， *Master.cs*，和*Master.designer.cs*文件被忽略。</span><span class="sxs-lookup"><span data-stu-id="1a092-305">You'll see that all of the *.cs* files, including *.aspx.cs*, *.aspx.designer.cs*, *Master.cs*, and *Master.designer.cs* files are omitted.</span></span> <span data-ttu-id="1a092-306">所有此代码编译为*ContosoUniversity.dll*和*ContosUniversity.pdb*将在中找到的文件*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="1a092-306">All of this code has been compiled into the *ContosoUniversity.dll* and *ContosUniversity.pdb* files that you'll find in the *bin* folder.</span></span> <span data-ttu-id="1a092-307">因为仅*.dll*需要的运行该应用程序，并且你前面指定应部署仅运行该应用程序所需的文件，则不*.cs*文件被复制到目标环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-307">Because only the *.dll* is needed to run the application, and you specified earlier that only files needed to run the application should be deployed, no *.cs* files were copied to the destination environment.</span></span> <span data-ttu-id="1a092-308">*Obj*文件夹和*ContosoUniversity.csproj*和*。 csproj.user*文件省略出于同样的原因。</span><span class="sxs-lookup"><span data-stu-id="1a092-308">The *obj* folder and the *ContosoUniversity.csproj* and *.csproj.user* files are omitted for the same reason.</span></span>

    <span data-ttu-id="1a092-309">单击**发布**将部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-309">Click **Publish** to deploy to the production environment.</span></span>
2. <span data-ttu-id="1a092-310">在生产环境，用于过渡执行同一过程中测试。</span><span class="sxs-lookup"><span data-stu-id="1a092-310">Test in production, following the same procedure you used for staging.</span></span>

    <span data-ttu-id="1a092-311">所有内容等同于过渡 URL 除外和没有*robots.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="1a092-311">Everything is identical to staging except for the URL and the absence of the *robots.txt* file.</span></span>

## <a name="summary"></a><span data-ttu-id="1a092-312">总结</span><span class="sxs-lookup"><span data-stu-id="1a092-312">Summary</span></span>

<span data-ttu-id="1a092-313">你现在已成功部署和测试你的 web 应用并可公开通过 Internet。</span><span class="sxs-lookup"><span data-stu-id="1a092-313">You have now successfully deployed and tested your web app and it is available publicly over the Internet.</span></span>

![主页生产](deploying-to-production/_static/image15.png)

<span data-ttu-id="1a092-315">在下一步的教程中，将更新应用程序代码，并将更改部署到测试、 过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="1a092-315">In the next tutorial, you'll update application code and deploy the change to the test, staging, and production environments.</span></span>

> [!NOTE]
> <span data-ttu-id="1a092-316">在生产环境中使用你的应用程序时你应实现恢复计划。</span><span class="sxs-lookup"><span data-stu-id="1a092-316">While your application is in use in the production environment you should be implementing a recovery plan.</span></span> <span data-ttu-id="1a092-317">也就是说，你应将定期备份你的数据库从生产应用到安全存储位置，并您应保留多个代这样的备份。</span><span class="sxs-lookup"><span data-stu-id="1a092-317">That is, you should be periodically backing up your databases from the production app to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="1a092-318">在更新数据库时，你应在更改之前立即从的备份副本。</span><span class="sxs-lookup"><span data-stu-id="1a092-318">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="1a092-319">然后，如果犯错，进而不发现它之前，部署到生产环境之后，你仍将能够将数据库恢复到它损坏之前的状态。</span><span class="sxs-lookup"><span data-stu-id="1a092-319">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span> <span data-ttu-id="1a092-320">有关详细信息，请参阅[Azure SQL Database 备份和还原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a092-320">For more information, see [Azure SQL Database Backup and Restore](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).</span></span>
> 
> 
> [!NOTE]
> <span data-ttu-id="1a092-321">在本教程中 SQL Server 部署到的版本是 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="1a092-321">In this tutorial the SQL Server edition that you are deploying to is Azure SQL Database.</span></span> <span data-ttu-id="1a092-322">类似于其他版本的 SQL Server 部署过程时，实际生产应用程序可能在某些情况下为 Azure SQL 数据库需要特殊的代码。</span><span class="sxs-lookup"><span data-stu-id="1a092-322">While the deployment process is similar to other editions of SQL Server, a real production application might require special code for Azure SQL Database in some scenarios.</span></span> <span data-ttu-id="1a092-323">有关详细信息，请参阅[使用 Azure SQL 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)和[SQL Server 和 Azure SQL 数据库之间进行选择](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。</span><span class="sxs-lookup"><span data-stu-id="1a092-323">For more information, see [Working with Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) and [Choosing between SQL Server and Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="1a092-324">[上一页](setting-folder-permissions.md)
> [下一页](deploying-a-code-update.md)</span><span class="sxs-lookup"><span data-stu-id="1a092-324">[Previous](setting-folder-permissions.md)
[Next](deploying-a-code-update.md)</span></span>
