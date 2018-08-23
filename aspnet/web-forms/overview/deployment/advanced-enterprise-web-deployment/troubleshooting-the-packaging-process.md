---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 打包过程故障排除 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在 M 使用 EnablePackageProcessLoggingAndAssert 属性可以收集有关打包过程的详细的信息...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 22be1ccc5a1ec52d143bedffd79264918c1a45e1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833244"
---
<a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="88219-103">打包过程故障排除</span><span class="sxs-lookup"><span data-stu-id="88219-103">Troubleshooting the Packaging Process</span></span>
====================
<span data-ttu-id="88219-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="88219-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="88219-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="88219-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="88219-106">本主题介绍如何使用可以收集有关打包过程的详细的信息**EnablePackageProcessLoggingAndAssert** Microsoft Build Engine (MSBuild) 中的属性。</span><span class="sxs-lookup"><span data-stu-id="88219-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="88219-107">当您将设置**EnablePackageProcessLoggingAndAssert**属性设置为**true**，MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="88219-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="88219-108">将有关打包过程的其他信息添加到生成日志。</span><span class="sxs-lookup"><span data-stu-id="88219-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="88219-109">例如，记录在某些情况下的错误，如果在打包列表中找到重复的文件。</span><span class="sxs-lookup"><span data-stu-id="88219-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="88219-110">创建中的日志目录*ProjectName*\_包文件夹并使用它来记录有关要打包的文件信息。</span><span class="sxs-lookup"><span data-stu-id="88219-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="88219-111">如果打包过程失败，或你的 web 部署包不包含预期的文件，您可以使用此信息进程和 pinpoint 进行故障排除的使用情况问题。</span><span class="sxs-lookup"><span data-stu-id="88219-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="88219-112">**EnablePackageProcessLoggingAndAssert**只有在生成项目使用，仅适用于属性**调试**配置。</span><span class="sxs-lookup"><span data-stu-id="88219-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="88219-113">在其他配置中将忽略此属性。</span><span class="sxs-lookup"><span data-stu-id="88219-113">The property is ignored in other configurations.</span></span>


<span data-ttu-id="88219-114">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="88219-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="88219-115">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="88219-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="88219-116">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="88219-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="88219-117">了解 EnablePackageProcessLoggingAndAssert 属性</span><span class="sxs-lookup"><span data-stu-id="88219-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="88219-118">[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)描述如何为 Web 发布管道 (WPP) 提供的一组扩展的 MSBuild 功能并使其能够与 Internet 信息服务 (IIS) Web 集成的 MSBuild 目标部署工具 （Web 部署）。</span><span class="sxs-lookup"><span data-stu-id="88219-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="88219-119">在打包 web 应用程序项目时，调用 WPP 目标。</span><span class="sxs-lookup"><span data-stu-id="88219-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="88219-120">许多这些 WPP 目标包括记录的其他信息的条件逻辑时**EnablePackageProcessLoggingAndAssert**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="88219-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="88219-121">例如，如果您查看**包**目标，可以看到它创建一个额外的日志目录，并将文件的列表写入到一个文本文件，如果**EnablePackageProcessLoggingAndAssert**等于 **，则返回 true**。</span><span class="sxs-lookup"><span data-stu-id="88219-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]


> [!NOTE]
> <span data-ttu-id="88219-122">在中定义的 WPP 目标*Microsoft.Web.Publishing.targets* %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="88219-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="88219-123">您可以打开此文件并查看 Visual Studio 2010 或任何 XML 编辑器中的目标。</span><span class="sxs-lookup"><span data-stu-id="88219-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="88219-124">请注意不要修改该文件的内容。</span><span class="sxs-lookup"><span data-stu-id="88219-124">Take care not to modify the contents of the file.</span></span>


## <a name="enabling-the-additional-logging"></a><span data-ttu-id="88219-125">启用其他日志记录</span><span class="sxs-lookup"><span data-stu-id="88219-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="88219-126">您可以提供的值**EnablePackageProcessLoggingAndAssert**以各种方式，具体取决于如何构建您的项目的属性。</span><span class="sxs-lookup"><span data-stu-id="88219-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="88219-127">如果生成你的项目从命令行，则可以提供的值**EnablePackageProcessLoggingAndAssert**属性作为命令行参数：</span><span class="sxs-lookup"><span data-stu-id="88219-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>


[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]


<span data-ttu-id="88219-128">如果您使用自定义项目文件来生成项目，则可以包括**EnablePackageProcessLoggingAndAssert**中的值**属性**属性的**MSBuild**任务：</span><span class="sxs-lookup"><span data-stu-id="88219-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]


<span data-ttu-id="88219-129">如果要使用 Team Foundation Server (TFS) 生成定义来构建您的项目，则可以提供的值**EnablePackageProcessLoggingAndAssert**属性中的**MSBuild 参数**行：![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="88219-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="88219-130">有关创建和配置生成定义的详细信息，请参阅[创建生成定义，支持部署](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="88219-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>


<span data-ttu-id="88219-131">或者，如果你想要在每次生成中包含的包，您可以修改 web 应用程序项目设置的项目文件**EnablePackageProcessLoggingAndAssert**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="88219-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="88219-132">应将属性添加到第一个**PropertyGroup** .csproj 或.vbproj 文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="88219-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]


## <a name="reviewing-the-log-files"></a><span data-ttu-id="88219-133">查看日志文件</span><span class="sxs-lookup"><span data-stu-id="88219-133">Reviewing the Log Files</span></span>

<span data-ttu-id="88219-134">当生成并打包 web 应用程序项目**EnablePackageProcessLoggingAndAssert**设置为**true**，MSBuild 将创建名为日志中的其他文件夹*ProjectName*\_包文件夹。</span><span class="sxs-lookup"><span data-stu-id="88219-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="88219-135">日志文件夹包含多个文件：</span><span class="sxs-lookup"><span data-stu-id="88219-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="88219-136">您看到的文件的列表将因你的项目和生成过程中的内容。</span><span class="sxs-lookup"><span data-stu-id="88219-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="88219-137">但是，这些文件通常用于记录的收集 WPP 打包过程的各个阶段的文件列表：</span><span class="sxs-lookup"><span data-stu-id="88219-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="88219-138">*PreExcludePipelineCollectFilesPhaseFileList.txt*文件列出了进行打包删除指定排除任何文件之前的 MSBuild 收集的文件。</span><span class="sxs-lookup"><span data-stu-id="88219-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="88219-139">*AfterExcludeFilesFilesList.txt*文件包含已修改的文件列表中移除指定排除任何文件之后。</span><span class="sxs-lookup"><span data-stu-id="88219-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="88219-140">从打包过程中排除文件和文件夹的详细信息，请参阅[不包括文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="88219-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="88219-141">*AfterTransformWebConfig.txt*文件列出了收集后任何打包的文件*Web.config*已执行转换。</span><span class="sxs-lookup"><span data-stu-id="88219-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="88219-142">在此列表中，任何配置特定于*Web.config*转换文件，如*Web.Debug.config*并*Web.Release.config*，从适用于的文件列表中排除打包。</span><span class="sxs-lookup"><span data-stu-id="88219-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="88219-143">转换的单个*Web.config*包含在其位置。</span><span class="sxs-lookup"><span data-stu-id="88219-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="88219-144">*PostAutoParameterizationWebConfigConnectionStrings.txt*文件后的连接字符串中包含的文件列表*Web.config*文件已参数化。</span><span class="sxs-lookup"><span data-stu-id="88219-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="88219-145">这是过程，您可以将连接字符串替换为目标环境的正确设置为部署包时。</span><span class="sxs-lookup"><span data-stu-id="88219-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="88219-146">*Prepackage.txt*文件包含的文件要包含在包中已完成的预生成列表。</span><span class="sxs-lookup"><span data-stu-id="88219-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="88219-147">额外的日志文件的名称通常与 WPP 目标相对应。</span><span class="sxs-lookup"><span data-stu-id="88219-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="88219-148">你可以通过检查来查看这些目标*Microsoft.Web.Publishing.targets* %programfiles (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="88219-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>


<span data-ttu-id="88219-149">如果 web 程序包的内容不是预期的内容，查看这些文件非常有用的方式来标识在处理操作中的哪个点发生了错误。</span><span class="sxs-lookup"><span data-stu-id="88219-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="88219-150">结束语</span><span class="sxs-lookup"><span data-stu-id="88219-150">Conclusion</span></span>

<span data-ttu-id="88219-151">本主题介绍如何使用**EnablePackageProcessLoggingAndAssert**在 MSBuild 中打包过程进行故障排除的属性。</span><span class="sxs-lookup"><span data-stu-id="88219-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="88219-152">所述的不同方法可以在其中提供属性值设置为生成过程中，并描述了将属性设置为时记录的其他信息 **，则返回 true**。</span><span class="sxs-lookup"><span data-stu-id="88219-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="88219-153">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="88219-153">Further Reading</span></span>

<span data-ttu-id="88219-154">使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="88219-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="88219-155">WPP 和它如何管理打包过程的详细信息，请参阅[构建和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="88219-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="88219-156">有关如何从 web 部署包中排除特定文件和文件夹的指导，请参阅[不包括文件和文件夹从部署](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="88219-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="88219-157">上一篇</span><span class="sxs-lookup"><span data-stu-id="88219-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
