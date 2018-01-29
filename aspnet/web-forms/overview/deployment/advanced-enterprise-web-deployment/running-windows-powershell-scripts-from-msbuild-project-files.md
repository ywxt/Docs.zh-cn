---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: "从 MSBuild 项目文件中运行 Windows PowerShell 脚本 |Microsoft 文档"
author: jrjlee
description: "本主题介绍如何生成和部署过程的一部分运行的 Windows PowerShell 脚本。 你可以在本地运行脚本 (换而言之，在 b。..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: afee7b0621df42a8bc70fc6f7c4a8fd0383fa83a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="c4065-104">从 MSBuild 项目文件中运行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="c4065-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>
====================
<span data-ttu-id="c4065-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c4065-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c4065-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="c4065-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c4065-107">本主题介绍如何生成和部署过程的一部分运行的 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="c4065-108">你可以 （换而言之，在生成服务器上） 中运行脚本本地或远程，如目标 web 服务器或数据库服务器上。</span><span class="sxs-lookup"><span data-stu-id="c4065-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="c4065-109">有很多可能需要运行 Windows PowerShell 的部署后脚本的原因。</span><span class="sxs-lookup"><span data-stu-id="c4065-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="c4065-110">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="c4065-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="c4065-111">向注册表添加自定义事件源。</span><span class="sxs-lookup"><span data-stu-id="c4065-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="c4065-112">生成用于上载的文件系统目录。</span><span class="sxs-lookup"><span data-stu-id="c4065-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="c4065-113">清除生成目录。</span><span class="sxs-lookup"><span data-stu-id="c4065-113">Clean up build directories.</span></span>
> - <span data-ttu-id="c4065-114">将条目写入到自定义的日志文件。</span><span class="sxs-lookup"><span data-stu-id="c4065-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="c4065-115">发送电子邮件邀请用户的新设置的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4065-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="c4065-116">创建具有适当权限的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="c4065-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="c4065-117">配置 SQL Server 实例之间的复制。</span><span class="sxs-lookup"><span data-stu-id="c4065-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="c4065-118">本主题将演示如何从 Microsoft Build Engine (MSBuild) 项目文件中的自定义目标本地和远程运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>


<span data-ttu-id="c4065-119">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案 （&） #x 2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 的 web 应用程序Communication Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="c4065-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="c4065-120">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在其中生成过程控制由两个项目文件 （&） #x 2014; 一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="c4065-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="c4065-121">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="c4065-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c4065-122">任务概述</span><span class="sxs-lookup"><span data-stu-id="c4065-122">Task Overview</span></span>

<span data-ttu-id="c4065-123">若要自动进行的或单步执行部署过程的一部分运行的 Windows PowerShell 脚本，你将需要完成这些高级任务：</span><span class="sxs-lookup"><span data-stu-id="c4065-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="c4065-124">将 Windows PowerShell 脚本添加到你的解决方案和源代码管理。</span><span class="sxs-lookup"><span data-stu-id="c4065-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="c4065-125">创建用于将调用 Windows PowerShell 脚本的命令。</span><span class="sxs-lookup"><span data-stu-id="c4065-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="c4065-126">在命令中的任何保留的 XML 字符进行转义。</span><span class="sxs-lookup"><span data-stu-id="c4065-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="c4065-127">在你自定义 MSBuild 项目文件中创建的目标和使用**Exec**任务以运行你的命令。</span><span class="sxs-lookup"><span data-stu-id="c4065-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="c4065-128">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="c4065-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="c4065-129">任务和本主题中的演练假定你已经熟悉 MSBuild 目标和属性，并确保你了解如何使用自定义 MSBuild 项目文件驱动器生成和部署过程。</span><span class="sxs-lookup"><span data-stu-id="c4065-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="c4065-130">有关详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="c4065-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="c4065-131">创建并添加 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="c4065-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="c4065-132">本主题中的任务使用名为的示例 Windows PowerShell 脚本**LogDeploy.ps1**演示如何从 MSBuild 运行脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="c4065-133">**LogDeploy.ps1**脚本包含的单行条目写入日志文件的简单函数：</span><span class="sxs-lookup"><span data-stu-id="c4065-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>


[!code-javascript[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.js)]


<span data-ttu-id="c4065-134">**LogDeploy.ps1**脚本接受两个参数。</span><span class="sxs-lookup"><span data-stu-id="c4065-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="c4065-135">第一个参数表示你想要添加一个条目的日志文件的完整路径和第二个参数表示你想要记录日志文件中的部署目标。</span><span class="sxs-lookup"><span data-stu-id="c4065-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="c4065-136">运行脚本时，它会将行添加到此格式中的日志文件中：</span><span class="sxs-lookup"><span data-stu-id="c4065-136">When you run the script, it adds a line to the log file in this format:</span></span>


[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]


<span data-ttu-id="c4065-137">若要使**LogDeploy.ps1**脚本供 MSBuild，你需要：</span><span class="sxs-lookup"><span data-stu-id="c4065-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="c4065-138">将脚本添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="c4065-138">Add the script to source control.</span></span>
- <span data-ttu-id="c4065-139">将脚本添加到你在 Visual Studio 2010 中的解决方案。</span><span class="sxs-lookup"><span data-stu-id="c4065-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="c4065-140">你不需要部署你的解决方案内容，无论你是否计划在生成服务器上或者远程计算机上运行该脚本的脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="c4065-141">一个选项是将脚本添加到解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4065-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="c4065-142">在联系人管理器示例中，由于你想要使用 Windows PowerShell 脚本作为部署过程中，最好将脚本添加到发布解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4065-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="c4065-143">解决方案文件夹中的内容被复制到源材料的生成服务器。</span><span class="sxs-lookup"><span data-stu-id="c4065-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="c4065-144">但是，它们构成任何项目输出的任何部分。</span><span class="sxs-lookup"><span data-stu-id="c4065-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="c4065-145">在生成服务器上执行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="c4065-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="c4065-146">在某些情况下，你可能想要生成你的项目的计算机上运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="c4065-147">例如，你可能使用 Windows PowerShell 脚本以清理生成文件夹或将条目写入到自定义的日志文件。</span><span class="sxs-lookup"><span data-stu-id="c4065-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="c4065-148">根据语法，MSBuild 项目文件从运行 Windows PowerShell 脚本等同于常规的命令提示符下运行的 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="c4065-149">你需要调用 powershell.exe 可执行文件，并使用**– 命令**交换机以提供所需 Windows PowerShell 以运行的命令。</span><span class="sxs-lookup"><span data-stu-id="c4065-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="c4065-150">(在 Windows PowerShell v2，你还可以使用**– 文件**切换)。</span><span class="sxs-lookup"><span data-stu-id="c4065-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="c4065-151">该命令应采取以下格式：</span><span class="sxs-lookup"><span data-stu-id="c4065-151">The command should take this format:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]


<span data-ttu-id="c4065-152">例如:</span><span class="sxs-lookup"><span data-stu-id="c4065-152">For example:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]


<span data-ttu-id="c4065-153">如果你的脚本的路径包含空格，您需要将文件路径括在单引号前面加 &。</span><span class="sxs-lookup"><span data-stu-id="c4065-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="c4065-154">不能使用双引号括起来，因为您已使用它们括起命令：</span><span class="sxs-lookup"><span data-stu-id="c4065-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]


<span data-ttu-id="c4065-155">在调用此命令从 MSBuild 时，有一些额外的注意事项。</span><span class="sxs-lookup"><span data-stu-id="c4065-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="c4065-156">首先，应包括**– NonInteractive**标志来确保安静地执行脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="c4065-157">接下来，你应包括**– ExecutionPolicy**具有相应的自变量值的标志。</span><span class="sxs-lookup"><span data-stu-id="c4065-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="c4065-158">这将指定 Windows PowerShell 将应用到你的脚本，并允许你重写默认执行策略，这可能会阻止脚本执行的执行策略。</span><span class="sxs-lookup"><span data-stu-id="c4065-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="c4065-159">你可以从这些自变量值中进行选择：</span><span class="sxs-lookup"><span data-stu-id="c4065-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="c4065-160">值为**不受限制的**将允许 Windows PowerShell 执行你的脚本，而不考虑是否已签名的脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="c4065-161">值为**RemoteSigned**将允许执行未签名的脚本在本地计算机上创建 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c4065-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="c4065-162">但是，在其他位置中创建的脚本必须进行签名。</span><span class="sxs-lookup"><span data-stu-id="c4065-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="c4065-163">（在实践中，你已创建的 Windows PowerShell 脚本本地生成服务器上的可能性非常小）。</span><span class="sxs-lookup"><span data-stu-id="c4065-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="c4065-164">值为**AllSigned**将允许 Windows PowerShell 执行签名的脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="c4065-165">默认执行策略是**Restricted**，它防止 Windows PowerShell 运行所有脚本文件。</span><span class="sxs-lookup"><span data-stu-id="c4065-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="c4065-166">最后，你需要在 Windows PowerShell 命令中发生任何保留的 XML 字符进行转义：</span><span class="sxs-lookup"><span data-stu-id="c4065-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="c4065-167">将使用单引号 **&amp;a p o s;**</span><span class="sxs-lookup"><span data-stu-id="c4065-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="c4065-168">将使用双引号 **&amp;q u o t;**</span><span class="sxs-lookup"><span data-stu-id="c4065-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="c4065-169">将使用 &  **&amp;amp;**</span><span class="sxs-lookup"><span data-stu-id="c4065-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="c4065-170">当你进行这些更改时，你的命令将类似如下：</span><span class="sxs-lookup"><span data-stu-id="c4065-170">When you make these changes, your command will resemble this:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]


<span data-ttu-id="c4065-171">在你自定义 MSBuild 项目文件中，你可以创建新的目标和使用**Exec**任务才能运行此命令：</span><span class="sxs-lookup"><span data-stu-id="c4065-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]


<span data-ttu-id="c4065-172">在此示例中，请注意:</span><span class="sxs-lookup"><span data-stu-id="c4065-172">In this example, note that:</span></span>

- <span data-ttu-id="c4065-173">任何变量，如参数值和 Windows PowerShell 可执行文件的位置被声明为 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="c4065-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="c4065-174">条件包含以使用户能够重写这些值从命令行。</span><span class="sxs-lookup"><span data-stu-id="c4065-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="c4065-175">**MSDeployComputerName**在项目文件中其他位置声明属性。</span><span class="sxs-lookup"><span data-stu-id="c4065-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="c4065-176">作为生成过程的一部分执行此目标时，Windows PowerShell 将运行你的命令和日志条目写入指定的文件。</span><span class="sxs-lookup"><span data-stu-id="c4065-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="c4065-177">在远程计算机上执行 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="c4065-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="c4065-178">Windows PowerShell 是能够在通过远程计算机上运行脚本[Windows 远程管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)(WinRM)。</span><span class="sxs-lookup"><span data-stu-id="c4065-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="c4065-179">若要执行此操作，你需要使用[Invoke-command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c4065-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="c4065-180">这使你无需将脚本复制到远程计算机执行你的脚本对一个或多个远程计算机。</span><span class="sxs-lookup"><span data-stu-id="c4065-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="c4065-181">任何结果返回到你从中运行脚本的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="c4065-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="c4065-182">在使用之前**Invoke-command** cmdlet 来执行 Windows PowerShell 脚本在远程计算机上，你需要配置 WinRM 侦听器，用于接受远程消息。</span><span class="sxs-lookup"><span data-stu-id="c4065-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="c4065-183">你可以通过运行命令执行此**winrm quickconfig**远程计算机上。</span><span class="sxs-lookup"><span data-stu-id="c4065-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="c4065-184">有关详细信息，请参阅[安装和配置 Windows 远程管理的](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4065-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>


<span data-ttu-id="c4065-185">从 Windows PowerShell 窗口中，将使用此语法来运行**LogDeploy.ps1**远程计算机上的脚本：</span><span class="sxs-lookup"><span data-stu-id="c4065-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>


[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]


> [!NOTE]
> <span data-ttu-id="c4065-186">有多种其他方法的使用**Invoke-command**运行脚本文件，但这种方法是最简单何时需要提供参数值和管理带空格的路径。</span><span class="sxs-lookup"><span data-stu-id="c4065-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>


<span data-ttu-id="c4065-187">当你运行此命令提示符下时，你需要调用 Windows PowerShell 可执行文件，并使用**– 命令**参数来提供你的说明进行操作：</span><span class="sxs-lookup"><span data-stu-id="c4065-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]


<span data-ttu-id="c4065-188">如之前，你需要提供一些其他开关和任何保留的 XML 字符进行转义，MSBuild 中运行命令时：</span><span class="sxs-lookup"><span data-stu-id="c4065-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]


<span data-ttu-id="c4065-189">最后，如前所述，可以使用**Exec**内用于执行命令的自定义 MSBuild 目标的任务：</span><span class="sxs-lookup"><span data-stu-id="c4065-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]


<span data-ttu-id="c4065-190">作为生成过程的一部分执行此目标时，Windows PowerShell 将在指定的计算机上运行你的脚本**– computername**自变量。</span><span class="sxs-lookup"><span data-stu-id="c4065-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c4065-191">结束语</span><span class="sxs-lookup"><span data-stu-id="c4065-191">Conclusion</span></span>

<span data-ttu-id="c4065-192">本主题介绍如何从 MSBuild 项目文件中运行 Windows PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c4065-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="c4065-193">此方法可用于自动进行的或单步执行的生成和部署过程的一部分运行的 Windows PowerShell 脚本，本地或远程计算机上。</span><span class="sxs-lookup"><span data-stu-id="c4065-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c4065-194">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="c4065-194">Further Reading</span></span>

<span data-ttu-id="c4065-195">有关 Windows PowerShell 脚本签名和管理执行策略的指南，请参阅[运行 Windows PowerShell 脚本](https://technet.microsoft.com/library/ee176949.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4065-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="c4065-196">有关从远程计算机运行 Windows PowerShell 命令的指南，请参阅[运行远程命令](https://technet.microsoft.com/library/dd819505.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4065-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="c4065-197">使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="c4065-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c4065-198">[上一页](taking-web-applications-offline-with-web-deploy.md)
[下一页](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="c4065-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
