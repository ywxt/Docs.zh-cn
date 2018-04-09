---
title: 使用 Visual Studio 的 Azure 和 ASP.NET Core 使用 Git 进行持续部署
author: rick-anderson
description: 了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/azure-continuous-deployment
ms.openlocfilehash: 4de1893e8c1f7f2f4d9af7278a110067ea777c61
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="continuous-deployment-to-azure-with-visual-studio-and-git-with-aspnet-core"></a><span data-ttu-id="3e147-103">使用 Visual Studio 的 Azure 和 ASP.NET Core 使用 Git 进行持续部署</span><span class="sxs-lookup"><span data-stu-id="3e147-103">Continuous deployment to Azure with Visual Studio and Git with ASP.NET Core</span></span>

<span data-ttu-id="3e147-104">作者：[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="3e147-104">By [Erik Reitan](https://github.com/Erikre)</span></span>

[!INCLUDE [Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

<span data-ttu-id="3e147-105">本教程演示如何创建使用 Visual Studio 的 ASP.NET 核心 web 应用并将其从 Visual Studio 部署到 Azure App Service，使用连续部署。</span><span class="sxs-lookup"><span data-stu-id="3e147-105">This tutorial shows how to create an ASP.NET Core web app using Visual Studio and deploy it from Visual Studio to Azure App Service using continuous deployment.</span></span>

<span data-ttu-id="3e147-106">另请参阅 [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)（使用 VSTS 生成并通过持续部署发布到 Azure Web 应用），其中演示如何使用 Visual Studio Team Services 为 [Azure App Service](/azure/app-service/app-service-web-overview) 配置持续交付 (CD) 工作流。</span><span class="sxs-lookup"><span data-stu-id="3e147-106">See also [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic), which shows how to configure a continuous delivery (CD) workflow for [Azure App Service](/azure/app-service/app-service-web-overview) using Visual Studio Team Services.</span></span> <span data-ttu-id="3e147-107">在 Team Services 的 azure 持续交付简化了可靠的部署管道的设置以发布托管在 Azure App Service 中的应用程序的更新。</span><span class="sxs-lookup"><span data-stu-id="3e147-107">Azure Continuous Delivery in Team Services simplifies setting up a robust deployment pipeline to publish updates for apps hosted in Azure App Service.</span></span> <span data-ttu-id="3e147-108">可以从 Azure 门户中生成、 运行测试，将部署到过渡槽中，以及然后部署到生产环境中配置管道。</span><span class="sxs-lookup"><span data-stu-id="3e147-108">The pipeline can be configured from the Azure portal to build, run tests, deploy to a staging slot, and then deploy to production.</span></span>

> [!NOTE]
> <span data-ttu-id="3e147-109">若要完成本教程，Microsoft Azure 帐户是必需的。</span><span class="sxs-lookup"><span data-stu-id="3e147-109">To complete this tutorial, a Microsoft Azure account is required.</span></span> <span data-ttu-id="3e147-110">若要获取帐户，[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F)或[注册一个免费试用版](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="3e147-110">To obtain an account, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e147-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="3e147-111">Prerequisites</span></span>

<span data-ttu-id="3e147-112">本教程假定安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="3e147-112">This tutorial assumes the following software is installed:</span></span>

* [<span data-ttu-id="3e147-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e147-113">Visual Studio</span></span>](https://www.visualstudio.com)
* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* <span data-ttu-id="3e147-114">用于 Windows 的 [Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="3e147-114">[Git](https://git-scm.com/downloads) for Windows</span></span>

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="3e147-115">创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="3e147-115">Create an ASP.NET Core web app</span></span>

1. <span data-ttu-id="3e147-116">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3e147-116">Start Visual Studio.</span></span>

1. <span data-ttu-id="3e147-117">从“文件”菜单中选择“新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="3e147-117">From the **File** menu, select **New** > **Project**.</span></span>

1. <span data-ttu-id="3e147-118">选择**ASP.NET Core Web 应用程序**项目模板。</span><span class="sxs-lookup"><span data-stu-id="3e147-118">Select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="3e147-119">它出现在“已安装” > “模板” > “Visual C#” > “.NET Core”下。</span><span class="sxs-lookup"><span data-stu-id="3e147-119">It appears under **Installed** > **Templates** > **Visual C#** > **.NET Core**.</span></span> <span data-ttu-id="3e147-120">将项目命名为 `SampleWebAppDemo`。</span><span class="sxs-lookup"><span data-stu-id="3e147-120">Name the project `SampleWebAppDemo`.</span></span> <span data-ttu-id="3e147-121">选择**创建新 Git 存储库**选项，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="3e147-121">Select the **Create new Git repository** option and click **OK**.</span></span>

   ![“新建项目”对话框](azure-continuous-deployment/_static/01-new-project.png)

1. <span data-ttu-id="3e147-123">在“新建 ASP.NET Core 项目”对话框中，选择 ASP.NET Core 的“空”模板，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3e147-123">In the **New ASP.NET Core Project** dialog, select the ASP.NET Core **Empty** template, then click **OK**.</span></span>

   ![“新建 ASP.NET 项目”对话框](azure-continuous-deployment/_static/02-web-site-template.png)

> [!NOTE]
> <span data-ttu-id="3e147-125">.NET 核心的最新版本为 2.0。</span><span class="sxs-lookup"><span data-stu-id="3e147-125">The most recent release of .NET Core is 2.0.</span></span>

### <a name="running-the-web-app-locally"></a><span data-ttu-id="3e147-126">本地运行 Web 应用</span><span class="sxs-lookup"><span data-stu-id="3e147-126">Running the web app locally</span></span>

1. <span data-ttu-id="3e147-127">Visual Studio 完成创建应用后，请选择“调试” > “启动调试”以运行该应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-127">Once Visual Studio finishes creating the app, run the app by selecting **Debug** > **Start Debugging**.</span></span> <span data-ttu-id="3e147-128">作为替代方法，按**F5**。</span><span class="sxs-lookup"><span data-stu-id="3e147-128">As an alternative, press **F5**.</span></span>

   <span data-ttu-id="3e147-129">可能需要一些时间对 Visual Studio 和新应用进行初始化。</span><span class="sxs-lookup"><span data-stu-id="3e147-129">It may take time to initialize Visual Studio and the new app.</span></span> <span data-ttu-id="3e147-130">完成后，浏览器将显示正在运行的应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-130">Once it's complete, the browser shows the running app.</span></span>

   ![显示正在运行的应用程序（显示“Hello World!”）的浏览器窗口](azure-continuous-deployment/_static/04-browser-runapp.png)

1. <span data-ttu-id="3e147-132">之后查看正在运行的 Web 应用，关闭浏览器，然后在 Visual Studio 以停止应用的工具栏中选择"停止调试"图标。</span><span class="sxs-lookup"><span data-stu-id="3e147-132">After reviewing the running Web app, close the browser and select the "Stop Debugging" icon in the toolbar of Visual Studio to stop the app.</span></span>

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="3e147-133">在 Azure 门户中创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="3e147-133">Create a web app in the Azure Portal</span></span>

<span data-ttu-id="3e147-134">以下步骤在 Azure 门户中创建 web 应用：</span><span class="sxs-lookup"><span data-stu-id="3e147-134">The following steps create a web app in the Azure Portal:</span></span>

1. <span data-ttu-id="3e147-135">登录到[Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3e147-135">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3e147-136">选择**新建**在左上角的门户界面。</span><span class="sxs-lookup"><span data-stu-id="3e147-136">Select **NEW** at the top left of the portal interface.</span></span>

1. <span data-ttu-id="3e147-137">选择**Web + 移动** > **Web 应用**。</span><span class="sxs-lookup"><span data-stu-id="3e147-137">Select **Web + Mobile** > **Web App**.</span></span>

   ![Microsoft Azure 门户：“新建”按钮：Marketplace 下的“Web + 移动”：“特别推荐的应用”下的“Web 应用”按钮](azure-continuous-deployment/_static/05-azure-newwebapp.png)

1. <span data-ttu-id="3e147-139">在“Web 应用”边栏选项卡中，输入“应用服务名称”的唯一值。</span><span class="sxs-lookup"><span data-stu-id="3e147-139">In the **Web App** blade, enter a unique value for the **App Service Name**.</span></span>

   ![“Web 应用”边栏选项卡](azure-continuous-deployment/_static/06-azure-newappblade.png)

   > [!NOTE]
   > <span data-ttu-id="3e147-141">**App Service 名称**名称必须唯一。</span><span class="sxs-lookup"><span data-stu-id="3e147-141">The **App Service Name** name must be unique.</span></span> <span data-ttu-id="3e147-142">门户执行此规则时提供的名称。</span><span class="sxs-lookup"><span data-stu-id="3e147-142">The portal enforces this rule when the name is provided.</span></span> <span data-ttu-id="3e147-143">如果提供不同的值，将替代的每个匹配项的值**SampleWebAppDemo**在本教程。</span><span class="sxs-lookup"><span data-stu-id="3e147-143">If providing a different value, substitute that value for each occurrence of **SampleWebAppDemo** in this tutorial.</span></span>

   <span data-ttu-id="3e147-144">另外，在“Web 应用”边栏选项卡中，选择现有“应用服务计划/位置”或新建一个。</span><span class="sxs-lookup"><span data-stu-id="3e147-144">Also in the **Web App** blade, select an existing **App Service Plan/Location** or create a new one.</span></span> <span data-ttu-id="3e147-145">如果创建新的计划，请选择定价层、 位置和其他选项。</span><span class="sxs-lookup"><span data-stu-id="3e147-145">If creating a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="3e147-146">App Service 计划的详细信息，请参阅[Azure App Service 计划深入概述](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。</span><span class="sxs-lookup"><span data-stu-id="3e147-146">For more information on App Service plans, see [Azure App Service plans in-depth overview](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

1. <span data-ttu-id="3e147-147">选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="3e147-147">Select **Create**.</span></span> <span data-ttu-id="3e147-148">Azure 将设置并启动 web 应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-148">Azure will provision and start the web app.</span></span>

   ![Azure 门户：示例 Web 应用演示 01 Essentials 边栏选项卡](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="3e147-150">为新 Web 应用启用 Git 发布</span><span class="sxs-lookup"><span data-stu-id="3e147-150">Enable Git publishing for the new web app</span></span>

<span data-ttu-id="3e147-151">Git 是一个分布式的版本控制系统，可用来部署 Azure App Service web 应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-151">Git is a distributed version control system that can be used to deploy an Azure App Service web app.</span></span> <span data-ttu-id="3e147-152">Web 应用程序代码存储在本地 Git 存储库，并且该代码通过将推送到远程存储库部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3e147-152">Web app code is stored in a local Git repository, and the code is deployed to Azure by pushing to a remote repository.</span></span>

1. <span data-ttu-id="3e147-153">登录到[Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3e147-153">Log into the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="3e147-154">选择**应用程序服务**以查看与 Azure 订阅关联的应用程序服务的列表。</span><span class="sxs-lookup"><span data-stu-id="3e147-154">Select **App Services** to view a list of the app services associated with the Azure subscription.</span></span>

1. <span data-ttu-id="3e147-155">选择在本教程的上一节中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-155">Select the web app created in the previous section of this tutorial.</span></span>

1. <span data-ttu-id="3e147-156">在“部署”边栏选项卡中，选择“部署选项” > “选择源” > “本地 Git 存储库”。</span><span class="sxs-lookup"><span data-stu-id="3e147-156">In the **Deployment** blade, select **Deployment options** > **Choose Source** > **Local Git Repository**.</span></span>

   ![“设置”边栏选项卡：“部署源”边栏选项卡：“选择源”边栏选项卡](azure-continuous-deployment/_static/deployment-options.png)

1. <span data-ttu-id="3e147-158">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="3e147-158">Select **OK**.</span></span>

1. <span data-ttu-id="3e147-159">如果以前尚未设置部署凭据用于发布 web 应用或其他 App Service 应用，它们现在设置：</span><span class="sxs-lookup"><span data-stu-id="3e147-159">If deployment credentials for publishing a web app or other App Service app haven't previously been set up, set them up now:</span></span>

   * <span data-ttu-id="3e147-160">选择**设置** > **部署凭据**。</span><span class="sxs-lookup"><span data-stu-id="3e147-160">Select **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="3e147-161">**设置部署凭据**显示边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="3e147-161">The **Set deployment credentials** blade is displayed.</span></span>
   * <span data-ttu-id="3e147-162">创建用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="3e147-162">Create a user name and password.</span></span> <span data-ttu-id="3e147-163">设置 Git 时，请保存以供将来使用的密码。</span><span class="sxs-lookup"><span data-stu-id="3e147-163">Save the password for later use when setting up Git.</span></span>
   * <span data-ttu-id="3e147-164">选择“保存”。</span><span class="sxs-lookup"><span data-stu-id="3e147-164">Select **Save**.</span></span>

1. <span data-ttu-id="3e147-165">在**Web 应用**边栏选项卡，选择**设置** > **属性**。</span><span class="sxs-lookup"><span data-stu-id="3e147-165">In the **Web App** blade, select **Settings** > **Properties**.</span></span> <span data-ttu-id="3e147-166">要将部署到远程 Git 存储库的 URL 将显示在**GIT URL**。</span><span class="sxs-lookup"><span data-stu-id="3e147-166">The URL of the remote Git repository to deploy to is shown under **GIT URL**.</span></span>

1. <span data-ttu-id="3e147-167">复制“GIT URL”的值，稍后将在本教程中用到。</span><span class="sxs-lookup"><span data-stu-id="3e147-167">Copy the **GIT URL** value for later use in the tutorial.</span></span>

   ![Azure 门户：应用程序“属性”边栏选项卡](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="3e147-169">将 web 应用发布到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e147-169">Publish the web app to Azure App Service</span></span>

<span data-ttu-id="3e147-170">在本部分中，创建使用 Visual Studio 和推送从该存储库到 Azure 来部署 web 应用的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="3e147-170">In this section, create a local Git repository using Visual Studio and push from that repository to Azure to deploy the web app.</span></span> <span data-ttu-id="3e147-171">涉及到的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="3e147-171">The steps involved include the following:</span></span>

* <span data-ttu-id="3e147-172">添加使用 GIT URL 值，因此可以将本地存储库部署到 Azure 的远程存储库设置。</span><span class="sxs-lookup"><span data-stu-id="3e147-172">Add the remote repository setting using the GIT URL value, so the local repository can be deployed to Azure.</span></span>
* <span data-ttu-id="3e147-173">提交项目进行的更改。</span><span class="sxs-lookup"><span data-stu-id="3e147-173">Commit project changes.</span></span>
* <span data-ttu-id="3e147-174">在 Azure 上，项目进行的更改从本地存储库推送到远程存储库。</span><span class="sxs-lookup"><span data-stu-id="3e147-174">Push project changes from the local repository to the remote repository on Azure.</span></span>

1. <span data-ttu-id="3e147-175">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="3e147-175">In **Solution Explorer** right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="3e147-176">**团队资源管理器**显示。</span><span class="sxs-lookup"><span data-stu-id="3e147-176">The **Team Explorer** is displayed.</span></span>

   ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/10-team-explorer.png)

1. <span data-ttu-id="3e147-178">在“团队资源管理器”中，选择“主页”（主页图标）>“设置” > “存储库设置”。</span><span class="sxs-lookup"><span data-stu-id="3e147-178">In **Team Explorer**, select the **Home** (home icon) > **Settings** > **Repository Settings**.</span></span>

1. <span data-ttu-id="3e147-179">在**远程网站**部分**存储库设置**，选择**添加**。</span><span class="sxs-lookup"><span data-stu-id="3e147-179">In the **Remotes** section of the **Repository Settings**, select **Add**.</span></span> <span data-ttu-id="3e147-180">**添加远程**对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="3e147-180">The **Add Remote** dialog box is displayed.</span></span>

1. <span data-ttu-id="3e147-181">将远程的“名称”设置为“Azure-SampleApp”。</span><span class="sxs-lookup"><span data-stu-id="3e147-181">Set the **Name** of the remote to **Azure-SampleApp**.</span></span>

1. <span data-ttu-id="3e147-182">将的值设置**提取**到**Git URL** ，在本教程前面部分中从 Azure 复制。</span><span class="sxs-lookup"><span data-stu-id="3e147-182">Set the value for **Fetch** to the **Git URL** that copied from Azure earlier in this tutorial.</span></span> <span data-ttu-id="3e147-183">请注意，此 URL 是以 .git 结尾的。</span><span class="sxs-lookup"><span data-stu-id="3e147-183">Note that this is the URL that ends with **.git**.</span></span>

   ![“编辑远程”对话框](azure-continuous-deployment/_static/11-add-remote.png)

   > [!NOTE]
   > <span data-ttu-id="3e147-185">作为替代方法，指定从远程存储库**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入命令。</span><span class="sxs-lookup"><span data-stu-id="3e147-185">As an alternative, specify the remote repository from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the command.</span></span> <span data-ttu-id="3e147-186">示例:</span><span class="sxs-lookup"><span data-stu-id="3e147-186">Example:</span></span>
   >
   > `git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`

1. <span data-ttu-id="3e147-187">选择“主页”（主页图标）>“设置” > “全局设置”。</span><span class="sxs-lookup"><span data-stu-id="3e147-187">Select the **Home** (home icon) > **Settings** > **Global Settings**.</span></span> <span data-ttu-id="3e147-188">确认设置的名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="3e147-188">Confirm that the name and email address are set.</span></span> <span data-ttu-id="3e147-189">选择**更新**必要情况。</span><span class="sxs-lookup"><span data-stu-id="3e147-189">Select **Update** if required.</span></span>

1. <span data-ttu-id="3e147-190">选择“主页” > “更改”以返回到“更改”视图。</span><span class="sxs-lookup"><span data-stu-id="3e147-190">Select **Home** > **Changes** to return to the **Changes** view.</span></span>

1. <span data-ttu-id="3e147-191">输入提交消息，如**初始推送 #1**和选择**提交**。</span><span class="sxs-lookup"><span data-stu-id="3e147-191">Enter a commit message, such as **Initial Push #1** and select **Commit**.</span></span> <span data-ttu-id="3e147-192">此操作将创建*提交*本地。</span><span class="sxs-lookup"><span data-stu-id="3e147-192">This action creates a *commit* locally.</span></span>

   ![“团队资源管理器连接”选项卡](azure-continuous-deployment/_static/12-initial-commit.png)

   > [!NOTE]
   > <span data-ttu-id="3e147-194">作为替代方法中的更改提交**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入 git 命令。</span><span class="sxs-lookup"><span data-stu-id="3e147-194">As an alternative, commit changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the git commands.</span></span> <span data-ttu-id="3e147-195">示例:</span><span class="sxs-lookup"><span data-stu-id="3e147-195">Example:</span></span>
   >
   > `git add .`
   >
   > `git commit -am "Initial Push #1"`

1. <span data-ttu-id="3e147-196">选择“主页” > “同步” > “操作” > “打开命令提示符”。</span><span class="sxs-lookup"><span data-stu-id="3e147-196">Select **Home** > **Sync** > **Actions** > **Open Command Prompt**.</span></span> <span data-ttu-id="3e147-197">命令提示打开的项目目录。</span><span class="sxs-lookup"><span data-stu-id="3e147-197">The command prompt opens to the project directory.</span></span>

1. <span data-ttu-id="3e147-198">在命令窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3e147-198">Enter the following command in the command window:</span></span>

   `git push -u Azure-SampleApp master`

1. <span data-ttu-id="3e147-199">输入 Azure**部署凭据**之前在 Azure 中创建的密码。</span><span class="sxs-lookup"><span data-stu-id="3e147-199">Enter the Azure **deployment credentials** password created earlier in Azure.</span></span>

   <span data-ttu-id="3e147-200">此命令启动将本地项目文件推送到 Azure 的过程。</span><span class="sxs-lookup"><span data-stu-id="3e147-200">This command starts the process of pushing the local project files to Azure.</span></span> <span data-ttu-id="3e147-201">上面的命令的输出由部署成功消息结尾。</span><span class="sxs-lookup"><span data-stu-id="3e147-201">The output from the above command ends with a message that the deployment was successful.</span></span>

   ```
   remote: Finished successfully.
   remote: Running post deployment command(s)...
   remote: Deployment successful.
   To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
   * [new branch]      master -> master
   Branch master set up to track remote branch master from Azure-SampleApp.
   ```

   > [!NOTE]
   > <span data-ttu-id="3e147-202">如果需要在项目上的协作，请考虑在推送到[GitHub](https://github.com)之前将推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3e147-202">If collaboration on the project is required, consider pushing to [GitHub](https://github.com) before pushing to Azure.</span></span>
 
### <a name="verify-the-active-deployment"></a><span data-ttu-id="3e147-203">验证活动的部署</span><span class="sxs-lookup"><span data-stu-id="3e147-203">Verify the Active Deployment</span></span>

<span data-ttu-id="3e147-204">验证与本地环境到 Azure web 应用程序传输成功。</span><span class="sxs-lookup"><span data-stu-id="3e147-204">Verify that the web app transfer from the local environment to Azure is successful.</span></span>

<span data-ttu-id="3e147-205">在[Azure 门户](https://portal.azure.com)，选择 web 应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-205">In the [Azure Portal](https://portal.azure.com), select the web app.</span></span> <span data-ttu-id="3e147-206">选择**部署** > **部署选项**。</span><span class="sxs-lookup"><span data-stu-id="3e147-206">Select **Deployment** > **Deployment options**.</span></span>

![Azure 门户：“设置”边栏选项卡：显示成功部署的“部署”边栏选项卡](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a><span data-ttu-id="3e147-208">在 Azure 中运行此应用</span><span class="sxs-lookup"><span data-stu-id="3e147-208">Run the app in Azure</span></span>

<span data-ttu-id="3e147-209">现在，web 应用部署到 Azure，运行该应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-209">Now that the web app is deployed to Azure, run the app.</span></span>

<span data-ttu-id="3e147-210">这可以通过两种方式实现：</span><span class="sxs-lookup"><span data-stu-id="3e147-210">This can be accomplished in two ways:</span></span>

* <span data-ttu-id="3e147-211">在 Azure 门户中，找到 web 应用的 web 应用边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="3e147-211">In the Azure Portal, locate the web app blade for the web app.</span></span> <span data-ttu-id="3e147-212">选择**浏览**在默认浏览器中查看应用。</span><span class="sxs-lookup"><span data-stu-id="3e147-212">Select **Browse** to view the app in the default browser.</span></span>
* <span data-ttu-id="3e147-213">打开浏览器并输入 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="3e147-213">Open a browser and enter the URL for the web app.</span></span> <span data-ttu-id="3e147-214">示例：`http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="3e147-214">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="update-the-web-app-and-republish"></a><span data-ttu-id="3e147-215">更新 web 应用程序并将重新发布</span><span class="sxs-lookup"><span data-stu-id="3e147-215">Update the web app and republish</span></span>

<span data-ttu-id="3e147-216">对本地代码进行更改后, 重新发布：</span><span class="sxs-lookup"><span data-stu-id="3e147-216">After making changes to the local code, republish:</span></span>

1. <span data-ttu-id="3e147-217">在 Visual Studio 的“解决方案资源管理器”中，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="3e147-217">In **Solution Explorer** of Visual Studio, open the *Startup.cs* file.</span></span>

1. <span data-ttu-id="3e147-218">在 `Configure` 方法中，修改 `Response.WriteAsync` 方法，使它显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="3e147-218">In the `Configure` method, modify the `Response.WriteAsync` method so that it appears as follows:</span></span>

   ```csharp
   await context.Response.WriteAsync("Hello World! Deploy to Azure.");
   ```

1. <span data-ttu-id="3e147-219">保存对*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="3e147-219">Save the changes to *Startup.cs*.</span></span>

1. <span data-ttu-id="3e147-220">在“解决方案资源管理器”中右键单击“解决方案 ‘SampleWebAppDemo’”并选择“提交”。</span><span class="sxs-lookup"><span data-stu-id="3e147-220">In **Solution Explorer**, right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="3e147-221">**团队资源管理器**显示。</span><span class="sxs-lookup"><span data-stu-id="3e147-221">The **Team Explorer** is displayed.</span></span>

1. <span data-ttu-id="3e147-222">输入提交消息，如`Update #2`。</span><span class="sxs-lookup"><span data-stu-id="3e147-222">Enter a commit message, such as `Update #2`.</span></span>

1. <span data-ttu-id="3e147-223">按“提交”按钮以提交项目更改。</span><span class="sxs-lookup"><span data-stu-id="3e147-223">Press the **Commit** button to commit the project changes.</span></span>

1. <span data-ttu-id="3e147-224">选择“主页” > “同步” > “操作” > “推送”。</span><span class="sxs-lookup"><span data-stu-id="3e147-224">Select **Home** > **Sync** > **Actions** > **Push**.</span></span>

> [!NOTE]
> <span data-ttu-id="3e147-225">作为替代方法，将从更改推送**命令窗口**通过打开**命令窗口**、 将更改为项目目录，然后输入 git 命令。</span><span class="sxs-lookup"><span data-stu-id="3e147-225">As an alternative, push the changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering a git command.</span></span> <span data-ttu-id="3e147-226">示例:</span><span class="sxs-lookup"><span data-stu-id="3e147-226">Example:</span></span>
> 
> `git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a><span data-ttu-id="3e147-227">在 Azure 中查看更新的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="3e147-227">View the updated web app in Azure</span></span>

<span data-ttu-id="3e147-228">通过选择查看更新的 web 应用**浏览**从 web 应用边栏选项卡在 Azure 门户或通过打开浏览器并输入 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="3e147-228">View the updated web app by selecting **Browse** from the web app blade in the Azure Portal or by opening a browser and entering the URL for the web app.</span></span> <span data-ttu-id="3e147-229">示例：`http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="3e147-229">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e147-230">其他资源</span><span class="sxs-lookup"><span data-stu-id="3e147-230">Additional resources</span></span>

* [<span data-ttu-id="3e147-231">VSTS 用于生成并发布到 Azure Web 应用程序使用连续部署</span><span class="sxs-lookup"><span data-stu-id="3e147-231">Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment</span></span>](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)
* [<span data-ttu-id="3e147-232">项目 Kudu</span><span class="sxs-lookup"><span data-stu-id="3e147-232">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
