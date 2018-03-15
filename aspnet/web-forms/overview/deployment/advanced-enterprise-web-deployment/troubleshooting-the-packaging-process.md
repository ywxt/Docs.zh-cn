---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: "打包过程的故障排除 |Microsoft 文档"
author: jrjlee
description: "本主题介绍如何使用在 M EnablePackageProcessLoggingAndAssert 属性可以收集有关打包过程的详细的信息..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 977077357eb5774193a40c55fabee9733dd5ab2f
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="47dcd-103">打包过程的故障排除</span><span class="sxs-lookup"><span data-stu-id="47dcd-103">Troubleshooting the Packaging Process</span></span>
====================
<span data-ttu-id="47dcd-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="47dcd-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="47dcd-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="47dcd-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="47dcd-106">本主题介绍如何使用可以收集有关打包过程的详细的信息**EnablePackageProcessLoggingAndAssert** Microsoft Build Engine (MSBuild) 中的属性。</span><span class="sxs-lookup"><span data-stu-id="47dcd-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="47dcd-107">当你将设置**EnablePackageProcessLoggingAndAssert**属性**true**，MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="47dcd-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="47dcd-108">将有关打包过程的其他信息添加到生成日志。</span><span class="sxs-lookup"><span data-stu-id="47dcd-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="47dcd-109">例如，记录在某些情况下的错误，如果打包列表中找到重复的文件。</span><span class="sxs-lookup"><span data-stu-id="47dcd-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="47dcd-110">创建中的日志目录*ProjectName*\_包文件夹，并使用它来记录有关要打包的文件信息。</span><span class="sxs-lookup"><span data-stu-id="47dcd-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="47dcd-111">如果在打包过程失败，或你的 web 部署包不包含预期的文件，你可以使用此信息进行故障排除的进程和定点其中事情的进展状况错误。</span><span class="sxs-lookup"><span data-stu-id="47dcd-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="47dcd-112">**EnablePackageProcessLoggingAndAssert**属性仅适用如果生成你的项目使用**调试**配置。</span><span class="sxs-lookup"><span data-stu-id="47dcd-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="47dcd-113">在其他配置，将忽略此属性。</span><span class="sxs-lookup"><span data-stu-id="47dcd-113">The property is ignored in other configurations.</span></span>


<span data-ttu-id="47dcd-114">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案 （&） #x 2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 的 web 应用程序Communication Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="47dcd-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="47dcd-115">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在其中生成过程控制由两个项目文件 （&） #x 2014; 一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="47dcd-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="47dcd-116">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="47dcd-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="47dcd-117">了解 EnablePackageProcessLoggingAndAssert 属性</span><span class="sxs-lookup"><span data-stu-id="47dcd-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="47dcd-118">[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)描述如何 Web 发布管道 (WPP) 提供了一套扩展 MSBuild 的功能，使其能够与 Internet Information Services (IIS) Web 集成 MSBuild 目标部署工具 （Web 部署）。</span><span class="sxs-lookup"><span data-stu-id="47dcd-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="47dcd-119">当打包 web 应用程序项目时，在调用 WPP 目标。</span><span class="sxs-lookup"><span data-stu-id="47dcd-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="47dcd-120">大量这些 WPP 目标包括记录的其他信息的条件逻辑时**EnablePackageProcessLoggingAndAssert**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="47dcd-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="47dcd-121">例如，如果你查看**包**目标，你可以看到它创建的其他日志目录和文件的列表写入一个文本文件中，如果**EnablePackageProcessLoggingAndAssert**等于**true**。</span><span class="sxs-lookup"><span data-stu-id="47dcd-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]


> [!NOTE]
> <span data-ttu-id="47dcd-122">在中定义的 WPP 目标*Microsoft.Web.Publishing.targets*在 %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="47dcd-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="47dcd-123">你可以打开此文件，并查看在 Visual Studio 2010 或任何 XML 编辑器中的目标。</span><span class="sxs-lookup"><span data-stu-id="47dcd-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="47dcd-124">请注意不要修改文件的内容。</span><span class="sxs-lookup"><span data-stu-id="47dcd-124">Take care not to modify the contents of the file.</span></span>


## <a name="enabling-the-additional-logging"></a><span data-ttu-id="47dcd-125">启用其他日志记录</span><span class="sxs-lookup"><span data-stu-id="47dcd-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="47dcd-126">你可以提供的值**EnablePackageProcessLoggingAndAssert**以多种方式，具体取决于如何生成你的项目的属性。</span><span class="sxs-lookup"><span data-stu-id="47dcd-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="47dcd-127">如果你从命令行的项目生成时，你可以提供的值**EnablePackageProcessLoggingAndAssert**作为命令行自变量的属性：</span><span class="sxs-lookup"><span data-stu-id="47dcd-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>


[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]


<span data-ttu-id="47dcd-128">如果你使用自定义项目文件生成你的项目，你可以包括**EnablePackageProcessLoggingAndAssert**中的值**属性**属性**MSBuild**任务：</span><span class="sxs-lookup"><span data-stu-id="47dcd-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]


<span data-ttu-id="47dcd-129">如果你使用 Team Foundation Server (TFS) 生成定义生成你的项目，则可以提供的值**EnablePackageProcessLoggingAndAssert**中的属性**MSBuild 参数**行：![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="47dcd-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="47dcd-130">有关创建和配置生成定义的详细信息，请参阅[创建生成定义，支持部署](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="47dcd-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>


<span data-ttu-id="47dcd-131">或者，如果你想要包含在每次生成中的包，你可以修改为 web 应用程序项目设置的项目文件**EnablePackageProcessLoggingAndAssert**属性**true**。</span><span class="sxs-lookup"><span data-stu-id="47dcd-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="47dcd-132">应将属性添加到第一个**PropertyGroup**在.csproj 或.vbproj 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="47dcd-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]


## <a name="reviewing-the-log-files"></a><span data-ttu-id="47dcd-133">查看日志文件</span><span class="sxs-lookup"><span data-stu-id="47dcd-133">Reviewing the Log Files</span></span>

<span data-ttu-id="47dcd-134">当生成并打包 web 应用程序项目**EnablePackageProcessLoggingAndAssert**设置为**true**，MSBuild 会创建名为登录的其他文件夹*ProjectName*\_包文件夹。</span><span class="sxs-lookup"><span data-stu-id="47dcd-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="47dcd-135">日志文件夹包含各种文件：</span><span class="sxs-lookup"><span data-stu-id="47dcd-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="47dcd-136">你看到的文件的列表将因你的项目和你的生成过程中的内容。</span><span class="sxs-lookup"><span data-stu-id="47dcd-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="47dcd-137">但是，这些文件通常用于记录的打包，各个阶段的过程 WPP 正在收集的文件的列表：</span><span class="sxs-lookup"><span data-stu-id="47dcd-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="47dcd-138">*PreExcludePipelineCollectFilesPhaseFileList.txt*文件列出了 MSBuild 收集的有关打包排除指定任何文件被删除之前的文件。</span><span class="sxs-lookup"><span data-stu-id="47dcd-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="47dcd-139">*AfterExcludeFilesFilesList.txt*后将删除指定排除任何文件，文件将包含的修改后的文件列表。</span><span class="sxs-lookup"><span data-stu-id="47dcd-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47dcd-140">有关从打包过程中排除文件和文件夹的详细信息，请参阅[排除文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="47dcd-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="47dcd-141">*AfterTransformWebConfig.txt*文件列出了收集后任何打包的文件*Web.config*转换已执行。</span><span class="sxs-lookup"><span data-stu-id="47dcd-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="47dcd-142">在此列表中，任何配置特定*Web.config*转换文件，如*Web.Debug.config*和*Web.Release.config*，从列表中的文件排除打包。</span><span class="sxs-lookup"><span data-stu-id="47dcd-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="47dcd-143">单个转换*Web.config*包含在它们的位置。</span><span class="sxs-lookup"><span data-stu-id="47dcd-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="47dcd-144">*PostAutoParameterizationWebConfigConnectionStrings.txt*文件后的连接字符串中包含的文件列表*Web.config*拥有已参数化的文件。</span><span class="sxs-lookup"><span data-stu-id="47dcd-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="47dcd-145">这是允许你在部署程序包时，将连接字符串替换为你的目标环境的正确设置的过程。</span><span class="sxs-lookup"><span data-stu-id="47dcd-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="47dcd-146">*Prepackage.txt*文件包含的文件在包中包括的完成预生成列表。</span><span class="sxs-lookup"><span data-stu-id="47dcd-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="47dcd-147">额外的日志文件的名称通常与 WPP 目标相对应。</span><span class="sxs-lookup"><span data-stu-id="47dcd-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="47dcd-148">你可以通过检查查看这些目标*Microsoft.Web.Publishing.targets*在 %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="47dcd-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>


<span data-ttu-id="47dcd-149">如果 web 包的内容不是所期望的内容，查看这些文件非常有用的方式来标识在过程操作中的哪个点发生了错误。</span><span class="sxs-lookup"><span data-stu-id="47dcd-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="47dcd-150">结束语</span><span class="sxs-lookup"><span data-stu-id="47dcd-150">Conclusion</span></span>

<span data-ttu-id="47dcd-151">本主题描述如何使用**EnablePackageProcessLoggingAndAssert** MSBuild 进行故障排除在打包过程中的属性。</span><span class="sxs-lookup"><span data-stu-id="47dcd-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="47dcd-152">它解释你可以在其中提供到生成过程中，属性值的不同方法，它描述了加密时，将属性设置为记录的其他信息**true**。</span><span class="sxs-lookup"><span data-stu-id="47dcd-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="47dcd-153">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="47dcd-153">Further Reading</span></span>

<span data-ttu-id="47dcd-154">使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="47dcd-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="47dcd-155">WPP 和它如何管理打包过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="47dcd-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="47dcd-156">有关如何从 web 部署包中排除特定文件和文件夹的指南，请参阅[排除文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="47dcd-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="47dcd-157">上一篇</span><span class="sxs-lookup"><span data-stu-id="47dcd-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
