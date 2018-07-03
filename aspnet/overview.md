---
uid: overview
title: ASP.NET 概述 |Microsoft Docs
author: rick-anderson
description: ASP.NET 中，免费的框架，用于创建网站、 web 应用程序和 web Api 的简介。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2010
ms.topic: article
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.technology: ''
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: de094258984e3ca09e4eadf21169cad9bfc67b22
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362257"
---
# <a name="aspnet-overview"></a>ASP.NET 概述

ASP.NET 是一个用于构建出色的网站和 web 应用程序使用 HTML、 CSS 和 JavaScript 的免费 web 框架。 您还可以创建 Web Api 和使用 Web 套接字等实时技术。

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)是 ASP.NET 的替代方法。  请参阅[有关如何以 ASP.NET 和 ASP.NET Core 之间进行选择指南](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)。

## <a name="get-started"></a>入门

[Visual Studio Community 2017](https://www.visualstudio.com/downloads/)、 免费 IDE，用于在 Windows 上的 ASP.NET。

## <a name="websites-and-web-applications"></a>网站和 web 应用程序

 ASP.NET 提供了三个框架用于创建 web 应用程序： Web 窗体、 ASP.NET MVC 和 ASP.NET Web Pages。 所有三个框架稳定且成熟，并且其中任何一个都可以创建功能强大的 web 应用程序。 无论选择何种框架，则会获得所有好处和无处不在 ASP.NET 的功能。

每个框架都针对不同的开发风格。 您选择何种取决于编程资产 （知识、 技能和开发体验） 的组合，你要创建应用程序和熟悉的开发方法的类型。

下面是每个框架和有关如何选择它们之间的一些观点的概述。 如果您喜欢的视频介绍，请参阅[使用 ASP.NET 进行网站](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)和[Web 工具是什么？](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | 如果有经验 | 开发风格 | 专业知识 | 
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms — Web 窗体 | 赢取窗体、 WPF、.NET | 使用丰富的封装的 HTML 标记的控件库的快速开发 | 中级、 高级 RAD |
| MVC       | Ruby on Rails、.NET  | 完全控制 HTML 标记、 代码和标记分隔，且易于编写测试的详细内容。 移动和单页面应用程序 (SPA) 最佳选择。 | 中等级别高级 |
| 网页  | 经典 ASP PHP     | HTML 标记和代码组合在一起位于同一文件中 | 新的、 中等级别 |

### <a name="web-forms"></a>Web Forms — Web 窗体

使用 ASP.NET Web 窗体，您可以构建动态网站，使用熟悉的拖放、 事件驱动模型。 设计图面和数百个控件和组件可以快速生成复杂且功能强大的 UI 驱动站点具有数据访问权限。 

[了解有关 Web 窗体的详细信息](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC，您可以生成动态网站，使完全分离关注点，让你完全控制标记进行愉快、 灵活的开发功能强大、 基于模式的方法。 ASP.NET MVC 包括许多功能，启用快速、 TDD 友好开发，以便创建使用最新的 web 标准的复杂应用程序。 

[了解有关 MVC 的详细信息](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET 网页

ASP.NET Web Pages 和 Razor 语法提供快速且易上手的轻型方法组合服务器代码与 HTML 以创建动态 web 内容。 连接到数据库，添加视频、 链接到社交网络网站，并包括许多详细的功能，可帮助您创建符合最新的 web 标准的精美网站。

[了解有关 Web 页面的详细信息](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>有关 Web 窗体、 MVC 和 Web Pages 的说明

所有这三种 ASP.NET 框架基于.NET Framework 和共享的.NET 和 ASP.NET 的核心功能。 例如，所有这三种框架提供基于成员身份，登录安全模型和所有这三个共享是核心 ASP.NET 功能的一部分用于管理请求、 处理会话等的相同功能。

此外，这三种框架不是完全独立的并选择一个不会阻止使用另一个。 由于框架可以共存于同一 web 应用程序，不奇怪编写使用不同的框架的应用程序的各个组件。 例如，可能会在 MVC 来优化标记中，而在 Web 窗体以充分利用数据控件和简单的数据访问中开发的数据访问和管理部分中开发的应用面向客户的部分。

## <a name="web-apis"></a>Web API

ASP.NET Web API 是一种框架，可以轻松地构建 HTTP 服务访问范围广泛的客户端，包括浏览器和移动设备。 ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。

[了解有关 Web API 的详细信息](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>实时技术

ASP.NET SignalR 是 ASP.NET 开发人员的新库，简化了开发实时 web 功能。 SignalR 允许服务器和客户端之间的双向通信。 服务器可以将内容推送到连接的客户端立即可用。 SignalR 支持 Web 套接字和将回退到旧版浏览器的其他兼容方法。 SignalR 包括用于连接管理的 Api （例如，连接和断开连接事件），分组连接和授权。

[了解有关 SignalR 的详细信息](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>移动应用和网站 

能够为 ASP.NET Web API 后端，以及使用响应式设计框架，例如 Twitter Bootstrap 的移动网站使用的本机移动应用。 如果您正在构建本机移动应用，很容易创建基于 JSON 的 Web API 与句柄数据访问、 身份验证，以及为你的应用的推送通知。 如果要构建响应迅速的移动站点，您可以使用任何 CSS 框架或打开网格系统更喜欢，也可以选择 jQuery Mobile 或 Sencha 和优秀使用 PhoneGap 的移动应用程序等功能强大的移动系统。

[了解有关移动应用和网站开发的详细信息](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>单页面应用程序 

ASP.NET 单页面应用程序 (SPA) 帮助您生成包含大量使用 HTML、 CSS 3 和 JavaScript 的客户端进行交互的应用程序。 Visual Studio 包含用于生成单页面应用程序使用 knockout.js 和 ASP.NET Web API 模板。 除了内置的 SPA 模板，社区创建 SPA 模板也已可供下载。

[了解有关单页面应用程序开发的详细信息](single-page-application/index.md)

## <a name="webhooks"></a>WebHook

Webhook 是轻量级 HTTP 模式一起编写 Web Api 和 SaaS 服务提供简单的发布/订阅模型。 在服务中发生的事件时, 通知中的 HTTP POST 请求的形式发送到已注册的订阅。 POST 请求包含有关事件使得接收方可以采取相应行动的信息。

Webhook 由大量包括 Dropbox、 GitHub、 Instagram、 MailChimp、 PayPal、 Slack、 Trello 和更多的服务公开。 例如，WebHook 可以指示文件已更改在 Dropbox 中，或已在 GitHub 中，提交代码更改或付款已启动 PayPal、 中或已在 Trello 中创建卡片。

[了解有关 Webhook 的详细信息](webhooks/index.md)





<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
