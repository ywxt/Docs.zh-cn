---
uid: web-api/overview/security/integrated-windows-authentication
title: 集成 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用集成 Windows 身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/18/2012
ms.topic: article
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: f11b9fe5d98118a252c6c00dd2997b2ee9a3da7a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381598"
---
<a name="integrated-windows-authentication"></a>集成的 Windows 身份验证
====================
通过[Mike Wasson](https://github.com/MikeWasson)

集成的 Windows 身份验证使用户能够使用其 Windows 凭据，使用 Kerberos 或 NTLM 进行登录。 客户端将 Authorization 标头中发送凭据。 Windows 身份验证是最适合 intranet 环境。 有关详细信息，请参阅[Windows 身份验证](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。

| 优点 | 缺点 |
| --- | --- |
| -内置到 IIS。 -不在请求中发送的用户凭据。 -如果客户端计算机属于域 （例如，intranet 应用程序），用户不必输入凭据。 | -不建议用于 Internet 应用程序。 -需要 Kerberos 或 NTLM 支持客户端中。 客户端必须位于 Active Directory 域中。 |

> [!NOTE]
> 如果你的应用程序托管在 Azure 上，并且必须在本地 Active Directory 域，请考虑你的本地 AD 与 Azure Active Directory 联合。 这样一来，用户可以登录其本地凭据，但由 Azure AD 执行身份验证。 有关详细信息，请参阅[Azure 身份验证](../../../visual-studio/overview/2012/windows-azure-authentication.md)。


若要创建使用集成 Windows 身份验证的应用程序，请在 MVC 4 项目向导中选择"Intranet 应用程序"模板。 此项目模板放入 Web.config 文件中的以下设置：

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

集成 Windows 身份验证适用于任何支持的浏览器客户端侧[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)身份验证方案，其中包括大多数主流浏览器。 对于.NET 客户端应用程序， **HttpClient**类支持 Windows 身份验证：

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 身份验证是易受到跨站点请求伪造 (CSRF) 攻击。 请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。
