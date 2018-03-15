---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: "了解生成过程 |Microsoft 文档"
author: jrjlee
description: "本主题提供的企业范围内生成和部署过程的演练。 本主题中介绍的方法使用自定义 Microsoft 生成 Engin..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 3efcefc40dc135ff42f55911036f8b38b5aa13b1
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="understanding-the-build-process"></a><span data-ttu-id="cb31e-104">了解生成过程</span><span class="sxs-lookup"><span data-stu-id="cb31e-104">Understanding the Build Process</span></span>
====================
<span data-ttu-id="cb31e-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="cb31e-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="cb31e-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="cb31e-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="cb31e-107">本主题提供的企业范围内生成和部署过程的演练。</span><span class="sxs-lookup"><span data-stu-id="cb31e-107">This topic provides a walkthrough of an enterprise-scale build and deployment process.</span></span> <span data-ttu-id="cb31e-108">本主题中介绍的方法使用自定义 Microsoft Build Engine (MSBuild) 项目文件来提供细粒度控制过程的各个方面。</span><span class="sxs-lookup"><span data-stu-id="cb31e-108">The approach described in this topic uses custom Microsoft Build Engine (MSBuild) project files to provide fine-grained control over every aspect of the process.</span></span> <span data-ttu-id="cb31e-109">在项目文件中，自定义 MSBuild 目标用于运行 Internet Information Services (IIS) Web 部署工具 (MSDeploy.exe) 类似的部署实用程序和数据库部署实用工具 VSDBCMD.exe。</span><span class="sxs-lookup"><span data-stu-id="cb31e-109">Within the project files, custom MSBuild targets are used to run deployment utilities like the Internet Information Services (IIS) Web Deployment Tool (MSDeploy.exe) and the database deployment utility VSDBCMD.exe.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="cb31e-110">前一个主题，[了解项目文件](understanding-the-project-file.md)、 所述的 MSBuild 项目文件的关键组件和引入拆分项目文件，以支持部署到多个目标环境的概念。</span><span class="sxs-lookup"><span data-stu-id="cb31e-110">The previous topic, [Understanding the Project File](understanding-the-project-file.md), described the key components of an MSBuild project file and introduced the concept of split project files to support deployment to multiple target environments.</span></span> <span data-ttu-id="cb31e-111">如果你尚不熟悉这些概念，你应查看[了解项目文件](understanding-the-project-file.md)通读本主题工作之前。</span><span class="sxs-lookup"><span data-stu-id="cb31e-111">If you're not already familiar with these concepts, you should review [Understanding the Project File](understanding-the-project-file.md) before you work through this topic.</span></span>


<span data-ttu-id="cb31e-112">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案 （&） #x 2014;[联系人管理器解决方案](the-contact-manager-solution.md)& #x 2014; 来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 的 web 应用程序Communication Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-112">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="cb31e-113">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](understanding-the-project-file.md)，在其中生成过程控制由两个项目文件 （&） #x 2014; 一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="cb31e-113">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="cb31e-114">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="cb31e-114">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="build-and-deployment-overview"></a><span data-ttu-id="cb31e-115">生成和部署概述</span><span class="sxs-lookup"><span data-stu-id="cb31e-115">Build and Deployment Overview</span></span>

<span data-ttu-id="cb31e-116">在[联系人管理器解决方案](the-contact-manager-solution.md)，三个文件控制的生成和部署过程：</span><span class="sxs-lookup"><span data-stu-id="cb31e-116">In the [Contact Manager solution](the-contact-manager-solution.md), three files control the build and deployment process:</span></span>

- <span data-ttu-id="cb31e-117">A*通用项目文件*(*Publish.proj*)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-117">A *universal project file* (*Publish.proj*).</span></span> <span data-ttu-id="cb31e-118">这包含不会更改目标环境之间的生成和部署说明。</span><span class="sxs-lookup"><span data-stu-id="cb31e-118">This contains build and deployment instructions that do not change between destination environments.</span></span>
- <span data-ttu-id="cb31e-119">*特定于环境的项目文件*(*Env Dev.proj*)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-119">An *environment-specific project file* (*Env-Dev.proj*).</span></span> <span data-ttu-id="cb31e-120">这包含特定于特定的目标环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="cb31e-120">This contains build and deployment settings that are specific to a particular destination environment.</span></span> <span data-ttu-id="cb31e-121">例如，可以使用*Env Dev.proj*文件提供用于开发人员或测试环境的设置并创建一个名为的备用文件*Env Stage.proj*来提供设置过渡环境。</span><span class="sxs-lookup"><span data-stu-id="cb31e-121">For example, you could use the *Env-Dev.proj* file to provide settings for a developer or test environment and create an alternative file named *Env-Stage.proj* to provide settings for a staging environment.</span></span>
- <span data-ttu-id="cb31e-122">A*命令文件*(*发布 Dev.cmd*)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-122">A *command file* (*Publish-Dev.cmd*).</span></span> <span data-ttu-id="cb31e-123">这包含指定你的项目文件的命令想要执行的 MSBuild.exe。</span><span class="sxs-lookup"><span data-stu-id="cb31e-123">This contains an MSBuild.exe command that specifies which project files you want to execute.</span></span> <span data-ttu-id="cb31e-124">你可以创建命令文件对于每个目标环境，其中的每个文件都包含的 MSBuild.exe 命令时，指定不同的特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-124">You can create a command file for every destination environment, where each file contains an MSBuild.exe command that specifies a different environment-specific project file.</span></span> <span data-ttu-id="cb31e-125">这使开发人员只需通过运行相应的命令文件，将部署到不同的环境。</span><span class="sxs-lookup"><span data-stu-id="cb31e-125">This lets the developer deploy to different environments simply by running the appropriate command file.</span></span>

<span data-ttu-id="cb31e-126">在示例解决方案中，你可以找到这些发布解决方案文件夹中的三个文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-126">In the sample solution, you can find these three files in the Publish solution folder.</span></span>

![](understanding-the-build-process/_static/image1.png)

<span data-ttu-id="cb31e-127">在这些文件中更详细地讨论之前，让我们看看时使用此方法的总体的生成过程的工作原理。</span><span class="sxs-lookup"><span data-stu-id="cb31e-127">Before you look at these files in more detail, let's take a look at how the overall build process works when you use this approach.</span></span> <span data-ttu-id="cb31e-128">在高级别中，生成和部署过程如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb31e-128">At a high level, the build and deployment process looks like this:</span></span>

![](understanding-the-build-process/_static/image2.png)

<span data-ttu-id="cb31e-129">第一件事是两个项目文件 （&） #x 2014; 一个包含通用生成和部署说明，以及一个包含特定于环境的设置 （&） #x 2014; 将合并到单个项目文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-129">The first thing that happens is that the two project files&#x2014;one containing universal build and deployment instructions, and one containing environment-specific settings&#x2014;are merged into a single project file.</span></span> <span data-ttu-id="cb31e-130">MSBuild 合作通过项目文件中的说明。</span><span class="sxs-lookup"><span data-stu-id="cb31e-130">MSBuild then works through the instructions in the project file.</span></span> <span data-ttu-id="cb31e-131">它将生成每个解决方案，每个项目使用项目文件中的项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-131">It builds each of the projects in the solution, using the project file for each project.</span></span> <span data-ttu-id="cb31e-132">然后，它调用到其他工具，如 Web Deploy (MSDeploy.exe) 并且将你的 web 内容和数据库部署到目标环境在 VSDBCMD 实用程序。</span><span class="sxs-lookup"><span data-stu-id="cb31e-132">It then calls out to other tools, like Web Deploy (MSDeploy.exe) and the VSDBCMD utility to deploy your web content and databases to the target environment.</span></span>

<span data-ttu-id="cb31e-133">从开始到结束，生成和部署过程执行这些任务：</span><span class="sxs-lookup"><span data-stu-id="cb31e-133">From start to finish, the build and deployment process performs these tasks:</span></span>

1. <span data-ttu-id="cb31e-134">它将删除输出目录中，在全新的版本的准备过程中的内容。</span><span class="sxs-lookup"><span data-stu-id="cb31e-134">It deletes the contents of the output directory, in preparation for a fresh build.</span></span>
2. <span data-ttu-id="cb31e-135">生成解决方案中的每个项目：</span><span class="sxs-lookup"><span data-stu-id="cb31e-135">It builds each project in the solution:</span></span>

    1. <span data-ttu-id="cb31e-136">面向 web 项目和 #x 2014; 在这种情况下，ASP.NET MVC web 应用程序和 WCF web 服务和 #x 2014年; 生成过程创建 web 部署包的每个项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-136">For web projects&#x2014;in this case, an ASP.NET MVC web application and a WCF web service&#x2014;the build process creates a web deployment package for each project.</span></span>
    2. <span data-ttu-id="cb31e-137">对于数据库项目，生成过程创建的每个项目的部署清单 （.deploymanifest 文件）。</span><span class="sxs-lookup"><span data-stu-id="cb31e-137">For database projects, the build process creates a deployment manifest (.deploymanifest file) for each project.</span></span>
3. <span data-ttu-id="cb31e-138">它使用 VSDBCMD.exe 实用程序来部署每个数据库项目中使用各种属性从项目文件 （#x 2014年; 目标连接字符串和数据库名称） #x 2014年; 以及.deploymanifest 文件的解决方案。</span><span class="sxs-lookup"><span data-stu-id="cb31e-138">It uses the VSDBCMD.exe utility to deploy each database project in the solution, using various properties from the project files&#x2014;a target connection string and a database name&#x2014;together with the .deploymanifest file.</span></span>
4. <span data-ttu-id="cb31e-139">它使用 MSDeploy.exe 实用程序来部署解决方案，使用项目文件中的各种属性来控制部署过程中每个 web 项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-139">It uses the MSDeploy.exe utility to deploy each web project in the solution, using various properties from the project files to control the deployment process.</span></span>

<span data-ttu-id="cb31e-140">示例解决方案可用于跟踪此过程的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="cb31e-140">You can use the sample solution to trace this process in more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-141">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[配置为目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-141">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="invoking-the-build-and-deployment-process"></a><span data-ttu-id="cb31e-142">调用的生成和部署过程</span><span class="sxs-lookup"><span data-stu-id="cb31e-142">Invoking the Build and Deployment Process</span></span>

<span data-ttu-id="cb31e-143">若要部署到开发人员测试环境的联系人管理器解决方案，开发人员运行*发布 Dev.cmd*命令文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-143">To deploy the Contact Manager solution to a developer test environment, the developer runs the *Publish-Dev.cmd* command file.</span></span> <span data-ttu-id="cb31e-144">这将调用 MSBuild.exe，指定*Publish.proj*作为要执行的项目文件和*Env Dev.proj*作为参数值。</span><span class="sxs-lookup"><span data-stu-id="cb31e-144">This invokes MSBuild.exe, specifying *Publish.proj* as the project file to execute and *Env-Dev.proj* as a parameter value.</span></span>


[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="cb31e-145">**/Fl**切换 (短，无法用于**/fileLogger**) 将生成输出记录到名为的文件*msbuild.log*当前目录中。</span><span class="sxs-lookup"><span data-stu-id="cb31e-145">The **/fl** switch (short for **/fileLogger**) logs the build output to a file named *msbuild.log* in the current directory.</span></span> <span data-ttu-id="cb31e-146">有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-146">For more information, see the [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="cb31e-147">此时，MSBuild 开始运行，加载*Publish.proj*文件，并开始处理其中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="cb31e-147">At this point, MSBuild starts running, loads the *Publish.proj* file, and starts processing the instructions within it.</span></span> <span data-ttu-id="cb31e-148">第一个指令告知导入项目的 MSBuild 文件**TargetEnvPropsFile**参数指定。</span><span class="sxs-lookup"><span data-stu-id="cb31e-148">The first instruction tells MSBuild to import the project file that the **TargetEnvPropsFile** parameter specifies.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]


<span data-ttu-id="cb31e-149">**TargetEnvPropsFile**参数指定*Env Dev.proj*文件，因此 MSBuild 将的内容合并*Env Dev.proj*文件到*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-149">The **TargetEnvPropsFile** parameter specifies the *Env-Dev.proj* file, so MSBuild merges the contents of the *Env-Dev.proj* file into the *Publish.proj* file.</span></span>

<span data-ttu-id="cb31e-150">MSBuild 遇到在合并的项目文件中的下一个元素是属性组。</span><span class="sxs-lookup"><span data-stu-id="cb31e-150">The next elements that MSBuild encounters in the merged project file are property groups.</span></span> <span data-ttu-id="cb31e-151">在文件中出现的顺序处理属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-151">Properties are processed in the order in which they appear in the file.</span></span> <span data-ttu-id="cb31e-152">MSBuild 创建提供满足任何指定的条件的键 / 值对每个属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-152">MSBuild creates a key-value pair for each property, providing that any specified conditions are met.</span></span> <span data-ttu-id="cb31e-153">更高版本的文件中定义的属性将覆盖具有相同名称在文件中前面定义的任何属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-153">Properties defined later in the file will overwrite any properties with the same name defined earlier in the file.</span></span> <span data-ttu-id="cb31e-154">例如，考虑**OutputRoot**属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-154">For example, consider the **OutputRoot** properties.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]


<span data-ttu-id="cb31e-155">当 MSBuild 处理第一个**OutputRoot**元素，提供类似名称的参数未提供，它将的值设置**OutputRoot**属性**...\Publish\Out**。当它遇到第二个**OutputRoot**元素，如果条件计算结果为**true**，它将覆盖的值**OutputRoot**具有的值的属性**OutDir**参数。</span><span class="sxs-lookup"><span data-stu-id="cb31e-155">When MSBuild processes the first **OutputRoot** element, providing a similarly named parameter has not been provided, it sets the value of the **OutputRoot** property to **..\Publish\Out**. When it encounters the second **OutputRoot** element, if the condition evaluates to **true**, it will overwrite the value of the **OutputRoot** property with the value of the **OutDir** parameter.</span></span>

<span data-ttu-id="cb31e-156">MSBuild 遇到下一个元素是一个包含名为的单个项组**ProjectsToBuild**。</span><span class="sxs-lookup"><span data-stu-id="cb31e-156">The next element that MSBuild encounters is a single item group, containing an item named **ProjectsToBuild**.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]


<span data-ttu-id="cb31e-157">MSBuild 的生成名为的项列表来处理此指令**ProjectsToBuild**。</span><span class="sxs-lookup"><span data-stu-id="cb31e-157">MSBuild processes this instruction by building an item list named **ProjectsToBuild**.</span></span> <span data-ttu-id="cb31e-158">在这种情况下，项列表包含的单个值 （&） #x 2014年; 的路径和文件名的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-158">In this case, the item list contains a single value&#x2014;the path and filename of the solution file.</span></span>

<span data-ttu-id="cb31e-159">此时，剩余的元素是目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-159">At this point, the remaining elements are targets.</span></span> <span data-ttu-id="cb31e-160">目标属性和项和 #x 2014年从以不同方式处理; 实质上，目标不会处理除非显式将它们指定用户或项目文件中的另一构造由调用。</span><span class="sxs-lookup"><span data-stu-id="cb31e-160">Targets are processed differently from properties and items&#x2014;essentially, targets are not processed unless they are either explicitly specified by the user or invoked by another construct within the project file.</span></span> <span data-ttu-id="cb31e-161">回想一下，打开**项目**标记包含**DefaultTargets**属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-161">Recall that the opening **Project** tag includes a **DefaultTargets** attribute.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]


<span data-ttu-id="cb31e-162">这会指示 MSBuild 来调用**FullPublish**目标，如果目标不指定何时调用 MSBuild.exe。</span><span class="sxs-lookup"><span data-stu-id="cb31e-162">This instructs MSBuild to invoke the **FullPublish** target, if targets are not specified when MSBuild.exe is invoked.</span></span> <span data-ttu-id="cb31e-163">**FullPublish**目标不包含任何任务; 而是只需指定依赖项的列表。</span><span class="sxs-lookup"><span data-stu-id="cb31e-163">The **FullPublish** target doesn't contain any tasks; instead it simply specifies a list of dependencies.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]


<span data-ttu-id="cb31e-164">此依赖关系指示 MSBuild 该按顺序执行**FullPublish**目标，它必须调用此列表中提供的顺序的目标：</span><span class="sxs-lookup"><span data-stu-id="cb31e-164">This dependency tells MSBuild that in order to execute the **FullPublish** target, it needs to invoke this list of targets in the order provided:</span></span>

1. <span data-ttu-id="cb31e-165">它必须调用**清理**目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-165">It must invoke the **Clean** target.</span></span>
2. <span data-ttu-id="cb31e-166">它必须调用**BuildProjects**目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-166">It must invoke the **BuildProjects** target.</span></span>
3. <span data-ttu-id="cb31e-167">它必须调用**GatherPackagesForPublishing**目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-167">It must invoke the **GatherPackagesForPublishing** target.</span></span>
4. <span data-ttu-id="cb31e-168">它必须调用**PublishDbPackages**目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-168">It must invoke the **PublishDbPackages** target.</span></span>
5. <span data-ttu-id="cb31e-169">它必须调用**PublishWebPackages**目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-169">It must invoke the **PublishWebPackages** target.</span></span>

### <a name="the-clean-target"></a><span data-ttu-id="cb31e-170">Clean 目标</span><span class="sxs-lookup"><span data-stu-id="cb31e-170">The Clean Target</span></span>

<span data-ttu-id="cb31e-171">**清理**目标基本上删除输出目录及其所有内容，在准备进行全新的版本。</span><span class="sxs-lookup"><span data-stu-id="cb31e-171">The **Clean** target basically deletes the output directory and all its contents, as preparation for a fresh build.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]


<span data-ttu-id="cb31e-172">请注意，目标包括**ItemGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="cb31e-172">Notice that the target includes an **ItemGroup** element.</span></span> <span data-ttu-id="cb31e-173">当你定义的属性或中的项**目标**元素，你要创建*动态*属性和项。</span><span class="sxs-lookup"><span data-stu-id="cb31e-173">When you define properties or items within a **Target** element, you're creating *dynamic* properties and items.</span></span> <span data-ttu-id="cb31e-174">换而言之，属性或项未处理执行目标时才可以。</span><span class="sxs-lookup"><span data-stu-id="cb31e-174">In other words, the properties or items aren't processed until the target is executed.</span></span> <span data-ttu-id="cb31e-175">输出目录可能不存在，或包含的任何文件，直到生成过程开始时，因此你不能生成 **\_FilesToDelete**为静态项列表; 你需要等待执行之前。</span><span class="sxs-lookup"><span data-stu-id="cb31e-175">The output directory might not exist or contain any files until the build process begins, so you can't build the **\_FilesToDelete** list as a static item; you have to wait until execution is underway.</span></span> <span data-ttu-id="cb31e-176">在这种情况下，作为在目标内的动态项生成列表。</span><span class="sxs-lookup"><span data-stu-id="cb31e-176">As such, you build the list as a dynamic item within the target.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-177">在这种情况下，因为**清理**目标是要执行的第一个，因此没有真正需要使用动态项组。</span><span class="sxs-lookup"><span data-stu-id="cb31e-177">In this case, because the **Clean** target is the first to be executed, there's no real need to use a dynamic item group.</span></span> <span data-ttu-id="cb31e-178">但是，当您可能想要按不同的顺序在某一时刻执行的目标是在这种情况下，使用动态属性和项的好办法。</span><span class="sxs-lookup"><span data-stu-id="cb31e-178">However, it's good practice to use dynamic properties and items in this type of scenario, as you might want to execute targets in a different order at some point.</span></span>  
> <span data-ttu-id="cb31e-179">您还应避免将声明将永远不会使用的项的目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-179">You should also aim to avoid declaring items that will never be used.</span></span> <span data-ttu-id="cb31e-180">如果你将仅由特定的目标的项，请考虑将它们放置在要删除任何不必要的开销的生成过程的目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-180">If you have items that will only be used by a specific target, consider placing them inside the target to remove any unnecessary overhead on the build process.</span></span>


<span data-ttu-id="cb31e-181">动态到某个位置，项**清理**目标将非常简单，并使用内置**消息**，**删除**，和**RemoveDir**到任务：</span><span class="sxs-lookup"><span data-stu-id="cb31e-181">Dynamic items aside, the **Clean** target is fairly straightforward and makes use of the built-in **Message**, **Delete**, and **RemoveDir** tasks to:</span></span>

1. <span data-ttu-id="cb31e-182">将一条消息发送到记录器。</span><span class="sxs-lookup"><span data-stu-id="cb31e-182">Send a message to the logger.</span></span>
2. <span data-ttu-id="cb31e-183">生成要删除文件的列表。</span><span class="sxs-lookup"><span data-stu-id="cb31e-183">Build a list of files to delete.</span></span>
3. <span data-ttu-id="cb31e-184">删除这些文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-184">Delete the files.</span></span>
4. <span data-ttu-id="cb31e-185">删除输出目录。</span><span class="sxs-lookup"><span data-stu-id="cb31e-185">Remove the output directory.</span></span>

### <a name="the-buildprojects-target"></a><span data-ttu-id="cb31e-186">BuildProjects 目标</span><span class="sxs-lookup"><span data-stu-id="cb31e-186">The BuildProjects Target</span></span>

<span data-ttu-id="cb31e-187">**BuildProjects**目标基本上生成的所有项目中的示例解决方案。</span><span class="sxs-lookup"><span data-stu-id="cb31e-187">The **BuildProjects** target basically builds all the projects in the sample solution.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]


<span data-ttu-id="cb31e-188">此目标中，在前面的主题中，某些详细信息中所述[了解项目文件](understanding-the-project-file.md)，来说明如何任务和目标引用属性和项。</span><span class="sxs-lookup"><span data-stu-id="cb31e-188">This target was described in some detail in the previous topic, [Understanding the Project File](understanding-the-project-file.md), to illustrate how tasks and targets reference properties and items.</span></span> <span data-ttu-id="cb31e-189">此时，你主要感兴趣**MSBuild**任务。</span><span class="sxs-lookup"><span data-stu-id="cb31e-189">At this point, you're mainly interested in the **MSBuild** task.</span></span> <span data-ttu-id="cb31e-190">此任务可用于生成多个项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-190">You can use this task to build multiple projects.</span></span> <span data-ttu-id="cb31e-191">任务不会创建 MSBuild.exe; 的新实例它使用当前正在运行的实例来生成每个项目。</span><span class="sxs-lookup"><span data-stu-id="cb31e-191">The task does not create a new instance of MSBuild.exe; it uses the current running instance to build each project.</span></span> <span data-ttu-id="cb31e-192">在此示例中的关键点是相关的部署属性：</span><span class="sxs-lookup"><span data-stu-id="cb31e-192">The key points of interest in this example are the deployment properties:</span></span>

- <span data-ttu-id="cb31e-193">**DeployOnBuild**属性指示 MSBuild 项目设置中运行任何部署说明，完成每个项目生成时。</span><span class="sxs-lookup"><span data-stu-id="cb31e-193">The **DeployOnBuild** property instructs MSBuild to run any deployment instructions in the project settings when the build of each project is complete.</span></span>
- <span data-ttu-id="cb31e-194">**DeployTarget**属性标识你想要调用后生成项目的目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-194">The **DeployTarget** property identifies the target that you want to invoke after the project is built.</span></span> <span data-ttu-id="cb31e-195">在这种情况下，**包**目标生成项目输出到一个可部署 web 包中。</span><span class="sxs-lookup"><span data-stu-id="cb31e-195">In this case, the **Package** target builds the project output into a deployable web package.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-196">**包**目标调用 Web 发布管道 (WPP)，它提供 MSBuild 和 Web 部署之间的集成。</span><span class="sxs-lookup"><span data-stu-id="cb31e-196">The **Package** target invokes the Web Publishing Pipeline (WPP), which provides integration between MSBuild and Web Deploy.</span></span> <span data-ttu-id="cb31e-197">如果你想要看一看的内置目标 WPP 提供，查看*Microsoft.Web.Publishing.targets*在 %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-197">If you want to take a look at the built-in targets that the WPP provides, review the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>


### <a name="the-gatherpackagesforpublishing-target"></a><span data-ttu-id="cb31e-198">GatherPackagesForPublishing 目标</span><span class="sxs-lookup"><span data-stu-id="cb31e-198">The GatherPackagesForPublishing Target</span></span>

<span data-ttu-id="cb31e-199">如果你先研究**GatherPackagesForPublishing**目标，你会注意到，它实际上并不包含任何任务。</span><span class="sxs-lookup"><span data-stu-id="cb31e-199">If you study the **GatherPackagesForPublishing** target, you'll notice that it doesn't actually contain any tasks.</span></span> <span data-ttu-id="cb31e-200">相反，它包含的单个项组的定义三个动态的项。</span><span class="sxs-lookup"><span data-stu-id="cb31e-200">Instead, it contains a single item group that defines three dynamic items.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]


<span data-ttu-id="cb31e-201">这些项是指创建时的部署包**BuildProjects**目标已执行。</span><span class="sxs-lookup"><span data-stu-id="cb31e-201">These items refer to the deployment packages that were created when the **BuildProjects** target was executed.</span></span> <span data-ttu-id="cb31e-202">你无法定义，这些项以静态方式在项目文件中，因为项目所引用的文件不存在直到**BuildProjects**执行目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-202">You couldn't define these items statically in the project file, because the files to which the items refer don't exist until the **BuildProjects** target is executed.</span></span> <span data-ttu-id="cb31e-203">相反，项必须定义动态目标不会被调用直到内后**BuildProjects**执行目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-203">Instead, the items must be defined dynamically within a target that is not invoked until after the **BuildProjects** target is executed.</span></span>

<span data-ttu-id="cb31e-204">在此目标 （&） #x 2014年中不使用项; 此目标中，只需生成的项和每个项值关联的元数据。</span><span class="sxs-lookup"><span data-stu-id="cb31e-204">The items are not used within this target&#x2014;this target simply builds the items and the metadata associated with each item value.</span></span> <span data-ttu-id="cb31e-205">这些元素处理后， **PublishPackages**项将包含两个值的路径*ContactManager.Mvc.deploy.cmd*文件和路径*ContactManager.Service.deploy.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-205">Once these elements are processed, the **PublishPackages** item will contain two values, the path to the *ContactManager.Mvc.deploy.cmd* file and the path to the *ContactManager.Service.deploy.cmd* file.</span></span> <span data-ttu-id="cb31e-206">Web 部署作为每个项目，web 包的一部分创建这些文件，并且这些是你必须调用的文件以便部署包的部署目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="cb31e-206">Web Deploy creates these files as part of the web package for each project, and these are the files that you must invoke on the destination server in order to deploy the packages.</span></span> <span data-ttu-id="cb31e-207">如果你打开这些文件之一，则基本上会看到使用各种生成特定的参数值的 MSDeploy.exe 命令。</span><span class="sxs-lookup"><span data-stu-id="cb31e-207">If you open up one of these files, you'll basically see an MSDeploy.exe command with various build-specific parameter values.</span></span>

<span data-ttu-id="cb31e-208">**DbPublishPackages**项将包含单个值的路径*ContactManager.Database.deploymanifest*文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-208">The **DbPublishPackages** item will contain a single value, the path to the *ContactManager.Database.deploymanifest* file.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-209">在生成数据库项目，和它将使用 MSBuild 项目文件相同的架构时，会生成一个.deploymanifest 文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-209">A .deploymanifest file is generated when you build a database project, and it uses the same schema as an MSBuild project file.</span></span> <span data-ttu-id="cb31e-210">它包含所有必需部署数据库，包括数据库架构 (.dbschema) 的位置和任何预先部署脚本和后期部署脚本的详细信息的信息。</span><span class="sxs-lookup"><span data-stu-id="cb31e-210">It contains all the information required to deploy a database, including the location of the database schema (.dbschema) and details of any pre-deployment and post-deployment scripts.</span></span> <span data-ttu-id="cb31e-211">有关详细信息，请参阅[概述的数据库生成和部署](https://msdn.microsoft.com/library/aa833165.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-211">For more information, see [An Overview of Database Build and Deployment](https://msdn.microsoft.com/library/aa833165.aspx).</span></span>


<span data-ttu-id="cb31e-212">你将了解有关如何创建和使用在部署包和数据库部署清单的详细信息[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)和[部署数据库项目](deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-212">You'll learn more about how deployment packages and database deployment manifests are created and used in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) and [Deploying Database Projects](deploying-database-projects.md).</span></span>

### <a name="the-publishdbpackages-target"></a><span data-ttu-id="cb31e-213">PublishDbPackages 目标</span><span class="sxs-lookup"><span data-stu-id="cb31e-213">The PublishDbPackages Target</span></span>

<span data-ttu-id="cb31e-214">简要来讲， **PublishDbPackages**目标调用 VSDBCMD 实用程序来部署**ContactManager**到目标环境的数据库。</span><span class="sxs-lookup"><span data-stu-id="cb31e-214">Briefly speaking, the **PublishDbPackages** target invokes the VSDBCMD utility to deploy the **ContactManager** database to a target environment.</span></span> <span data-ttu-id="cb31e-215">配置数据库部署涉及大量的决策和细微差异，并且你将了解有关这个中[部署数据库项目](deploying-database-projects.md)和[将数据库部署自定义为多个环境](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).</span><span class="sxs-lookup"><span data-stu-id="cb31e-215">Configuring database deployment involves lots of decisions and nuances, and you'll learn more about this in [Deploying Database Projects](deploying-database-projects.md) and [Customizing Database Deployments for Multiple Environments](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="cb31e-216">在本主题中，我们将重点此目标的实际函数。</span><span class="sxs-lookup"><span data-stu-id="cb31e-216">In this topic, we'll focus on how this target actually functions.</span></span>

<span data-ttu-id="cb31e-217">首先，请注意，开始标记包含**输出**属性。</span><span class="sxs-lookup"><span data-stu-id="cb31e-217">First, notice that the opening tag includes an **Outputs** attribute.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]


<span data-ttu-id="cb31e-218">这是一个示例的*目标批处理*。</span><span class="sxs-lookup"><span data-stu-id="cb31e-218">This is an example of *target batching*.</span></span> <span data-ttu-id="cb31e-219">在 MSBuild 项目文件中，批处理是一种技术来循环访问集合。</span><span class="sxs-lookup"><span data-stu-id="cb31e-219">In MSBuild project files, batching is a technique for iterating over collections.</span></span> <span data-ttu-id="cb31e-220">值**输出**属性， **"%(DbPublishPackages.Identity)"**，是指**标识**元数据属性**DbPublishPackages**项列表。</span><span class="sxs-lookup"><span data-stu-id="cb31e-220">The value of the **Outputs** attribute, **"%(DbPublishPackages.Identity)"**, refers to the **Identity** metadata property of the **DbPublishPackages** item list.</span></span> <span data-ttu-id="cb31e-221">这一表示法，**Outputs=%***(ItemList.ItemMetadataName)*，将被转换为：</span><span class="sxs-lookup"><span data-stu-id="cb31e-221">This notation, **Outputs=%***(ItemList.ItemMetadataName)*, is translated as:</span></span>

- <span data-ttu-id="cb31e-222">拆分中的项**DbPublishPackages**为包含相同的项目的多个批**标识**元数据值。</span><span class="sxs-lookup"><span data-stu-id="cb31e-222">Split the items in **DbPublishPackages** into batches of items that contain the same **Identity** metadata value.</span></span>
- <span data-ttu-id="cb31e-223">执行一次每批的目标。</span><span class="sxs-lookup"><span data-stu-id="cb31e-223">Execute the target once per batch.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-224">**标识**是之一[内置的元数据值](https://msdn.microsoft.com/library/ms164313.aspx)，分配给在创建的每个项。</span><span class="sxs-lookup"><span data-stu-id="cb31e-224">**Identity** is one of the [built-in metadata values](https://msdn.microsoft.com/library/ms164313.aspx) that is assigned to every item on creation.</span></span> <span data-ttu-id="cb31e-225">它引用的值**包括**属性中**项**元素和 #x 2014年; 换而言之的路径和文件名的项。</span><span class="sxs-lookup"><span data-stu-id="cb31e-225">It refers to the value of the **Include** attribute in the **Item** element&#x2014;in other words, the path and filename of the item.</span></span>


<span data-ttu-id="cb31e-226">在这种情况下，应该永远不会有多个项具有相同的路径和文件名，因为我们实质上正在使用的一个批次大小。</span><span class="sxs-lookup"><span data-stu-id="cb31e-226">In this case, because there should never be more than one item with the same path and filename, we're essentially working with batch sizes of one.</span></span> <span data-ttu-id="cb31e-227">对于每个数据库包，目标被执行一次。</span><span class="sxs-lookup"><span data-stu-id="cb31e-227">The target is executed once for every database package.</span></span>

<span data-ttu-id="cb31e-228">你可以看到中的类似表示法 **\_Cmd**属性，用于生成具有相应的开关的 VSDBCMD 命令。</span><span class="sxs-lookup"><span data-stu-id="cb31e-228">You can see a similar notation in the **\_Cmd** property, which builds a VSDBCMD command with the appropriate switches.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]


<span data-ttu-id="cb31e-229">在这种情况下， **%(DbPublishPackages.DatabaseConnectionString)**， **%(DbPublishPackages.TargetDatabase)**，和**%(DbPublishPackages.FullPath)**所有引用元数据值的**DbPublishPackages**项集合。</span><span class="sxs-lookup"><span data-stu-id="cb31e-229">In this case, **%(DbPublishPackages.DatabaseConnectionString)**, **%(DbPublishPackages.TargetDatabase)**, and **%(DbPublishPackages.FullPath)** all refer to metadata values of the **DbPublishPackages** item collection.</span></span> <span data-ttu-id="cb31e-230"> **\_Cmd**属性由**Exec**任务，调用该命令。</span><span class="sxs-lookup"><span data-stu-id="cb31e-230">The **\_Cmd** property is used by the **Exec** task, which invokes the command.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]


<span data-ttu-id="cb31e-231">由于这一表示法， **Exec**任务将创建基于的独特组合的批次**DatabaseConnectionString**， **TargetDatabase**，和**FullPath**元数据值，并且任务将执行一次每个批处理。</span><span class="sxs-lookup"><span data-stu-id="cb31e-231">As a result of this notation, the **Exec** task will create batches based on unique combinations of the **DatabaseConnectionString**, **TargetDatabase**, and **FullPath** metadata values, and the task will execute once for each batch.</span></span> <span data-ttu-id="cb31e-232">这是一个示例的*任务批处理*。</span><span class="sxs-lookup"><span data-stu-id="cb31e-232">This is an example of *task batching*.</span></span> <span data-ttu-id="cb31e-233">但是，因为目标级别批处理已划分为单个项的批次，我们项集合**Exec**任务将运行一次，并且每个迭代的目标的一次。</span><span class="sxs-lookup"><span data-stu-id="cb31e-233">However, because the target-level batching has already divided our item collection into single-item batches, the **Exec** task will run once and only once for each iteration of the target.</span></span> <span data-ttu-id="cb31e-234">换而言之，此任务时，将调用一次为解决方案中每个数据库包 VSDBCMD 实用程序。</span><span class="sxs-lookup"><span data-stu-id="cb31e-234">In other words, this task invokes the VSDBCMD utility once for each database package in the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="cb31e-235">目标和任务批处理的详细信息，请参阅 MSBuild[批处理](https://msdn.microsoft.com/library/ms171473.aspx)，[目标批处理中的项元数据](https://msdn.microsoft.com/library/ms228229.aspx)，和[任务批处理中的项元数据](https://msdn.microsoft.com/library/ms171474.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-235">For more information on target and task batching, see MSBuild [Batching](https://msdn.microsoft.com/library/ms171473.aspx), [Item Metadata in Target Batching](https://msdn.microsoft.com/library/ms228229.aspx), and [Item Metadata in Task Batching](https://msdn.microsoft.com/library/ms171474.aspx).</span></span>


### <a name="the-publishwebpackages-target"></a><span data-ttu-id="cb31e-236">PublishWebPackages 目标</span><span class="sxs-lookup"><span data-stu-id="cb31e-236">The PublishWebPackages Target</span></span>

<span data-ttu-id="cb31e-237">通过此点已调用**BuildProjects**目标，生成的每个项目的 web 部署包中的示例解决方案。</span><span class="sxs-lookup"><span data-stu-id="cb31e-237">By this point, you've invoked the **BuildProjects** target, which generates a web deployment package for each project in the sample solution.</span></span> <span data-ttu-id="cb31e-238">伴随每个包会*deploy.cmd*文件，其中包含将包部署到目标环境所需的 MSDeploy.exe 命令，和一个*SetParameters.xml*文件，它指定目标环境的必要的详细信息。</span><span class="sxs-lookup"><span data-stu-id="cb31e-238">Accompanying each package is a *deploy.cmd* file, which contains the MSDeploy.exe commands required to deploy the package to the target environment, and a *SetParameters.xml* file, which specifies the necessary details of the target environment.</span></span> <span data-ttu-id="cb31e-239">您已调用**GatherPackagesForPublishing**目标，生成一个项集合，其中包含*deploy.cmd*你感兴趣的文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-239">You've also invoked the **GatherPackagesForPublishing** target, which generates an item collection containing the *deploy.cmd* files you're interested in.</span></span> <span data-ttu-id="cb31e-240">从根本上来说， **PublishWebPackages**目标执行这些功能：</span><span class="sxs-lookup"><span data-stu-id="cb31e-240">Essentially, the **PublishWebPackages** target performs these functions:</span></span>

- <span data-ttu-id="cb31e-241">它操作*SetParameters.xml*每个包以便包含目标环境的正确详细信息的文件使用**XmlPoke**任务。</span><span class="sxs-lookup"><span data-stu-id="cb31e-241">It manipulates the *SetParameters.xml* file for each package to include the correct details for the target environment, using the **XmlPoke** task.</span></span>
- <span data-ttu-id="cb31e-242">它将调用*deploy.cmd*文件对于每个包，使用相应的开关。</span><span class="sxs-lookup"><span data-stu-id="cb31e-242">It invokes the *deploy.cmd* file for each package, using the appropriate switches.</span></span>

<span data-ttu-id="cb31e-243">就像**PublishDbPackages**目标， **PublishWebPackages**目标使用目标批处理以确保目标执行一次，每个 web 包。</span><span class="sxs-lookup"><span data-stu-id="cb31e-243">Just like the **PublishDbPackages** target, the **PublishWebPackages** target uses target batching to ensure that the target is executed once for each web package.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]


<span data-ttu-id="cb31e-244">在目标， **Exec**任务用于运行*deploy.cmd*为每个 web 包的文件。</span><span class="sxs-lookup"><span data-stu-id="cb31e-244">Within the target, the **Exec** task is used to run the *deploy.cmd* file for each web package.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]


<span data-ttu-id="cb31e-245">有关配置 web 包的部署的详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="cb31e-245">For more information on configuring the deployment of web packages, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="cb31e-246">结束语</span><span class="sxs-lookup"><span data-stu-id="cb31e-246">Conclusion</span></span>

<span data-ttu-id="cb31e-247">本主题提供如何使用拆分项目文件来控制从开始到完成的联系人管理器示例解决方案的生成和部署过程的演练。</span><span class="sxs-lookup"><span data-stu-id="cb31e-247">This topic provided a walkthrough of how split project files are used to control the build and deployment process from start to finish for the Contact Manager sample solution.</span></span> <span data-ttu-id="cb31e-248">使用此方法只需通过运行特定于环境的命令文件允许你运行复杂，在单个、 可重复执行步骤中，企业级部署。</span><span class="sxs-lookup"><span data-stu-id="cb31e-248">Using this approach lets you run complex, enterprise-scale deployments in a single, repeatable step, simply by running an environment-specific command file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="cb31e-249">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="cb31e-249">Further Reading</span></span>

<span data-ttu-id="cb31e-250">项目文件和 WPP 的更深入介绍，请参阅[内 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。</span><span class="sxs-lookup"><span data-stu-id="cb31e-250">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="cb31e-251">[上一页](understanding-the-project-file.md)
[下一页](building-and-packaging-web-application-projects.md)</span><span class="sxs-lookup"><span data-stu-id="cb31e-251">[Previous](understanding-the-project-file.md)
[Next](building-and-packaging-web-application-projects.md)</span></span>
