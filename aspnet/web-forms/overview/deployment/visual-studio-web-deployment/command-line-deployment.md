---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: acc4a0e7f4744a3759b90e0f1b159da68b7c7362
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890523"
---
<a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="20f4d-103">使用 Visual Studio 的 ASP.NET Web 部署： 命令行部署</span><span class="sxs-lookup"><span data-stu-id="20f4d-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>
====================
<span data-ttu-id="20f4d-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="20f4d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="20f4d-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="20f4d-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="20f4d-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="20f4d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="20f4d-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="20f4d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="20f4d-108">概述</span><span class="sxs-lookup"><span data-stu-id="20f4d-108">Overview</span></span>

<span data-ttu-id="20f4d-109">本教程演示如何调用 Visual Studio web 发布管道从命令行。</span><span class="sxs-lookup"><span data-stu-id="20f4d-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="20f4d-110">这是适用于方案中，你希望[自动执行部署过程](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)而不要手动 Visual Studio 中，通常通过使用[源代码版本控制系统中](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="20f4d-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="20f4d-111">若要部署更改</span><span class="sxs-lookup"><span data-stu-id="20f4d-111">Make a change to deploy</span></span>

<span data-ttu-id="20f4d-112">当前关于页面显示的模板代码。</span><span class="sxs-lookup"><span data-stu-id="20f4d-112">Currently the About page displays the template code.</span></span>

![有关使用模板代码页](command-line-deployment/_static/image1.png)

<span data-ttu-id="20f4d-114">你将将其替换为显示学生登记的摘要的代码。</span><span class="sxs-lookup"><span data-stu-id="20f4d-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="20f4d-115">打开*About.aspx*页上，删除所有内部标记`MainContent``Content`元素，并插入其位置中的以下标记：</span><span class="sxs-lookup"><span data-stu-id="20f4d-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="20f4d-116">运行该项目并选择**有关**页。</span><span class="sxs-lookup"><span data-stu-id="20f4d-116">Run the project and select the **About** page.</span></span>

![“关于”页面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="20f4d-118">通过使用命令行，将部署到测试</span><span class="sxs-lookup"><span data-stu-id="20f4d-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="20f4d-119">你不会部署另一个数据库更改，因此禁用 dbDacFx 数据库部署 aspnet ContosoUniversity 数据库。</span><span class="sxs-lookup"><span data-stu-id="20f4d-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="20f4d-120">打开**发布 Web**向导，以及在这三个发布配置文件中，清除**更新数据库**上的复选框**设置**选项卡。</span><span class="sxs-lookup"><span data-stu-id="20f4d-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="20f4d-121">在 Windows 8 起始页中，搜索**vs2012 的开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="20f4d-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="20f4d-122">右键单击的图标**vs2012 的开发人员命令提示**单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="20f4d-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="20f4d-123">输入以下命令在命令提示符下，将解决方案文件的路径替换为你的解决方案文件的路径：</span><span class="sxs-lookup"><span data-stu-id="20f4d-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="20f4d-124">MSBuild 生成解决方案，并将其部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="20f4d-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![命令行输出](command-line-deployment/_static/image3.png)

<span data-ttu-id="20f4d-126">打开浏览器并转到`http://localhost/ContosoUniversity`，然后单击**有关**页后，可以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="20f4d-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="20f4d-127">如果你尚未创建任何学生在测试中，你将看到在下的一个空页**学生正文统计信息**标题。</span><span class="sxs-lookup"><span data-stu-id="20f4d-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="20f4d-128">转到**学生**页上，单击**添加学生**，和添加一些学生，然后返回到**有关**页后，可以查看学生统计信息。</span><span class="sxs-lookup"><span data-stu-id="20f4d-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![有关测试环境中的页面](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="20f4d-130">密钥的命令行选项</span><span class="sxs-lookup"><span data-stu-id="20f4d-130">Key command line options</span></span>

<span data-ttu-id="20f4d-131">你输入的命令传递到 MSBuild 的解决方案文件路径和两个属性：</span><span class="sxs-lookup"><span data-stu-id="20f4d-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="20f4d-132">部署与部署单个项目解决方案</span><span class="sxs-lookup"><span data-stu-id="20f4d-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="20f4d-133">指定的解决方案文件导致要生成解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="20f4d-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="20f4d-134">如果解决方案中有多个 web 项目，则 MSBuild 适用以下行为：</span><span class="sxs-lookup"><span data-stu-id="20f4d-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="20f4d-135">在命令行指定的属性传递给每个项目。</span><span class="sxs-lookup"><span data-stu-id="20f4d-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="20f4d-136">因此，每个 web 项目都必须具有你指定的名称的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="20f4d-137">如果指定`/p:PublishProfile=Test`，每个 web 项目都必须具有名为的发布配置文件*测试*。</span><span class="sxs-lookup"><span data-stu-id="20f4d-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="20f4d-138">即使不生成另一个时，可能会成功发布一个项目。</span><span class="sxs-lookup"><span data-stu-id="20f4d-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="20f4d-139">有关详细信息，请参阅 stackoverflow 线程[MSBuild 失败，两个包](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。</span><span class="sxs-lookup"><span data-stu-id="20f4d-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="20f4d-140">如果指定单个项目而不是一种解决方案，你必须添加一个参数，指定 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="20f4d-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="20f4d-141">如果你正在使用 Visual Studio 2012 命令行应类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="20f4d-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="20f4d-142">Visual Studio 2010 版本的版本号为 10.0。</span><span class="sxs-lookup"><span data-stu-id="20f4d-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="20f4d-143">有关详细信息，请参阅[Visual Studio 项目兼容性和 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi 博客上。</span><span class="sxs-lookup"><span data-stu-id="20f4d-143">For more information, see [Visual Studio project compatability and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="20f4d-144">指定的发布配置文件</span><span class="sxs-lookup"><span data-stu-id="20f4d-144">Specifying the publish profile</span></span>

<span data-ttu-id="20f4d-145">按名称或完整路径，可以指定发布配置文件 *.pubxml*文件，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="20f4d-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="20f4d-146">Web 发布命令行发布支持的方法</span><span class="sxs-lookup"><span data-stu-id="20f4d-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="20f4d-147">三个发布方法支持用于命令行发布：</span><span class="sxs-lookup"><span data-stu-id="20f4d-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="20f4d-148">`MSDeploy` -通过使用 Web 部署发布。</span><span class="sxs-lookup"><span data-stu-id="20f4d-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="20f4d-149">`Package` 通过创建 Web 部署包发布。</span><span class="sxs-lookup"><span data-stu-id="20f4d-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="20f4d-150">必须独立于创建它的 MSBuild 命令安装包。</span><span class="sxs-lookup"><span data-stu-id="20f4d-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="20f4d-151">`FileSystem` 通过将文件复制到指定的文件夹发布。</span><span class="sxs-lookup"><span data-stu-id="20f4d-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="20f4d-152">指定生成配置和平台</span><span class="sxs-lookup"><span data-stu-id="20f4d-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="20f4d-153">在 Visual Studio 或命令行上，必须设置生成配置和平台。</span><span class="sxs-lookup"><span data-stu-id="20f4d-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="20f4d-154">发布配置文件还包括命名的属性`LastUsedBuildConfiguration`和`LastUsedPlatform`，但无法设置这些属性，以确定如何生成该项目。</span><span class="sxs-lookup"><span data-stu-id="20f4d-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="20f4d-155">有关详细信息，请参阅[MSBuild： 如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)Sayed Hashimi 博客上。</span><span class="sxs-lookup"><span data-stu-id="20f4d-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="20f4d-156">部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="20f4d-156">Deploy to staging</span></span>

<span data-ttu-id="20f4d-157">若要部署到 Azure，必须将密码添加到命令行中。</span><span class="sxs-lookup"><span data-stu-id="20f4d-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="20f4d-158">如果您在 Visual Studio 中的发布配置文件中保存了密码，它已存储在加密形式你 *。 pubxml.user*文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="20f4d-159">当你执行操作的命令行部署，因此你必须在密码命令行参数中传递，MSBuild 不访问该文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="20f4d-160">复制中所需的密码 *.publishsettings*前面为过渡网站下载的文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="20f4d-161">密码是值`userPWD`用于 Web 部署的属性`publishProfile`元素。</span><span class="sxs-lookup"><span data-stu-id="20f4d-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web 部署密码](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="20f4d-163">在 Windows 8 起始页中，搜索**vs2012 的开发人员命令提示**，然后单击图标以打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="20f4d-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="20f4d-164">（你不需要它以管理员身份打开这一次因为你不部署到 IIS 在本地计算机上。）</span><span class="sxs-lookup"><span data-stu-id="20f4d-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="20f4d-165">输入以下命令在命令提示符下，解决方案文件的路径替换为你的解决方案文件和你的密码与密码的路径：</span><span class="sxs-lookup"><span data-stu-id="20f4d-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="20f4d-166">请注意，此命令行包含了额外的参数： `/p:AllowUntrustedCertificate=true`。</span><span class="sxs-lookup"><span data-stu-id="20f4d-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="20f4d-167">本教程正在编写的如`AllowUntrustedCertificate`属性必须设置从命令行发布到 Azure 时。</span><span class="sxs-lookup"><span data-stu-id="20f4d-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="20f4d-168">当发布此 bug 修复后时，你不需要该参数。</span><span class="sxs-lookup"><span data-stu-id="20f4d-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="20f4d-169">打开浏览器并转至你暂存站点的 URL，然后单击**有关**页后，可以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="20f4d-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="20f4d-170">如你此前看到的针对测试环境，你可能需要创建一些学生上查看统计信息**有关**页。</span><span class="sxs-lookup"><span data-stu-id="20f4d-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="20f4d-171">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="20f4d-171">Deploy to production</span></span>

<span data-ttu-id="20f4d-172">部署到生产环境的过程是临时的过程相似。</span><span class="sxs-lookup"><span data-stu-id="20f4d-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="20f4d-173">复制中所需的密码 *.publishsettings*前面为生产 web 站点下载的文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="20f4d-174">打开**vs2012 的开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="20f4d-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="20f4d-175">输入以下命令在命令提示符下，解决方案文件的路径替换为你的解决方案文件和你的密码与密码的路径：</span><span class="sxs-lookup"><span data-stu-id="20f4d-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="20f4d-176">用于实际生产站点时，如果还没有数据库更改，你会通常将复制*应用\_offline.htm*文件之前，作为部署站点并将其删除成功部署后。</span><span class="sxs-lookup"><span data-stu-id="20f4d-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="20f4d-177">打开浏览器并转至你暂存站点的 URL，然后单击**有关**页后，可以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="20f4d-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="20f4d-178">总结</span><span class="sxs-lookup"><span data-stu-id="20f4d-178">Summary</span></span>

<span data-ttu-id="20f4d-179">现在，你已通过使用命令行来部署应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="20f4d-179">You have now deployed an application update by using the command line.</span></span>

![有关测试环境中的页面](command-line-deployment/_static/image6.png)

<span data-ttu-id="20f4d-181">在下一步的教程中，你将看到举例说明如何扩展 web 发布管道。</span><span class="sxs-lookup"><span data-stu-id="20f4d-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="20f4d-182">该示例将演示如何部署应用程序不包括在项目文件。</span><span class="sxs-lookup"><span data-stu-id="20f4d-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20f4d-183">[上一页](deploying-a-database-update.md)
> [下一页](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="20f4d-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
