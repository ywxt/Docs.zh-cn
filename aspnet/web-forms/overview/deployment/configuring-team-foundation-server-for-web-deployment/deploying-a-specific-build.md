---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定生成 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何部署 web 包和数据库脚本从特定的上一个生成到新的目标，如过渡或生产环境的流程图...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6d55497dbc13133aa9c8b8eaecca0f6915fd9ed0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388219"
---
<a name="deploying-a-specific-build"></a><span data-ttu-id="bc9bb-103">部署特定生成</span><span class="sxs-lookup"><span data-stu-id="bc9bb-103">Deploying a Specific Build</span></span>
====================
<span data-ttu-id="bc9bb-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="bc9bb-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="bc9bb-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="bc9bb-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="bc9bb-106">本主题介绍如何部署 web 包和数据库脚本从特定的上一个生成到新的目标，如过渡或生产环境。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>


<span data-ttu-id="bc9bb-107">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="bc9bb-108">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="bc9bb-109">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="bc9bb-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="bc9bb-110">Task Overview</span></span>

<span data-ttu-id="bc9bb-111">到目前为止，本教程系列中的主题有侧重于如何构建、 打包和部署 web 应用程序和数据库的单步执行一部分或过程自动化。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="bc9bb-112">但是，在某些常见的情况下，你将想要从生成中的放置文件夹的列表中选择了你部署的资源。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="bc9bb-113">换而言之，最新版本可能不是你想要部署的生成。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="bc9bb-114">请考虑在前一个主题中所述的持续集成 (CI) 场景[创建生成定义，支持部署](creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="bc9bb-115">你已在 Team Foundation Server (TFS) 2010年创建生成定义。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="bc9bb-116">每次一名开发人员将代码签入 TFS，Team Build 将生成代码、 创建 web 包和数据库脚本作为生成过程的一部分，运行任何单元测试，并将资源部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="bc9bb-117">具体取决于在创建生成定义时配置的保留策略，TFS 将保留一定数量的上一生成。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="bc9bb-118">现在，假设您执行了验证和验证测试针对其中一种生成在测试环境中，并已准备好应用程序部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="bc9bb-119">在此期间，开发人员可能签入新代码。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="bc9bb-120">不想要重新生成解决方案并将其部署到过渡环境中，并且你不想要将最新版本部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="bc9bb-121">相反，你想要部署的特定生成的已验证，并在测试服务器上进行验证。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="bc9bb-122">若要实现此目的，需要告知 Microsoft Build Engine (MSBuild) 若要查找的 web 包和特定生成的生成的数据库脚本的位置。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="bc9bb-123">重写 OutputRoot 属性</span><span class="sxs-lookup"><span data-stu-id="bc9bb-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="bc9bb-124">在中[示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)，则*Publish.proj*文件声明一个名为属性**OutputRoot**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="bc9bb-125">顾名思义，这是包含的生成过程生成的所有内容的根文件夹。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="bc9bb-126">在中*Publish.proj*文件，您所见， **OutputRoot**属性指的是部署的所有资源的根位置。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="bc9bb-127">**OutputRoot**是常用的属性名称。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="bc9bb-128">Visual C# 和 Visual Basic 项目文件还声明此属性来存储所有生成输出的根位置。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


<span data-ttu-id="bc9bb-129">如果你想在项目文件来部署 web 包和数据库从不同位置的脚本&#x2014;像上一个 TFS 生成的输出&#x2014;只需重写**OutputRoot**属性。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="bc9bb-130">在 Team Build 服务器上，您应设置为相关生成文件夹的属性值。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="bc9bb-131">如果从命令行运行 MSBuild，可以指定的值**OutputRoot**作为命令行参数：</span><span class="sxs-lookup"><span data-stu-id="bc9bb-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


<span data-ttu-id="bc9bb-132">在实践中，但是，您还想要跳过**构建**目标&#x2014;就不必在构建您的解决方案，如果不打算使用生成输出。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="bc9bb-133">通过指定想要从命令行执行的目标，无法执行此操作：</span><span class="sxs-lookup"><span data-stu-id="bc9bb-133">You could do this by specifying the targets you want to execute from the command line:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


<span data-ttu-id="bc9bb-134">但是，在大多数情况下，你将想要为 TFS 生成定义，生成你的部署逻辑。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="bc9bb-135">这使用户与**生成排队**触发到 TFS 服务器通过连接任何 Visual Studio 安装中的部署的权限。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="bc9bb-136">创建生成定义以部署特定生成</span><span class="sxs-lookup"><span data-stu-id="bc9bb-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="bc9bb-137">下一个过程介绍如何创建生成定义，使用户触发器部署到过渡环境使用单个命令。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="bc9bb-138">在这种情况下，不想要实际生成的任何内容的生成定义&#x2014;不仅希望其在你的自定义项目文件中执行的部署逻辑。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="bc9bb-139">*Publish.proj*文件包含将跳过的条件逻辑**生成**如果在 Team Build 中运行该文件为目标。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="bc9bb-140">这是通过评估内置**BuildingInTeamBuild**属性，它将自动设置为**true**如果您在 Team Build 中运行你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="bc9bb-141">因此，你可以跳过生成过程，只需运行要部署的现有生成的项目文件。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="bc9bb-142">**若要创建生成定义，若要手动触发部署**</span><span class="sxs-lookup"><span data-stu-id="bc9bb-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="bc9bb-143">在 Visual Studio 2010 中，在**团队资源管理器**窗口中，展开你的团队项目节点，右键单击**生成**，然后单击**新建生成定义**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="bc9bb-144">上**常规**选项卡上，为生成定义指定一个名称 (例如， **DeployToStaging**) 和可选描述。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="bc9bb-145">上**触发器**选项卡上，选择**手动-签入不会触发新的生成**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="bc9bb-146">上**生成默认值**选项卡上，在**生成输出复制到以下放置文件夹**框中，键入 drop 文件夹的通用命名约定 (UNC) 路径 (例如，  **\\TFSBUILD\Drops**)。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="bc9bb-147">上**进程**选项卡上，在**生成过程文件**下拉列表中，保留**DefaultTemplate.xaml**选定。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="bc9bb-148">这是添加到所有新的团队项目的默认生成过程模板之一。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="bc9bb-149">在中**生成过程参数**表中，单击在**生成的项**行，然后依次**省略号**按钮。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="bc9bb-150">在中**生成的项**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="bc9bb-151">在中**类型的项**下拉列表中选择**MSBuild 项目文件**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="bc9bb-152">浏览到与其控件部署过程中，选择的文件，然后单击的自定义项目文件的位置**确定**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="bc9bb-153">在中**生成的项**对话框中，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="bc9bb-154">在中**生成过程参数**表中，展开**高级**部分。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="bc9bb-155">在中**MSBuild 参数**行，指定特定于环境的项目文件的位置并为生成文件夹的位置添加一个占位符：</span><span class="sxs-lookup"><span data-stu-id="bc9bb-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="bc9bb-156">你将需要重写**OutputRoot**值每次对生成进行排队。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="bc9bb-157">下一过程中对此进行了。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="bc9bb-158">单击“保存” 。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-158">Click **Save**.</span></span>

<span data-ttu-id="bc9bb-159">当触发生成时，你需要更新**OutputRoot**属性以指向要部署的生成。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="bc9bb-160">**若要部署特定生成的生成定义中**</span><span class="sxs-lookup"><span data-stu-id="bc9bb-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="bc9bb-161">在中**团队资源管理器**窗口中，右键单击生成定义，然后单击**使新生成入队**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="bc9bb-162">在中**使生成入队**对话框中，在**参数**选项卡上，展开**高级**部分。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="bc9bb-163">在中**MSBuild 参数**行中，将的值为**OutputRoot**生成文件夹的位置的属性。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="bc9bb-164">例如：</span><span class="sxs-lookup"><span data-stu-id="bc9bb-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="bc9bb-165">请务必包括尾部反斜杠生成文件夹的路径的末尾。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="bc9bb-166">单击**队列**。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-166">Click **Queue**.</span></span>

<span data-ttu-id="bc9bb-167">当对生成进行排队、 项目文件将部署的数据库脚本和 web 包从生成放置文件夹中指定**OutputRoot**属性。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bc9bb-168">结束语</span><span class="sxs-lookup"><span data-stu-id="bc9bb-168">Conclusion</span></span>

<span data-ttu-id="bc9bb-169">本主题介绍了如何将发布部署资源，如 web 包和数据库脚本、 从上一个特定的生成使用拆分项目文件的部署模型。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="bc9bb-170">本文介绍了如何重写**OutputRoot**属性以及如何将部署逻辑合并到 TFS 生成定义。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="bc9bb-171">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="bc9bb-171">Further Reading</span></span>

<span data-ttu-id="bc9bb-172">创建生成定义的详细信息，请参阅[创建基本生成定义](https://msdn.microsoft.com/library/ms181716.aspx)并[定义生成过程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="bc9bb-173">生成排队的更多指导，请参阅[对生成进行排队](https://msdn.microsoft.com/library/ms181722.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc9bb-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bc9bb-174">[上一页](creating-a-build-definition-that-supports-deployment.md)
> [下一页](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="bc9bb-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
