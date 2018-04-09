---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 与实体框架 6 使用 Web API 2 |Microsoft 文档
author: MikeWasson
description: 本教程将教您创建的 ASP.NET Web API 的 web 应用程序的基础知识后端。 本教程使用 Entity Framework 6 的数据布局...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 8e6d381509a121e3036ca3af91ea3b9bd0be33c2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="166bf-104">与实体框架 6 使用 Web API 2</span><span class="sxs-lookup"><span data-stu-id="166bf-104">Using Web API 2 with Entity Framework 6</span></span>
====================
<span data-ttu-id="166bf-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="166bf-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="166bf-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="166bf-106">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="166bf-107">本教程将教您创建的 ASP.NET Web API 的 web 应用程序的基础知识后端。</span><span class="sxs-lookup"><span data-stu-id="166bf-107">This tutorial will teach you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="166bf-108">本教程使用 Entity Framework 6 进行的数据层和 Knockout.js 进行客户端 JavaScript 应用程序。</span><span class="sxs-lookup"><span data-stu-id="166bf-108">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="166bf-109">本教程还演示如何将应用部署到 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="166bf-109">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="166bf-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="166bf-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="166bf-111">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="166bf-111">Web API 2.1</span></span>
> - [<span data-ttu-id="166bf-112">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="166bf-112">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="166bf-113">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="166bf-113">Entity Framework 6</span></span>
> - <span data-ttu-id="166bf-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="166bf-114">.NET 4.5</span></span>
> - <span data-ttu-id="166bf-115">[Knockout.js](http://knockoutjs.com/) 3.1</span><span class="sxs-lookup"><span data-stu-id="166bf-115">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>


<span data-ttu-id="166bf-116">本教程使用 Entity Framework 6 和 ASP.NET Web API 2 创建的 web 应用程序操作后端数据库。</span><span class="sxs-lookup"><span data-stu-id="166bf-116">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="166bf-117">下面是应用的将创建程序的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="166bf-117">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="166bf-118">该应用使用单页面应用程序 (SPA) 设计。</span><span class="sxs-lookup"><span data-stu-id="166bf-118">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="166bf-119">"单页面应用程序"是 web 应用程序加载单个 HTML 页，然后页动态更新，而不是加载新页面常用术语。</span><span class="sxs-lookup"><span data-stu-id="166bf-119">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="166bf-120">初始页加载后, 应用程序介绍与通过 AJAX 请求服务器。</span><span class="sxs-lookup"><span data-stu-id="166bf-120">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="166bf-121">AJAX 请求返回的 JSON 数据，应用程序用它来更新 UI。</span><span class="sxs-lookup"><span data-stu-id="166bf-121">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="166bf-122">AJAX 不是新的但目前有更加轻松地生成和维护一个大型的复杂的 SPA 应用程序的 JavaScript 框架。</span><span class="sxs-lookup"><span data-stu-id="166bf-122">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="166bf-123">本教程使用[Knockout.js](http://knockoutjs.com/)，但你可以使用任一 JavaScript 客户端框架。</span><span class="sxs-lookup"><span data-stu-id="166bf-123">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="166bf-124">下面是此应用程序主要构建基块：</span><span class="sxs-lookup"><span data-stu-id="166bf-124">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="166bf-125">ASP.NET MVC 创建 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="166bf-125">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="166bf-126">ASP.NET Web API 处理 AJAX 请求，并返回 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="166bf-126">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="166bf-127">Knockout.js 数据绑定的 HTML 元素 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="166bf-127">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="166bf-128">实体框架与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="166bf-128">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="166bf-129">请参阅在 Azure 上运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="166bf-129">See this App Running on Azure</span></span>

<span data-ttu-id="166bf-130">若要查看与实时 web 应用运行的已完成的站点吗？</span><span class="sxs-lookup"><span data-stu-id="166bf-130">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="166bf-131">只需单击下面的按钮，可以将应用程序的完整版本部署到你的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="166bf-131">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="166bf-132">你需要将此解决方案部署到 Azure 的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="166bf-132">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="166bf-133">如果你还没有帐户，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="166bf-133">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="166bf-134">[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度来试用付费版 Azure 服务，你可以使用和甚至在用完后，最多可以保留帐户和使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="166bf-134">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="166bf-135">[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅为你的信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="166bf-135">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="166bf-136">创建项目</span><span class="sxs-lookup"><span data-stu-id="166bf-136">Create the Project</span></span>

<span data-ttu-id="166bf-137">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="166bf-137">Open Visual Studio.</span></span> <span data-ttu-id="166bf-138">从**文件**菜单上，选择**新建**，然后选择**项目**。</span><span class="sxs-lookup"><span data-stu-id="166bf-138">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="166bf-139">(或单击**新项目**起始页上。)</span><span class="sxs-lookup"><span data-stu-id="166bf-139">(Or click **New Project** on the Start page.)</span></span>

<span data-ttu-id="166bf-140">在**新项目**对话框中，单击**Web**的左窗格中和**ASP.NET Web 应用程序**在中间窗格中。</span><span class="sxs-lookup"><span data-stu-id="166bf-140">In the **New Project** dialog, click **Web** in the left pane and **ASP.NET Web Application** in the middle pane.</span></span> <span data-ttu-id="166bf-141">将项目 BookService，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="166bf-141">Name the project BookService and click **OK**.</span></span>

[![](part-1/_static/image4.png)](part-1/_static/image3.png)

<span data-ttu-id="166bf-142">在**新建 ASP.NET 项目**对话框中，选择**Web API**模板。</span><span class="sxs-lookup"><span data-stu-id="166bf-142">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image6.png)](part-1/_static/image5.png)

<span data-ttu-id="166bf-143">如果你想要托管在 Azure App Service 中的项目，请将**在云中托管**选中框。</span><span class="sxs-lookup"><span data-stu-id="166bf-143">If you want to host the project in a Azure App Service, leave the **Host in the cloud** box checked.</span></span>

<span data-ttu-id="166bf-144">单击“确定”，创建项目。</span><span class="sxs-lookup"><span data-stu-id="166bf-144">Click **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="166bf-145">配置 Azure 设置 （可选）</span><span class="sxs-lookup"><span data-stu-id="166bf-145">Configure Azure Settings (Optional)</span></span>

<span data-ttu-id="166bf-146">如果保留**云中的主机**选中选项，Visual Studio 将提示你登录到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="166bf-146">If you left the **Host in Cloud** option checked, Visual Studio will prompt you to sign in to Microsoft Azure</span></span>

[![](part-1/_static/image8.png)](part-1/_static/image7.png)

<span data-ttu-id="166bf-147">登录到 Azure 后，Visual Studio 会提示你配置 web 应用。</span><span class="sxs-lookup"><span data-stu-id="166bf-147">After you sign in to Azure, Visual Studio prompts you to configure the web app.</span></span> <span data-ttu-id="166bf-148">输入站点的名称，选择你的 Azure 订阅，然后选择地理区域。</span><span class="sxs-lookup"><span data-stu-id="166bf-148">Enter a name for the site, select your Azure subscription, and select a geographical region.</span></span> <span data-ttu-id="166bf-149">下**数据库服务器**，选择**创建新的服务器**。</span><span class="sxs-lookup"><span data-stu-id="166bf-149">Under **Database server**, select **Create new server**.</span></span> <span data-ttu-id="166bf-150">输入管理员用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="166bf-150">Enter an administrator username and password.</span></span>

[![](part-1/_static/image10.png)](part-1/_static/image9.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="166bf-151">下一篇</span><span class="sxs-lookup"><span data-stu-id="166bf-151">Next</span></span>](part-2.md)
