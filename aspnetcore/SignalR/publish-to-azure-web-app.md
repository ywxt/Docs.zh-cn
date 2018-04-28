---
title: 发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用
author: rachelappel
description: 发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 04/20/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/publish-to-azure-web-app
ms.openlocfilehash: fd7d38ad47d9004db2ae7b5858dc22609943f601
ms.sourcegitcommit: 2ab550f8c46e1a8a5d45e58be44d151c676af256
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a><span data-ttu-id="017a6-103">发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="017a6-103">Publish an ASP.NET Core SignalR app to an Azure Web App</span></span>

<span data-ttu-id="017a6-104">[Azure Web 应用程序](/azure/app-service/app-service-web-overview)是[Microsoft 云计算](https://azure.microsoft.com/)用于承载 web 应用，包括 ASP.NET 核心平台服务。</span><span class="sxs-lookup"><span data-stu-id="017a6-104">[Azure Web App](/azure/app-service/app-service-web-overview) is a [Microsoft cloud computing](https://azure.microsoft.com/) platform service for hosting web apps, including ASP.NET Core.</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="017a6-105">发布应用</span><span class="sxs-lookup"><span data-stu-id="017a6-105">Publish the app</span></span>

<span data-ttu-id="017a6-106">Visual Studio 提供的内置工具发布到 Azure Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="017a6-106">Visual Studio provides built-in tools for publishing to an Azure Web App.</span></span> <span data-ttu-id="017a6-107">可以使用 visual Studio Code 用户[Azure CLI](/cli/azure)命令以将应用发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="017a6-107">Visual Studio Code user can use [Azure CLI](/cli/azure) commands to publish apps to Azure.</span></span> <span data-ttu-id="017a6-108">本文介绍如何发布使用 Visual Studio 中的工具。</span><span class="sxs-lookup"><span data-stu-id="017a6-108">This article covers publishing using the tools in Visual Studio.</span></span> <span data-ttu-id="017a6-109">若要发布应用程序使用 Azure CLI，请参阅[将 ASP.NET Core 应用发布到 Azure 中，使用命令行工具](xref:tutorials/publish-to-azure-webapp-using-cli)。</span><span class="sxs-lookup"><span data-stu-id="017a6-109">To publish an app using Azure CLI, see [Publish an ASP.NET Core app to Azure with command line tools](xref:tutorials/publish-to-azure-webapp-using-cli).</span></span>

<span data-ttu-id="017a6-110">右键单击该项目中**解决方案资源管理器**和选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="017a6-110">Right-click on the project in **Solution Explorer** and select **Publish**.</span></span> <span data-ttu-id="017a6-111">确认**新建**签入**选取发布目标**对话框中，然后选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="017a6-111">Confirm that **Create new** is checked in the **Pick a publish target** dialog, and select **Publish**.</span></span>

![选取发布目标](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

<span data-ttu-id="017a6-113">输入中的以下信息**创建 App Service**对话框，然后选择**创建**。</span><span class="sxs-lookup"><span data-stu-id="017a6-113">Enter the following information in the **Create App Service** dialog and select **Create**.</span></span>

| <span data-ttu-id="017a6-114">项</span><span class="sxs-lookup"><span data-stu-id="017a6-114">Item</span></span> | <span data-ttu-id="017a6-115">描述</span><span class="sxs-lookup"><span data-stu-id="017a6-115">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="017a6-116">**应用程序名称**</span><span class="sxs-lookup"><span data-stu-id="017a6-116">**App name**</span></span> | <span data-ttu-id="017a6-117">应用的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="017a6-117">A unique name of the app.</span></span> |
| <span data-ttu-id="017a6-118">**订阅**</span><span class="sxs-lookup"><span data-stu-id="017a6-118">**Subscription**</span></span> | <span data-ttu-id="017a6-119">该应用使用 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="017a6-119">The Azure subscription that the app uses.</span></span> |
| <span data-ttu-id="017a6-120">**资源组**</span><span class="sxs-lookup"><span data-stu-id="017a6-120">**Resource Group**</span></span> | <span data-ttu-id="017a6-121">为应用程序所属的相关资源的组。</span><span class="sxs-lookup"><span data-stu-id="017a6-121">The group of related resources to which the app belongs.</span></span>  |
| <span data-ttu-id="017a6-122">**托管计划**</span><span class="sxs-lookup"><span data-stu-id="017a6-122">**Hosting Plan**</span></span> | <span data-ttu-id="017a6-123">用于 web 应用的定价计划。</span><span class="sxs-lookup"><span data-stu-id="017a6-123">The pricing plan for the web app.</span></span> |

![创建应用程序服务](publish-to-azure-web-app/_static/create-app-service-dialog.png)

<span data-ttu-id="017a6-125">Visual Studio 完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="017a6-125">Visual Studio completes the following tasks:</span></span>

* <span data-ttu-id="017a6-126">创建发布配置文件包含发布设置。</span><span class="sxs-lookup"><span data-stu-id="017a6-126">Creates a Publish Profile containing publish settings.</span></span>
* <span data-ttu-id="017a6-127">创建或使用现有*Azure Web 应用*具有提供的详细信息。</span><span class="sxs-lookup"><span data-stu-id="017a6-127">Creates or uses an existing *Azure Web App* with the provided details.</span></span>
* <span data-ttu-id="017a6-128">发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="017a6-128">Publishes the app.</span></span>
* <span data-ttu-id="017a6-129">将浏览器中，启动发布的 web 应用程序加载。</span><span class="sxs-lookup"><span data-stu-id="017a6-129">Launches a browser, with the published web app loaded.</span></span>

<span data-ttu-id="017a6-130">请注意 URL 的格式，应用程序 *{应用名称}.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="017a6-130">Notice the format of the URL for the app is *{app name}.azurewebsites.net*.</span></span> <span data-ttu-id="017a6-131">例如，名为的应用`SignalRChattR`具有一个如下所示的 URL `https://signalrchattr.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="017a6-131">For example, an app named `SignalRChattR` has a URL that looks like `https://signalrchattr.azurewebsites.net`.</span></span>

<span data-ttu-id="017a6-132">如果发生 HTTP 502.2 错误，请参阅[到 Azure App Service 部署 ASP.NET Core 预览版](xref:host-and-deploy/azure-apps/index)来解决。</span><span class="sxs-lookup"><span data-stu-id="017a6-132">If an HTTP 502.2 error occurs, see [Deploy ASP.NET Core preview release to Azure App Service](xref:host-and-deploy/azure-apps/index) to resolve it.</span></span>

## <a name="configure-signalr-web-app"></a><span data-ttu-id="017a6-133">SignalR web 应用程序配置</span><span class="sxs-lookup"><span data-stu-id="017a6-133">Configure SignalR web app</span></span>

<span data-ttu-id="017a6-134">ASP.NET 核心 SignalR 应用程序作为 Azure Web 应用必须发布[ARR 地缘](https://en.wikipedia.org/wiki/Application_Request_Routing)启用。</span><span class="sxs-lookup"><span data-stu-id="017a6-134">ASP.NET Core SignalR apps that are published as an Azure Web App must have [ARR Affinity](https://en.wikipedia.org/wiki/Application_Request_Routing) enabled.</span></span> <span data-ttu-id="017a6-135">[Websocket](xref:fundamentals/websockets)应支持，以允许 Websocket 传输到该函数。</span><span class="sxs-lookup"><span data-stu-id="017a6-135">[WebSockets](xref:fundamentals/websockets) should be enabled, to allow the WebSockets transport to function.</span></span>

<span data-ttu-id="017a6-136">在 Azure 门户中，导航到**应用设置**web 应用。</span><span class="sxs-lookup"><span data-stu-id="017a6-136">In the Azure portal, navigate to **App Settings** for your web app.</span></span> <span data-ttu-id="017a6-137">设置**Websocket**到**上**，并验证**ARR 地缘**是**上**。</span><span class="sxs-lookup"><span data-stu-id="017a6-137">Set **WebSockets** to **On**, and verify **ARR Affinity** is **On**.</span></span>

![在 Azure 门户中的 azure Web 应用设置](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 <span data-ttu-id="017a6-139">Websocket 传输和其他传输[受到基于 App Service 计划](/azure/azure-subscription-service-limits#app-service-limits)。</span><span class="sxs-lookup"><span data-stu-id="017a6-139">WebSockets and other transports [are limited based on the App Service Plan](/azure/azure-subscription-service-limits#app-service-limits).</span></span>

## <a name="related-resources"></a><span data-ttu-id="017a6-140">相关资源</span><span class="sxs-lookup"><span data-stu-id="017a6-140">Related resources</span></span>

* [<span data-ttu-id="017a6-141">使用命令行工具将 ASP.NET Core 应用发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="017a6-141">Publish an ASP.NET Core app to Azure with command line tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli?tabs=windows)
* [<span data-ttu-id="017a6-142">向具有 Visual Studio 的 Azure 发布 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="017a6-142">Publish an ASP.NET Core app to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)
* [<span data-ttu-id="017a6-143">承载并将其部署在 Azure 上的 ASP.NET 核心预览应用</span><span class="sxs-lookup"><span data-stu-id="017a6-143">Host and deploy ASP.NET Core Preview apps on Azure</span></span>](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
