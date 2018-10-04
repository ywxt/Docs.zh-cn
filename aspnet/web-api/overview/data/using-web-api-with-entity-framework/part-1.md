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
ms.openlocfilehash: d65c0ea35ec766ef9d9093c6502230f9de72a3f3
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795204"
---
<a name="using-web-api-2-with-entity-framework-6"></a>通过 Entity Framework 6 使用 Web API 2
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

> 本教程将讲述使用 ASP.NET Web API 创建 web 应用程序的基础知识后端。 本教程使用 Entity Framework 6 进行的数据层和 Knockout.js 进行客户端的 JavaScript 应用程序。 本教程还演示如何将应用部署到 Azure 应用服务 Web 应用。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
> - Web API 2.1
> - Visual Studio 2013 (下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.5
> - [Knockout.js](http://knockoutjs.com/) 3.1

本教程中使用 Entity Framework 6 与 ASP.NET Web API 2 创建操作后端数据库的 web 应用程序。 下面是您将创建的应用程序的屏幕截图。

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

该应用使用单页面应用程序 (SPA) 设计。 "单页面应用程序"是加载单个 HTML 页面，然后页面动态更新，而不是加载新页面的 web 应用程序的常规术语。 初始页面加载后该应用通过 AJAX 请求与服务器通信。 AJAX 请求返回 JSON 数据时，应用程序用它来更新 UI。

AJAX 并不新鲜，但如今有更加轻松地构建和维护大型复杂的 SPA 应用程序的 JavaScript 框架。 本教程使用[Knockout.js](http://knockoutjs.com/)，但您可以使用任何 JavaScript 客户端框架。

下面是此应用的主要构建基块：

- ASP.NET MVC 创建 HTML 页面。
- ASP.NET Web API 处理 AJAX 请求，并返回 JSON 数据。
- Knockout.js 数据绑定 HTML 元素的 JSON 数据。
- 实体框架与数据库通信。

## <a name="see-this-app-running-on-azure"></a>请参阅在 Azure 上运行此应用程序

若要查看已完成的站点作为实时 web 应用运行吗？ 只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果你还没有帐户，你具有以下选项：

- [免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。
- [激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。

## <a name="create-the-project"></a>创建项目

打开 Visual Studio。 从**文件**菜单中，选择**新建**，然后选择**项目**。 (或单击**新的项目**起始页上。)

在**新的项目**对话框中，单击**Web**左窗格中并**ASP.NET Web 应用程序**在中间窗格中。 项目 BookService 命名，然后单击**确定**。

[![](part-1/_static/image4.png)](part-1/_static/image3.png)

在中**新建 ASP.NET 项目**对话框中，选择**Web API**模板。

[![](part-1/_static/image6.png)](part-1/_static/image5.png)

如果你想要承载 Azure 应用服务中的项目，请将**在云中托管**选中框。

单击“确定”，创建项目。

## <a name="configure-azure-settings-optional"></a>配置 Azure 设置 （可选）

如果你离开**在云中托管**选中选项，Visual Studio 会提示你登录到 Microsoft Azure

[![](part-1/_static/image8.png)](part-1/_static/image7.png)

登录到 Azure 后，Visual Studio 会提示您配置 web 应用。 输入站点的名称，选择你的 Azure 订阅，然后选择地理区域。 下**数据库服务器**，选择**创建新的服务器**。 输入管理员用户名和密码。

[![](part-1/_static/image10.png)](part-1/_static/image9.png)

> [!div class="step-by-step"]
> [下一篇](part-2.md)
