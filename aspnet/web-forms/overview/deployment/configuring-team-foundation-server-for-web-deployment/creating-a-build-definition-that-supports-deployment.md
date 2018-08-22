---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 创建生成定义支持部署 |Microsoft Docs
author: jrjlee
description: 如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，您需要创建你的团队项目中的生成定义。 此主题 des...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: 33ebde3074603801945c676ace64b26ca5bbf44a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823529"
---
<a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="87040-104">创建生成定义支持部署</span><span class="sxs-lookup"><span data-stu-id="87040-104">Creating a Build Definition That Supports Deployment</span></span>
====================
<span data-ttu-id="87040-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="87040-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="87040-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="87040-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="87040-107">如果你想要执行任何种类的生成在 Team Foundation Server (TFS) 2010年，您需要创建你的团队项目中的生成定义。</span><span class="sxs-lookup"><span data-stu-id="87040-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="87040-108">本主题介绍如何在 TFS 中创建新的生成定义以及如何控制 web 部署作为 Team Build 中的生成过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="87040-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>


<span data-ttu-id="87040-109">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="87040-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="87040-110">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。</span><span class="sxs-lookup"><span data-stu-id="87040-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="87040-111">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="87040-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="87040-112">任务概述</span><span class="sxs-lookup"><span data-stu-id="87040-112">Task Overview</span></span>

<span data-ttu-id="87040-113">生成定义是控制如何以及何时在 TFS 中的团队项目进行生成的机制。</span><span class="sxs-lookup"><span data-stu-id="87040-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="87040-114">指定每个生成定义：</span><span class="sxs-lookup"><span data-stu-id="87040-114">Each build definition specifies:</span></span>

- <span data-ttu-id="87040-115">你想要生成 Visual Studio 解决方案文件或自定义 Microsoft Build Engine (MSBuild) 项目文件等操作。</span><span class="sxs-lookup"><span data-stu-id="87040-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="87040-116">确定何时生成应采取的条件放置，如手动触发器，持续集成 (CI) 或封闭签入。</span><span class="sxs-lookup"><span data-stu-id="87040-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="87040-117">Team Build 应向其发送生成输出，其中包括像 web 包和数据库脚本的部署项目的位置。</span><span class="sxs-lookup"><span data-stu-id="87040-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="87040-118">应保留每个生成的时间量。</span><span class="sxs-lookup"><span data-stu-id="87040-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="87040-119">生成过程的各种其他参数。</span><span class="sxs-lookup"><span data-stu-id="87040-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="87040-120">生成定义的详细信息，请参阅[定义在生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="87040-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>


<span data-ttu-id="87040-121">本主题将演示如何创建使用 CI，生成定义，以便开发人员签入新的内容时触发生成。</span><span class="sxs-lookup"><span data-stu-id="87040-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="87040-122">如果生成成功，生成服务在运行要将解决方案部署到测试环境的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="87040-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="87040-123">当触发生成时，这些操作需要执行：</span><span class="sxs-lookup"><span data-stu-id="87040-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="87040-124">首先，Team Build 应生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="87040-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="87040-125">作为此过程的一部分，Team Build 将调用 Web 发布管道 (WPP) 为每个解决方案中的 web 应用程序项目中生成 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="87040-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="87040-126">Team Build 还将运行与解决方案关联的任何单元测试。</span><span class="sxs-lookup"><span data-stu-id="87040-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="87040-127">如果解决方案生成失败，Team Build 应采取任何进一步的操作。</span><span class="sxs-lookup"><span data-stu-id="87040-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="87040-128">应将单元测试失败视为生成失败。</span><span class="sxs-lookup"><span data-stu-id="87040-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="87040-129">如果解决方案生成成功，Team Build 应运行控制解决方案的部署的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="87040-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="87040-130">作为此过程的一部分，Team Build 将调用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 在目标 web 服务器上安装打包的 web 应用程序，并且它会调用 VSDBCMD.exe 实用工具来运行数据库创建目标数据库服务器上的脚本。</span><span class="sxs-lookup"><span data-stu-id="87040-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="87040-131">这说明了该过程：</span><span class="sxs-lookup"><span data-stu-id="87040-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="87040-132">[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案包括自定义 MSBuild 项目文件中， *Publish.proj*，可以从 MSBuild 或 Team Build 中运行。</span><span class="sxs-lookup"><span data-stu-id="87040-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="87040-133">如中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，此项目文件定义逻辑，用于将你的 web 包和数据库部署到目标环境。</span><span class="sxs-lookup"><span data-stu-id="87040-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="87040-134">该文件包含运行时将其在 Team Build，离开只需部署要运行的任务中省略的构建和打包过程的逻辑。</span><span class="sxs-lookup"><span data-stu-id="87040-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="87040-135">这是因为时自动执行这种方式中的部署，通常需要确保已成功生成解决方案并在部署过程开始之前，将传递任何单元测试。</span><span class="sxs-lookup"><span data-stu-id="87040-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="87040-136">下一部分介绍如何通过创建新的生成定义来实现此过程。</span><span class="sxs-lookup"><span data-stu-id="87040-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="87040-137">此过程&#x2014;中一个自动执行过程会生成、 测试，并将解决方案部署&#x2014;很可能是最适合部署以供测试环境。</span><span class="sxs-lookup"><span data-stu-id="87040-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="87040-138">为过渡和生产环境，您更可能想要将内容从以前生成的已验证并验证在测试环境中部署。</span><span class="sxs-lookup"><span data-stu-id="87040-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="87040-139">这种方法下一主题中所述[部署特定生成](deploying-a-specific-build.md)。</span><span class="sxs-lookup"><span data-stu-id="87040-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>


### <a name="who-performs-this-procedure"></a><span data-ttu-id="87040-140">此过程的执行者是谁？</span><span class="sxs-lookup"><span data-stu-id="87040-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="87040-141">通常情况下，TFS 管理员执行此过程。</span><span class="sxs-lookup"><span data-stu-id="87040-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="87040-142">在某些情况下，开发人员团队负责人可能需要在 TFS 中的负责的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="87040-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="87040-143">若要创建新的生成定义，您需要的成员**项目集合生成管理员**组包含解决方案的团队项目集合。</span><span class="sxs-lookup"><span data-stu-id="87040-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="87040-144">创建 CI 和部署的生成定义</span><span class="sxs-lookup"><span data-stu-id="87040-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="87040-145">下一步的过程描述如何创建 CI 触发的生成定义。</span><span class="sxs-lookup"><span data-stu-id="87040-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="87040-146">如果生成成功，将解决方案部署的自定义 MSBuild 项目文件中使用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="87040-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="87040-147">**若要创建的 CI 和部署的生成定义**</span><span class="sxs-lookup"><span data-stu-id="87040-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="87040-148">在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目节点，右键单击**生成**，然后单击**新建生成定义**。</span><span class="sxs-lookup"><span data-stu-id="87040-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="87040-149">上**常规**选项卡上，为生成定义指定一个名称 (例如， **DeployToTest**) 和可选描述。</span><span class="sxs-lookup"><span data-stu-id="87040-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="87040-150">上**触发器**选项卡上，选择你想要触发新的生成的条件。</span><span class="sxs-lookup"><span data-stu-id="87040-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="87040-151">例如，如果你想要生成解决方案，每次一名开发人员签入新代码时，将部署到测试环境，选择**持续集成**。</span><span class="sxs-lookup"><span data-stu-id="87040-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="87040-152">上**生成默认值**选项卡上，在**生成输出复制到以下放置文件夹**框中，键入 drop 文件夹的通用命名约定 (UNC) 路径 (例如，  **\\TFSBUILD\Drops**)。</span><span class="sxs-lookup"><span data-stu-id="87040-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="87040-153">此放置位置存储多个生成，具体取决于你配置的保留策略。</span><span class="sxs-lookup"><span data-stu-id="87040-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="87040-154">当你想要发布到过渡或生产环境的部署项目从特定的生成时，这是您可以找到它们。</span><span class="sxs-lookup"><span data-stu-id="87040-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="87040-155">上**进程**选项卡上，在**生成过程文件**下拉列表中，保留**DefaultTemplate.xaml**选定。</span><span class="sxs-lookup"><span data-stu-id="87040-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="87040-156">这是添加到所有新的团队项目的默认生成过程模板之一。</span><span class="sxs-lookup"><span data-stu-id="87040-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="87040-157">在中**生成过程参数**表中，单击在**生成的项**行，然后依次**省略号**按钮。</span><span class="sxs-lookup"><span data-stu-id="87040-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="87040-158">在中**生成的项**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="87040-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="87040-159">浏览到你的解决方案文件的位置，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="87040-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="87040-160">在中**生成的项**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="87040-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="87040-161">在中**类型的项**下拉列表中选择**MSBuild 项目文件**。</span><span class="sxs-lookup"><span data-stu-id="87040-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="87040-162">浏览到与其控件部署过程中，选择的文件，然后单击的自定义项目文件的位置**确定**。</span><span class="sxs-lookup"><span data-stu-id="87040-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="87040-163">**生成的项**对话框现在应显示两个项。</span><span class="sxs-lookup"><span data-stu-id="87040-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="87040-164">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="87040-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="87040-165">上**进程**选项卡上，在**生成过程参数**表中，展开**高级**部分。</span><span class="sxs-lookup"><span data-stu-id="87040-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="87040-166">在中**MSBuild 参数**行中，添加任何 MSBuild 命令行自变量的*任一*项构建的需要。</span><span class="sxs-lookup"><span data-stu-id="87040-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="87040-167">在联系人管理器解决方案方案中，这些参数是必需的：</span><span class="sxs-lookup"><span data-stu-id="87040-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="87040-168">在此示例中：</span><span class="sxs-lookup"><span data-stu-id="87040-168">In this example:</span></span>

    1. <span data-ttu-id="87040-169">**DeployOnBuild = true**并**DeployTarget = 包**时生成 Contact Manager 解决方案，是必需参数。</span><span class="sxs-lookup"><span data-stu-id="87040-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="87040-170">这会指示 MSBuild 创建 web 部署包后生成每个 web 应用程序项目，如中所述[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="87040-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="87040-171">**TargetEnvPropsFile**参数是必需的在生成时*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="87040-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="87040-172">此属性指示的特定于环境的配置文件的位置，如中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="87040-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="87040-173">上**保留策略**选项卡上，配置想要根据需要保留每种类型的多少生成。</span><span class="sxs-lookup"><span data-stu-id="87040-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="87040-174">单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="87040-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="87040-175">将生成排入队列</span><span class="sxs-lookup"><span data-stu-id="87040-175">Queue a Build</span></span>

<span data-ttu-id="87040-176">此时，您已创建至少一个新的生成定义。</span><span class="sxs-lookup"><span data-stu-id="87040-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="87040-177">您定义的生成过程现在将根据你在生成定义中指定的触发器运行。</span><span class="sxs-lookup"><span data-stu-id="87040-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="87040-178">如果已配置生成定义，以使用 CI，可以通过两种方式来测试你的生成定义：</span><span class="sxs-lookup"><span data-stu-id="87040-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="87040-179">签入到团队项目，以触发自动生成的一些内容。</span><span class="sxs-lookup"><span data-stu-id="87040-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="87040-180">手动对生成进行排队。</span><span class="sxs-lookup"><span data-stu-id="87040-180">Queue a build manually.</span></span>

<span data-ttu-id="87040-181">**若要手动对生成进行排队**</span><span class="sxs-lookup"><span data-stu-id="87040-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="87040-182">在中**团队资源管理器**窗口中，右键单击生成定义，然后单击**使新生成入队**。</span><span class="sxs-lookup"><span data-stu-id="87040-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="87040-183">在中**使生成入队**对话框中，查看生成属性，然后单击**队列**。</span><span class="sxs-lookup"><span data-stu-id="87040-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="87040-184">若要查看进度和结果生成的&#x2014;而不考虑它是否触发手动或自动&#x2014;双击中的生成定义**团队资源管理器**窗口。</span><span class="sxs-lookup"><span data-stu-id="87040-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="87040-185">这将打开**生成资源管理器**选项卡。</span><span class="sxs-lookup"><span data-stu-id="87040-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="87040-186">在这里，可以排查生成失败。</span><span class="sxs-lookup"><span data-stu-id="87040-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="87040-187">如果您双击各个生成，可以查看摘要信息，并单击浏览详细的日志文件。</span><span class="sxs-lookup"><span data-stu-id="87040-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="87040-188">此信息可用于对生成失败进行故障排除和解决任何问题，然后再尝试另一个生成。</span><span class="sxs-lookup"><span data-stu-id="87040-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="87040-189">执行部署逻辑生成很可能失败，直到已授予生成服务器中的目标环境所需的任何权限。</span><span class="sxs-lookup"><span data-stu-id="87040-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="87040-190">有关详细信息，请参阅[团队生成部署配置的权限](configuring-permissions-for-team-build-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="87040-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>


## <a name="monitor-the-build-process"></a><span data-ttu-id="87040-191">监视生成过程</span><span class="sxs-lookup"><span data-stu-id="87040-191">Monitor the Build Process</span></span>

<span data-ttu-id="87040-192">TFS 提供范围广泛的功能来帮助你监视生成过程。</span><span class="sxs-lookup"><span data-stu-id="87040-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="87040-193">例如，TFS 可以向你发送一封电子邮件或在完成生成时在任务栏通知区域中显示警告。</span><span class="sxs-lookup"><span data-stu-id="87040-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="87040-194">有关详细信息，请参阅[运行并监视生成](https://msdn.microsoft.com/library/ms181721.aspx)。</span><span class="sxs-lookup"><span data-stu-id="87040-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="87040-195">结束语</span><span class="sxs-lookup"><span data-stu-id="87040-195">Conclusion</span></span>

<span data-ttu-id="87040-196">本主题介绍了如何在 TFS 中创建生成定义。</span><span class="sxs-lookup"><span data-stu-id="87040-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="87040-197">生成定义配置为使用 CI，因此，生成过程运行时开发人员签入到团队项目的内容。</span><span class="sxs-lookup"><span data-stu-id="87040-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="87040-198">生成定义执行自定义的 MSBuild 项目文件，以将 web 包和数据库脚本部署到目标服务器环境。</span><span class="sxs-lookup"><span data-stu-id="87040-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="87040-199">为了使自动部署成功完成生成过程的一部分，你将需要授予访问目标 web 服务器和目标数据库服务器上的生成服务帐户的适当权限。</span><span class="sxs-lookup"><span data-stu-id="87040-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="87040-200">在本教程的最后一个主题[团队生成部署配置的权限](configuring-permissions-for-team-build-deployment.md)，介绍如何标识和配置用于从 Team Build 服务器的自动部署所需的权限。</span><span class="sxs-lookup"><span data-stu-id="87040-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="87040-201">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="87040-201">Further Reading</span></span>

<span data-ttu-id="87040-202">创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)并[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="87040-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="87040-203">生成排队的更多指导，请参阅[对生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。</span><span class="sxs-lookup"><span data-stu-id="87040-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="87040-204">[上一页](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一页](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="87040-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
