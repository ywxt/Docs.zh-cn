---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3649f0250e830b76c42d832e51038c2c52ed4561
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368209"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="d1ea6-103">使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新</span><span class="sxs-lookup"><span data-stu-id="d1ea6-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>
====================
<span data-ttu-id="d1ea6-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d1ea6-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d1ea6-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="d1ea6-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="d1ea6-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="d1ea6-107">有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="d1ea6-108">概述</span><span class="sxs-lookup"><span data-stu-id="d1ea6-108">Overview</span></span>

<span data-ttu-id="d1ea6-109">在初始部署后持续维护和开发您的网站的工作，并在长时间之前你将想要将更新部署。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="d1ea6-110">本教程将指导你完成更新部署到应用程序代码的过程。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="d1ea6-111">实现和部署本教程中的更新不涉及数据库更改;您将看到有关部署下一教程中的数据库更改的差异。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="d1ea6-112">提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="d1ea6-113">进行代码更改</span><span class="sxs-lookup"><span data-stu-id="d1ea6-113">Make a code change</span></span>

<span data-ttu-id="d1ea6-114">作为对应用程序更新的简单示例，你将添加到**讲师**页由所选讲师的课程列表。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="d1ea6-115">如果在运行**讲师**页上，您会注意到，有**选择**链接在网格中，但他们不使以外的任何行背景变灰。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![选择讲师页](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="d1ea6-117">现在，你将添加代码运行时**选择**链接单击，并显示由所选讲师的课程列表。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="d1ea6-118">在中*Instructors.aspx*，添加以下标记后立即**ErrorMessageLabel** `Label`控件：</span><span class="sxs-lookup"><span data-stu-id="d1ea6-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="d1ea6-119">运行该页并选择讲师。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-119">Run the page and select an instructor.</span></span> <span data-ttu-id="d1ea6-120">请参阅由讲师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-120">You see a list of courses taught by that instructor.</span></span>

    ![使用教授的课程讲师页](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="d1ea6-122">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="d1ea6-123">将代码更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="d1ea6-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="d1ea6-124">可以使用发布配置文件将部署到测试、 过渡和生产环境之前，需要更改数据库的发布选项。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="d1ea6-125">不再需要运行成员资格数据库的授权和数据部署脚本。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="d1ea6-126">打开**发布 Web**右键单击 ContosoUniversity 项目并单击向导**发布**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="d1ea6-127">单击**测试**分析中的**配置文件**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="d1ea6-128">单击**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="d1ea6-129">下**DefaultConnection**中**数据库**部分中，清除**更新数据库**复选框。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="d1ea6-130">单击**配置文件**选项卡，然后依次**过渡**分析中的**配置文件**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="d1ea6-131">当系统询问你是否想要保存所做的更改**测试**配置文件中，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="d1ea6-132">临时配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="d1ea6-133">重复该过程以在生产配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="d1ea6-134">关闭**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="d1ea6-135">部署到测试环境是现在只需运行一次单击即可重新发布。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="d1ea6-136">若要使此过程更快，可以使用**Web 单键发布**工具栏。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="d1ea6-137">在中**视图**菜单中，选择**工具栏**，然后选择**Web 单键发布**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="d1ea6-139">在中**解决方案资源管理器**，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="d1ea6-140">**Web 单键发布**工具栏上，选择**测试**发布配置文件，然后单击**发布 Web** （其箭头指向左侧和右侧的图标）。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="d1ea6-142">Visual Studio 部署更新的应用程序，并在主页上会自动打开浏览器。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="d1ea6-143">运行讲师页并选择一名讲师，若要验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="d1ea6-144">通常会同样进行回归测试 （也就是说，测试以确保新的更改不会破坏任何现有功能的站点的其余部分）。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="d1ea6-145">但对于本教程将跳过该步骤并继续将更新部署到过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="d1ea6-146">时重新部署，Web 部署自动确定哪些文件已更改，并仅将更改为服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="d1ea6-147">默认情况下，Web 部署使用上次更改日期的文件以确定哪些已更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="d1ea6-148">某些源代码管理系统文件更改日期甚至时不要更改该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="d1ea6-149">在这种情况下，你可能想要配置 Web 部署可以使用文件校验和来确定哪些文件已更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="d1ea6-150">有关详细信息，请参阅[为何执行操作的所有文件重新部署虽然我没有改变它们？](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) ASP.NET 部署常见问题解答中。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="d1ea6-151">使应用程序脱机部署过程</span><span class="sxs-lookup"><span data-stu-id="d1ea6-151">Take the application offline during deployment</span></span>

<span data-ttu-id="d1ea6-152">要部署的更改现在是单个页面的简单更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="d1ea6-153">但有时您部署较大的更改，或部署代码和数据库更改，以及站点可能会出现错误的行为之前部署完成后，用户请求页面时。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="d1ea6-154">若要防止用户访问站点，在进行部署时，可以使用*应用程序\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="d1ea6-155">当将名为的文件*应用程序\_offline.htm*在你的应用程序的根文件夹中，IIS 会自动显示该文件而不是运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="d1ea6-156">因此为了防止访问在部署期间，您将放*应用程序\_offline.htm*根文件夹中运行部署过程中，，然后删除*应用\_offline.htm*后成功部署。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="d1ea6-157">你可以配置 Web 部署以将默认值自动*应用程序\_offline.htm*启动部署时在服务器上的文件并将在它完成后将其删除。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="d1ea6-158">若要执行所有您只需是下面的 XML 元素添加到发布配置文件 (.pubxml) 文件：</span><span class="sxs-lookup"><span data-stu-id="d1ea6-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="d1ea6-159">对于本教程中，您将看到如何创建和使用自定义*应用程序\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="d1ea6-160">使用*应用程序\_offline.htm*暂存网站中不是必需的因为你没有访问暂存站点的用户。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="d1ea6-161">但最好使用暂存所有内容测试你计划在生产环境中部署的方式。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-appofflinehtm"></a><span data-ttu-id="d1ea6-162">创建应用\_offline.htm</span><span class="sxs-lookup"><span data-stu-id="d1ea6-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="d1ea6-163">在中**解决方案资源管理器**，右键单击该解决方案，然后单击**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="d1ea6-164">创建**HTML 页面**名为*应用\_offline.htm* (在删除最后一个"l" *.html*扩展 Visual Studio 将创建默认情况下)。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="d1ea6-165">模板标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="d1ea6-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="d1ea6-166">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-166">Save and close the file.</span></span>

### <a name="copy-appofflinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="d1ea6-167">复制应用\_offline.htm web 站点的根文件夹</span><span class="sxs-lookup"><span data-stu-id="d1ea6-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="d1ea6-168">可以使用任何 FTP 工具将文件复制到该网站。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="d1ea6-169">[FileZilla](http://filezilla-project.org/)是 FTP 工具和屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="d1ea6-170">若要使用 FTP 工具，需要以下三项： FTP URL、 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="d1ea6-171">URL 显示在网站的仪表板页上，在 Azure 管理门户中，并可以中找到用户名和密码 FTP *.publishsettings*前面下载的文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="d1ea6-172">以下步骤演示如何获取这些值。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="d1ea6-173">在 Azure 管理门户中，单击**网站**选项卡，然后单击过渡 web 站点。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="d1ea6-174">上**仪表板**页上，向下滚动到的 FTP 主机名中查找**速览**部分。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 主机名](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="d1ea6-176">打开暂存 *.publishsettings*在记事本或其他文本编辑器中的文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="d1ea6-177">查找`publishProfile`FTP 配置文件的元素。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="d1ea6-178">复制`userName`和`userPWD`值。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 凭据](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="d1ea6-180">打开你的 FTP 工具和登录到 FTP URL。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="d1ea6-181">复制*应用程序\_offline.htm*到解决方案文件夹从 */site/wwwroot*过渡站点中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![复制 app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="d1ea6-183">浏览到将过渡站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="d1ea6-184">可以看到*应用程序\_offline.htm*页现在显示而不是您的主页。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![在浏览器窗口 app_offline.htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="d1ea6-186">现在你现可部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="d1ea6-187">将代码更新部署到过渡和生产</span><span class="sxs-lookup"><span data-stu-id="d1ea6-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="d1ea6-188">在中**Web 单键发布**工具栏上，选择**过渡**发布配置文件，然后单击**发布 Web**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="d1ea6-189">Visual Studio 部署更新的应用程序和网站的主页上浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="d1ea6-190">*应用程序\_offline.htm*显示文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="d1ea6-191">您可以对其进行测试以验证是否成功的部署之前，必须删除*应用程序\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="d1ea6-192">返回到您的 FTP 工具，并删除**应用程序\_offline.htm**从过渡站点。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="d1ea6-193">在浏览器中的临时站点，打开讲师页并选择讲师来验证已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="d1ea6-194">相同的步骤用于生产之前用于过渡。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="d1ea6-195">查看更改和部署特定的文件</span><span class="sxs-lookup"><span data-stu-id="d1ea6-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="d1ea6-196">Visual Studio 2012 还提供了部署单独的文件的能力。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="d1ea6-197">所选文件可以查看本地版本和已部署的版本之间的差异、 将文件部署到目标环境中，或从目标环境将文件复制到本地项目。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="d1ea6-198">在本教程的本部分中，您将看到如何使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="d1ea6-199">若要部署更改</span><span class="sxs-lookup"><span data-stu-id="d1ea6-199">Make a change to deploy</span></span>

1. <span data-ttu-id="d1ea6-200">打开*Content/Site.css*，并查找的块`body`标记。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="d1ea6-201">更改的值`background-color`从`#fff`到`darkblue`。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="d1ea6-202">在发布预览窗口中查看更改</span><span class="sxs-lookup"><span data-stu-id="d1ea6-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="d1ea6-203">当你使用**发布 Web**向导以发布该项目，您可以看到更改要发布的中双击该文件**预览**窗口。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="d1ea6-204">右键单击 ContosoUniversity 项目，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="d1ea6-205">从**配置文件**下拉列表中，选择**测试**发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="d1ea6-206">单击**预览版**，然后单击**开始预览**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="d1ea6-207">在中**预览版**窗格中，双击**Site.css**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![双击 Site.css](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="d1ea6-209">**预览更改**对话框显示的更改将在其中部署预览。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![对 Site.css 预览更改](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="d1ea6-211">如果您双击*Web.config*文件中，**预览更改**对话框显示了生成的效果配置转换和发布配置文件转换。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="d1ea6-212">此时你尚未这样做会导致的任何内容*Web.config*若要更改，因此您会不看到任何更改在服务器上的文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="d1ea6-213">但是，**预览更改**窗口错误地显示了两项更改。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="d1ea6-214">看起来，将删除两个 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="d1ea6-215">当您选择，发布过程会添加这些元素**执行 Code First 迁移应用程序启动**Code First 的上下文类。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="d1ea6-216">发布过程添加这些元素，因此看起来，尽管它们不会删除要被删除之前进行比较。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="d1ea6-217">将在将来的版本中更正此错误。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="d1ea6-218">单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-218">Click **Close**.</span></span>
6. <span data-ttu-id="d1ea6-219">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-219">Click **Publish**.</span></span>
7. <span data-ttu-id="d1ea6-220">当浏览器打开到测试站点的主页上时，按 CTRL + F5 来硬刷新才能看到 CSS 更改的效果。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 更改的效果](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="d1ea6-222">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="d1ea6-223">发布解决方案资源管理器中的特定文件</span><span class="sxs-lookup"><span data-stu-id="d1ea6-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="d1ea6-224">假设不喜欢蓝色背景，并想要恢复为原始的颜色。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="d1ea6-225">在本部分中，您将恢复原始设置通过直接从特定文件发布**解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="d1ea6-226">打开*Content/Site.css*和还原`background-color`设置为`#fff`。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="d1ea6-227">在中**解决方案资源管理器**，右键单击*Content/Site.css*文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="d1ea6-228">上下文菜单显示了三个发布选项。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-228">The context menu shows three publish options.</span></span>

    ![发布解决方案资源管理器选项](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="d1ea6-230">单击**预览更改为 Site.css**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="d1ea6-231">窗口将打开以显示目标环境中的本地文件和它的版本之间的差异。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="d1ea6-233">在中**解决方案资源管理器**，右键单击**Site.css**再次单击**发布 Site.css**。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="d1ea6-234">**Web 发布活动**窗口将显示已发布文件。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Web 发布活动窗口](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="d1ea6-236">浏览器中打开`http://localhost/contosouniversity`URL，然后按 CTRL + F5 来导致一种较难刷新才能查看更改的 CSS 的效果。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![使用普通 CSS 的主页](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="d1ea6-238">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="d1ea6-239">总结</span><span class="sxs-lookup"><span data-stu-id="d1ea6-239">Summary</span></span>

<span data-ttu-id="d1ea6-240">现在，已了解多种方式来部署应用程序更新不涉及数据库更改，并已了解如何预览更改后，若要验证，将更新的内容是你期望的内容。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="d1ea6-241">讲师页现在具有**讲授课程**部分。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-241">The Instructors page now has a **Courses Taught** section.</span></span>

![使用教授的课程讲师页](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="d1ea6-243">下一步的教程演示如何部署数据库更改： 将将 birthdate 字段添加到数据库和讲师页。</span><span class="sxs-lookup"><span data-stu-id="d1ea6-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1ea6-244">[上一页](deploying-to-production.md)
> [下一页](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="d1ea6-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
