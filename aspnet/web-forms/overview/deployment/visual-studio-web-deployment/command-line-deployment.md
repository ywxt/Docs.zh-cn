---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: f079beabccd253ff13c19d3192181ddbdf00b3bf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830962"
---
<a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="91078-103">使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署</span><span class="sxs-lookup"><span data-stu-id="91078-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>
====================
<span data-ttu-id="91078-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="91078-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="91078-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="91078-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="91078-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="91078-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="91078-107">有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="91078-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="91078-108">概述</span><span class="sxs-lookup"><span data-stu-id="91078-108">Overview</span></span>

<span data-ttu-id="91078-109">本教程演示如何调用 Visual Studio web 发布管道从命令行。</span><span class="sxs-lookup"><span data-stu-id="91078-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="91078-110">这可用于方案，即向[自动执行部署过程](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)而不手动完成 Visual Studio 中，通常通过使用[源代码版本控制系统](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="91078-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="91078-111">若要部署更改</span><span class="sxs-lookup"><span data-stu-id="91078-111">Make a change to deploy</span></span>

<span data-ttu-id="91078-112">当前关于页面显示的模板代码。</span><span class="sxs-lookup"><span data-stu-id="91078-112">Currently the About page displays the template code.</span></span>

![有关使用模板代码页](command-line-deployment/_static/image1.png)

<span data-ttu-id="91078-114">您将替换为用于显示摘要学生注册代码。</span><span class="sxs-lookup"><span data-stu-id="91078-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="91078-115">打开*About.aspx*页上，删除所有标记内`MainContent``Content`元素，并插入其原位置中的以下标记：</span><span class="sxs-lookup"><span data-stu-id="91078-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="91078-116">运行该项目并选择**有关**页。</span><span class="sxs-lookup"><span data-stu-id="91078-116">Run the project and select the **About** page.</span></span>

![“关于”页面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="91078-118">通过使用命令行部署到测试</span><span class="sxs-lookup"><span data-stu-id="91078-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="91078-119">您不会部署另一个数据库更改，因此禁用 dbDacFx 数据库部署为 aspnet ContosoUniversity 数据库。</span><span class="sxs-lookup"><span data-stu-id="91078-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="91078-120">打开**发布 Web**向导，以及在这三个发布配置文件，清除**更新数据库**上的复选框**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="91078-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="91078-121">在 Windows 8 启动页上，搜索**VS2012 的开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="91078-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="91078-122">右键单击图标**VS2012 的开发人员命令提示**然后单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="91078-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="91078-123">输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件的路径：</span><span class="sxs-lookup"><span data-stu-id="91078-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="91078-124">MSBuild 生成解决方案，并将其部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="91078-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![命令行输出](command-line-deployment/_static/image3.png)

<span data-ttu-id="91078-126">打开浏览器并转到`http://localhost/ContosoUniversity`，然后单击**有关**页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="91078-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="91078-127">如果在测试中尚未创建任何学生，则会看到下的一个空白页面**学生正文统计信息**标题。</span><span class="sxs-lookup"><span data-stu-id="91078-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="91078-128">转到**学生**页上，单击**添加学生**，并添加一些学生，并返回到**有关**页以查看学生统计信息。</span><span class="sxs-lookup"><span data-stu-id="91078-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![有关在测试环境中的页面](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="91078-130">密钥的命令行选项</span><span class="sxs-lookup"><span data-stu-id="91078-130">Key command line options</span></span>

<span data-ttu-id="91078-131">您输入的命令传递到 MSBuild 解决方案文件路径和两个属性：</span><span class="sxs-lookup"><span data-stu-id="91078-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="91078-132">部署与部署的各个项目的解决方案</span><span class="sxs-lookup"><span data-stu-id="91078-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="91078-133">指定解决方案文件中要生成该解决方案将导致所有项目。</span><span class="sxs-lookup"><span data-stu-id="91078-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="91078-134">如果解决方案中有多个 web 项目，以下 MSBuild 行为适用：</span><span class="sxs-lookup"><span data-stu-id="91078-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="91078-135">在命令行指定的属性将传递给每个项目。</span><span class="sxs-lookup"><span data-stu-id="91078-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="91078-136">因此，每个 web 项目必须具有与你指定的名称的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="91078-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="91078-137">如果指定`/p:PublishProfile=Test`，每个 web 项目必须具有名为的发布配置文件*测试*。</span><span class="sxs-lookup"><span data-stu-id="91078-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="91078-138">甚至不会生成另一个时，您可能已成功发布一个项目。</span><span class="sxs-lookup"><span data-stu-id="91078-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="91078-139">有关详细信息，请参阅 stackoverflow 线程[MSBuild 失败，出现两个包](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。</span><span class="sxs-lookup"><span data-stu-id="91078-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="91078-140">如果指定单个项目而不是一种解决方案，您必须添加一个参数，指定 Visual Studio 的版本。</span><span class="sxs-lookup"><span data-stu-id="91078-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="91078-141">如果你正在使用 Visual Studio 2012 命令行应类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="91078-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="91078-142">Visual Studio 2010 版本的版本号是 10.0。</span><span class="sxs-lookup"><span data-stu-id="91078-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="91078-143">有关详细信息，请参阅[Visual Studio 项目兼容性和 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi 的博客上。</span><span class="sxs-lookup"><span data-stu-id="91078-143">For more information, see [Visual Studio project compatability and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="91078-144">指定发布配置文件</span><span class="sxs-lookup"><span data-stu-id="91078-144">Specifying the publish profile</span></span>

<span data-ttu-id="91078-145">按名称或完整路径，可以指定发布配置文件 *.pubxml*文件，在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="91078-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="91078-146">Web 发布所支持的命令行发布方法</span><span class="sxs-lookup"><span data-stu-id="91078-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="91078-147">三个发布方法支持用于命令行发布：</span><span class="sxs-lookup"><span data-stu-id="91078-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="91078-148">`MSDeploy` -使用 Web 部署发布。</span><span class="sxs-lookup"><span data-stu-id="91078-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="91078-149">`Package` -通过创建 Web 部署包发布。</span><span class="sxs-lookup"><span data-stu-id="91078-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="91078-150">您必须单独安装包，从创建它的 MSBuild 命令。</span><span class="sxs-lookup"><span data-stu-id="91078-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="91078-151">`FileSystem` -通过将文件复制到指定的文件夹来发布。</span><span class="sxs-lookup"><span data-stu-id="91078-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="91078-152">指定生成配置和平台</span><span class="sxs-lookup"><span data-stu-id="91078-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="91078-153">在 Visual Studio 或命令行上，必须设置生成配置和平台。</span><span class="sxs-lookup"><span data-stu-id="91078-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="91078-154">发布配置文件还包括命名的属性`LastUsedBuildConfiguration`和`LastUsedPlatform`，但不能设置这些属性以确定如何生成该项目。</span><span class="sxs-lookup"><span data-stu-id="91078-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="91078-155">有关详细信息，请参阅[MSBuild： 如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)Sayed Hashimi 的博客上。</span><span class="sxs-lookup"><span data-stu-id="91078-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="91078-156">部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="91078-156">Deploy to staging</span></span>

<span data-ttu-id="91078-157">若要部署到 Azure，必须将密码添加到命令行中。</span><span class="sxs-lookup"><span data-stu-id="91078-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="91078-158">如果您在 Visual Studio 中发布配置文件中保存了密码，它存储在加密表单中您 *.pubxml 用户*文件。</span><span class="sxs-lookup"><span data-stu-id="91078-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="91078-159">当进行命令行部署，因此您必须在密码命令行参数中传递时，MSBuild 不访问该文件。</span><span class="sxs-lookup"><span data-stu-id="91078-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="91078-160">复制从所需的密码 *.publishsettings*前面为过渡网站下载的文件。</span><span class="sxs-lookup"><span data-stu-id="91078-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="91078-161">密码为的值`userPWD`属性用于 Web 部署`publishProfile`元素。</span><span class="sxs-lookup"><span data-stu-id="91078-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web 部署密码](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="91078-163">在 Windows 8 启动页上，搜索**VS2012 的开发人员命令提示**，并单击图标以打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="91078-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="91078-164">（您无需打开它以管理员身份这一次因为你不部署到 IIS 在本地计算机上。）</span><span class="sxs-lookup"><span data-stu-id="91078-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="91078-165">输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件并将密码与你的密码的路径：</span><span class="sxs-lookup"><span data-stu-id="91078-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="91078-166">请注意，此命令行包含一个额外的参数： `/p:AllowUntrustedCertificate=true`。</span><span class="sxs-lookup"><span data-stu-id="91078-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="91078-167">本教程是在编写，`AllowUntrustedCertificate`时从命令行发布到 Azure，必须设置属性。</span><span class="sxs-lookup"><span data-stu-id="91078-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="91078-168">当发布此 bug 的修复程序后时，你不需要该参数。</span><span class="sxs-lookup"><span data-stu-id="91078-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="91078-169">打开浏览器并转到将过渡站点的 URL，然后单击**有关**页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="91078-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="91078-170">如上文针对测试环境中，您可能需要创建一些学生上查看统计信息**有关**页。</span><span class="sxs-lookup"><span data-stu-id="91078-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="91078-171">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="91078-171">Deploy to production</span></span>

<span data-ttu-id="91078-172">部署到生产环境的过程是类似于过渡的过程。</span><span class="sxs-lookup"><span data-stu-id="91078-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="91078-173">复制从所需的密码 *.publishsettings*前面为生产 web 站点下载的文件。</span><span class="sxs-lookup"><span data-stu-id="91078-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="91078-174">打开**VS2012 的开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="91078-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="91078-175">输入以下命令在命令提示符下，解决方案文件的路径替换为您的解决方案文件并将密码与你的密码的路径：</span><span class="sxs-lookup"><span data-stu-id="91078-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="91078-176">对于实际的生产站点，如果还没有数据库更改，通常复制*应用程序\_offline.htm*到部署之前站点文件，并成功部署后将其删除。</span><span class="sxs-lookup"><span data-stu-id="91078-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="91078-177">打开浏览器并转到将过渡站点的 URL，然后单击**有关**页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="91078-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="91078-178">总结</span><span class="sxs-lookup"><span data-stu-id="91078-178">Summary</span></span>

<span data-ttu-id="91078-179">现已通过使用命令行部署应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="91078-179">You have now deployed an application update by using the command line.</span></span>

![有关在测试环境中的页面](command-line-deployment/_static/image6.png)

<span data-ttu-id="91078-181">在下一步的教程中，你将看到举例说明如何扩展 web 发布管道。</span><span class="sxs-lookup"><span data-stu-id="91078-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="91078-182">该示例将演示如何部署项目中不包含的文件。</span><span class="sxs-lookup"><span data-stu-id="91078-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="91078-183">[上一页](deploying-a-database-update.md)
> [下一页](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="91078-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
