---
title: 发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用
author: rachelappel
description: 发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 04/20/2018
uid: signalr/publish-to-azure-web-app
ms.openlocfilehash: 0d98c6b24b9695c0af0170173f13902bac5f55ed
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36271913"
---
# <a name="publish-an-aspnet-core-signalr-app-to-an-azure-web-app"></a>发布 ASP.NET Core SignalR 应用程序到 Azure Web 应用程序

[Azure Web 应用程序](/azure/app-service/app-service-web-overview)是[Microsoft 云计算](https://azure.microsoft.com/)用于承载 web 应用，包括 ASP.NET Core 平台服务。

> [!NOTE]
> 本文是指从 Visual Studio 发布 ASP.NET Core SignalR 应用程序。 请访问[Azure 的 SignalR 服务](https://azure.microsoft.com/en-gb/services/signalr-service?)有关在 Azure 上使用 SignalR 的详细信息。

## <a name="publish-the-app"></a>发布应用

Visual Studio 提供的内置工具发布到 Azure Web 应用程序。 可以使用 visual Studio Code 用户[Azure CLI](/cli/azure)命令以将应用发布到 Azure。 本文介绍如何发布使用 Visual Studio 中的工具。 若要发布应用程序使用 Azure CLI，请参阅[将 ASP.NET Core 应用发布到 Azure 中，使用命令行工具](xref:tutorials/publish-to-azure-webapp-using-cli)。

右键单击该项目中**解决方案资源管理器**和选择**发布**。 确认**新建**签入**选取发布目标**对话框中，然后选择**发布**。

![选取发布目标](publish-to-azure-web-app/_static/pick-publish-target-dialog.png)

输入中的以下信息**创建 App Service**对话框，然后选择**创建**。

| 项 | 描述 |
| ---- | ----------- |
| **应用程序名称** | 应用的唯一名称。 |
| **订阅** | 该应用使用 Azure 订阅。 |
| **资源组** | 为应用程序所属的相关资源的组。  |
| **托管计划** | 用于 web 应用的定价计划。 |

![创建应用程序服务](publish-to-azure-web-app/_static/create-app-service-dialog.png)

Visual Studio 完成以下任务：

* 创建发布配置文件包含发布设置。
* 创建或使用现有*Azure Web 应用*具有提供的详细信息。
* 发布应用程序。
* 将浏览器中，启动发布的 web 应用程序加载。

请注意 URL 的格式，应用程序 *{应用名称}.azurewebsites.net*。 例如，名为的应用`SignalRChattR`具有一个如下所示的 URL `https://signalrchattr.azurewebsites.net`。

如果发生 HTTP 502.2 错误，请参阅[到 Azure App Service 部署 ASP.NET Core 预览版](xref:host-and-deploy/azure-apps/index)来解决。

## <a name="configure-signalr-web-app"></a>SignalR web 应用程序配置

ASP.NET Core SignalR 应用程序作为 Azure Web 应用必须发布[ARR 地缘](https://en.wikipedia.org/wiki/Application_Request_Routing)启用。 [Websocket](xref:fundamentals/websockets)应支持，以允许 Websocket 传输到该函数。

在 Azure 门户中，导航到**应用设置**web 应用。 设置**Websocket**到**上**，并验证**ARR 地缘**是**上**。

![在 Azure 门户中的 azure Web 应用设置](publish-to-azure-web-app/_static/azure-web-app-settings.png)

 Websocket 传输和其他传输[受到基于 App Service 计划](/azure/azure-subscription-service-limits#app-service-limits)。

## <a name="related-resources"></a>相关资源

* [使用命令行工具将 ASP.NET Core 应用发布到 Azure](xref:tutorials/publish-to-azure-webapp-using-cli?tabs=windows)
* [向具有 Visual Studio 的 Azure 发布 ASP.NET Core 应用](xref:tutorials/publish-to-azure-webapp-using-vs)
* [承载并将其部署在 Azure 上的 ASP.NET Core 预览应用](xref:host-and-deploy/azure-apps/index#deploy-aspnet-core-preview-release-to-azure-app-service)
