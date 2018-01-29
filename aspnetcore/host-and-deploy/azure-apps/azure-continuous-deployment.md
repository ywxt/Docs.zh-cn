---
title: "使用 Visual Studio 和 Git 持续部署到 Azure"
author: rick-anderson
description: "了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。"
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/azure-apps/azure-continuous-deployment
ms.openlocfilehash: c1d25b109bbf211eb476860ff77b649565960b62
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="continuous-deployment-to-azure-for-aspnet-core-with-visual-studio-and-git"></a><span data-ttu-id="071f3-103">ASP.NET Core 与 Visual Studio 和 Git 的连续部署到 Azure 的</span><span class="sxs-lookup"><span data-stu-id="071f3-103">Continuous deployment to Azure for ASP.NET Core with Visual Studio and Git</span></span>

<span data-ttu-id="071f3-104">作者：[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="071f3-104">By [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="071f3-105">本教程演示如何创建使用 Visual Studio 的 ASP.NET 核心 web 应用并将其从 Visual Studio 部署到 Azure App Service，使用连续部署。</span><span class="sxs-lookup"><span data-stu-id="071f3-105">This tutorial shows how to create an ASP.NET Core web app using Visual Studio and deploy it from Visual Studio to Azure App Service using continuous deployment.</span></span>

<span data-ttu-id="071f3-106">另请参阅 [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)（使用 VSTS 生成并通过持续部署发布到 Azure Web 应用），其中演示如何使用 Visual Studio Team Services 为 [Azure App Service](/azure/app-service/app-service-web-overview) 配置持续交付 (CD) 工作流。</span><span class="sxs-lookup"><span data-stu-id="071f3-106">See also [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic), which shows how to configure a continuous delivery (CD) workflow for [Azure App Service](/azure/app-service/app-service-web-overview) using Visual Studio Team Services.</span></span> <span data-ttu-id="071f3-107">在 Team Services 的 azure 持续交付简化了可靠的部署管道的设置以发布托管在 Azure App Service 中的应用程序的更新。</span><span class="sxs-lookup"><span data-stu-id="071f3-107">Azure Continuous Delivery in Team Services simplifies setting up a robust deployment pipeline to publish updates for apps hosted in Azure App Service.</span></span> <span data-ttu-id="071f3-108">可以从 Azure 门户中生成、 运行测试，将部署到过渡槽中，以及然后部署到生产环境中配置管道。</span><span class="sxs-lookup"><span data-stu-id="071f3-108">The pipeline can be configured from the Azure portal to build, run tests, deploy to a staging slot, and then deploy to production.</span></span>

> [!NOTE]
> <span data-ttu-id="071f3-109">若要完成本教程，Microsoft Azure 帐户是必需的。</span><span class="sxs-lookup"><span data-stu-id="071f3-109">To complete this tutorial, a Microsoft Azure account is required.</span></span> <span data-ttu-id="071f3-110">若要获取帐户，[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F)或[注册一个免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="071f3-110">To obtain an account, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="071f3-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="071f3-111">Prerequisites</span></span>

<span data-ttu-id="071f3-112">本教程假定安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="071f3-112">This tutorial assumes the following software is installed:</span></span>

* [<span data-ttu-id="071f3-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="071f3-113">Visual Studio</span></span>](https://www.visualstudio.com)
* <span data-ttu-id="071f3-114">[.NET 核心 SDK](https://www.microsoft.com/net/download/core) (运行时和工具)</span><span class="sxs-lookup"><span data-stu-id="071f3-114">[.NET Core SDK](https://www.microsoft.com/net/download/core) (runtime and tooling)</span></span>
* <span data-ttu-id="071f3-115">用于 Windows 的 [Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="071f3-115">[Git](https://git-scm.com/downloads) for Windows</span></span>

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="071f3-116">创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="071f3-116">Create an ASP.NET Core web app</span></span>

1. <span data-ttu-id="071f3-117">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="071f3-117">Start Visual Studio.</span></span>

1. <span data-ttu-id="071f3-118">从“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="071f3-118">From the **File** menu, select **New** > **Project**.</span></span>

1. <span data-ttu-id="071f3-119">选择“ASP.NET Core Web 应用程序”项目模板。</span><span class="sxs-lookup"><span data-stu-id="071f3-119">Select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="071f3-120">它出现在“已安装” > “模板” > “Visual C#” > “.NET Core”下。</span><span class="sxs-lookup"><span data-stu-id="071f3-120">It appears under **Installed** > **Templates** > **Visual C#** > **.NET Core**.</span></span> <span data-ttu-id="071f3-121">将项目命名为 `SampleWebAppDemo`。</span><span class="sxs-lookup"><span data-stu-id="071f3-121">Name the project `SampleWebAppDemo`.</span></span> <span data-ttu-id="071f3-122">选择“创建新 Git 存储库”选项，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="071f3-122">Select the **Create new Git respository** option and click **OK**.</span></span>

   ![“新建项目”对话框](azure-continuous-deployment/_static/01-new-project.png)

1. <span data-ttu-id="071f3-124">在“新建 ASP.NET Core 项目”对话框中，选择 ASP.NET Core 的“空”模板，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="071f3-124">In the **New ASP.NET Core Project** dialog, select the ASP.NET Core **Empty** template, then click **OK**.</span></span>

   ![“新建 ASP.NET 项目”对话框](azure-continuous-deployment/_static/02-web-site-template.png)

> [!NOTE]
> <span data-ttu-id="071f3-126">.NET 核心的最新版本为 2.0。</span><span class="sxs-lookup"><span data-stu-id="071f3-126">The most recent release of .NET Core is 2.0.</span></span>

### <a name="running-the-web-app-locally"></a><span data-ttu-id="071f3-127">本地运行 Web 应用</span><span class="sxs-lookup"><span data-stu-id="071f3-127">Running the web app locally</span></span>

1. <span data-ttu-id="071f3-128">Visual Studio 完成创建应用后，请选择“调试” > “启动调试”以运行该应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-128">Once Visual Studio finishes creating the app, run the app by selecting **Debug** > **Start Debugging**.</span></span> <span data-ttu-id="071f3-129">作为替代方法，按**F5**。</span><span class="sxs-lookup"><span data-stu-id="071f3-129">As an alternative, press **F5**.</span></span>

   <span data-ttu-id="071f3-130">可能需要一些时间对 Visual Studio 和新应用进行初始化。</span><span class="sxs-lookup"><span data-stu-id="071f3-130">It may take time to initialize Visual Studio and the new app.</span></span> <span data-ttu-id="071f3-131">完成后，浏览器将显示正在运行的应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-131">Once it's complete, the browser shows the running app.</span></span>

   ![显示正在运行的应用程序（显示“Hello World!”）的浏览器窗口](azure-continuous-deployment/_static/04-browser-runapp.png)

1. <span data-ttu-id="071f3-133">之后查看正在运行的 Web 应用，关闭浏览器，然后在 Visual Studio 以停止应用的工具栏中选择"停止调试"图标。</span><span class="sxs-lookup"><span data-stu-id="071f3-133">After reviewing the running Web app, close the browser and select the "Stop Debugging" icon in the toolbar of Visual Studio to stop the app.</span></span>

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="071f3-134">在 Azure 门户中创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="071f3-134">Create a web app in the Azure Portal</span></span>

<span data-ttu-id="071f3-135">以下步骤在 Azure 门户中创建 web 应用：</span><span class="sxs-lookup"><span data-stu-id="071f3-135">The following steps create a web app in the Azure Portal:</span></span>

1. <span data-ttu-id="071f3-136">登录到[Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="071f3-136">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="071f3-137">选择**新建**在左上角的门户界面。</span><span class="sxs-lookup"><span data-stu-id="071f3-137">Select **NEW** at the top left of the portal interface.</span></span>

1. <span data-ttu-id="071f3-138">选择**Web + 移动** > **Web 应用**。</span><span class="sxs-lookup"><span data-stu-id="071f3-138">Select **Web + Mobile** > **Web App**.</span></span>

   ![Microsoft Azure 门户：“新建”按钮：Marketplace 下的“Web + 移动”：“特别推荐的应用”下的“Web 应用”按钮](azure-continuous-deployment/_static/05-azure-newwebapp.png)

1. <span data-ttu-id="071f3-140">在“Web 应用”边栏选项卡中，输入“应用服务名称”的唯一值。</span><span class="sxs-lookup"><span data-stu-id="071f3-140">In the **Web App** blade, enter a unique value for the **App Service Name**.</span></span>

   ![“Web 应用”边栏选项卡](azure-continuous-deployment/_static/06-azure-newappblade.png)

   > [!NOTE]
   > <span data-ttu-id="071f3-142">**App Service 名称**名称必须唯一。</span><span class="sxs-lookup"><span data-stu-id="071f3-142">The **App Service Name** name must be unique.</span></span> <span data-ttu-id="071f3-143">门户执行此规则时提供的名称。</span><span class="sxs-lookup"><span data-stu-id="071f3-143">The portal enforces this rule when the name is provided.</span></span> <span data-ttu-id="071f3-144">如果提供不同的值，将替代的每个匹配项的值**SampleWebAppDemo**在本教程。</span><span class="sxs-lookup"><span data-stu-id="071f3-144">If providing a different value, substitute that value for each occurrence of **SampleWebAppDemo** in this tutorial.</span></span>

   <span data-ttu-id="071f3-145">另外，在“Web 应用”边栏选项卡中，选择现有“应用服务计划/位置”或新建一个。</span><span class="sxs-lookup"><span data-stu-id="071f3-145">Also in the **Web App** blade, select an existing **App Service Plan/Location** or create a new one.</span></span> <span data-ttu-id="071f3-146">如果创建新的计划，请选择定价层、 位置和其他选项。</span><span class="sxs-lookup"><span data-stu-id="071f3-146">If creating a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="071f3-147">App Service 计划的详细信息，请参阅[Azure App Service 计划深入概述](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。</span><span class="sxs-lookup"><span data-stu-id="071f3-147">For more information on App Service plans, see [Azure App Service plans in-depth overview](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

1. <span data-ttu-id="071f3-148">选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="071f3-148">Select **Create**.</span></span> <span data-ttu-id="071f3-149">Azure 将设置并启动 web 应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-149">Azure will provision and start the web app.</span></span>

   ![Azure 门户：示例 Web 应用演示 01 Essentials 边栏选项卡](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="071f3-151">为新 Web 应用启用 Git 发布</span><span class="sxs-lookup"><span data-stu-id="071f3-151">Enable Git publishing for the new web app</span></span>

<span data-ttu-id="071f3-152">Git 是一个分布式的版本控制系统，可用来部署 Azure App Service web 应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-152">Git is a distributed version control system that can be used to deploy an Azure App Service web app.</span></span> <span data-ttu-id="071f3-153">Web 应用程序代码存储在本地 Git 存储库，并且该代码通过将推送到远程存储库部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="071f3-153">Web app code is stored in a local Git repository, and the code is deployed to Azure by pushing to a remote repository.</span></span>

1. <span data-ttu-id="071f3-154">登录到[Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="071f3-154">Log into the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="071f3-155">选择**应用程序服务**以查看与 Azure 订阅关联的应用程序服务的列表。</span><span class="sxs-lookup"><span data-stu-id="071f3-155">Select **App Services** to view a list of the app services associated with the Azure subscription.</span></span>

1. <span data-ttu-id="071f3-156">选择在本教程的上一节中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-156">Select the web app created in the previous section of this tutorial.</span></span>

1. <span data-ttu-id="071f3-157">在“部署”边栏选项卡中，选择“部署选项” > “选择源” > “本地 Git 存储库”。</span><span class="sxs-lookup"><span data-stu-id="071f3-157">In the **Deployment** blade, select **Deployment options** > **Choose Source** > **Local Git Repository**.</span></span>

   ![“设置”边栏选项卡：“部署源”边栏选项卡：“选择源”边栏选项卡](azure-continuous-deployment/_static/deployment-options.png)

1. <span data-ttu-id="071f3-159">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="071f3-159">Select **OK**.</span></span>

1. <span data-ttu-id="071f3-160">如果以前尚未设置部署凭据用于发布 web 应用或其他 App Service 应用，它们现在设置：</span><span class="sxs-lookup"><span data-stu-id="071f3-160">If deployment credentials for publishing a web app or other App Service app haven't previously been set up, set them up now:</span></span>

   * <span data-ttu-id="071f3-161">选择**设置** > **部署凭据**。</span><span class="sxs-lookup"><span data-stu-id="071f3-161">Select **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="071f3-162">**设置部署凭据**显示边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="071f3-162">The **Set deployment credentials** blade is displayed.</span></span>
   * <span data-ttu-id="071f3-163">创建用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="071f3-163">Create a user name and password.</span></span> <span data-ttu-id="071f3-164">设置 Git 时，请保存以供将来使用的密码。</span><span class="sxs-lookup"><span data-stu-id="071f3-164">Save the password for later use when setting up Git.</span></span>
   * <span data-ttu-id="071f3-165">选择“保存”。</span><span class="sxs-lookup"><span data-stu-id="071f3-165">Select **Save**.</span></span>

1. <span data-ttu-id="071f3-166">在**Web 应用**边栏选项卡，选择**设置** > **属性**。</span><span class="sxs-lookup"><span data-stu-id="071f3-166">In the **Web App** blade, select **Settings** > **Properties**.</span></span> <span data-ttu-id="071f3-167">要将部署到远程 Git 存储库的 URL 将显示在**GIT URL**。</span><span class="sxs-lookup"><span data-stu-id="071f3-167">The URL of the remote Git repository to deploy to is shown under **GIT URL**.</span></span>

1. <span data-ttu-id="071f3-168">复制“GIT URL”的值，稍后将在本教程中用到。</span><span class="sxs-lookup"><span data-stu-id="071f3-168">Copy the **GIT URL** value for later use in the tutorial.</span></span>

   ![Azure 门户：应用程序“属性”边栏选项卡](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="071f3-170">将 web 应用发布到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="071f3-170">Publish the web app to Azure App Service</span></span>

<span data-ttu-id="071f3-171">在本部分中，创建使用 Visual Studio 和推送从该存储库到 Azure 来部署 web 应用的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="071f3-171">In this section, create a local Git repository using Visual Studio and push from that repository to Azure to deploy the web app.</span></span> <span data-ttu-id="071f3-172">涉及到的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="071f3-172">The steps involved include the following:</span></span>

* <span data-ttu-id="071f3-173">添加使用 GIT URL 值，因此可以将本地存储库部署到 Azure 的远程存储库设置。</span><span class="sxs-lookup"><span data-stu-id="071f3-173">Add the remote repository setting using the GIT URL value, so the local repository can be deployed to Azure.</span></span>
* <span data-ttu-id="071f3-174">提交项目进行的更改。</span><span class="sxs-lookup"><span data-stu-id="071f3-174">Commit project changes.</span></span>
* <span data-ttu-id="071f3-175">在 Azure 上，项目进行的更改从本地存储库推送到远程存储库。</span><span class="sxs-lookup"><span data-stu-id="071f3-175">Push project changes from the local repository to the remote repository on Azure.</span></span>

1. <span data-ttu-id="071f3-176">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="071f3-176">In **Solution Explorer** right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="071f3-177">**团队资源管理器**显示。</span><span class="sxs-lookup"><span data-stu-id="071f3-177">The **Team Explorer** is displayed.</span></span>

   ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/10-team-explorer.png)

1. <span data-ttu-id="071f3-179">在“团队资源管理器”中，选择“主页”（主页图标）>“设置” > “存储库设置”。</span><span class="sxs-lookup"><span data-stu-id="071f3-179">In **Team Explorer**, select the **Home** (home icon) > **Settings** > **Repository Settings**.</span></span>

1. <span data-ttu-id="071f3-180">在**远程网站**部分**存储库设置**，选择**添加**。</span><span class="sxs-lookup"><span data-stu-id="071f3-180">In the **Remotes** section of the **Repository Settings**, select **Add**.</span></span> <span data-ttu-id="071f3-181">**添加远程**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="071f3-181">The **Add Remote** dialog box is displayed.</span></span>

1. <span data-ttu-id="071f3-182">将远程的“名称”设置为“Azure-SampleApp”。</span><span class="sxs-lookup"><span data-stu-id="071f3-182">Set the **Name** of the remote to **Azure-SampleApp**.</span></span>

1. <span data-ttu-id="071f3-183">将的值设置**提取**到**Git URL** ，在本教程前面部分中从 Azure 复制。</span><span class="sxs-lookup"><span data-stu-id="071f3-183">Set the value for **Fetch** to the **Git URL** that copied from Azure earlier in this tutorial.</span></span> <span data-ttu-id="071f3-184">请注意，此 URL 是以 .git 结尾的。</span><span class="sxs-lookup"><span data-stu-id="071f3-184">Note that this is the URL that ends with **.git**.</span></span>

   ![“编辑远程”对话框](azure-continuous-deployment/_static/11-add-remote.png)

   > [!NOTE]
   > <span data-ttu-id="071f3-186">作为替代方法，指定从远程存储库**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入命令。</span><span class="sxs-lookup"><span data-stu-id="071f3-186">As an alternative, specify the remote repository from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the command.</span></span> <span data-ttu-id="071f3-187">示例:</span><span class="sxs-lookup"><span data-stu-id="071f3-187">Example:</span></span>
   >
   > `git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`

1. <span data-ttu-id="071f3-188">选择“主页”（主页图标）>“设置” > “全局设置”。</span><span class="sxs-lookup"><span data-stu-id="071f3-188">Select the **Home** (home icon) > **Settings** > **Global Settings**.</span></span> <span data-ttu-id="071f3-189">确认设置的名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="071f3-189">Confirm that the name and email address are set.</span></span> <span data-ttu-id="071f3-190">选择**更新**必要情况。</span><span class="sxs-lookup"><span data-stu-id="071f3-190">Select **Update** if required.</span></span>

1. <span data-ttu-id="071f3-191">选择“主页” > “更改”以返回到“更改”视图。</span><span class="sxs-lookup"><span data-stu-id="071f3-191">Select **Home** > **Changes** to return to the **Changes** view.</span></span>

1. <span data-ttu-id="071f3-192">输入提交消息，如**初始推送 #1**和选择**提交**。</span><span class="sxs-lookup"><span data-stu-id="071f3-192">Enter a commit message, such as **Initial Push #1** and select **Commit**.</span></span> <span data-ttu-id="071f3-193">此操作将创建*提交*本地。</span><span class="sxs-lookup"><span data-stu-id="071f3-193">This action creates a *commit* locally.</span></span>

   ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/12-initial-commit.png)

   > [!NOTE]
   > <span data-ttu-id="071f3-195">作为替代方法中的更改提交**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入 git 命令。</span><span class="sxs-lookup"><span data-stu-id="071f3-195">As an alternative, commit changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the git commands.</span></span> <span data-ttu-id="071f3-196">示例:</span><span class="sxs-lookup"><span data-stu-id="071f3-196">Example:</span></span>
   >
   > `git add .`
   >
   > `git commit -am "Initial Push #1"`

1. <span data-ttu-id="071f3-197">选择“主页” > “同步” > “操作” > “打开命令提示符”。</span><span class="sxs-lookup"><span data-stu-id="071f3-197">Select **Home** > **Sync** > **Actions** > **Open Command Prompt**.</span></span> <span data-ttu-id="071f3-198">命令提示打开的项目目录。</span><span class="sxs-lookup"><span data-stu-id="071f3-198">The command prompt opens to the project directory.</span></span>

1. <span data-ttu-id="071f3-199">在命令窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="071f3-199">Enter the following command in the command window:</span></span>

   `git push -u Azure-SampleApp master`

1. <span data-ttu-id="071f3-200">输入 Azure**部署凭据**之前在 Azure 中创建的密码。</span><span class="sxs-lookup"><span data-stu-id="071f3-200">Enter the Azure **deployment credentials** password created earlier in Azure.</span></span>

   <span data-ttu-id="071f3-201">此命令启动将本地项目文件推送到 Azure 的过程。</span><span class="sxs-lookup"><span data-stu-id="071f3-201">This command starts the process of pushing the local project files to Azure.</span></span> <span data-ttu-id="071f3-202">上面的命令的输出由部署成功消息结尾。</span><span class="sxs-lookup"><span data-stu-id="071f3-202">The output from the above command ends with a message that the deployment was successful.</span></span>

   ```
   remote: Finished successfully.
   remote: Running post deployment command(s)...
   remote: Deployment successful.
   To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
   * [new branch]      master -> master
   Branch master set up to track remote branch master from Azure-SampleApp.
   ```

   > [!NOTE]
   > <span data-ttu-id="071f3-203">如果需要在项目上的协作，请考虑在推送到[GitHub](https://github.com)之前将推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="071f3-203">If collaboration on the project is required, consider pushing to [GitHub](https://github.com) before pushing to Azure.</span></span>
 
### <a name="verify-the-active-deployment"></a><span data-ttu-id="071f3-204">验证活动的部署</span><span class="sxs-lookup"><span data-stu-id="071f3-204">Verify the Active Deployment</span></span>

<span data-ttu-id="071f3-205">验证与本地环境到 Azure web 应用程序传输成功。</span><span class="sxs-lookup"><span data-stu-id="071f3-205">Verify that the web app transfer from the local environment to Azure is successful.</span></span>

<span data-ttu-id="071f3-206">在[Azure 门户](https://portal.azure.com)，选择 web 应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-206">In the [Azure Portal](https://portal.azure.com), select the web app.</span></span> <span data-ttu-id="071f3-207">选择**部署** > **部署选项**。</span><span class="sxs-lookup"><span data-stu-id="071f3-207">Select **Deployment** > **Deployment options**.</span></span>

![Azure 门户：“设置”边栏选项卡：显示成功部署的“部署”边栏选项卡](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a><span data-ttu-id="071f3-209">在 Azure 中运行此应用</span><span class="sxs-lookup"><span data-stu-id="071f3-209">Run the app in Azure</span></span>

<span data-ttu-id="071f3-210">现在，web 应用部署到 Azure，运行该应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-210">Now that the web app is deployed to Azure, run the app.</span></span>

<span data-ttu-id="071f3-211">这可以通过两种方式实现：</span><span class="sxs-lookup"><span data-stu-id="071f3-211">This can be accomplished in two ways:</span></span>

* <span data-ttu-id="071f3-212">在 Azure 门户中，找到 web 应用的 web 应用边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="071f3-212">In the Azure Portal, locate the web app blade for the web app.</span></span> <span data-ttu-id="071f3-213">选择**浏览**在默认浏览器中查看应用。</span><span class="sxs-lookup"><span data-stu-id="071f3-213">Select **Browse** to view the app in the default browser.</span></span>
* <span data-ttu-id="071f3-214">打开浏览器并输入 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="071f3-214">Open a browser and enter the URL for the web app.</span></span> <span data-ttu-id="071f3-215">示例：`http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="071f3-215">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="update-the-web-app-and-republish"></a><span data-ttu-id="071f3-216">更新 web 应用程序并将重新发布</span><span class="sxs-lookup"><span data-stu-id="071f3-216">Update the web app and republish</span></span>

<span data-ttu-id="071f3-217">对本地代码进行更改后, 重新发布：</span><span class="sxs-lookup"><span data-stu-id="071f3-217">After making changes to the local code, republish:</span></span>

1. <span data-ttu-id="071f3-218">在 Visual Studio 的“解决方案资源管理器”中，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="071f3-218">In **Solution Explorer** of Visual Studio, open the *Startup.cs* file.</span></span>

1. <span data-ttu-id="071f3-219">在 `Configure` 方法中，修改 `Response.WriteAsync` 方法，使它显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="071f3-219">In the `Configure` method, modify the `Response.WriteAsync` method so that it appears as follows:</span></span>

   ```csharp
   await context.Response.WriteAsync("Hello World! Deploy to Azure.");
   ```

1. <span data-ttu-id="071f3-220">保存对*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="071f3-220">Save the changes to *Startup.cs*.</span></span>

1. <span data-ttu-id="071f3-221">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="071f3-221">In **Solution Explorer**, right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="071f3-222">**团队资源管理器**显示。</span><span class="sxs-lookup"><span data-stu-id="071f3-222">The **Team Explorer** is displayed.</span></span>

1. <span data-ttu-id="071f3-223">输入提交消息，如`Update #2`。</span><span class="sxs-lookup"><span data-stu-id="071f3-223">Enter a commit message, such as `Update #2`.</span></span>

1. <span data-ttu-id="071f3-224">按“提交”按钮以提交项目更改。</span><span class="sxs-lookup"><span data-stu-id="071f3-224">Press the **Commit** button to commit the project changes.</span></span>

1. <span data-ttu-id="071f3-225">选择“主页” > “同步” > “操作” > “推送”。</span><span class="sxs-lookup"><span data-stu-id="071f3-225">Select **Home** > **Sync** > **Actions** > **Push**.</span></span>

> [!NOTE]
> <span data-ttu-id="071f3-226">作为替代方法，将从更改推送**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入 git 命令。</span><span class="sxs-lookup"><span data-stu-id="071f3-226">As an alternative, push the changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering a git command.</span></span> <span data-ttu-id="071f3-227">示例:</span><span class="sxs-lookup"><span data-stu-id="071f3-227">Example:</span></span>
> 
> `git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a><span data-ttu-id="071f3-228">在 Azure 中查看更新的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="071f3-228">View the updated web app in Azure</span></span>

<span data-ttu-id="071f3-229">通过选择查看更新的 web 应用**浏览**从 web 应用边栏选项卡在 Azure 门户或通过打开浏览器并输入 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="071f3-229">View the updated web app by selecting **Browse** from the web app blade in the Azure Portal or by opening a browser and entering the URL for the web app.</span></span> <span data-ttu-id="071f3-230">示例：`http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="071f3-230">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="071f3-231">其他资源</span><span class="sxs-lookup"><span data-stu-id="071f3-231">Additional resources</span></span>

* [<span data-ttu-id="071f3-232">VSTS 用于生成并发布到 Azure Web 应用程序使用连续部署</span><span class="sxs-lookup"><span data-stu-id="071f3-232">Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment</span></span>](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)
* [<span data-ttu-id="071f3-233">项目 Kudu</span><span class="sxs-lookup"><span data-stu-id="071f3-233">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
