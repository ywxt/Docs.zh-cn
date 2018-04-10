---
title: ASP.NET Core 安全性概述
author: rachelappel
description: 了解 ASP.NET Core 中的身份验证、授权和安全基础知识。
manager: wpickett
ms.author: rachelap
ms.date: 11/01/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/index
ms.openlocfilehash: da3829b2d5ae5db1861c7423da5afc7acbee6697
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="overview-of-aspnet-core-security"></a>ASP.NET Core 安全性概述

通过 ASP.NET Core，开发者可轻松配置和管理其应用的安全性。 ASP.NET Core 的功能包括管理身份验证、授权、数据保护、SSL 强制、应用机密、请求防伪保护及 CORS 管理。 通过这些安全功能，可以生成安全可靠的 ASP.NET Core 应用。

## <a name="aspnet-core-security-features"></a>ASP.NET Core 安全性功能

ASP.NET Core 提供许多用于保护应用安全的工具和库（包括内置标识提供程序），但也可使用第三方标志服务（如 Facebook、Twitter 或 LinkedIn）。 利用 ASP.NET Core 可以轻松管理应用机密，无需将机密信息暴露在代码中就可存储和使用它们。

## <a name="authentication-vs-authorization"></a>身份验证 vs授权

身份验证是这样一个过程：由用户提供凭据，然后将其与存储在操作系统、数据库、应用或资源中的凭据进行比较。 在授权过程中，如果凭据匹配，则用户身份验证成功，可执行已向其授权的操作。 授权指判断允许用户执行的操作的过程。

对身份验证的另一种理解是将其看作进入某一空间（如服务器、数据库、应用或资源）的方式，而将授权看作用户可对该空间（服务器、数据库或应用）内的对象执行的操作。

## <a name="common-vulnerabilities-in-software"></a>软件中的常见漏洞

ASP.NET Core 和 EF 提供维护应用安全、预防安全漏洞的功能。 下表中链接的文档详细介绍了在 Web 应用中避免最常见安全漏洞的技术：

* [跨站点脚本攻击](xref:security/cross-site-scripting)
* [SQL 注入式攻击](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [跨站点请求伪造 (CSRF)](xref:security/anti-request-forgery)
* [打开重定向攻击](xref:security/preventing-open-redirects)

还应注意其他漏洞。 有关详细信息，请参阅本文档中关于 ASP.NET Core 安全文档的部分。

## <a name="aspnet-security-documentation"></a>ASP.NET Core 安全文档

*   [身份验证](xref:security/authentication/index)
    *   [标识简介](xref:security/authentication/identity)
    *   [启用使用 Facebook、Google 和其他外部提供程序的身份验证](xref:security/authentication/social/index)
    *   [通过 WS 联合身份验证启用身份验证](xref:security/authentication/ws-federation)
    * [配置 Windows 身份验证](xref:security/authentication/windowsauth)
    *   [帐户确认和密码恢复](xref:security/authentication/accconfirm)
    *   [使用 SMS 设置双因素身份验证](xref:security/authentication/2fa)
    *   [在没有标识的情况下使用 cookie 身份验证](xref:security/authentication/cookie)
    *   [Azure Active Directory](xref:security/authentication/azure-active-directory/index)
        *   [将 Azure AD 集成到 ASP.NET Core Web 应用中](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [使用 Azure AD 从 WPF 应用调用 ASP.NET Core Web API](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [使用 Azure AD 在 ASP.NET Core Web 应用中调用 Web API](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [带有 Azure AD B2C 的 ASP.NET Core Web 应用](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [使用 IdentityServer4 保护 ASP.NET Core 应用](https://identityserver4.readthedocs.io)
*   [授权](xref:security/authorization/index)
    *   [介绍](xref:security/authorization/introduction)
    *   [通过授权保护的用户数据创建应用](xref:security/authorization/secure-data)
    *   [简单授权](xref:security/authorization/simple)
    *   [基于角色的授权](xref:security/authorization/roles)
    *   [基于声明的授权](xref:security/authorization/claims)
    *   [基于策略的授权](xref:security/authorization/policies)
    *   [要求处理程序中的依赖关系注入](xref:security/authorization/dependencyinjection)
    *   [基于资源的授权](xref:security/authorization/resourcebased)
    *   [基于视图的授权](xref:security/authorization/views)
    *   [使用方案限制标识](xref:security/authorization/limitingidentitybyscheme)
*   [数据保护](xref:security/data-protection/index)
    *   [数据保护简介](xref:security/data-protection/introduction)
    *   [数据保护 API 入门](xref:security/data-protection/using-data-protection)
    *   [使用者 API](xref:security/data-protection/consumer-apis/index)
        *   [使用者 API 概述](xref:security/data-protection/consumer-apis/overview)
        *   [目标字符串](xref:security/data-protection/consumer-apis/purpose-strings)
        *   [目标层次结构和多租户](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)
        *   [哈希密码](xref:security/data-protection/consumer-apis/password-hashing)
        *   [限制受保护负载的生存期](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)
        *   [取消保护已撤消其密钥的负载](xref:security/data-protection/consumer-apis/dangerous-unprotect)
    *   [配置](xref:security/data-protection/configuration/index)
        *   [配置数据保护](xref:security/data-protection/configuration/overview)
        *   [默认设置](xref:security/data-protection/configuration/default-settings)
        *   [计算机范围的策略](xref:security/data-protection/configuration/machine-wide-policy)
        *   [非 DI 感知方案](xref:security/data-protection/configuration/non-di-scenarios)
    *   [扩展性 API](xref:security/data-protection/extensibility/index)
        *   [核心加密扩展性](xref:security/data-protection/extensibility/core-crypto)
        *   [密钥管理扩展性](xref:security/data-protection/extensibility/key-management)
        *   [其他 API](xref:security/data-protection/extensibility/misc-apis)
    *   [实现](xref:security/data-protection/implementation/index)
        *   [已验证的加密详细信息](xref:security/data-protection/implementation/authenticated-encryption-details)
        *   [子项派生和已验证的加密](xref:security/data-protection/implementation/subkeyderivation)
        *   [上下文标头](xref:security/data-protection/implementation/context-headers)
        *   [密钥管理](xref:security/data-protection/implementation/key-management)
        *   [密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)
        *   [静态密钥加密](xref:security/data-protection/implementation/key-encryption-at-rest)
        *   [密钥永久性和设置](xref:security/data-protection/implementation/key-immutability)
        *   [密钥存储格式](xref:security/data-protection/implementation/key-storage-format)
        *   [短数据保护提供程序](xref:security/data-protection/implementation/key-storage-ephemeral)
    *   [兼容性](xref:security/data-protection/compatibility/index)
        *   [在 ASP.NET 中替换 <machineKey>](xref:security/data-protection/compatibility/replacing-machinekey)
*   [通过授权保护的用户数据创建应用](xref:security/authorization/secure-data)
*   [在开发期间安全存储应用机密](xref:security/app-secrets)
*   [Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)
*   [强制实施 SSL](xref:security/enforcing-ssl)
*   [防请求伪造](xref:security/anti-request-forgery)
*   [阻止打开重定向攻击](xref:security/preventing-open-redirects)
*   [阻止跨站点脚本编写](xref:security/cross-site-scripting)
*   [启用跨域请求 (CORS)](xref:security/cors)
*   [在应用之间共享 Cookie](xref:security/cookie-sharing)
