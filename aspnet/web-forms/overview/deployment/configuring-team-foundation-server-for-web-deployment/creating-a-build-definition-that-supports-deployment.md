---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 创建生成定义支持部署 |Microsoft 文档
author: jrjlee
description: 如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，你需要创建你的团队项目中的生成定义。 此主题 des...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: c5ea0bd9f01bb57b96abd349741f304c0093d887
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
ms.locfileid: "30880357"
---
<a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="f7421-104">创建生成定义支持部署</span><span class="sxs-lookup"><span data-stu-id="f7421-104">Creating a Build Definition That Supports Deployment</span></span>
====================
<span data-ttu-id="f7421-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f7421-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f7421-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f7421-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f7421-107">如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，你需要创建你的团队项目中的生成定义。</span><span class="sxs-lookup"><span data-stu-id="f7421-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="f7421-108">本主题介绍如何在 TFS 中创建新的生成定义以及如何控制 Team Build 中的生成过程的一部分的 web 部署。</span><span class="sxs-lookup"><span data-stu-id="f7421-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>


<span data-ttu-id="f7421-109">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案&#x2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="f7421-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="f7421-110">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制其&#x2014;一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="f7421-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="f7421-111">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="f7421-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="f7421-112">任务概述</span><span class="sxs-lookup"><span data-stu-id="f7421-112">Task Overview</span></span>

<span data-ttu-id="f7421-113">生成定义是控制 TFS 中团队项目的方式和时间进行生成的机制。</span><span class="sxs-lookup"><span data-stu-id="f7421-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="f7421-114">指定每个生成定义：</span><span class="sxs-lookup"><span data-stu-id="f7421-114">Each build definition specifies:</span></span>

- <span data-ttu-id="f7421-115">你希望生成时，Visual Studio 解决方案文件或自定义 Microsoft Build Engine (MSBuild) 项目文件等操作。</span><span class="sxs-lookup"><span data-stu-id="f7421-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="f7421-116">确定何时应执行生成的条件放置，如手动触发器，持续集成 (CI)，或者封闭签入的。</span><span class="sxs-lookup"><span data-stu-id="f7421-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="f7421-117">Team Build 应向其发送生成输出，包括部署 web 包和数据库脚本等项目，项目的位置。</span><span class="sxs-lookup"><span data-stu-id="f7421-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="f7421-118">应保留每个生成的时间量。</span><span class="sxs-lookup"><span data-stu-id="f7421-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="f7421-119">在生成过程中的各种其他参数。</span><span class="sxs-lookup"><span data-stu-id="f7421-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="f7421-120">生成定义的详细信息，请参阅[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7421-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>


<span data-ttu-id="f7421-121">本主题将演示如何创建使用 CI 使用，请生成定义，以便开发人员签入新的内容时触发生成。</span><span class="sxs-lookup"><span data-stu-id="f7421-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="f7421-122">如果生成成功，则生成服务运行将解决方案部署到测试环境的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="f7421-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="f7421-123">时触发的生成，这些操作将需要发生这种情况：</span><span class="sxs-lookup"><span data-stu-id="f7421-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="f7421-124">首先，Team Build 应生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7421-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="f7421-125">此过程的一部分，作为团队生成可调用 Web 发布管道 (WPP) 为每个解决方案中的 web 应用程序项目中生成 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="f7421-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="f7421-126">Team Build 还将运行任何单元测试与解决方案相关联。</span><span class="sxs-lookup"><span data-stu-id="f7421-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="f7421-127">如果解决方案生成失败，则 Team Build 应执行任何进一步操作。</span><span class="sxs-lookup"><span data-stu-id="f7421-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="f7421-128">单元测试失败应视为生成失败。</span><span class="sxs-lookup"><span data-stu-id="f7421-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="f7421-129">如果解决方案生成成功，则 Team Build 应运行控制部署解决方案的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="f7421-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="f7421-130">此过程的一部分，作为团队生成将会调用 Internet 信息服务 (IIS) Web 部署工具 (Web Deploy) 以在目标 web 服务器上安装打包的 web 应用程序和它将调用 VSDBCMD.exe 实用工具来运行数据库创建在目标数据库服务器上的脚本。</span><span class="sxs-lookup"><span data-stu-id="f7421-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="f7421-131">这说明了该过程：</span><span class="sxs-lookup"><span data-stu-id="f7421-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="f7421-132">[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案包含自定义 MSBuild 项目文件中， *Publish.proj*，你可以运行 MSBuild 或 Team Build。</span><span class="sxs-lookup"><span data-stu-id="f7421-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="f7421-133">中所述[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，此项目文件定义将你的 web 包和数据库部署到目标环境的逻辑。</span><span class="sxs-lookup"><span data-stu-id="f7421-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="f7421-134">该文件包含运行时将其在 Team Build 离开只需部署任务运行中省略的构建和打包过程的逻辑。</span><span class="sxs-lookup"><span data-stu-id="f7421-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="f7421-135">这是因为在自动化部署以这种方式时，将通常想要确保成功生成解决方案，并通过任何单元测试，在部署过程开始之前。</span><span class="sxs-lookup"><span data-stu-id="f7421-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="f7421-136">下一部分将说明如何通过创建新的生成定义来实现此过程。</span><span class="sxs-lookup"><span data-stu-id="f7421-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="f7421-137">此过程&#x2014;中单个自动完成过程将生成，测试，并部署解决方案&#x2014;可能是最适合部署以测试环境。</span><span class="sxs-lookup"><span data-stu-id="f7421-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="f7421-138">有关过渡和生产环境，你很多更有可能想要将内容从以前的生成，你已经验证并验证在测试环境中部署。</span><span class="sxs-lookup"><span data-stu-id="f7421-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="f7421-139">这种方法下一主题中所述[部署对特定生成](deploying-a-specific-build.md)。</span><span class="sxs-lookup"><span data-stu-id="f7421-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>


### <a name="who-performs-this-procedure"></a><span data-ttu-id="f7421-140">此过程的执行者是谁？</span><span class="sxs-lookup"><span data-stu-id="f7421-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="f7421-141">通常，TFS 管理员执行此过程。</span><span class="sxs-lookup"><span data-stu-id="f7421-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="f7421-142">在某些情况下，开发人员团队主管可能在 TFS 中需要负责的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="f7421-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="f7421-143">若要创建新的生成定义，你需要是成员的**项目集合生成管理员**组包含你的解决方案的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="f7421-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="f7421-144">CI 和部署创建生成定义</span><span class="sxs-lookup"><span data-stu-id="f7421-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="f7421-145">下一步的过程描述如何创建 CI 触发的生成定义。</span><span class="sxs-lookup"><span data-stu-id="f7421-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="f7421-146">如果生成成功，部署了解决方案，在自定义 MSBuild 项目文件中使用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="f7421-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="f7421-147">**若要为 CI 和部署创建生成定义**</span><span class="sxs-lookup"><span data-stu-id="f7421-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="f7421-148">在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目节点，右键单击**生成**，然后单击**新建生成定义**。</span><span class="sxs-lookup"><span data-stu-id="f7421-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="f7421-149">上**常规**选项卡上，为生成定义指定一个名称 (例如， **DeployToTest**) 和可选描述。</span><span class="sxs-lookup"><span data-stu-id="f7421-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="f7421-150">上**触发器**选项卡上，选择你要在其触发新的生成的条件。</span><span class="sxs-lookup"><span data-stu-id="f7421-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="f7421-151">例如，如果你想要生成解决方案，每次开发人员签入新代码时，将部署到测试环境，选择**持续集成**。</span><span class="sxs-lookup"><span data-stu-id="f7421-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="f7421-152">上**生成默认值**选项卡上，在**生成输出复制到以下放置文件夹**框中，键入 drop 文件夹的通用命名约定 (UNC) 路径 (例如，  **\\TFSBUILD\Drops**)。</span><span class="sxs-lookup"><span data-stu-id="f7421-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="f7421-153">此放置位置存储几个版本，具体取决于你配置的保留策略。</span><span class="sxs-lookup"><span data-stu-id="f7421-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="f7421-154">当你想要发布到过渡或生产环境的部署项目从特定生成时，这将是你可以找到它们。</span><span class="sxs-lookup"><span data-stu-id="f7421-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="f7421-155">上**过程**选项卡上，在**生成过程文件**下拉列表中，保留**DefaultTemplate.xaml**选。</span><span class="sxs-lookup"><span data-stu-id="f7421-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="f7421-156">这是添加到新的所有团队项目的默认生成过程模板之一。</span><span class="sxs-lookup"><span data-stu-id="f7421-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="f7421-157">在**生成过程参数**表，请单击中**生成的项**行，然后依次**省略号**按钮。</span><span class="sxs-lookup"><span data-stu-id="f7421-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="f7421-158">在**生成的项**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="f7421-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="f7421-159">浏览到你的解决方案文件的位置，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="f7421-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="f7421-160">在**生成的项**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="f7421-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="f7421-161">在**类型的项**下拉列表中，选择**MSBuild 项目文件**。</span><span class="sxs-lookup"><span data-stu-id="f7421-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="f7421-162">浏览到与其控制部署过程，选择的文件，然后单击自定义项目文件的位置**确定**。</span><span class="sxs-lookup"><span data-stu-id="f7421-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="f7421-163">**生成的项**对话框现在应显示两个项。</span><span class="sxs-lookup"><span data-stu-id="f7421-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="f7421-164">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="f7421-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="f7421-165">上**过程**选项卡上，在**生成过程参数**表中，展开**高级**部分。</span><span class="sxs-lookup"><span data-stu-id="f7421-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="f7421-166">在**MSBuild 参数**行中，添加任何 MSBuild 命令行参数，*任一*项目生成的需要。</span><span class="sxs-lookup"><span data-stu-id="f7421-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="f7421-167">在联系人管理器解决方案方案中，这些自变量是必需的：</span><span class="sxs-lookup"><span data-stu-id="f7421-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="f7421-168">在此示例中：</span><span class="sxs-lookup"><span data-stu-id="f7421-168">In this example:</span></span>

    1. <span data-ttu-id="f7421-169">**DeployOnBuild = true**和**DeployTarget = 包**参数是必需的当你构建联系人管理器解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7421-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="f7421-170">这会指示 MSBuild 创建 web 部署包生成每个 web 应用程序项目之后, 中所述[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="f7421-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="f7421-171">**TargetEnvPropsFile**参数是必需的在生成时*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="f7421-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="f7421-172">此属性指示的位置特定于环境的配置文件中所述[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="f7421-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="f7421-173">上**保留策略**选项卡上，配置想要根据需要保留每种类型的多少生成。</span><span class="sxs-lookup"><span data-stu-id="f7421-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="f7421-174">单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="f7421-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="f7421-175">将生成排入队列</span><span class="sxs-lookup"><span data-stu-id="f7421-175">Queue a Build</span></span>

<span data-ttu-id="f7421-176">此时，你已创建至少一个新的生成定义。</span><span class="sxs-lookup"><span data-stu-id="f7421-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="f7421-177">你定义的生成过程现在将根据你在生成定义中指定的触发器运行。</span><span class="sxs-lookup"><span data-stu-id="f7421-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="f7421-178">如果已配置你的生成定义，以使用 CI，你可以通过两种方式来测试你的生成定义：</span><span class="sxs-lookup"><span data-stu-id="f7421-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="f7421-179">签入到团队项目来触发自动生成一些内容。</span><span class="sxs-lookup"><span data-stu-id="f7421-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="f7421-180">手动对生成进行排队。</span><span class="sxs-lookup"><span data-stu-id="f7421-180">Queue a build manually.</span></span>

<span data-ttu-id="f7421-181">**若要手动对生成进行排队**</span><span class="sxs-lookup"><span data-stu-id="f7421-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="f7421-182">在**团队资源管理器**窗口中，右键单击生成定义，并依次**使新生成入队**。</span><span class="sxs-lookup"><span data-stu-id="f7421-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="f7421-183">在**队列生成**对话框中，查看生成属性中，，然后单击**队列**。</span><span class="sxs-lookup"><span data-stu-id="f7421-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="f7421-184">若要查看的进度和生成的结果&#x2014;而不考虑它是否触发手动或自动&#x2014;双击生成定义中的**团队资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="f7421-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="f7421-185">这将打开**生成资源管理器**选项卡。</span><span class="sxs-lookup"><span data-stu-id="f7421-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="f7421-186">从这里，您可以解决失败的生成。</span><span class="sxs-lookup"><span data-stu-id="f7421-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="f7421-187">如果双击的单个生成后，你可以查看摘要信息和详细的日志文件通过单击。</span><span class="sxs-lookup"><span data-stu-id="f7421-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="f7421-188">可以使用此信息来排查生成失败，并解决任何问题，然后再尝试另一个生成。</span><span class="sxs-lookup"><span data-stu-id="f7421-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="f7421-189">执行部署逻辑的生成很可能之前已在目标环境所需的任何权限授予生成服务器失败。</span><span class="sxs-lookup"><span data-stu-id="f7421-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="f7421-190">有关详细信息，请参阅[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f7421-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>


## <a name="monitor-the-build-process"></a><span data-ttu-id="f7421-191">监视器生成过程</span><span class="sxs-lookup"><span data-stu-id="f7421-191">Monitor the Build Process</span></span>

<span data-ttu-id="f7421-192">TFS 提供广泛的功能来帮助你监视生成过程。</span><span class="sxs-lookup"><span data-stu-id="f7421-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="f7421-193">例如，TFS 可以向你发送一封电子邮件或生成完成后，在任务栏通知区域显示警报。</span><span class="sxs-lookup"><span data-stu-id="f7421-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="f7421-194">有关详细信息，请参阅[运行和监视器生成](https://msdn.microsoft.com/library/ms181721.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7421-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="f7421-195">结束语</span><span class="sxs-lookup"><span data-stu-id="f7421-195">Conclusion</span></span>

<span data-ttu-id="f7421-196">本主题描述如何在 TFS 中创建生成定义。</span><span class="sxs-lookup"><span data-stu-id="f7421-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="f7421-197">因此，生成过程运行只要开发人员将签入到团队项目的内容，将为 CI 使用，请配置生成定义。</span><span class="sxs-lookup"><span data-stu-id="f7421-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="f7421-198">生成定义执行自定义的 MSBuild 项目文件，以将 web 包和数据库脚本部署到目标服务器环境。</span><span class="sxs-lookup"><span data-stu-id="f7421-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="f7421-199">为了使自动部署才能成功生成过程的一部分，你将需要授予对生成服务帐户的目标 web 服务器和目标数据库服务器上的合适权限。</span><span class="sxs-lookup"><span data-stu-id="f7421-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="f7421-200">在本教程的最后一个主题[配置团队生成部署的权限](configuring-permissions-for-team-build-deployment.md)，介绍如何标识和配置用于从 Team Build 服务器的自动部署所需的权限。</span><span class="sxs-lookup"><span data-stu-id="f7421-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="f7421-201">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="f7421-201">Further Reading</span></span>

<span data-ttu-id="f7421-202">创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)和[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7421-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="f7421-203">队列生成的更多指南，请参阅[对生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7421-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7421-204">[上一页](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一页](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="f7421-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
