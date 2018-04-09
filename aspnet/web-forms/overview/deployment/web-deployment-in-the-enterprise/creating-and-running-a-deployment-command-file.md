---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 创建并运行部署命令文件 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何构建命令文件，以便可以运行使用 Microsoft Build Engine (MSBuild) 项目文件作为单步重新部署...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: e5fb034a67bc9f2ea549af269eae51a49acc4d98
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="4aea3-103">创建并运行部署命令文件</span><span class="sxs-lookup"><span data-stu-id="4aea3-103">Creating and Running a Deployment Command File</span></span>
====================
<span data-ttu-id="4aea3-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4aea3-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4aea3-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="4aea3-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4aea3-106">本主题介绍如何生成一个，可以运行作为一个单步执行、 可重复的过程中使用 Microsoft Build Engine (MSBuild) 项目文件的部署的命令文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>


<span data-ttu-id="4aea3-107">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案&#x2014;[联系人管理器](the-contact-manager-solution.md)解决方案&#x2014;来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="4aea3-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="4aea3-108">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解该生成过程](understanding-the-build-process.md)，两个项目文件中的生成过程控制通过&#x2014;另一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="4aea3-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="4aea3-109">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="4aea3-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="4aea3-110">过程概述</span><span class="sxs-lookup"><span data-stu-id="4aea3-110">Process Overview</span></span>

<span data-ttu-id="4aea3-111">在本主题中，你将学习如何创建和运行使用这些项目文件来执行可重复部署到你的目标环境的命令文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="4aea3-112">实质上，命令文件只需包含的 MSBuild 命令的：</span><span class="sxs-lookup"><span data-stu-id="4aea3-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="4aea3-113">指示要执行环境不可知的 MSBuild *Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="4aea3-114">告知*Publish.proj*哪些文件包含特定于环境的项目设置和在哪里可以找到它的文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="4aea3-115">创建的 MSBuild 命令</span><span class="sxs-lookup"><span data-stu-id="4aea3-115">Create an MSBuild Command</span></span>

<span data-ttu-id="4aea3-116">中所述[了解该生成过程](understanding-the-build-process.md)，特定于环境的项目文件&#x2014;例如*Env Dev.proj*&#x2014;设计要导入环境无关*Publish.proj*在生成时的文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="4aea3-117">在一起，这两个文件提供一组完整的说明，以告诉 MSBuild 如何生成和部署你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="4aea3-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="4aea3-118">*Publish.proj*文件使用**导入**元素导入特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>


[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]


<span data-ttu-id="4aea3-119">在这种情况下，当你使用 MSBuild.exe 生成和部署联系人管理器解决方案，你需要：</span><span class="sxs-lookup"><span data-stu-id="4aea3-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="4aea3-120">在上运行 MSBuild.exe *Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="4aea3-121">通过提供一个名为的命令行参数来指定特定于环境的项目文件的位置**TargetEnvPropsFile**。</span><span class="sxs-lookup"><span data-stu-id="4aea3-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="4aea3-122">若要执行此操作，MSBuild 命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="4aea3-122">To do this, your MSBuild command should resemble this:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]


<span data-ttu-id="4aea3-123">从这里，它将是简单的步骤将移至可重复、 单步执行部署。</span><span class="sxs-lookup"><span data-stu-id="4aea3-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="4aea3-124">你需要做是将 MSBuild 命令添加到一个.cmd 文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="4aea3-125">在联系人管理器解决方案中，发布文件夹包含名为的文件*发布 Dev.cmd*正好可以实现此执行。</span><span class="sxs-lookup"><span data-stu-id="4aea3-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="4aea3-126">**/Fl**开关将指示 MSBuild 将创建一个名为的日志文件*msbuild.log*在其中调用 MSBuild.exe 的工作目录中。</span><span class="sxs-lookup"><span data-stu-id="4aea3-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>


<span data-ttu-id="4aea3-127">若要部署或重新部署联系人管理器解决方案，你需要做运行*发布 Dev.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="4aea3-128">在您运行该文件，MSBuild 将：</span><span class="sxs-lookup"><span data-stu-id="4aea3-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="4aea3-129">生成解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="4aea3-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="4aea3-130">生成 web 应用程序项目的可部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="4aea3-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="4aea3-131">生成数据库项目的.dbschema 和.deploymanifest 文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="4aea3-132">将 web 包部署到 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4aea3-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="4aea3-133">将数据库部署到数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="4aea3-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="4aea3-134">运行部署</span><span class="sxs-lookup"><span data-stu-id="4aea3-134">Run the Deployment</span></span>

<span data-ttu-id="4aea3-135">当你已为你的目标环境中创建命令文件时，你应能够通过只需运行该文件来完成整个部署。</span><span class="sxs-lookup"><span data-stu-id="4aea3-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="4aea3-136">**若要将联系人管理器解决方案部署到你的测试环境**</span><span class="sxs-lookup"><span data-stu-id="4aea3-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="4aea3-137">你开发人员在工作站上，打开 Windows 资源管理器，然后浏览到的位置*发布 Dev.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="4aea3-138">双击该文件以运行它。</span><span class="sxs-lookup"><span data-stu-id="4aea3-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="4aea3-139">如果**打开的文件 – 安全警告**显示对话框，请单击**运行**。</span><span class="sxs-lookup"><span data-stu-id="4aea3-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="4aea3-140">如果你的配置设置和测试服务器设置是否正确，命令提示符窗口将显示**生成成功**消息时 MSBuild 已完成处理的项目文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="4aea3-141">如果这是首次已将解决方案部署到此环境，你将需要添加到测试 web 服务器计算机帐户**db\_datawriter**和**db\_datareader**上的角色**ContactManager**数据库。</span><span class="sxs-lookup"><span data-stu-id="4aea3-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="4aea3-142">中介绍了此过程[配置用于 Web 部署发布的数据库服务器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4aea3-143">只需创建数据库时分配这些权限。</span><span class="sxs-lookup"><span data-stu-id="4aea3-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="4aea3-144">默认情况下，每个部署上的数据库将重新生成过程创建&#x2014;相反，它将比较最新的架构的现有数据库并进行所需更改。</span><span class="sxs-lookup"><span data-stu-id="4aea3-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="4aea3-145">因此，只需将这些数据库角色映射第一次部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="4aea3-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="4aea3-146">打开 Internet Explorer 并浏览到联系人管理器应用程序的 URL (例如， `http://testweb1:85/ContactManager/`)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="4aea3-147">验证应用程序按预期方式工作并且你能够添加联系人。</span><span class="sxs-lookup"><span data-stu-id="4aea3-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="4aea3-148">结束语</span><span class="sxs-lookup"><span data-stu-id="4aea3-148">Conclusion</span></span>

<span data-ttu-id="4aea3-149">创建命令文件包含 MSBuild 说明可为你提供快速轻松地构建和部署到特定目标环境的多项目解决方案中。</span><span class="sxs-lookup"><span data-stu-id="4aea3-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="4aea3-150">如果需要反复将你的解决方案部署到多个目标环境，你可以创建多个命令文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="4aea3-151">在每个命令文件中，MSBuild 命令将生成相同的通用项目文件中，但它将指定不同的特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="4aea3-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="4aea3-152">例如，若要将发布到开发人员或测试环境的命令文件可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="4aea3-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]


<span data-ttu-id="4aea3-153">要将发布到过渡环境的命令文件可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="4aea3-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="4aea3-154">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[配置为目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


<span data-ttu-id="4aea3-155">你还可以通过重写属性或在 MSBuild 命令中设置各种其他开关自定义生成过程中的为每个环境。</span><span class="sxs-lookup"><span data-stu-id="4aea3-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="4aea3-156">有关详细信息，请参阅[MSBuild 命令行参考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4aea3-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4aea3-157">[上一页](deploying-database-projects.md)
> [下一页](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4aea3-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
