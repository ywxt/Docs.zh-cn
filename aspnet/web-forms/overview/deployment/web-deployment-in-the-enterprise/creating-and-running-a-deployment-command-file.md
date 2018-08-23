---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 创建和运行的部署命令文件 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何生成命令文件，以便可以运行使用 Microsoft Build Engine (MSBuild) 项目文件作为单步，重新部署...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: 121df7482f7cbd70b191e518bae791f0642ccc7c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831855"
---
<a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="f7b10-103">创建和运行部署命令文件</span><span class="sxs-lookup"><span data-stu-id="f7b10-103">Creating and Running a Deployment Command File</span></span>
====================
<span data-ttu-id="f7b10-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f7b10-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f7b10-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f7b10-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f7b10-106">本主题介绍如何生成将允许您运行作为一个单步执行、 可重复的过程中使用 Microsoft Build Engine (MSBuild) 项目文件的部署的命令文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>


<span data-ttu-id="f7b10-107">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014;[联系人管理器](the-contact-manager-solution.md)解决方案&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="f7b10-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="f7b10-108">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解构建过程](understanding-the-build-process.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="f7b10-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="f7b10-109">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="f7b10-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="f7b10-110">过程概述</span><span class="sxs-lookup"><span data-stu-id="f7b10-110">Process Overview</span></span>

<span data-ttu-id="f7b10-111">在本主题中，您将学习如何创建和运行使用这些项目文件来执行可重复部署到目标环境的命令文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="f7b10-112">从根本上来说，命令文件只需包含的 MSBuild 命令的：</span><span class="sxs-lookup"><span data-stu-id="f7b10-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="f7b10-113">告知 MSBuild 执行环境不可知*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="f7b10-114">告知*Publish.proj*哪些文件包含特定于环境的项目设置和在哪里可以找到它的文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="f7b10-115">创建 MSBuild 命令</span><span class="sxs-lookup"><span data-stu-id="f7b10-115">Create an MSBuild Command</span></span>

<span data-ttu-id="f7b10-116">如中所述[了解构建过程](understanding-the-build-process.md)，特定于环境的项目文件&#x2014;等*Env Dev.proj*&#x2014;设计要导入到环境不可知*Publish.proj*在生成时的文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="f7b10-117">在一起，这两个文件提供一组完整的说明，告知 MSBuild 如何生成和部署你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7b10-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="f7b10-118">*Publish.proj*文件使用**导入**元素导入特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>


[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]


<span data-ttu-id="f7b10-119">在这种情况下，当您使用 MSBuild.exe 生成和部署 Contact Manager 解决方案，您需要：</span><span class="sxs-lookup"><span data-stu-id="f7b10-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="f7b10-120">在上运行 MSBuild.exe *Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="f7b10-121">通过提供一个名为的命令行参数来指定特定于环境的项目文件的位置**TargetEnvPropsFile**。</span><span class="sxs-lookup"><span data-stu-id="f7b10-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="f7b10-122">若要执行此操作，MSBuild 命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="f7b10-122">To do this, your MSBuild command should resemble this:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]


<span data-ttu-id="f7b10-123">在这里，它是一个简单的步骤，以将移至可重复、 单步执行部署。</span><span class="sxs-lookup"><span data-stu-id="f7b10-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="f7b10-124">您需要做是将您的 MSBuild 命令添加到.cmd 文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="f7b10-125">Contact Manager 解决方案，在 Publish 文件夹包含名为的文件*发布 Dev.cmd* ，正好可以实现此。</span><span class="sxs-lookup"><span data-stu-id="f7b10-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="f7b10-126">**/Fl**开关指示 MSBuild 创建名为的日志文件*msbuild.log*调用 MSBuild.exe 时的工作目录中。</span><span class="sxs-lookup"><span data-stu-id="f7b10-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>


<span data-ttu-id="f7b10-127">若要部署或重新部署 Contact Manager 解决方案，只需运行*发布 Dev.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="f7b10-128">当您运行该文件时，则 MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="f7b10-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="f7b10-129">生成解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="f7b10-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="f7b10-130">生成 web 应用程序项目的可部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="f7b10-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="f7b10-131">生成数据库项目的.dbschema 和.deploymanifest 文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="f7b10-132">将 web 程序包部署到 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f7b10-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="f7b10-133">将数据库部署到数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f7b10-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="f7b10-134">运行部署</span><span class="sxs-lookup"><span data-stu-id="f7b10-134">Run the Deployment</span></span>

<span data-ttu-id="f7b10-135">已为你的目标环境创建命令文件，应该能够完成整个部署，只需运行该文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="f7b10-136">**若要将 Contact Manager 解决方案部署到你的测试环境**</span><span class="sxs-lookup"><span data-stu-id="f7b10-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="f7b10-137">在开发人员工作站中，打开 Windows 资源管理器，然后浏览到的位置*发布 Dev.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="f7b10-138">双击该文件以运行它。</span><span class="sxs-lookup"><span data-stu-id="f7b10-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="f7b10-139">如果**打开文件 – 安全警告**出现对话框，请单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="f7b10-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="f7b10-140">如果你的配置设置和测试服务器将设置正确，在命令提示符窗口将显示**生成成功**MSBuild 已完成处理的项目文件时，消息。</span><span class="sxs-lookup"><span data-stu-id="f7b10-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="f7b10-141">如果这是首次已将解决方案部署到此环境，你将需要添加到测试 web 服务器计算机帐户**db\_datawriter**并**db\_datareader**上的角色**ContactManager**数据库。</span><span class="sxs-lookup"><span data-stu-id="f7b10-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="f7b10-142">此过程所述[数据库服务器配置用于 Web 部署发布](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f7b10-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7b10-143">只需创建数据库时分配这些权限。</span><span class="sxs-lookup"><span data-stu-id="f7b10-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="f7b10-144">默认情况下，生成过程将不会重新创建每个部署上的数据库&#x2014;相反，它将比较最新的架构的现有数据库并进行所需更改。</span><span class="sxs-lookup"><span data-stu-id="f7b10-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="f7b10-145">因此，只需将这些数据库角色映射第一次部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7b10-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="f7b10-146">打开 Internet Explorer 并浏览到联系人管理器应用程序的 URL (例如， `http://testweb1:85/ContactManager/`)。</span><span class="sxs-lookup"><span data-stu-id="f7b10-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="f7b10-147">验证应用程序按预期方式正常工作，您可以添加联系人。</span><span class="sxs-lookup"><span data-stu-id="f7b10-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="f7b10-148">结束语</span><span class="sxs-lookup"><span data-stu-id="f7b10-148">Conclusion</span></span>

<span data-ttu-id="f7b10-149">创建命令文件包含 MSBuild 说明为您提供构建和部署到特定的目标环境的多项目解决方案的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="f7b10-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="f7b10-150">如果需要反复将你的解决方案部署到多个目标环境，可以创建多个命令文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="f7b10-151">在每个命令文件中，MSBuild 命令将生成相同的通用项目文件中，但它将指定不同的特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="f7b10-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="f7b10-152">例如，若要将发布到开发人员或测试环境的命令文件可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="f7b10-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]


<span data-ttu-id="f7b10-153">要将发布到过渡环境的命令文件可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="f7b10-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="f7b10-154">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="f7b10-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


<span data-ttu-id="f7b10-155">你还可以通过重写属性或在 MSBuild 命令中设置各种其他开关来定义每个环境的生成过程。</span><span class="sxs-lookup"><span data-stu-id="f7b10-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="f7b10-156">有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7b10-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7b10-157">[上一页](deploying-database-projects.md)
> [下一页](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f7b10-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
