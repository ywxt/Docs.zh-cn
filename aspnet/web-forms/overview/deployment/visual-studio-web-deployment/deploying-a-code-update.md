---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: "使用 Visual Studio 的 ASP.NET Web 部署： 部署某一代码更新 |Microsoft 文档"
author: tdykstra
description: "本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: f6861c702c1ccb19e5a4eee484a622079e205f86
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="5b137-103">使用 Visual Studio 的 ASP.NET Web 部署： 部署某一代码更新</span><span class="sxs-lookup"><span data-stu-id="5b137-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>
====================
<span data-ttu-id="5b137-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5b137-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="5b137-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="5b137-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="5b137-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="5b137-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="5b137-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5b137-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="5b137-108">概述</span><span class="sxs-lookup"><span data-stu-id="5b137-108">Overview</span></span>

<span data-ttu-id="5b137-109">在初始部署后维护和开发您的网站的工作仍然存在，并且在长时间之前你将想要将更新部署。</span><span class="sxs-lookup"><span data-stu-id="5b137-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="5b137-110">本教程将指导您完成将更新部署到你的应用程序代码的过程。</span><span class="sxs-lookup"><span data-stu-id="5b137-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="5b137-111">实现和部署在本教程中的更新不涉及数据库更改;你将看到有关部署下一教程中的数据库更改的差异。</span><span class="sxs-lookup"><span data-stu-id="5b137-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="5b137-112">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="5b137-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="5b137-113">进行代码更改</span><span class="sxs-lookup"><span data-stu-id="5b137-113">Make a code change</span></span>

<span data-ttu-id="5b137-114">为你的应用程序到更新的简单示例，你将添加到**教师**页上通过所选教师讲授的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="5b137-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="5b137-115">如果你运行**教师**页上，你会注意到没有**选择**链接在网格中，但它们不执行任何操作生成以外行背景变灰。</span><span class="sxs-lookup"><span data-stu-id="5b137-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![选择教师页](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="5b137-117">现在你将添加时运行的代码**选择**链接单击，并显示由所选教师讲授的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="5b137-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="5b137-118">在*Instructors.aspx*，添加以下标记后立即**ErrorMessageLabel** `Label`控件：</span><span class="sxs-lookup"><span data-stu-id="5b137-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="5b137-119">运行页面，然后选择一个教师。</span><span class="sxs-lookup"><span data-stu-id="5b137-119">Run the page and select an instructor.</span></span> <span data-ttu-id="5b137-120">你看到通过该教师讲授的课程的列表。</span><span class="sxs-lookup"><span data-stu-id="5b137-120">You see a list of courses taught by that instructor.</span></span>

    ![讲授的课程教师页](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="5b137-122">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="5b137-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="5b137-123">将代码更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="5b137-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="5b137-124">你可以使用发布配置文件将部署到测试、 过渡和生产之前，你需要更改数据库发布选项。</span><span class="sxs-lookup"><span data-stu-id="5b137-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="5b137-125">不再需要运行用于成员资格数据库的 grant 和数据部署脚本。</span><span class="sxs-lookup"><span data-stu-id="5b137-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="5b137-126">打开**发布 Web**向导通过右键单击 ContosoUniversity 项目并单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="5b137-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="5b137-127">单击**测试**在配置文件中**配置文件**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="5b137-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="5b137-128">单击**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="5b137-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="5b137-129">下**DefaultConnection**中**数据库**部分中，清除**更新数据库**复选框。</span><span class="sxs-lookup"><span data-stu-id="5b137-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="5b137-130">单击**配置文件**选项卡上，并依次**过渡**在配置文件中**配置文件**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="5b137-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="5b137-131">当系统询问你是否要保存到所做的更改**测试**配置文件，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="5b137-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="5b137-132">临时配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="5b137-133">重复此过程以生产配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="5b137-134">关闭**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="5b137-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="5b137-135">部署到测试环境，现在运行一次单击即可重新发布。</span><span class="sxs-lookup"><span data-stu-id="5b137-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="5b137-136">若要使此过程更快，可以使用**Web 单键发布**工具栏。</span><span class="sxs-lookup"><span data-stu-id="5b137-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="5b137-137">在**视图**菜单上，选择**工具栏**，然后选择**Web 单键发布**。</span><span class="sxs-lookup"><span data-stu-id="5b137-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="5b137-139">在**解决方案资源管理器**，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="5b137-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="5b137-140">**Web 单键发布**工具栏上，选择**测试**发布配置文件，然后单击**发布 Web** （带有箭头指向左侧和右侧的图标）。</span><span class="sxs-lookup"><span data-stu-id="5b137-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="5b137-142">Visual Studio 部署更新的应用程序，并浏览器将自动打开到主页。</span><span class="sxs-lookup"><span data-stu-id="5b137-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="5b137-143">运行教师页并选择一个教师以验证更新成功部署。</span><span class="sxs-lookup"><span data-stu-id="5b137-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="5b137-144">你通常会还执行回归测试 （即，测试站点后，若要确保新的更改不中断任何现有功能的其余部分）。</span><span class="sxs-lookup"><span data-stu-id="5b137-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="5b137-145">但对于本教程将跳过该步骤并继续将更新部署到过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="5b137-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="5b137-146">当重新部署时，Web 部署自动确定哪些文件已更改，以及仅副本更改为服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="5b137-147">默认情况下，Web 部署使用上次更改日期上文件来确定哪些功能已更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="5b137-148">在不更改文件内容时，某些源代码管理系统将更改文件甚至的日期。</span><span class="sxs-lookup"><span data-stu-id="5b137-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="5b137-149">在这种情况下，你可能想要配置 Web Deploy 以使用文件校验和以确定哪些文件已更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="5b137-150">有关详细信息，请参阅[为什么执行所有我的文件获取重新部署未更改其虽然？](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 部署常见问题中。</span><span class="sxs-lookup"><span data-stu-id="5b137-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="5b137-151">使应用程序脱机在部署过程</span><span class="sxs-lookup"><span data-stu-id="5b137-151">Take the application offline during deployment</span></span>

<span data-ttu-id="5b137-152">要部署的更改现在是对单个页面的简单更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="5b137-153">但有时你部署较大的更改，或部署代码和数据库的更改，以及如果用户请求页，在部署完成之前，该站点可能会错误地那样。</span><span class="sxs-lookup"><span data-stu-id="5b137-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="5b137-154">若要防止用户访问站点，正在进行部署时，可以使用*应用\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="5b137-155">当将一个名为文件*应用\_offline.htm*在你的应用程序根文件夹中，IIS 会自动显示该文件而不是运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5b137-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="5b137-156">因此，若要在部署过程中阻止访问，你将*应用\_offline.htm*在根文件夹中，运行在部署过程，然后删除*应用\_offline.htm*后成功部署。</span><span class="sxs-lookup"><span data-stu-id="5b137-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="5b137-157">你可以配置 Web 部署以将默认自动*应用\_offline.htm*启动部署时服务器上的文件并将其删除完成时。</span><span class="sxs-lookup"><span data-stu-id="5b137-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="5b137-158">若要执行所有您需要做即可将下面的 XML 元素添加到你的发布配置文件 (.pubxml) 文件：</span><span class="sxs-lookup"><span data-stu-id="5b137-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="5b137-159">对于本教程中，你将看到如何创建和使用自定义*应用\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="5b137-160">使用*应用\_offline.htm*中的暂存站点不是必需的因为你不具有访问暂存站点的用户。</span><span class="sxs-lookup"><span data-stu-id="5b137-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="5b137-161">但作为最佳做法，使用临时测试的所有内容你打算在生产中部署的方式。</span><span class="sxs-lookup"><span data-stu-id="5b137-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-appofflinehtm"></a><span data-ttu-id="5b137-162">创建应用\_offline.htm</span><span class="sxs-lookup"><span data-stu-id="5b137-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="5b137-163">在**解决方案资源管理器**，右键单击该解决方案，然后单击**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="5b137-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="5b137-164">创建**HTML 页**名为*应用\_offline.htm* (中删除最后一个"l" *.html*扩展 Visual Studio 将创建默认情况下)。</span><span class="sxs-lookup"><span data-stu-id="5b137-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="5b137-165">将模板标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="5b137-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="5b137-166">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-166">Save and close the file.</span></span>

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="5b137-167">复制应用\_offline.htm 到网站的根文件夹</span><span class="sxs-lookup"><span data-stu-id="5b137-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="5b137-168">你可以使用任何 FTP 工具将文件复制到网站。</span><span class="sxs-lookup"><span data-stu-id="5b137-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="5b137-169">[FileZilla](http://filezilla-project.org/)是 FTP 工具和屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="5b137-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="5b137-170">若要使用 FTP 工具，需要以下三项： FTP URL、 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="5b137-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="5b137-171">URL 将显示在网站的仪表板页上，在 Azure 管理门户中，并且可以在中找到的用户名和密码 FTP *.publishsettings*前面下载的文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="5b137-172">以下步骤演示如何获取这些值。</span><span class="sxs-lookup"><span data-stu-id="5b137-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="5b137-173">在 Azure 管理门户中，单击**网站**选项卡，然后单击过渡网站。</span><span class="sxs-lookup"><span data-stu-id="5b137-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="5b137-174">上**仪表板**页上，向下滚动到的 FTP 主机中的名称的查找**速览**部分。</span><span class="sxs-lookup"><span data-stu-id="5b137-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 主机名](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="5b137-176">打开过渡*.publishsettings*在记事本或其他文本编辑器中的文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="5b137-177">查找`publishProfile`FTP 配置文件的元素。</span><span class="sxs-lookup"><span data-stu-id="5b137-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="5b137-178">复制`userName`和`userPWD`值。</span><span class="sxs-lookup"><span data-stu-id="5b137-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 凭据](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="5b137-180">打开你的 FTP 工具并登录到 FTP URL。</span><span class="sxs-lookup"><span data-stu-id="5b137-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="5b137-181">复制*应用\_offline.htm*解决方案文件夹中找到到*/站点/wwwroot*文件夹中的暂存站点。</span><span class="sxs-lookup"><span data-stu-id="5b137-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![复制 app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="5b137-183">浏览到暂存站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="5b137-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="5b137-184">你看到*应用\_offline.htm*页现在显示而不是你的主页。</span><span class="sxs-lookup"><span data-stu-id="5b137-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![在浏览器窗口的 app_offline.htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="5b137-186">现在你就可以部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="5b137-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="5b137-187">将代码更新部署到过渡和生产</span><span class="sxs-lookup"><span data-stu-id="5b137-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="5b137-188">在**Web 单键发布**工具栏上，选择**过渡**发布配置文件，然后单击**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="5b137-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="5b137-189">Visual Studio 将部署更新的应用程序，并打开浏览器向站点的主页。</span><span class="sxs-lookup"><span data-stu-id="5b137-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="5b137-190">*应用\_offline.htm*显示文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="5b137-191">你可以对其进行测试以验证是否成功的部署之前，必须删除*应用\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="5b137-192">返回到你的 FTP 工具，并删除**应用\_offline.htm**从暂存站点。</span><span class="sxs-lookup"><span data-stu-id="5b137-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="5b137-193">在浏览器中，在过渡站点中，打开教师页，然后选择一个教师以验证更新成功部署。</span><span class="sxs-lookup"><span data-stu-id="5b137-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="5b137-194">就像过渡，请按照生产同样的过程。</span><span class="sxs-lookup"><span data-stu-id="5b137-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="5b137-195">查看更改并部署特定的文件</span><span class="sxs-lookup"><span data-stu-id="5b137-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="5b137-196">Visual Studio 2012 还为你提供了部署单独的文件的功能。</span><span class="sxs-lookup"><span data-stu-id="5b137-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="5b137-197">选中的文件中，你可以查看本地版本和已部署的版本之间的差异、 将文件部署到目标环境中，或目标环境中的文件复制到本地项目。</span><span class="sxs-lookup"><span data-stu-id="5b137-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="5b137-198">在本教程的本部分中，你将看到如何使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="5b137-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="5b137-199">若要部署更改</span><span class="sxs-lookup"><span data-stu-id="5b137-199">Make a change to deploy</span></span>

1. <span data-ttu-id="5b137-200">打开*Content/Site.css*，并找到的块`body`标记。</span><span class="sxs-lookup"><span data-stu-id="5b137-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="5b137-201">值更改`background-color`从`#fff`到`darkblue`。</span><span class="sxs-lookup"><span data-stu-id="5b137-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="5b137-202">在发布预览窗口中查看更改</span><span class="sxs-lookup"><span data-stu-id="5b137-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="5b137-203">当你使用**发布 Web**向导以发布该项目，你可以查看更改是否要通过双击中的文件发布**预览**窗口。</span><span class="sxs-lookup"><span data-stu-id="5b137-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="5b137-204">右键单击 ContosoUniversity 项目并单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="5b137-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="5b137-205">从**配置文件**下拉列表中，选择**测试**发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="5b137-206">单击**预览**，然后单击**开始预览**。</span><span class="sxs-lookup"><span data-stu-id="5b137-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="5b137-207">在**预览**窗格中，双击**Site.css**。</span><span class="sxs-lookup"><span data-stu-id="5b137-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![双击 Site.css](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="5b137-209">**预览更改**对话框显示预览将部署的更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![预览更改为 Site.css](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="5b137-211">如果双击*Web.config*文件，**预览更改**对话框显示配置转换的生成的效果和发布配置文件转换。</span><span class="sxs-lookup"><span data-stu-id="5b137-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="5b137-212">此时你尚未这样做将导致的任何内容*Web.config*要发生变化，因此你会不看到任何更改的服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="5b137-213">但是，**预览更改**窗口错误地将显示两个更改。</span><span class="sxs-lookup"><span data-stu-id="5b137-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="5b137-214">看起来，将删除两个 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="5b137-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="5b137-215">这些元素添加发布过程中，当你选择**执行 Code First 迁移应用程序启动**Code First 的上下文类。</span><span class="sxs-lookup"><span data-stu-id="5b137-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="5b137-216">在发布过程添加这些元素，以便看起来，尽管它们不会删除它们要删除之前进行比较。</span><span class="sxs-lookup"><span data-stu-id="5b137-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="5b137-217">未来版本中，将更正此错误。</span><span class="sxs-lookup"><span data-stu-id="5b137-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="5b137-218">单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="5b137-218">Click **Close**.</span></span>
6. <span data-ttu-id="5b137-219">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="5b137-219">Click **Publish**.</span></span>
7. <span data-ttu-id="5b137-220">当浏览器打开到测试站点主页后时，按 CTRL + F5 才能看到 CSS 更改的效果导致硬刷新。</span><span class="sxs-lookup"><span data-stu-id="5b137-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 更改效果](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="5b137-222">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="5b137-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="5b137-223">将特定文件从解决方案资源管理器发布</span><span class="sxs-lookup"><span data-stu-id="5b137-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="5b137-224">假设你不喜欢背景是蓝色，并且想要还原到原始的颜色。</span><span class="sxs-lookup"><span data-stu-id="5b137-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="5b137-225">在本部分中，你将还原原始设置通过发布特定文件直接从**解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="5b137-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="5b137-226">打开*Content/Site.css*和还原`background-color`将设置为`#fff`。</span><span class="sxs-lookup"><span data-stu-id="5b137-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="5b137-227">在**解决方案资源管理器**，右键单击*Content/Site.css*文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="5b137-228">上下文菜单显示三个发布选项。</span><span class="sxs-lookup"><span data-stu-id="5b137-228">The context menu shows three publish options.</span></span>

    ![发布解决方案资源管理器选项](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="5b137-230">单击**预览更改为 Site.css**。</span><span class="sxs-lookup"><span data-stu-id="5b137-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="5b137-231">窗口将打开以显示在目标环境中的本地文件和它的版本之间的差异。</span><span class="sxs-lookup"><span data-stu-id="5b137-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="5b137-233">在**解决方案资源管理器**，右键单击**Site.css**再次单击**发布 Site.css**。</span><span class="sxs-lookup"><span data-stu-id="5b137-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="5b137-234">**Web 发布活动**窗口显示已发布文件。</span><span class="sxs-lookup"><span data-stu-id="5b137-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Web 发布活动窗口](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="5b137-236">浏览器中打开`http://localhost/contosouniversity`URL，，然后按 CTRL + F5 可导致硬刷新才能查看更改的 css 的效果。</span><span class="sxs-lookup"><span data-stu-id="5b137-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![正常的 CSS 附带的主页](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="5b137-238">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="5b137-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="5b137-239">摘要</span><span class="sxs-lookup"><span data-stu-id="5b137-239">Summary</span></span>

<span data-ttu-id="5b137-240">现在，你已了解通过多种方式来部署应用程序更新不包含数据库更改，并已了解如何预览更改以验证将更新的内容符合预期。</span><span class="sxs-lookup"><span data-stu-id="5b137-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="5b137-241">现在，教师页面包含**课程讲授**部分。</span><span class="sxs-lookup"><span data-stu-id="5b137-241">The Instructors page now has a **Courses Taught** section.</span></span>

![讲授的课程教师页](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="5b137-243">下一教程演示如何将数据库更改部署： 到数据库和教师页，你将添加的出生日期字段。</span><span class="sxs-lookup"><span data-stu-id="5b137-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="5b137-244">[上一页](deploying-to-production.md)
[下一页](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="5b137-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
