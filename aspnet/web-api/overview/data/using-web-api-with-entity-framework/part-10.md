---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 将应用发布到 Azure 的 Azure 应用服务 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: 0290b392c1b292d0f3cc080dbfa25ec6103b2751
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400799"
---
<a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="38430-102">将应用发布到 Azure 的 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="38430-102">Publish the App to Azure Azure App Service</span></span>
====================
<span data-ttu-id="38430-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="38430-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="38430-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="38430-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="38430-105">作为最后一个步骤中，您将发布到 Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="38430-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="38430-106">在解决方案资源管理器，右键单击该项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="38430-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="38430-107">单击**发布**调用**发布 Web**对话框。</span><span class="sxs-lookup"><span data-stu-id="38430-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="38430-108">如果您选中**在云中托管**时首次创建项目，然后连接并已配置设置。</span><span class="sxs-lookup"><span data-stu-id="38430-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="38430-109">在这种情况下，只需单击**设置**选项卡并选中&quot;执行 Code First 迁移&quot;。</span><span class="sxs-lookup"><span data-stu-id="38430-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="38430-110">(如果未选中**云中的主机**在开始时，然后按照中的步骤[下一节](#new-website)。)</span><span class="sxs-lookup"><span data-stu-id="38430-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="38430-111">若要将应用部署，请单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="38430-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="38430-112">您可以查看中发布的进度**Web 发布活动**窗口。</span><span class="sxs-lookup"><span data-stu-id="38430-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="38430-113">(从**视图**菜单中，选择**其他 Windows**，然后选择**Web 发布活动**。)</span><span class="sxs-lookup"><span data-stu-id="38430-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="38430-114">完成 Visual Studio 部署应用后，默认浏览器会自动打开指向已部署网站的 URL 和你创建的应用程序现在在云中运行。</span><span class="sxs-lookup"><span data-stu-id="38430-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="38430-115">浏览器地址栏中的 URL 显示正在从 Internet 加载该站点。</span><span class="sxs-lookup"><span data-stu-id="38430-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="38430-116">部署到新网站</span><span class="sxs-lookup"><span data-stu-id="38430-116">Deploying to a New Website</span></span>

<span data-ttu-id="38430-117">如果未选中**在云中托管**时首次创建项目时，您可以立即配置新的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="38430-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="38430-118">在解决方案资源管理器，右键单击该项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="38430-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="38430-119">选择**配置文件**选项卡，单击**Microsoft Azure 网站**。</span><span class="sxs-lookup"><span data-stu-id="38430-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="38430-120">如果当前未登录到 Azure，系统会提示您登录。</span><span class="sxs-lookup"><span data-stu-id="38430-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="38430-121">在中**的现有网站**对话框中，单击**新建**。</span><span class="sxs-lookup"><span data-stu-id="38430-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="38430-122">输入站点名称。</span><span class="sxs-lookup"><span data-stu-id="38430-122">Enter a site name.</span></span> <span data-ttu-id="38430-123">选择你的 Azure 订阅和区域。</span><span class="sxs-lookup"><span data-stu-id="38430-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="38430-124">下**数据库服务器**，选择**创建新的服务器**，或选择现有的服务器。</span><span class="sxs-lookup"><span data-stu-id="38430-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="38430-125">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="38430-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="38430-126">单击**设置**选项卡并选中&quot;执行 Code First 迁移&quot;。</span><span class="sxs-lookup"><span data-stu-id="38430-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="38430-127">然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="38430-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="38430-128">上一篇</span><span class="sxs-lookup"><span data-stu-id="38430-128">Previous</span></span>](part-9.md)
