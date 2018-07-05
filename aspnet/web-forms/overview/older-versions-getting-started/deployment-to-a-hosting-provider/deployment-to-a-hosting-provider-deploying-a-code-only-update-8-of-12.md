---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 Code-Only 更新-8 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: 16a9e48034536964d526717ecde2a9b813818963
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816079"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="85246-103">使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 Code-Only 更新-8 12</span><span class="sxs-lookup"><span data-stu-id="85246-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>
====================
<span data-ttu-id="85246-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="85246-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="85246-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="85246-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="85246-106">本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="85246-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="85246-107">如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="85246-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="85246-108">该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="85246-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="85246-109">显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="85246-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="85246-110">概述</span><span class="sxs-lookup"><span data-stu-id="85246-110">Overview</span></span>

<span data-ttu-id="85246-111">在初始部署后持续维护和开发您的网站的工作，并在长时间之前你将想要将更新部署。</span><span class="sxs-lookup"><span data-stu-id="85246-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="85246-112">本教程将指导你完成更新部署到应用程序代码的过程。</span><span class="sxs-lookup"><span data-stu-id="85246-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="85246-113">此更新不涉及数据库更改;您将看到有关部署下一教程中的数据库更改的差异。</span><span class="sxs-lookup"><span data-stu-id="85246-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="85246-114">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="85246-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="85246-115">进行代码更改</span><span class="sxs-lookup"><span data-stu-id="85246-115">Making a Code Change</span></span>

<span data-ttu-id="85246-116">作为对应用程序更新的简单示例，你将添加到**讲师**页由所选讲师的课程列表。</span><span class="sxs-lookup"><span data-stu-id="85246-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="85246-117">如果在运行**讲师**页上，您会注意到，有**选择**链接在网格中，但他们不使以外的任何行背景变灰。</span><span class="sxs-lookup"><span data-stu-id="85246-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="85246-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="85246-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="85246-119">现在，你将添加代码运行时**选择**链接单击，并显示由所选讲师的课程列表。</span><span class="sxs-lookup"><span data-stu-id="85246-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="85246-120">在中*Instructors.aspx*，添加以下标记后立即**ErrorMessageLabel** `Label`控件：</span><span class="sxs-lookup"><span data-stu-id="85246-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="85246-121">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="85246-121">Run the page and select an instructor.</span></span> <span data-ttu-id="85246-122">请参阅由讲师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="85246-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="85246-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="85246-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="85246-124">代码将更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="85246-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="85246-125">部署到测试环境很简单，只需单击一次运行的重新发布。</span><span class="sxs-lookup"><span data-stu-id="85246-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="85246-126">若要使此过程更快，可以使用**Web 单键发布**工具栏。</span><span class="sxs-lookup"><span data-stu-id="85246-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="85246-127">在中**视图**菜单中，选择**工具栏**，然后选择**Web 单键发布**。</span><span class="sxs-lookup"><span data-stu-id="85246-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="85246-129">在中**解决方案资源管理器**，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="85246-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="85246-130">**Web 单键发布**工具栏上，选择**测试**发布配置文件，然后单击**发布 Web** （其箭头指向左侧和右侧的图标）。</span><span class="sxs-lookup"><span data-stu-id="85246-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="85246-132">Visual Studio 部署更新的应用程序，并在主页上会自动打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="85246-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="85246-133">运行讲师页并选择一名讲师，若要验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="85246-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="85246-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="85246-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="85246-135">通常会同样进行回归测试 （也就是说，测试以确保新的更改不会破坏任何现有功能的站点的其余部分）。</span><span class="sxs-lookup"><span data-stu-id="85246-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="85246-136">但对于本教程将跳过该步骤并继续将更新部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="85246-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="85246-137">阻止重新部署到生产环境的初始数据库状态</span><span class="sxs-lookup"><span data-stu-id="85246-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="85246-138">在实际的应用程序，用户在初始部署之后与您的生产站点和数据库填充了实时数据。</span><span class="sxs-lookup"><span data-stu-id="85246-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="85246-139">因此，您不想要重新部署成员资格数据库中所有的实时数据会擦除其初始状态。</span><span class="sxs-lookup"><span data-stu-id="85246-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="85246-140">由于 SQL Server Compact 数据库中的文件*应用程序\_数据*文件夹中，您必须防止出现这种通过更改部署设置，因此，中的文件*应用\_数据*文件夹不被部署。</span><span class="sxs-lookup"><span data-stu-id="85246-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="85246-141">打开**项目属性**ContosoUniversity 项目，然后选择窗口**打包/发布 Web**选项卡。请确保**配置**下拉列表框已**处于活动状态 （发布）** 或**版本**选择，选择**将应用程序中排除文件\_数据文件夹**。</span><span class="sxs-lookup"><span data-stu-id="85246-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="85246-143">如果你决定在将来部署的调试版本，它最好进行调试生成配置的相同的更改： 更改**配置**到**调试**，然后选择**排除应用程序中的文件\_数据文件夹**。</span><span class="sxs-lookup"><span data-stu-id="85246-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="85246-144">保存并关闭**打包/发布 Web**选项卡。</span><span class="sxs-lookup"><span data-stu-id="85246-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="85246-145">请确保不会**删除目标处的其他文件**选择发布配置文件中。</span><span class="sxs-lookup"><span data-stu-id="85246-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="85246-146">如果选择该选项时，部署过程将删除的数据库的应用中有\_中的数据已部署的站点，以及它将删除应用\_数据文件夹本身。</span><span class="sxs-lookup"><span data-stu-id="85246-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>


## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="85246-147">到生产站点更新的过程中阻止用户访问权限</span><span class="sxs-lookup"><span data-stu-id="85246-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="85246-148">要部署的更改现在是单个页面的简单更改。</span><span class="sxs-lookup"><span data-stu-id="85246-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="85246-149">但有时部署较大的更改，并在这种情况下该站点可以出现异常行为如果之前部署完成后，用户请求页面。</span><span class="sxs-lookup"><span data-stu-id="85246-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="85246-150">若要防止此情况，可以使用*应用程序\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="85246-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="85246-151">当将名为的文件*应用程序\_offline.htm*在你的应用程序的根文件夹中，IIS 会自动显示该文件而不是运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="85246-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="85246-152">因此为了防止访问在部署期间，您将放*应用程序\_offline.htm*根文件夹中运行部署过程中，，然后删除*应用\_offline.htm*。</span><span class="sxs-lookup"><span data-stu-id="85246-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="85246-153">在中**解决方案资源管理器**，右键单击该解决方案 （而不是项目的），然后选择**新解决方案文件夹**。</span><span class="sxs-lookup"><span data-stu-id="85246-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="85246-155">将文件夹命名为*SolutionFiles*。</span><span class="sxs-lookup"><span data-stu-id="85246-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="85246-156">在新文件夹中创建名为的 HTML 页*应用程序\_offline.htm*。</span><span class="sxs-lookup"><span data-stu-id="85246-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="85246-157">现有内容替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="85246-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="85246-158">可以将复制*应用程序\_offline.htm*通过使用 FTP 连接的站点的文件或**文件管理器**实用工具托管提供商的控制面板中。</span><span class="sxs-lookup"><span data-stu-id="85246-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="85246-159">对于本教程中，你将使用**文件管理器**。</span><span class="sxs-lookup"><span data-stu-id="85246-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="85246-160">打开控制面板，然后选择**文件管理器**中那样[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="85246-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="85246-161">选择**contosouniversity.com** ，然后**wwwroot**以获取应用程序的根文件夹，然后单击**上载**。</span><span class="sxs-lookup"><span data-stu-id="85246-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="85246-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="85246-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="85246-163">在中**上传文件**对话框中，选择*应用\_offline.htm*文件，然后单击**上载**。</span><span class="sxs-lookup"><span data-stu-id="85246-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="85246-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="85246-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="85246-165">浏览到你网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="85246-165">Browse to your site's URL.</span></span> <span data-ttu-id="85246-166">可以看到*应用程序\_offline.htm*页现在显示而不是您的主页。</span><span class="sxs-lookup"><span data-stu-id="85246-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="85246-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="85246-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="85246-168">现在你现可部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="85246-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="85246-169">代码将更新部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="85246-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="85246-170">在中**Web 单键发布**工具栏上，选择**生产**发布配置文件，然后单击**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="85246-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="85246-171">Visual Studio 部署更新的应用程序和网站的主页上浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="85246-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="85246-172">*应用程序\_offline.htm*显示文件。</span><span class="sxs-lookup"><span data-stu-id="85246-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="85246-173">您可以对其进行测试以验证是否成功的部署之前，必须删除*应用程序\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="85246-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="85246-174">返回到**文件管理器**控制面板中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="85246-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="85246-175">选择**contosouniversity.com**并**wwwroot**，选择**应用\_offline.htm**，然后单击**删除**。</span><span class="sxs-lookup"><span data-stu-id="85246-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="85246-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="85246-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="85246-177">在浏览器中，在公共网站中，打开讲师页并选择讲师来验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="85246-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="85246-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="85246-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="85246-179">现在，你已部署不涉及数据库更改的应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="85246-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="85246-180">下一步的教程演示了如何部署数据库更改。</span><span class="sxs-lookup"><span data-stu-id="85246-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85246-181">[上一页](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="85246-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
