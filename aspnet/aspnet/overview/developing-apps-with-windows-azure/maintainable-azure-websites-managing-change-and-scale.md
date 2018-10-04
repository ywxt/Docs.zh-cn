---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 动手实验： 可维护 Azure 网站： 管理更改和缩放 |Microsoft Docs
author: rick-anderson
description: 在此实验中，了解如何 Microsoft Azure 轻松生成和部署到生产环境的网站。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: 05181ae1b2d857eea45983d378b28011c1cd755a
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578128"
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="8a3e1-103">动手实验： 可维护 Azure 网站： 管理更改和缩放</span><span class="sxs-lookup"><span data-stu-id="8a3e1-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>
====================
<span data-ttu-id="8a3e1-104">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="8a3e1-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="8a3e1-105">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="8a3e1-106">Microsoft Azure 轻松生成和部署到生产环境的网站。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="8a3e1-107">但你还未完成实时应用程序时，您只是开始 ！</span><span class="sxs-lookup"><span data-stu-id="8a3e1-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="8a3e1-108">你将需要处理不断变化的要求、 数据库更新、 缩放性和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="8a3e1-109">幸运的是，Azure 应用服务提供你的需求，并提供充足的功能，可帮助您保留你的网站平稳运行。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="8a3e1-110">Azure 提供安全而灵活的开发、 部署和扩展任何规模的 web 应用程序的选项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="8a3e1-111">利用现有工具创建和部署应用程序，无需费力管理基础结构。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="8a3e1-112">通过预配生产 web 应用程序自己在几分钟内轻松地部署使用你最喜欢的开发工具创建的内容。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="8a3e1-113">可以部署现有网站直接从源代码管理支持**Git**， **GitHub**， **Bitbucket**， **TFS**，并甚至**DropBox**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="8a3e1-114">直接从你喜爱的 IDE 或使用脚本部署**PowerShell**在 Windows 中或**CLI**任何操作系统上运行的工具。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="8a3e1-115">部署完成后，可以保留你的网站同时支持连续部署持续保持最新状态。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="8a3e1-116">大型或小型，azure 会为任何数据，提供规模可变、 耐用的云存储、 备份和恢复解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="8a3e1-117">当应用程序部署到生产环境，如表、 Blob 和 SQL 数据库的存储服务，帮助您缩放云应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="8a3e1-118">使用 SQL 数据库，务必使您提高工作效率的数据库部署新版本的应用程序时保持最新。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="8a3e1-119">为感谢**Entity Framework Code First 迁移**，已简化的开发和部署你的数据模型以在几分钟内更新你的环境。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="8a3e1-120">本动手实验中将显示在 web 应用部署到 Microsoft Azure 中的生产环境时，可能会遇到的不同主题。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="8a3e1-121">在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-121">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="8a3e1-122">本主题的更多深入介绍，请参阅[构建实际云应用程序与 Azure 的电子书](building-real-world-cloud-apps-with-windows-azure/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="8a3e1-123">概述</span><span class="sxs-lookup"><span data-stu-id="8a3e1-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="8a3e1-124">目标</span><span class="sxs-lookup"><span data-stu-id="8a3e1-124">Objectives</span></span>

<span data-ttu-id="8a3e1-125">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="8a3e1-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="8a3e1-126">让 Entity Framework 迁移使用现有模型</span><span class="sxs-lookup"><span data-stu-id="8a3e1-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="8a3e1-127">更新对象模型和相应地使用 Entity Framework 迁移数据库</span><span class="sxs-lookup"><span data-stu-id="8a3e1-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="8a3e1-128">将部署到 Azure 应用服务中使用 Git</span><span class="sxs-lookup"><span data-stu-id="8a3e1-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="8a3e1-129">回滚到以前的部署使用 Azure 管理门户</span><span class="sxs-lookup"><span data-stu-id="8a3e1-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="8a3e1-130">使用 Azure 存储来缩放 web 应用</span><span class="sxs-lookup"><span data-stu-id="8a3e1-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="8a3e1-131">配置使用 Azure 管理门户的 web 应用程序的自动缩放</span><span class="sxs-lookup"><span data-stu-id="8a3e1-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="8a3e1-132">创建和配置 Visual Studio 中负载测试项目</span><span class="sxs-lookup"><span data-stu-id="8a3e1-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="8a3e1-133">系统必备</span><span class="sxs-lookup"><span data-stu-id="8a3e1-133">Prerequisites</span></span>

<span data-ttu-id="8a3e1-134">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="8a3e1-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="8a3e1-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="8a3e1-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="8a3e1-136">Azure SDK for.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="8a3e1-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="8a3e1-137">GIT 版本控制系统</span><span class="sxs-lookup"><span data-stu-id="8a3e1-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="8a3e1-138">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="8a3e1-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="8a3e1-139">注册[免费试用版](http://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-139">Sign up for a [Free Trial](http://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="8a3e1-140">如果你是 Visual Studio Professional、 Test Professional、 Premium 或 Ultimate with MSDN 或 MSDN 平台订户，激活你[MSDN 权益](http://aka.ms/watk-msdn)现在以开始开发和测试 Azure 上</span><span class="sxs-lookup"><span data-stu-id="8a3e1-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](http://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="8a3e1-141">[BizSpark](http://aka.ms/watk-bizspark)成员自动获得 Azure 通过其 Visual Studio Ultimate with MSDN 订阅权益</span><span class="sxs-lookup"><span data-stu-id="8a3e1-141">[BizSpark](http://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="8a3e1-142">成员[Microsoft 合作伙伴网络](http://aka.ms/watk-mpn)Cloud Essentials 计划接收免费的月度 Azure 额度</span><span class="sxs-lookup"><span data-stu-id="8a3e1-142">Members of the [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="8a3e1-143">安装</span><span class="sxs-lookup"><span data-stu-id="8a3e1-143">Setup</span></span>

<span data-ttu-id="8a3e1-144">若要运行本动手实验中练习，需要先设置你的环境。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="8a3e1-145">打开 Windows 资源管理器并浏览到实验室**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="8a3e1-146">右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="8a3e1-147">如果显示用户帐户控制对话框中，确认要继续执行的操作。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3e1-148">请确保您运行安装程序之前已为此实验室的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="8a3e1-149">使用代码片段</span><span class="sxs-lookup"><span data-stu-id="8a3e1-149">Using the Code Snippets</span></span>

<span data-ttu-id="8a3e1-150">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="8a3e1-151">为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3e1-152">每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="8a3e1-153">请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="8a3e1-154">在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="8a3e1-155">如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="8a3e1-156">练习</span><span class="sxs-lookup"><span data-stu-id="8a3e1-156">Exercises</span></span>

<span data-ttu-id="8a3e1-157">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="8a3e1-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="8a3e1-158">使用 Entity Framework 迁移</span><span class="sxs-lookup"><span data-stu-id="8a3e1-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="8a3e1-159">Web 应用部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="8a3e1-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="8a3e1-160">在生产环境中执行部署回滚</span><span class="sxs-lookup"><span data-stu-id="8a3e1-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="8a3e1-161">使用 Azure 存储进行缩放</span><span class="sxs-lookup"><span data-stu-id="8a3e1-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="8a3e1-162">[使用适用于 Web 应用自动缩放](#Exercise5)（对于 Visual Studio 2013 旗舰版中的可选）</span><span class="sxs-lookup"><span data-stu-id="8a3e1-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="8a3e1-163">估计的时间才能完成此实验： **75 分钟**</span><span class="sxs-lookup"><span data-stu-id="8a3e1-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="8a3e1-164">在首次启动 Visual Studio，您必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="8a3e1-165">每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="8a3e1-166">此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="8a3e1-167">如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="8a3e1-168">练习 1： 使用 Entity Framework 迁移</span><span class="sxs-lookup"><span data-stu-id="8a3e1-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="8a3e1-169">当正在开发的应用时，你的数据模型可能随时间变化。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="8a3e1-170">（如果要创建新的版本），这些更改可能会影响你的数据库中的现有模型，必须使数据库保持最新的以防止出现错误。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="8a3e1-171">若要简化您的模型，这些更改跟踪**Entity Framework Code First 迁移**会自动检测更改比较您的模型与数据库架构并生成特定的代码来更新您的数据库，创建新*版本*的数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="8a3e1-172">此练习展示如何能够**迁移**你的应用程序以及如何可以轻松地检测和生成更改来更新您的数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="8a3e1-173">任务 1 – 启用迁移</span><span class="sxs-lookup"><span data-stu-id="8a3e1-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="8a3e1-174">在此任务中，您将了解到启用的步骤**Entity Framework Code First 迁移**到**极客测验**数据库更改的模型和了解如何将这些更改反映在数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="8a3e1-175">打开 Visual Studio 并打开**GeekQuiz.sln**解决方案文件从**Source\Ex1 UsingEntityFrameworkMigrations\Begin**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="8a3e1-176">生成解决方案，若要下载和安装**NuGet**包的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="8a3e1-177">若要执行此操作，右键单击解决方案，然后单击**生成解决方案**或按**Ctrl + Shift + B**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="8a3e1-178">从**工具**在 Visual Studio 中，选择菜单**库程序包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-178">From the **Tools** menu in Visual Studio, select **Library Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="8a3e1-179">在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="8a3e1-180">将创建基于现有模型的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="8a3e1-181">![启用迁移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "启用迁移")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="8a3e1-182">*启用迁移*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-183">此命令将添加**迁移**文件夹，对包含文件的极客测验项目名为**Configuration.cs**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="8a3e1-184">**配置**类允许您配置的迁移对于您的上下文的行为方式。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="8a3e1-185">你需要使用已启用迁移，更新**配置**类，以使用初始数据填充数据库的**极客测验**要求。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="8a3e1-186">下**迁移**，替换**Configuration.cs**与文件位于**Source\Assets**本实验的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-187">由于**迁移**将调用**种子**与每个数据库更新方法，您需要以确保在数据库中的用户不能重复记录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="8a3e1-188">**AddOrUpdate**方法将有助于防止重复的数据。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="8a3e1-189">若要添加初始迁移，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-190">请确保没有名为数据库&quot;GeekQuizProd&quot; LocalDB 实例中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="8a3e1-191">![添加基础架构迁移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "添加基础架构迁移")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="8a3e1-192">*添加基础架构迁移*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-193">**添加迁移**将基于之后创建的最后一个迁移对您的模型所做的更改下一步迁移搭建基架。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="8a3e1-194">在这种情况下，由于它是项目的初始迁移时，它将添加用于创建中定义的所有表的脚本**TriviaContext**类。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="8a3e1-195">执行迁移后，通过运行以下命令来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="8a3e1-196">此命令将指定**Verbose**标志以查看要应用到目标数据库的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="8a3e1-197">![创建初始数据库](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "创建初始数据库")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="8a3e1-198">*创建初始数据库*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-199">**更新数据库**应用所有挂起的迁移到数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="8a3e1-200">在这种情况下，它将创建使用 web.config 文件中定义的连接字符串的数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="8a3e1-201">转到**视图**菜单，然后打开**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="8a3e1-202">![在 SQL Server 对象资源管理器中打开](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 对象资源管理器中打开")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="8a3e1-203">*在 SQL Server 对象资源管理器中打开*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="8a3e1-204">在中**SQL Server 对象资源管理器**窗口中，右键单击连接到 LocalDB 实例**SQL Server**节点并选择**添加 SQL Server...** 选项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="8a3e1-205">![添加 SQL Server 实例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "添加 SQL Server 实例")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="8a3e1-206">*将 SQL Server 实例添加到 SQL Server 对象资源管理器*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="8a3e1-207">设置**服务器名称**到 *(localdb) \v11.0*并保留**Windows 身份验证**作为身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="8a3e1-208">单击**Connect**以继续。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="8a3e1-209">![连接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "连接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="8a3e1-210">*连接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="8a3e1-211">打开**GeekQuizProd**数据库中，展开**表**节点。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="8a3e1-212">正如您所看到的**Update-database**命令生成中定义的所有表**TriviaContext**类。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="8a3e1-213">找到**dbo。TriviaQuestions**表，然后打开列节点。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="8a3e1-214">将在下一任务中，将新列添加到此表并更新数据库使用**迁移**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="8a3e1-215">![琐碎内容问题列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "琐碎内容问题列")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="8a3e1-216">*琐碎内容问题列*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="8a3e1-217">任务 2 – 使用迁移更新数据库架构</span><span class="sxs-lookup"><span data-stu-id="8a3e1-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="8a3e1-218">在本任务中，您将使用**Entity Framework Code First 迁移**检测您的模型中的更改并生成所需的代码来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="8a3e1-219">你将更新**TriviaQuestions**通过向其添加一个新的属性的实体。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="8a3e1-220">然后，将运行命令以创建新的迁移在表中包含的新列。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="8a3e1-221">在中**解决方案资源管理器**，双击**TriviaQuestion.cs**文件位于内部**模型**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="8a3e1-222">添加名为的新属性**提示**，如以下代码片段中所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="8a3e1-223">在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="8a3e1-224">将专用于反映将我们的模型中的更改创建新的迁移。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="8a3e1-225">![添加迁移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "添加迁移")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="8a3e1-226">*添加迁移*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-227">迁移文件组成的两种方法**向上**并**向下**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="8a3e1-228">**向上**方法将用于指定哪些更改我们的应用程序需要将应用于数据库的当前版本。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="8a3e1-229">**向下**用于撤消所做的更改我们已添加到**向上**方法。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="8a3e1-230">当数据库迁移更新数据库时，将所有迁移都运行中的时间戳顺序，且只有自上次更新以来未使用过 (\_跟踪已应用哪些迁移的 MigrationHistory 表)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="8a3e1-231">**向上**所有迁移的方法将调用，并将使我们具有指定数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="8a3e1-232">如果返回到先前的迁移，我们决定**向下**将调用方法以重做以反向顺序进行更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="8a3e1-233">在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="8a3e1-234">输出**Update-database**生成命令**Alter Table** SQL 语句，以添加到一个新列**TriviaQuestions**表，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="8a3e1-235">![添加列生成的 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "添加列生成的 SQL 语句")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="8a3e1-236">*添加列生成的 SQL 语句*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="8a3e1-237">在中**SQL Server 对象资源管理器**，刷新**dbo。TriviaQuestions**表，以检查新**提示**显示列。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="8a3e1-238">![显示新的提示列](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "显示新的提示列")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="8a3e1-239">*显示新的提示列*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="8a3e1-240">回到**TriviaQuestion.cs**编辑器中，添加**StringLength**约束*提示*属性，如下面的代码段中所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="8a3e1-241">在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="8a3e1-242">在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="8a3e1-243">输出**Update-database**生成命令**Alter Table** SQL 语句，以更新*提示*类型的列**TriviaQuestions**表，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="8a3e1-244">![更改列生成的 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 语句生成")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="8a3e1-245">*更改列生成的 SQL 语句*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="8a3e1-246">在中**SQL Server 对象资源管理器**，刷新**dbo。TriviaQuestions**表，然后检查**提示**列的类型**nvarchar(150)**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="8a3e1-247">![显示新约束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "显示新约束")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="8a3e1-248">*显示新约束*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="8a3e1-249">练习 2： 将 Web 应用部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="8a3e1-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="8a3e1-250">**Azure 应用服务中的 web 应用**使您可以执行分阶段的发布。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="8a3e1-251">过渡的发布创建的每个默认生产站点过渡站点槽，便于你以交换这些槽，但无需停机时间。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="8a3e1-252">这是非常适用于向公众发布之前验证更改，以增量方式集成站点内容，并回滚任何更改都不会按预期工作。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="8a3e1-253">在此练习中，你将部署**极客测验**应用程序到 web 应用使用 Git 源代码管理的过渡环境。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="8a3e1-254">若要执行此操作，将创建 web 应用和预配在管理门户所需的组件，配置**Git**的源存储库和推送应用程序代码从本地计算机到过渡槽。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="8a3e1-255">你还将更新与生产数据库**Code First 迁移**你在上一练习中创建。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="8a3e1-256">然后，您将在此测试环境以验证其操作中执行应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="8a3e1-257">后它按预期正常工作，将升级到生产环境的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3e1-258">若要启用暂存的发布，web 应用必须处于**标准模式**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="8a3e1-259">请注意是否你的 web 应用更改为标准模式将产生额外的费用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="8a3e1-260">有关定价的详细信息，请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="8a3e1-261">任务 1 – 在 Azure 应用服务中创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="8a3e1-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="8a3e1-262">在本任务中，您将创建中的 web 应用**Azure 应用服务**从管理门户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="8a3e1-263">你还将配置**SQL 数据库**以持久保存应用程序数据，并配置本地 Git 存储库进行源代码管理。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="8a3e1-264">转到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![登录到 Azure 管理门户](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="8a3e1-266">*登录到 Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="8a3e1-267">单击**新建**在页面底部的命令栏中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="8a3e1-268">![创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "创建新的 web 应用")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="8a3e1-269">*创建新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="8a3e1-270">单击**计算**，**网站**，然后**自定义创建**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="8a3e1-271">![创建新的 web 应用使用自定义创建](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "创建使用自定义创建新的 web 应用")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="8a3e1-272">*创建使用自定义创建新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="8a3e1-273">在中**新建网站-自定义创建**对话框框中，提供一个可用**URL** (例如*极客测验*)，选择中的某个位置**区域**下拉列表，然后选择**创建新的 SQL 数据库**中**数据库**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="8a3e1-274">最后，选择**从源控制发布**复选框，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![自定义新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="8a3e1-276">*自定义新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="8a3e1-277">指定数据库设置的以下信息：</span><span class="sxs-lookup"><span data-stu-id="8a3e1-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="8a3e1-278">在中**名称**文字框中，输入数据库名称 (例如*geekquiz\_db*)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="8a3e1-279">在服务器中**下拉**列表中，选择**新建 SQL 数据库服务器**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="8a3e1-280">或者，可以选择现有的服务器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="8a3e1-281">在中**数据库用户名**并**数据库密码**框中，SQL 数据库服务器输入管理员用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="8a3e1-282">如果选择一个服务器已创建，系统将提示输入密码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![指定数据库设置](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="8a3e1-284">*指定数据库设置*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="8a3e1-285">单击 **“下一步”** 以继续。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="8a3e1-286">选择**本地 Git 存储库**源控件使用，并单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-287">您可能会提示输入部署凭据 （用户名和密码）。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![创建 Git 存储库](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="8a3e1-289">*创建 Git 存储库*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="8a3e1-290">等待，直到创建新的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-291">默认情况下，Azure 提供在域*azurewebsites.net*但还可以设置自定义域使用 Azure 管理门户的可能性。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="8a3e1-292">但是，如果您使用的某些 Azure 应用服务模式下，仅可以管理自定义域。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="8a3e1-293">Azure 应用服务有免费、 共享、 基本、 标准和高级版本。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="8a3e1-294">在免费和共享模式下，所有 web 应用在多租户环境中运行，并针对 CPU、 内存和网络使用情况采用的配额。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="8a3e1-295">免费的应用程序的最大数目可能会因你的计划。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="8a3e1-296">在标准模式下，您可以选择到标准 Azure 相对应的专用虚拟机上运行的应用的计算资源。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="8a3e1-297">您可以发现中的 web 应用模式下配置**规模**web 应用的菜单。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="8a3e1-298">![Azure 应用服务模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure 应用服务模式")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="8a3e1-299">如果使用的**共享**或**标准**模式下，你将能够通过转到您的应用程序管理 web 应用的自定义域**配置**菜单，然后单击**管理域**下*域名*。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="8a3e1-300">![管理域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理域")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="8a3e1-301">![管理自定义域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自定义域")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="8a3e1-302">创建 web 应用后，单击下面的链接**URL**列来检查新的 web 应用正在运行。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![浏览到新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="8a3e1-304">*浏览到新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-304">*Browsing to the new web app*</span></span>

    ![运行 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="8a3e1-306">*运行 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="8a3e1-307">任务 2 – 创建生产 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="8a3e1-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="8a3e1-308">在本任务中，您将使用**Entity Framework Code First 迁移**若要创建的数据库目标**Azure SQL 数据库**你在上一任务中创建的实例。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="8a3e1-309">在管理门户中，导航到上一个任务中创建的 web 应用并转到其**仪表板**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="8a3e1-310">在中**仪表板**页上，单击**查看连接字符串**下链接**速览**部分。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="8a3e1-311">![查看连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看连接字符串")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="8a3e1-312">*查看连接字符串*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-312">*View connection strings*</span></span>
3. <span data-ttu-id="8a3e1-313">复制**连接字符串**值，并关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="8a3e1-314">![在 Azure 管理门户中的连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理门户中的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="8a3e1-315">*在 Azure 管理门户中的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="8a3e1-316">单击**SQL 数据库**若要查看在 Azure 中的 SQL 数据库的列表</span><span class="sxs-lookup"><span data-stu-id="8a3e1-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="8a3e1-317">![SQL 数据库菜单](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 数据库菜单")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="8a3e1-318">*SQL 数据库菜单*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="8a3e1-319">找到在上一任务中创建的数据库并单击该服务器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="8a3e1-320">![SQL 数据库服务器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 数据库服务器")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="8a3e1-321">*SQL 数据库服务器*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-321">*SQL Database server*</span></span>
6. <span data-ttu-id="8a3e1-322">在中**快速启动**页上的服务器上，单击**配置**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="8a3e1-323">![配置菜单](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "配置菜单")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="8a3e1-324">*配置菜单*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-324">*Configure menu*</span></span>
7. <span data-ttu-id="8a3e1-325">在中**允许的 IP 地址**部分中，单击**将添加到允许的 IP 地址**链接，以启用你的 IP 连接到 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="8a3e1-326">![允许的 IP 地址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允许的 IP 地址")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="8a3e1-327">*允许的 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="8a3e1-328">单击**保存**要完成该步骤的页的底部。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="8a3e1-329">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="8a3e1-330">在中**程序包管理器控制台**，执行以下命令替换 *[YOUR CONNECTION STRING]* 占位符替换为从 Azure 复制连接字符串</span><span class="sxs-lookup"><span data-stu-id="8a3e1-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="8a3e1-331">![针对 Windows Azure SQL 数据库更新数据库](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "面向 Windows Azure SQL 数据库更新数据库")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="8a3e1-332">*更新目标 Azure SQL 数据库的数据库*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="8a3e1-333">任务 3 – 部署到过渡环境使用 Git 的极客测验</span><span class="sxs-lookup"><span data-stu-id="8a3e1-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="8a3e1-334">在本任务中，将 web 应用程序中启用过渡的发布。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="8a3e1-335">然后，将使用 Git 发布极客测验应用程序直接从本地计算机到你的 web 应用的过渡环境。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="8a3e1-336">返回到门户并单击下的 web 应用名称**名称**列中显示的管理页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![打开 web 应用程序管理页面](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="8a3e1-338">*打开 web 应用程序管理页面*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="8a3e1-339">导航到**规模**页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="8a3e1-340">下**常规**部分中，选择**标准**作为配置，然后单击**保存**命令栏中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-341">若要在当前区域和订阅中的运行的所有 web 应用**标准**模式下，保留**全**中所选的复选框**选择站点**配置。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="8a3e1-342">否则，请清除**全**复选框。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="8a3e1-343">![升级到标准模式的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "升级到标准模式的 web 应用")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="8a3e1-344">*升级到标准模式的 Web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="8a3e1-345">单击**是**以确认所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="8a3e1-346">![确认更改为标准模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "继续执行更改的 web 应用程序模式")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="8a3e1-347">*确认更改为标准模式*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="8a3e1-348">转到**仪表板**页上，单击**启用过渡发布**下**速览**部分。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="8a3e1-349">![启用过渡的发布](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "启用过渡发布")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="8a3e1-350">*启用过渡的发布*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="8a3e1-351">单击**是**才能启用过渡的发布。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="8a3e1-352">![确认过渡发布](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "单击是以启用暂存的发布")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="8a3e1-353">*确认过渡的发布*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="8a3e1-354">在 web 应用程序的列表中，展开左侧的 web 应用的名称以显示过渡站点槽的标记。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="8a3e1-355">它具有的应用，然后在 web 应用名称 ***（过渡）***。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="8a3e1-356">单击以转到管理页面的临时站点。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="8a3e1-357">![导航到过渡 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "导航到过渡 web 应用")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="8a3e1-358">*导航到过渡应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="8a3e1-359">请注意，他管理页面看起来像任何其他 web 应用程序的管理页面。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="8a3e1-360">导航到**部署**页并复制**Git URL**值。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="8a3e1-361">稍后在本练习中，将使用它。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-361">You will use it later in this exercise.</span></span>

    ![复制 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="8a3e1-363">*复制 Git URL 值*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="8a3e1-364">打开一个新**Git Bash**控制台并执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="8a3e1-365">更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案中，位于**Source\Ex1 DeployingWebSiteToStaging\Begin**文件夹此实验室中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和第一次提交](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="8a3e1-367">*Git 初始化和第一次提交*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="8a3e1-368">运行以下命令以将你的 web 应用推送到远程**Git**存储库。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="8a3e1-369">将占位符替换为从管理门户获取的 URL。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="8a3e1-370">系统会提示输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![将推送到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="8a3e1-372">*将推送到 Azure*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-373">当将内容部署到的 FTP 主机或 GIT 存储库的 web 应用时，您必须使用进行身份验证**部署凭据**创建的 web 应用**快速启动**或**仪表板**管理页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="8a3e1-374">如果不知道你的部署凭据，可以轻松地重置它们使用管理门户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="8a3e1-375">打开 web 应用**仪表板**页上，单击**重置部署凭据**链接。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="8a3e1-376">提供新密码，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="8a3e1-377">部署凭据可用于与你的订阅相关联的所有 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="8a3e1-378">若要验证 web 应用已成功推送到 Azure，请返回到管理门户并单击**网站**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="8a3e1-379">找到你的 web 应用并展开以显示过渡站点槽的条目。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="8a3e1-380">单击其**名称**转到管理页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="8a3e1-381">单击**部署**若要查看**部署历史记录**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="8a3e1-382">验证是否有**活动的部署**与你*&quot;初始提交&quot;*。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![活动部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="8a3e1-384">*活动部署*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-384">*Active deployment*</span></span>
13. <span data-ttu-id="8a3e1-385">最后，单击**浏览**以转到 web 应用的命令栏中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![浏览 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="8a3e1-387">*浏览 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-387">*Browse web app*</span></span>
14. <span data-ttu-id="8a3e1-388">如果已成功部署应用程序，您将看到的极客测验登录页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-389">部署的应用程序的地址 URL 包含后跟 web 应用的名称 *-暂存*。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![在过渡环境中运行的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="8a3e1-391">*在过渡环境中运行的应用程序*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="8a3e1-392">如果你想要浏览应用程序，请单击**注册**注册一个新用户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="8a3e1-393">通过输入用户名、 电子邮件地址和密码来填写帐户详细信息。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="8a3e1-394">接下来，该应用程序显示测验的第一个问题。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="8a3e1-395">回答几个问题，请确保按预期工作。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![应用程序可供使用](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="8a3e1-397">*应用程序可供使用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="8a3e1-398">任务 4 – 将提升到生产 Web 应用</span><span class="sxs-lookup"><span data-stu-id="8a3e1-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="8a3e1-399">现在，已验证 web 应用在过渡环境中正常运行，你现可提升到生产环境。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="8a3e1-400">在此任务中，将交换过渡站点槽与生产站点槽。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="8a3e1-401">返回到管理门户并选择过渡站点槽。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="8a3e1-402">单击**交换**命令栏中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-402">Click **Swap** in the command bar.</span></span>

    ![切换到生产环境](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="8a3e1-404">*切换到生产环境*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-404">*Swap to production*</span></span>
2. <span data-ttu-id="8a3e1-405">单击**是**在确认对话框中，若要继续进行交换操作。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="8a3e1-406">Azure 会立即交换的暂存站点内容的生产站点内容。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-407">某些设置从暂存版本将自动复制到生产版本 （例如连接字符串替代、 处理程序映射等），但其他设置将不会更改 （例如 DNS 终结点、 SSL 绑定等）。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![确认交换操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="8a3e1-409">*确认交换操作*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="8a3e1-410">交换完成后，选择生产槽，然后单击**浏览**命令栏中打开生产站点中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="8a3e1-411">请注意地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-412">您可能需要刷新浏览器以清除缓存。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="8a3e1-413">在 Internet Explorer 中，您可以执行此操作通过按**CTRL + R**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![在生产环境中运行的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="8a3e1-415">在中**GitBash**控制台中，更新本地 Git 存储库的远程 URL 以面向生产槽。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="8a3e1-416">若要执行此操作，运行以下命令将占位符替换为部署用户名和 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-417">在以下练习中，会将更改推送到生产站点，而不是过渡环境，实验室起见。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="8a3e1-418">在实际方案中，建议以提升到生产环境之前验证在过渡环境中的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="8a3e1-419">练习 3： 在生产环境中执行部署回滚</span><span class="sxs-lookup"><span data-stu-id="8a3e1-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="8a3e1-420">您不产生的过渡槽以热之间执行交换过渡和生产环境，例如，如果你正在使用的情况下**免费**或**共享**模式。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="8a3e1-421">在这些情况下，你应测试应用程序在测试环境中 （本地或远程站点中） 部署到生产环境之前。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="8a3e1-422">但是，有可能在测试阶段未检测到的问题可能会出现在生产站点中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="8a3e1-423">在这种情况下，务必要有一种机制来轻松地尽可能快地切换到上一个和更稳定版本的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="8a3e1-424">在中**Azure 应用服务**，从源代码管理的连续部署功能可使此可能要归功于**重新部署**管理门户中提供的操作。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="8a3e1-425">Azure 跟踪与推送到存储库的提交相关联的部署，并提供了一个选项以重新部署在任何时间使用任何以前部署的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="8a3e1-426">在此练习中将执行中的代码的更改**极客测验**有意注入的应用程序*bug*。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="8a3e1-427">将部署到生产应用程序，以查看错误，，然后您将利用重新部署功能，请返回到以前的状态。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="8a3e1-428">任务 1 – 极客测验应用程序更新</span><span class="sxs-lookup"><span data-stu-id="8a3e1-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="8a3e1-429">在此任务中，将重构代码的一小段**TriviaController**类提取到一个新的方法从数据库中检索所选的测验选项的逻辑的一部分。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="8a3e1-430">切换到包含 Visual Studio 实例**GeekQuiz**从上一练习的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="8a3e1-431">在中**解决方案资源管理器**，打开**TriviaController.cs**文件**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="8a3e1-432">找到**StoreAsync**方法，然后选择下图中突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![选择的代码](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="8a3e1-434">*选择的代码*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-434">*Selecting the code*</span></span>
4. <span data-ttu-id="8a3e1-435">右键单击所选的代码中，展开**重构**菜单，然后选择**提取方法...**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![作为新方法提取代码](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="8a3e1-437">*选择提取方法*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="8a3e1-438">在中**提取方法**对话框中，名称的新方法*MatchesOption*然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![指定方法名称](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="8a3e1-440">*指定提取的方法的名称*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="8a3e1-441">所选的代码然后提取到**MatchesOption**方法。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="8a3e1-442">生成的代码如以下代码片段所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="8a3e1-443">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="8a3e1-444">任务 2 – 重新部署极客测验应用程序</span><span class="sxs-lookup"><span data-stu-id="8a3e1-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="8a3e1-445">现在将推送到存储库，这将触发新部署到生产环境前一个任务中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="8a3e1-446">然后，您将使用诊断的故障问题**F12 开发工具**提供的 Internet Explorer，然后执行回滚到以前的部署从 Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="8a3e1-447">打开一个新**Git Bash**控制台部署到 Azure 应用服务更新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="8a3e1-448">执行以下命令以将所做的更改推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="8a3e1-449">更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="8a3e1-450">系统会提示输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![将重构的代码推送到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="8a3e1-452">*将重构的代码推送到 Azure*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="8a3e1-453">打开 Internet Explorer 并导航到你的 web 应用 (例如`http://<your-web-site>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="8a3e1-454">使用前面创建的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="8a3e1-455">按**F12**若要启动的开发工具，选择**网络**选项卡，单击**播放**按钮开始录制。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="8a3e1-456">![启动网络录制](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "启动网络录制")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="8a3e1-457">*启动网络录制*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-457">*Starting network recording*</span></span>
5. <span data-ttu-id="8a3e1-458">选择任何选项测验。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-458">Select any option of the quiz.</span></span> <span data-ttu-id="8a3e1-459">你将看到没有任何反应。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="8a3e1-460">在中**F12**窗口中，与 POST HTTP 请求对应的条目显示了 HTTP **500**结果。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 错误](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="8a3e1-462">*HTTP 500 错误*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="8a3e1-463">选择**控制台**选项卡。可能的原因的详细信息记录错误。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![记录的错误](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="8a3e1-465">*记录的错误*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-465">*Logged error*</span></span>
8. <span data-ttu-id="8a3e1-466">找到错误的详细信息部分。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-466">Locate the details part of the error.</span></span> <span data-ttu-id="8a3e1-467">很明显，重构您的上一步骤中提交的代码导致此错误。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="8a3e1-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="8a3e1-469">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-469">Do not close the browser.</span></span>
10. <span data-ttu-id="8a3e1-470">在新浏览器实例中，导航到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="8a3e1-471">选择**网站**单击在练习 2 中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="8a3e1-472">导航到**部署**页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="8a3e1-473">请注意，所有提交都执行部署历史记录中列出。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![现有部署的列表](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="8a3e1-475">*现有部署的列表*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="8a3e1-476">选择上一个提交，然后单击**重新部署**命令栏上。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![重新部署以前的提交](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="8a3e1-478">*重新部署以前的提交*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="8a3e1-479">当系统提示你确认，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-479">When prompted to confirm, click **Yes**.</span></span>

    ![确认重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="8a3e1-481">部署完成后，切换回浏览器实例与您的 web 应用和按**CTRL + F5**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="8a3e1-482">单击任一选项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-482">Click any of the options.</span></span> <span data-ttu-id="8a3e1-483">翻转动画现在需要的位置并将结果 (*正确/错误*) 将显示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="8a3e1-484">（可选）切换到**Git Bash**控制台并执行以下命令，以恢复到上一个提交。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-485">这些命令创建新的提交，撤消中 Git 存储库中的错误提交所做的所有更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="8a3e1-486">然后，azure 将重新部署应用程序使用新的提交。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="8a3e1-487">练习 4： 使用 Azure 存储进行缩放</span><span class="sxs-lookup"><span data-stu-id="8a3e1-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="8a3e1-488">**Blob**是最简单的方式来存储大量非结构化的文本或二进制数据，例如视频、 音频和图像。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="8a3e1-489">移动应用程序以存储静态内容，可通过直接向浏览器提供图像或文档中缩放应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="8a3e1-490">在此练习中，将移动到 Blob 容器的应用程序的静态内容。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="8a3e1-491">然后将配置应用程序以添加**ASP.NET URL 重写规则**中**Web.config**重定向到 Blob 容器的内容。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="8a3e1-492">任务 1 – 创建一个 Azure 存储帐户</span><span class="sxs-lookup"><span data-stu-id="8a3e1-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="8a3e1-493">在此任务中，您将学习如何创建新的存储帐户使用管理门户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="8a3e1-494">导航到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="8a3e1-495">选择**新 |数据服务 |存储 |快速创建**开始创建新的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="8a3e1-496">输入该帐户，然后选择的唯一名称**区域**从列表中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="8a3e1-497">单击**创建存储帐户**以继续。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="8a3e1-498">![创建新的存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "创建新的存储帐户")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="8a3e1-499">*创建新的存储帐户*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="8a3e1-500">在中**存储**部分中，等到新存储帐户的状态更改为*联机*才能继续执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="8a3e1-501">![创建存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "创建存储帐户")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="8a3e1-502">*创建存储帐户*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-502">*Storage Account created*</span></span>
4. <span data-ttu-id="8a3e1-503">单击存储帐户名称，然后单击**仪表板**在页面顶部的链接。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="8a3e1-504">**仪表板**页为您提供的帐户，而且可以在你的应用程序中使用的服务终结点的状态信息。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="8a3e1-505">![显示存储帐户仪表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "显示存储帐户仪表板")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="8a3e1-506">*显示存储帐户仪表板*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="8a3e1-507">单击**管理访问密钥**导航栏中的按钮。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="8a3e1-508">![管理访问密钥按钮](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "管理访问密钥按钮")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="8a3e1-509">*管理访问密钥按钮*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="8a3e1-510">在中**管理访问密钥**对话框中，复制**存储帐户名称**并**主访问密钥**因为你将在以下练习中需要它们。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="8a3e1-511">然后，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="8a3e1-512">![管理访问密钥对话框](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "管理访问密钥对话框")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="8a3e1-513">*管理访问密钥对话框*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="8a3e1-514">任务 2 – 将资产上传到 Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="8a3e1-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="8a3e1-515">在此任务中，将使用从 Visual Studio 服务器资源管理器窗口连接到你的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="8a3e1-516">然后，将创建 blob 容器，并将具有极客测验徽标的文件上传到容器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="8a3e1-517">切换到包含 Visual Studio 实例**GeekQuiz**从上一练习的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="8a3e1-518">从菜单栏中，选择**视图**，然后单击**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="8a3e1-519">在中**服务器资源管理器**，右键单击**Azure**节点，然后选择**连接到 Azure...**.使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![连接到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="8a3e1-521">*连接到 Azure*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="8a3e1-522">展开**Azure**节点，右键单击**存储**，然后选择**附加外部存储...**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="8a3e1-523">在中**添加新的存储帐户**对话框框中，输入**帐户名称**并**帐户密钥**获取在上一任务和单击**确定**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![新的存储帐户添加对话框](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="8a3e1-525">*新的存储帐户添加对话框*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="8a3e1-526">应显示你的存储帐户**存储**节点。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="8a3e1-527">展开你的存储帐户中，右键单击**Blob** ，然后选择**创建 Blob 容器...**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="8a3e1-528">![创建 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "创建 Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="8a3e1-529">*创建 Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="8a3e1-530">在中**创建 Blob 容器**对话框中，输入 blob 容器的名称，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="8a3e1-531">![创建 Blob 容器对话框](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "创建 Blob 容器对话框")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="8a3e1-532">*创建 Blob 容器对话框的*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="8a3e1-533">新的 blob 容器应添加到**Blob**节点。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="8a3e1-534">更改容器中的访问权限，以使容器公开。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="8a3e1-535">若要执行此操作，右键单击**映像**容器，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="8a3e1-536">![映像容器属性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "映像容器属性")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="8a3e1-537">*图像容器属性*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-537">*Images container properties*</span></span>
9. <span data-ttu-id="8a3e1-538">在中**属性**窗口中，将**公共读取访问权限**到**容器**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="8a3e1-539">![更改公共读取访问权限属性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "更改公共读取访问权限属性")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="8a3e1-540">*更改公共读取访问权限属性*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="8a3e1-541">当系统提示你是否确实要更改的公共访问权限属性，请单击**是**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="8a3e1-542">![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="8a3e1-543">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="8a3e1-544">在中**服务器资源管理器**，右键单击**映像**blob 容器，然后选择**查看 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="8a3e1-545">![查看 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "查看 Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="8a3e1-546">*查看 Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-546">*View Blob Container*</span></span>
12. <span data-ttu-id="8a3e1-547">图像容器应在新窗口中打开，并应显示图例没有项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="8a3e1-548">单击**上传**图标以将文件上传到 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="8a3e1-549">![没有任何项的图像容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "没有任何项的图像容器")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="8a3e1-550">*没有任何项的图像容器*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="8a3e1-551">在中**上传 Blob**对话框框中，导航到**资产**实验室的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="8a3e1-552">选择**徽标 big.png**文件，并单击**打开**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="8a3e1-553">等待，直到上传文件。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="8a3e1-554">上传完成后，应在图像容器中列出该文件。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="8a3e1-555">右键单击文件条目，然后选择**复制 URL**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="8a3e1-556">![复制 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "复制 blob 文件 URL")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="8a3e1-557">*复制 blob URL*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="8a3e1-558">打开 Internet Explorer 并粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="8a3e1-559">下图应在浏览器中所示。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="8a3e1-560">![徽标 big.png 图像从 Windows Blob 存储](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "徽标 big.png 图像从存储")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="8a3e1-561">*从 Azure Blob 存储的徽标 big.png 图像*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="8a3e1-562">任务 3 – 正在更新解决方案来使用从 Azure Blob 存储的静态内容</span><span class="sxs-lookup"><span data-stu-id="8a3e1-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="8a3e1-563">在本任务中，您将配置**GeekQuiz**解决方案，以使用该映像上传到 Azure Blob 存储 （而不是位于 web 应用中的映像） 通过添加在 ASP.NET URL 重写规则**web.config**文件。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="8a3e1-564">在 Visual Studio 中打开**Web.config**文件内**GeekQuiz**项目，然后找到**&lt;system.webServer&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="8a3e1-565">添加以下代码以添加一个 URL 重写规则，更新存储帐户名称的占位符。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="8a3e1-566">(代码段- *WebSitesInProduction-Ex4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="8a3e1-567">URL 重写是侦听传入 Web 请求并将请求重定向到不同的资源的过程。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="8a3e1-568">URL 重写规则可以使一个请求时需要重定向，并应它们在其中重定向，重写的引擎。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="8a3e1-569">重写规则两个字符串组成： 要在所请求 URL 中查找的模式 （通常情况下，使用正则表达式），并找到要替换的模式，如果该字符串。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="8a3e1-570">有关详细信息，请参阅[在 ASP.NET 中 URL 重写](https://msdn.microsoft.com/library/ms972974.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="8a3e1-571">按**CTRL + S**以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="8a3e1-572">打开一个新**Git Bash**控制台部署到 Azure 应用服务更新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="8a3e1-573">执行以下命令以将所做的更改推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="8a3e1-574">更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="8a3e1-575">系统会提示输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![将更新部署到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="8a3e1-577">*将更新部署到 Azure*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="8a3e1-578">任务 4 – 验证</span><span class="sxs-lookup"><span data-stu-id="8a3e1-578">Task 4 – Verification</span></span>

<span data-ttu-id="8a3e1-579">在此任务将使用**Internet Explorer**若要浏览**极客测验**应用程序并检查 URL 重写规则映像有效并且你将重定向到上托管的映像**Azure Blob存储**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="8a3e1-580">打开 Internet Explorer 并导航到你的 web 应用 (例如`http://<your-web-site>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="8a3e1-581">使用前面创建的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="8a3e1-582">![显示与映像极客测验 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "显示与映像极客测验 web 应用")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="8a3e1-583">*显示与映像极客测验 web 应用*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="8a3e1-584">按**F12**若要启动的开发工具，选择**网络**选项卡上，并开始记录。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="8a3e1-585">![启动网络录制](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "启动网络录制")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="8a3e1-586">*启动网络录制*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-586">*Starting network recording*</span></span>
3. <span data-ttu-id="8a3e1-587">按**CTRL + F5**刷新 web 页面。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="8a3e1-588">页面完成加载后，应看到的 HTTP 请求 **/img/logo-big.png**的 HTTP URL **301**结果 （重定向） 和另一个请求`http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png`URL 的 HTTP **200**结果。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="8a3e1-589">![验证 URL 重定向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "显示开发人员工具中的重定向")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="8a3e1-590">*验证 URL 重定向*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="8a3e1-591">练习 5： 使用自动缩放 Web 应用</span><span class="sxs-lookup"><span data-stu-id="8a3e1-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="8a3e1-592">本练习中是可选的因为它需要支持的 Web 负载&amp;性能测试，仅可用于**Visual Studio 2013 Ultimate Edition**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="8a3e1-593">有关特定 Visual Studio 2013 功能的详细信息，比较版本[此处](https://www.microsoft.com/visualstudio/eng/products/compare)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>


<span data-ttu-id="8a3e1-594">**Azure 应用服务 Web 应用**提供的自动缩放功能的 web 应用中运行**标准模式**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="8a3e1-595">自动缩放可以让 Azure 自动缩放根据负载 web 应用的实例计数。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="8a3e1-596">启用自动缩放后，Azure 一次每 5 分钟检查 web 应用的 CPU，并根据需要在某个时间点添加实例。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="8a3e1-597">如果 CPU 使用率较低，Azure 将删除实例一次每隔两小时以确保你的 web 应用的性能不会降低。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="8a3e1-598">在此练习中您将了解到配置所需的步骤**自动缩放**的功能**极客测验**web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="8a3e1-599">通过运行 Visual Studio 负载测试，以生成足够的 CPU 负载在要触发实例升级的应用程序，你将验证此功能。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="8a3e1-600">任务 1 – 根据 CPU 指标配置自动缩放</span><span class="sxs-lookup"><span data-stu-id="8a3e1-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="8a3e1-601">在此任务将使用 Azure 管理门户来启用您在练习 2 中创建的 web 应用的自动缩放功能。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="8a3e1-602">在中[Azure 管理门户](https://manage.windowsazure.com/)，选择**网站**单击在练习 2 中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="8a3e1-603">导航到**规模**页。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="8a3e1-604">下**容量**部分中，选择**CPU**有关**按度量值缩放**配置。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-605">时通过 CPU 进行缩放，Azure 会动态调整应用程序使用的 CPU 使用率更改的实例数。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="8a3e1-606">![选择按 CPU 进行缩放](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "选择的 CPU 指标的自动缩放")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="8a3e1-607">*选择按 CPU 进行缩放*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="8a3e1-608">更改**目标 CPU**配置到**20**-**40** %。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-609">此范围表示你的 web 应用的平均 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="8a3e1-610">Azure 将添加或删除实例以使您的 web 应用程序保持在此范围内。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="8a3e1-611">中指定最小值和最大缩放所用的实例数**实例计数**配置。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="8a3e1-612">Azure 将永远不会高于或超过该限制。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="8a3e1-613">默认值**目标 CPU**只是为了本实验的目的而修改的值。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="8a3e1-614">通过使用小的值配置 CPU 范围，你将要在中等负载放置在应用程序时增加触发自动缩放的可能性。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="8a3e1-615">![更改目标必须介于 20 和 40%的 CPU](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "更改要介于 20 到 40%的目标 CPU")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="8a3e1-616">*更改目标 CPU 必须介于 20 和 40%*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="8a3e1-617">单击**保存**以保存所做的更改的命令栏中。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="8a3e1-618">任务 2 – 通过 Visual Studio 负载测试</span><span class="sxs-lookup"><span data-stu-id="8a3e1-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="8a3e1-619">既然**自动缩放**已配置，您将创建**Web 性能和负载测试项目**在 Visual Studio 生成 web 应用上的一些 CPU 负载。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="8a3e1-620">打开**Visual Studio Ultimate 2013** ，然后选择**文件 |新 |项目...** 启动一个新的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="8a3e1-621">![创建新的项目](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "创建新的项目")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="8a3e1-622">*创建新的项目*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-622">*Creating a new project*</span></span>
2. <span data-ttu-id="8a3e1-623">在中**新的项目**对话框中，选择**Web 性能和负载测试项目**下**Visual C# |测试**选项卡。请确保 **.NET Framework 4.5**已选中，将项目命名*WebAndLoadTestProject*，选择**位置**然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="8a3e1-624">![创建新的 Web 和负载测试项目](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "创建新的 Web 和负载测试项目")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="8a3e1-625">*创建新的 Web 和负载测试项目*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="8a3e1-626">在中**WebTest1.webtest**右键单击**WebTest1**节点，然后单击**添加请求**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="8a3e1-627">![将请求添加到 WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "将请求添加到 WebTest1")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="8a3e1-628">*将请求添加到 WebTest1*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="8a3e1-629">在中**属性**窗口中的新的请求节点中，更新**Url**属性以指向你的 web 应用的 URL (例如*[ http://geek-quiz.azurewebsites.net/ ](http://geek-quiz.azurewebsites.net/)*).</span><span class="sxs-lookup"><span data-stu-id="8a3e1-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="8a3e1-630">![更改 Url 属性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "更改 Url 属性")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="8a3e1-631">*更改 Url 属性*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="8a3e1-632">在中**WebTest1.webtest**窗口中，右键单击**WebTest1**单击**添加循环...**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="8a3e1-633">![将循环添加到 WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "向 WebTest1 中添加循环")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="8a3e1-634">*向 WebTest1 中添加循环*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="8a3e1-635">在中**向循环添加条件规则和项**对话框中，选择**For 循环**规则，并修改以下属性。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="8a3e1-636">**终止值：** 1000年</span><span class="sxs-lookup"><span data-stu-id="8a3e1-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="8a3e1-637">**上下文参数名称：** 迭代器</span><span class="sxs-lookup"><span data-stu-id="8a3e1-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="8a3e1-638">**增量值：** 1</span><span class="sxs-lookup"><span data-stu-id="8a3e1-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="8a3e1-639">![选中该 For 循环规则，更新的属性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "选中该 For 循环规则，更新属性")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="8a3e1-640">*选中该 For 循环规则，更新属性*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="8a3e1-641">下**循环中的项**部分中，选择你之前创建为 for 循环的第一个和最后一个项的请求。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="8a3e1-642">单击“确定”  继续。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="8a3e1-643">![选择循环的第一个和最后一项](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "选择循环的第一个和最后一个项")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="8a3e1-644">*选择循环的第一个和最后一个项*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="8a3e1-645">在中**解决方案资源管理器**，右键单击**WebAndLoadTestProject**项目中，展开**添加**菜单，然后选择**负载测试...**.</span><span class="sxs-lookup"><span data-stu-id="8a3e1-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="8a3e1-646">![将负载测试添加到 WebAndLoadTestProject 项目](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "将负载测试添加到 WebAndLoadTestProject 项目")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="8a3e1-647">*将负载测试添加到 WebAndLoadTestProject 项目*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="8a3e1-648">在中**新建负载测试向导**对话框中，单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="8a3e1-649">![新建负载测试向导](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新建负载测试向导")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="8a3e1-650">*新建负载测试向导*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="8a3e1-651">在中**方案**页上，选择**不使用思考时间**然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="8a3e1-652">![选择不应使用思考时间](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "选择不应使用思考时间")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="8a3e1-653">*选择不使用思考时间*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="8a3e1-654">在中**负载模式**页上，请确保**常量负载**选择选项。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="8a3e1-655">更改**用户计数**将设置为**250**用户，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="8a3e1-656">![更改的用户计数为 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "为 250 更改的用户计数")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="8a3e1-657">*更改的用户计数为 250*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="8a3e1-658">在中**测试组合模型**页上，选择**基于顺序测试顺序**然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="8a3e1-659">![选择测试组合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "选择测试组合模型")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="8a3e1-660">*选择测试组合模型*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="8a3e1-661">在中**测试组合模型**页上，单击**添加...** 添加到组合的测试。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="8a3e1-662">![将测试添加到测试组合](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "将测试添加到测试组合")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="8a3e1-663">*将测试添加到测试组合*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="8a3e1-664">在中**添加测试**对话框中，双击**WebTest1**若要添加到测试**选定的测试**列表。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="8a3e1-665">单击“确定”  继续。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="8a3e1-666">![添加 WebTest1 测试](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "添加 WebTest1 测试")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="8a3e1-667">*添加 WebTest1 测试*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="8a3e1-668">回到**测试组合**页上，单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="8a3e1-669">![完成测试组合页](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "完成测试组合页")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="8a3e1-670">*完成测试组合页*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="8a3e1-671">在中**网络组合**页上，单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="8a3e1-672">![单击网络组合页中的下一个](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "接下来在网络组合页上单击")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="8a3e1-673">*单击网络组合页中的下一步*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="8a3e1-674">在中**浏览器组合**页上，选择**Internet Explorer 10.0**作为浏览器类型，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="8a3e1-675">![选择浏览器类型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "选择浏览器类型")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="8a3e1-676">*选择浏览器类型*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="8a3e1-677">在中**计数器集**页上，单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="8a3e1-678">![在计数器集页中单击下一步](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "单击下一步中计数器集页")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="8a3e1-679">*在计数器集页中单击下一步*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="8a3e1-680">在中**运行设置**页上，将**负载测试持续时间**到**5 分钟**然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="8a3e1-681">![将负载测试持续时间设置为 5 分钟](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "将负载测试持续时间设置为 5 分钟")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="8a3e1-682">*将负载测试持续时间设置为 5 分钟*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="8a3e1-683">在中**解决方案资源管理器**，双击**Local.settings**要探索测试设置文件。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="8a3e1-684">默认情况下，Visual Studio 使用本地计算机以运行测试。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-685">或者，您可以将测试项目配置为运行在云中使用负载测试**Azure 测试计划**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="8a3e1-686">Azure 测试计划提供了基于云的负载测试模拟实际负载的服务，避免本地环境约束，例如 CPU 容量、 可用内存和网络带宽。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="8a3e1-687">有关使用 Azure 的测试计划运行负载测试的详细信息，请参阅[负载测试方案](/azure/devops/test/load-test/overview?view=vsts)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![测试设置](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="8a3e1-689">任务 3 – 自动缩放验证</span><span class="sxs-lookup"><span data-stu-id="8a3e1-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="8a3e1-690">现在将执行你在上一任务中创建负载测试，请参阅你的 web 应用在负载下的行为方式。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="8a3e1-691">在中**解决方案资源管理器**，双击**LoadTest1.loadtest**以打开负载测试。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="8a3e1-692">![打开 LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "打开 LoadTest1.loadtest")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="8a3e1-693">*打开 LoadTest1.loadtest*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="8a3e1-694">在中**LoadTest1.loadtest**窗口中，单击工具箱以运行负载测试中的第一个按钮。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="8a3e1-695">![运行负载测试](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "运行负载测试")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="8a3e1-696">*运行负载测试*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-696">*Running the load test*</span></span>
3. <span data-ttu-id="8a3e1-697">等待，直到负载测试完成。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-698">负载测试模拟多个用户同时将请求发送到 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="8a3e1-699">当运行测试时，可以监视可用的计数器以检测任何错误、 警告或与你的负载测试运行相关的其他信息。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="8a3e1-700">![负载测试运行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "等待，直到完成加载测试")</span><span class="sxs-lookup"><span data-stu-id="8a3e1-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="8a3e1-701">*负载测试运行*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-701">*Load test running*</span></span>
4. <span data-ttu-id="8a3e1-702">完成测试后，请返回到管理门户并导航到**规模**web 应用的页面。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="8a3e1-703">下**容量**部分中，您应在图形中看到已自动部署的新实例。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![自动部署的新实例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="8a3e1-705">*自动部署的新实例*</span><span class="sxs-lookup"><span data-stu-id="8a3e1-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a3e1-706">它可能需要几分钟时间才会显示在图中的更改 (按**CTRL + F5**定期以刷新页面)。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="8a3e1-707">如果没有看到任何更改，可以尝试以下：</span><span class="sxs-lookup"><span data-stu-id="8a3e1-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="8a3e1-708">增加的负载测试的持续时间 (例如**10 分钟**)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="8a3e1-709">减少的最大和最小值**目标 CPU**范围中的 web 应用自动缩放配置</span><span class="sxs-lookup"><span data-stu-id="8a3e1-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="8a3e1-710">在云中运行负载测试**Azure 测试计划**。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="8a3e1-711">详细信息[此处](/azure/devops/test/load-test/index?view=vsts)</span><span class="sxs-lookup"><span data-stu-id="8a3e1-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="8a3e1-712">总结</span><span class="sxs-lookup"><span data-stu-id="8a3e1-712">Summary</span></span>

<span data-ttu-id="8a3e1-713">在本动手实验，您学习了如何设置和应用程序部署到 Azure 中的生产 web 应用。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="8a3e1-714">通过检测并更新数据库启动**Entity Framework Code First 迁移**，然后继续通过部署新版本的站点使用**Git**和执行回滚到你的站点的最新稳定版本。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="8a3e1-715">此外，您学习了如何缩放应用程序使用存储将静态内容移动到 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8a3e1-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
