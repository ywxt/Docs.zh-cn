---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 通过 Entity Framework 6 使用 Web API 2 |Microsoft Docs
author: MikeWasson
description: 本教程将讲述使用 ASP.NET Web API 创建 web 应用程序的基础知识后端。 本教程使用 Entity Framework 6 的数据布局...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 4abe0e06dfd927765efd8e566584e111cf4117d5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834131"
---
<a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="07778-104">通过 Entity Framework 6 使用 Web API 2</span><span class="sxs-lookup"><span data-stu-id="07778-104">Using Web API 2 with Entity Framework 6</span></span>
====================
<span data-ttu-id="07778-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="07778-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="07778-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="07778-106">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="07778-107">本教程将讲述使用 ASP.NET Web API 创建 web 应用程序的基础知识后端。</span><span class="sxs-lookup"><span data-stu-id="07778-107">This tutorial will teach you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="07778-108">本教程使用 Entity Framework 6 进行的数据层和 Knockout.js 进行客户端的 JavaScript 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07778-108">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="07778-109">本教程还演示如何将应用部署到 Azure 应用服务 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="07778-109">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="07778-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="07778-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="07778-111">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="07778-111">Web API 2.1</span></span>
> - [<span data-ttu-id="07778-112">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="07778-112">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="07778-113">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="07778-113">Entity Framework 6</span></span>
> - <span data-ttu-id="07778-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="07778-114">.NET 4.5</span></span>
> - <span data-ttu-id="07778-115">[Knockout.js](http://knockoutjs.com/) 3.1</span><span class="sxs-lookup"><span data-stu-id="07778-115">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>


<span data-ttu-id="07778-116">本教程中使用 Entity Framework 6 与 ASP.NET Web API 2 创建操作后端数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07778-116">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="07778-117">下面是您将创建的应用程序的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="07778-117">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="07778-118">该应用使用单页面应用程序 (SPA) 设计。</span><span class="sxs-lookup"><span data-stu-id="07778-118">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="07778-119">"单页面应用程序"是加载单个 HTML 页面，然后页面动态更新，而不是加载新页面的 web 应用程序的常规术语。</span><span class="sxs-lookup"><span data-stu-id="07778-119">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="07778-120">初始页面加载后该应用通过 AJAX 请求与服务器通信。</span><span class="sxs-lookup"><span data-stu-id="07778-120">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="07778-121">AJAX 请求返回 JSON 数据时，应用程序用它来更新 UI。</span><span class="sxs-lookup"><span data-stu-id="07778-121">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="07778-122">AJAX 并不新鲜，但如今有更加轻松地构建和维护大型复杂的 SPA 应用程序的 JavaScript 框架。</span><span class="sxs-lookup"><span data-stu-id="07778-122">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="07778-123">本教程使用[Knockout.js](http://knockoutjs.com/)，但您可以使用任何 JavaScript 客户端框架。</span><span class="sxs-lookup"><span data-stu-id="07778-123">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="07778-124">下面是此应用的主要构建基块：</span><span class="sxs-lookup"><span data-stu-id="07778-124">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="07778-125">ASP.NET MVC 创建 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="07778-125">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="07778-126">ASP.NET Web API 处理 AJAX 请求，并返回 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="07778-126">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="07778-127">Knockout.js 数据绑定 HTML 元素的 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="07778-127">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="07778-128">实体框架与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="07778-128">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="07778-129">请参阅在 Azure 上运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="07778-129">See this App Running on Azure</span></span>

<span data-ttu-id="07778-130">若要查看已完成的站点作为实时 web 应用运行吗？</span><span class="sxs-lookup"><span data-stu-id="07778-130">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="07778-131">只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="07778-131">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="07778-132">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="07778-132">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="07778-133">如果你还没有帐户，你具有以下选项：</span><span class="sxs-lookup"><span data-stu-id="07778-133">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="07778-134">[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="07778-134">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="07778-135">[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="07778-135">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="07778-136">创建项目</span><span class="sxs-lookup"><span data-stu-id="07778-136">Create the Project</span></span>

<span data-ttu-id="07778-137">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="07778-137">Open Visual Studio.</span></span> <span data-ttu-id="07778-138">从**文件**菜单中，选择**新建**，然后选择**项目**。</span><span class="sxs-lookup"><span data-stu-id="07778-138">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="07778-139">(或单击**新的项目**起始页上。)</span><span class="sxs-lookup"><span data-stu-id="07778-139">(Or click **New Project** on the Start page.)</span></span>

<span data-ttu-id="07778-140">在**新的项目**对话框中，单击**Web**左窗格中并**ASP.NET Web 应用程序**在中间窗格中。</span><span class="sxs-lookup"><span data-stu-id="07778-140">In the **New Project** dialog, click **Web** in the left pane and **ASP.NET Web Application** in the middle pane.</span></span> <span data-ttu-id="07778-141">项目 BookService 命名，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="07778-141">Name the project BookService and click **OK**.</span></span>

[![](part-1/_static/image4.png)](part-1/_static/image3.png)

<span data-ttu-id="07778-142">在中**新建 ASP.NET 项目**对话框中，选择**Web API**模板。</span><span class="sxs-lookup"><span data-stu-id="07778-142">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image6.png)](part-1/_static/image5.png)

<span data-ttu-id="07778-143">如果你想要承载 Azure 应用服务中的项目，请将**在云中托管**选中框。</span><span class="sxs-lookup"><span data-stu-id="07778-143">If you want to host the project in a Azure App Service, leave the **Host in the cloud** box checked.</span></span>

<span data-ttu-id="07778-144">单击“确定”，创建项目。</span><span class="sxs-lookup"><span data-stu-id="07778-144">Click **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="07778-145">配置 Azure 设置 （可选）</span><span class="sxs-lookup"><span data-stu-id="07778-145">Configure Azure Settings (Optional)</span></span>

<span data-ttu-id="07778-146">如果你离开**在云中托管**选中选项，Visual Studio 会提示你登录到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="07778-146">If you left the **Host in Cloud** option checked, Visual Studio will prompt you to sign in to Microsoft Azure</span></span>

[![](part-1/_static/image8.png)](part-1/_static/image7.png)

<span data-ttu-id="07778-147">登录到 Azure 后，Visual Studio 会提示您配置 web 应用。</span><span class="sxs-lookup"><span data-stu-id="07778-147">After you sign in to Azure, Visual Studio prompts you to configure the web app.</span></span> <span data-ttu-id="07778-148">输入站点的名称，选择你的 Azure 订阅，然后选择地理区域。</span><span class="sxs-lookup"><span data-stu-id="07778-148">Enter a name for the site, select your Azure subscription, and select a geographical region.</span></span> <span data-ttu-id="07778-149">下**数据库服务器**，选择**创建新的服务器**。</span><span class="sxs-lookup"><span data-stu-id="07778-149">Under **Database server**, select **Create new server**.</span></span> <span data-ttu-id="07778-150">输入管理员用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="07778-150">Enter an administrator username and password.</span></span>

[![](part-1/_static/image10.png)](part-1/_static/image9.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="07778-151">下一篇</span><span class="sxs-lookup"><span data-stu-id="07778-151">Next</span></span>](part-2.md)
