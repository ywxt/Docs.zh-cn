---
uid: web-api/overview/security/forms-authentication
title: 在 ASP.NET Web API 中窗体身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用窗体身份验证。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 35d62a83382553085ed8a728dcdcdae0e93090b8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832520"
---
<a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API 中的窗体身份验证
====================
通过[Mike Wasson](https://github.com/MikeWasson)

窗体身份验证使用 HTML 窗体向服务器发送用户的凭据。 它不是一种 Internet 标准。 窗体身份验证是仅适用于 web 的 web 应用，从调用的 Api，以便用户可以与 HTML 窗体进行交互。

| 优点 | 缺点 |
| --- | --- |
| -可轻松实现： 内置到 ASP.NET。 -使用 ASP.NET 成员资格提供程序，可以轻松管理用户帐户。 | -未一个标准的 HTTP 身份验证机制;使用 HTTP cookie 而不是标准授权标头。 -需要浏览器客户端。 的以纯文本形式发送凭据。 -易受到跨站点请求伪造 (CSRF);需要反 CSRF 的度量值。 -难以 nonbrowser 客户端配合使用。 登录要求浏览器。 的在请求中发送用户凭据。 -某些用户禁用 cookie。 |

简单地说，在 ASP.NET 中的窗体身份验证的工作方式如下：

1. 客户端请求需要身份验证的资源。
2. 如果用户未经过身份验证，服务器将返回 HTTP 302 （已找到），并将重定向到登录页。
3. 用户输入凭据，并提交窗体。
4. 服务器将返回另一个 HTTP 302 重定向回原始的 URI。 此响应包括身份验证 cookie。
5. 客户端再次请求该资源。 请求包含身份验证 cookie，因此服务器授予请求。

![](forms-authentication/_static/image1.png)

有关详细信息，请参阅[概述的窗体身份验证。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>将窗体身份验证用于 Web API

若要创建使用窗体身份验证的应用程序，请在 MVC 4 项目向导中选择"Internet 应用程序"模板。 此模板创建 MVC 控制器用于帐户管理。 此外可以使用"单页面应用程序"模板，在 ASP.NET Fall 2012 Update 中可用。

在你的 web API 控制器，你可以通过使用限制访问`[Authorize]`属性，如中所述[使用 [Authorize] 特性](authentication-and-authorization-in-aspnet-web-api.md#auth3)。

窗体身份验证使用会话 cookie 进行身份验证请求。 浏览器自动向目标网站发送所有相关 cookie。 此功能使窗体身份验证可能易受到跨站点请求伪造 (CSRF) 攻击，请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。

窗体身份验证不会加密用户的凭据。 因此，不使用 SSL 安全窗体身份验证。 请参阅[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。
