---
title: "ASP.NET Core 安全性概述 | Microsoft Docs"
author: rachelappel
description: "了解 ASP.NET Core 中的身份验证、授权和安全基础知识"
ms.author: rachelap
manager: wpickett
ms.date: 11/01/2017
ms.topic: article
ms.assetid: a8fb7eb7-e0e5-4394-84f3-1f1dbe012345
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/index
ms.openlocfilehash: 3f4df08d6cf5d183735ae4b4ec4f07ed60a9623a
ms.sourcegitcommit: f1436107b4c022b26f5235dddef103cec5aa6bff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2017
---
# <a name="aspnet-core-security-overview"></a><span data-ttu-id="23010-103">ASP.NET Core 安全性概述</span><span class="sxs-lookup"><span data-stu-id="23010-103">ASP.NET Core Security Overview</span></span>

<span data-ttu-id="23010-104">通过 ASP.NET Core，开发者可轻松配置和管理其应用的安全性。</span><span class="sxs-lookup"><span data-stu-id="23010-104">ASP.NET Core enables developers to easily configure and manage security for their apps.</span></span> <span data-ttu-id="23010-105">ASP.NET Core 的功能包括管理身份验证、授权、数据保护、SSL 强制、应用机密、请求防伪保护及 CORS 管理。</span><span class="sxs-lookup"><span data-stu-id="23010-105">ASP.NET Core contains features for managing authentication, authorization, data protection, SSL enforcement, app secrets, anti-request forgery protection, and CORS management.</span></span> <span data-ttu-id="23010-106">通过这些安全功能，可以生成安全可靠的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="23010-106">These security features allow you to build robust yet secure ASP.NET Core apps.</span></span> 

## <a name="aspnet-core-security-features"></a><span data-ttu-id="23010-107">ASP.NET Core 安全性功能</span><span class="sxs-lookup"><span data-stu-id="23010-107">ASP.NET Core security features</span></span>

<span data-ttu-id="23010-108">ASP.NET Core 提供许多用于保护应用安全的工具和库（包括内置标识提供程序），但也可使用第三方标志服务（如 Facebook、Twitter 或 LinkedIn）。</span><span class="sxs-lookup"><span data-stu-id="23010-108">ASP.NET Core provides many tools and libraries to secure your apps including built-in Identity providers but you can use 3rd party identity services such as Facebook, Twitter, or LinkedIn.</span></span> <span data-ttu-id="23010-109">利用 ASP.NET Core 可以轻松管理应用机密，无需将机密信息暴露在代码中就可存储和使用它们。</span><span class="sxs-lookup"><span data-stu-id="23010-109">With ASP.NET Core, you can easily manage app secrets, which are a way to store and use confidential information without having to expose it in the code.</span></span> 

## <a name="authentication-vs-authorization"></a><span data-ttu-id="23010-110">身份验证 vs授权</span><span class="sxs-lookup"><span data-stu-id="23010-110">Authentication vs. Authorization</span></span>

<span data-ttu-id="23010-111">身份验证是这样一个过程：由用户提供凭据，然后将其与存储在操作系统、数据库、应用或资源中的凭据进行比较。</span><span class="sxs-lookup"><span data-stu-id="23010-111">Authentication is a process in which a user provides credentials that are then compared to those stored in an operating system, database, app or resource.</span></span> <span data-ttu-id="23010-112">在授权过程中，如果凭据匹配，则用户身份验证成功，可执行已向其授权的操作。</span><span class="sxs-lookup"><span data-stu-id="23010-112">If they match, users authenticate successfully, and can then perform actions that they are authorized for, during an authorization process.</span></span> <span data-ttu-id="23010-113">授权指判断允许用户执行的操作的过程。</span><span class="sxs-lookup"><span data-stu-id="23010-113">The authorization refers to the process that determines what a user is allowed to do.</span></span> 

<span data-ttu-id="23010-114">对身份验证的另一种理解是将其看作进入某一空间（如服务器、数据库、应用或资源）的方式，而将授权看作用户可对该空间（服务器、数据库或应用）内的对象执行的操作。</span><span class="sxs-lookup"><span data-stu-id="23010-114">Another way to think of authentication is to consider it as a way to enter a space, such as a server, database, app or resource, while authorization is which actions the user can perform to which objects inside that space (server, database, or app).</span></span>

## <a name="common-vulnerabilities-in-software"></a><span data-ttu-id="23010-115">软件中的常见漏洞</span><span class="sxs-lookup"><span data-stu-id="23010-115">Common Vulnerabilities in software</span></span>

<span data-ttu-id="23010-116">ASP.NET Core 和 EF 提供维护应用安全、预防安全漏洞的功能。</span><span class="sxs-lookup"><span data-stu-id="23010-116">ASP.NET Core and EF contain features that help you secure your apps and prevent security breaches.</span></span> <span data-ttu-id="23010-117">下表中链接的文档详细介绍了在 Web 应用中避免最常见安全漏洞的技术：</span><span class="sxs-lookup"><span data-stu-id="23010-117">The following list of links takes you to documentation detailing techniques to avoid the most common security vulnerabilities in web apps:</span></span>

* [<span data-ttu-id="23010-118">跨站点脚本攻击</span><span class="sxs-lookup"><span data-stu-id="23010-118">Cross site scripting attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/cross-site-scripting)
* [<span data-ttu-id="23010-119">SQL 注入式攻击</span><span class="sxs-lookup"><span data-stu-id="23010-119">SQL Injection attacks</span></span>](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [<span data-ttu-id="23010-120">跨站点请求伪造 (CSRF)</span><span class="sxs-lookup"><span data-stu-id="23010-120">Cross-Site Request Forgery (CSRF)</span></span>](https://docs.microsoft.com/aspnet/core/security/anti-request-forgery)
* [<span data-ttu-id="23010-121">打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="23010-121">Open redirect attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/preventing-open-redirects)

<span data-ttu-id="23010-122">还应注意其他漏洞。</span><span class="sxs-lookup"><span data-stu-id="23010-122">There are more vulnerabilities that you should be aware of.</span></span> <span data-ttu-id="23010-123">有关详细信息，请参阅本文档中关于 ASP.NET Core 安全文档的部分。</span><span class="sxs-lookup"><span data-stu-id="23010-123">For more information, see the section in this document on *ASP.NET Security Documentation*.</span></span> 

## <a name="aspnet-security-documentation"></a><span data-ttu-id="23010-124">ASP.NET Core 安全文档</span><span class="sxs-lookup"><span data-stu-id="23010-124">ASP.NET Security Documentation</span></span>

*   [<span data-ttu-id="23010-125">身份验证</span><span class="sxs-lookup"><span data-stu-id="23010-125">Authentication</span></span>](authentication/index.md)
    *   [<span data-ttu-id="23010-126">标识简介</span><span class="sxs-lookup"><span data-stu-id="23010-126">Introduction to Identity</span></span>](authentication/identity.md)
    *   [<span data-ttu-id="23010-127">启用使用 Facebook、Google 和其他外部提供程序的身份验证</span><span class="sxs-lookup"><span data-stu-id="23010-127">Enabling authentication using Facebook, Google and other external providers</span></span>](authentication/social/index.md)
    * [<span data-ttu-id="23010-128">配置 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="23010-128">Configure Windows Authentication</span></span>](authentication/windowsauth.md)
    *   [<span data-ttu-id="23010-129">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="23010-129">Account Confirmation and Password Recovery</span></span>](authentication/accconfirm.md)
    *   [<span data-ttu-id="23010-130">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="23010-130">Two-factor authentication with SMS</span></span>](authentication/2fa.md) 
    *   [<span data-ttu-id="23010-131">在没有 ASP.NET Core 标识的情况下使用 Cookie 身份验证</span><span class="sxs-lookup"><span data-stu-id="23010-131">Using Cookie Authentication without ASP.NET Core Identity</span></span>](authentication/cookie.md)
    *   [<span data-ttu-id="23010-132">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23010-132">Azure Active Directory</span></span>](authentication/azure-active-directory/index.md)
        *   <span data-ttu-id="23010-133">[Integrating Azure AD Into an ASP.NET Core Web App](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)（将 Azure AD 集成到 ASP.NET Core Web 应用中）</span><span class="sxs-lookup"><span data-stu-id="23010-133">[Integrating Azure AD Into an ASP.NET Core Web App](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)</span></span>
        *   <span data-ttu-id="23010-134">[Calling a ASP.NET Core Web API From a WPF Application Using Azure AD](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)（从使用 Azure AD 的 WPF 应用程序调用 ASP.NET Core Web API）</span><span class="sxs-lookup"><span data-stu-id="23010-134">[Calling a ASP.NET Core Web API From a WPF Application Using Azure AD](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)</span></span>
        *   <span data-ttu-id="23010-135">[Calling a Web API in an ASP.NET Core Web Application Using Azure AD](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)（在使用 Azure AD 的 ASP.NET Core Web 应用程序中调用 Web API）</span><span class="sxs-lookup"><span data-stu-id="23010-135">[Calling a Web API in an ASP.NET Core Web Application Using Azure AD](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)</span></span>
        *   [<span data-ttu-id="23010-136">带有 Azure AD B2C 的 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="23010-136">An ASP.NET Core web app with Azure AD B2C</span></span>](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [<span data-ttu-id="23010-137">使用 IdentityServer4 保护 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="23010-137">Securing ASP.NET Core apps with IdentityServer4</span></span>](https://identityserver4.readthedocs.io)
*   [<span data-ttu-id="23010-138">授权</span><span class="sxs-lookup"><span data-stu-id="23010-138">Authorization</span></span>](authorization/index.md)
    *   [<span data-ttu-id="23010-139">介绍</span><span class="sxs-lookup"><span data-stu-id="23010-139">Introduction</span></span>](authorization/introduction.md)
    *   [<span data-ttu-id="23010-140">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="23010-140">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
    *   [<span data-ttu-id="23010-141">简单授权</span><span class="sxs-lookup"><span data-stu-id="23010-141">Simple Authorization</span></span>](authorization/simple.md)
    *   [<span data-ttu-id="23010-142">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="23010-142">Role based Authorization</span></span>](authorization/roles.md)
    *   [<span data-ttu-id="23010-143">基于声明的授权</span><span class="sxs-lookup"><span data-stu-id="23010-143">Claims-Based Authorization</span></span>](authorization/claims.md)
    *   [<span data-ttu-id="23010-144">基于自定义策略的授权</span><span class="sxs-lookup"><span data-stu-id="23010-144">Custom policy-based authorization</span></span>](authorization/policies.md)
    *   [<span data-ttu-id="23010-145">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="23010-145">Dependency Injection in requirement handlers</span></span>](authorization/dependencyinjection.md)
    *   [<span data-ttu-id="23010-146">基于资源的授权</span><span class="sxs-lookup"><span data-stu-id="23010-146">Resource-based authorization</span></span>](authorization/resourcebased.md)
    *   [<span data-ttu-id="23010-147">基于视图的授权</span><span class="sxs-lookup"><span data-stu-id="23010-147">View-based authorization</span></span>](authorization/views.md)
    *   [<span data-ttu-id="23010-148">使用方案限制标识</span><span class="sxs-lookup"><span data-stu-id="23010-148">Limiting identity by scheme</span></span>](authorization/limitingidentitybyscheme.md)
*   [<span data-ttu-id="23010-149">数据保护</span><span class="sxs-lookup"><span data-stu-id="23010-149">Data Protection</span></span>](data-protection/index.md)
    *   [<span data-ttu-id="23010-150">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="23010-150">Introduction to Data Protection</span></span>](data-protection/introduction.md)
    *   [<span data-ttu-id="23010-151">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="23010-151">Getting Started with the Data Protection APIs</span></span>](data-protection/using-data-protection.md)
    *   [<span data-ttu-id="23010-152">使用者 API</span><span class="sxs-lookup"><span data-stu-id="23010-152">Consumer APIs</span></span>](data-protection/consumer-apis/index.md)
        *   [<span data-ttu-id="23010-153">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="23010-153">Consumer APIs Overview</span></span>](data-protection/consumer-apis/overview.md)
        *   [<span data-ttu-id="23010-154">目标字符串</span><span class="sxs-lookup"><span data-stu-id="23010-154">Purpose Strings</span></span>](data-protection/consumer-apis/purpose-strings.md)
        *   [<span data-ttu-id="23010-155">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="23010-155">Purpose hierarchy and multi-tenancy</span></span>](data-protection/consumer-apis/purpose-strings-multitenancy.md)
        *   [<span data-ttu-id="23010-156">密码哈希</span><span class="sxs-lookup"><span data-stu-id="23010-156">Password Hashing</span></span>](data-protection/consumer-apis/password-hashing.md)
        *   [<span data-ttu-id="23010-157">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="23010-157">Limiting the lifetime of protected payloads</span></span>](data-protection/consumer-apis/limited-lifetime-payloads.md)
        *   [<span data-ttu-id="23010-158">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="23010-158">Unprotecting payloads whose keys have been revoked</span></span>](data-protection/consumer-apis/dangerous-unprotect.md)
    *   [<span data-ttu-id="23010-159">配置</span><span class="sxs-lookup"><span data-stu-id="23010-159">Configuration</span></span>](data-protection/configuration/index.md)
        *   [<span data-ttu-id="23010-160">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="23010-160">Configuring Data Protection</span></span>](data-protection/configuration/overview.md)
        *   [<span data-ttu-id="23010-161">默认设置</span><span class="sxs-lookup"><span data-stu-id="23010-161">Default Settings</span></span>](data-protection/configuration/default-settings.md)
        *   [<span data-ttu-id="23010-162">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="23010-162">Machine Wide Policy</span></span>](data-protection/configuration/machine-wide-policy.md)
        *   [<span data-ttu-id="23010-163">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="23010-163">Non DI Aware Scenarios</span></span>](data-protection/configuration/non-di-scenarios.md)
    *   [<span data-ttu-id="23010-164">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="23010-164">Extensibility APIs</span></span>](data-protection/extensibility/index.md)
        *   [<span data-ttu-id="23010-165">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="23010-165">Core cryptography extensibility</span></span>](data-protection/extensibility/core-crypto.md)
        *   [<span data-ttu-id="23010-166">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="23010-166">Key management extensibility</span></span>](data-protection/extensibility/key-management.md)
        *   [<span data-ttu-id="23010-167">其他 API</span><span class="sxs-lookup"><span data-stu-id="23010-167">Miscellaneous APIs</span></span>](data-protection/extensibility/misc-apis.md)
    *   [<span data-ttu-id="23010-168">实现</span><span class="sxs-lookup"><span data-stu-id="23010-168">Implementation</span></span>](data-protection/implementation/index.md)
        *   [<span data-ttu-id="23010-169">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="23010-169">Authenticated encryption details</span></span>](data-protection/implementation/authenticated-encryption-details.md)
        *   [<span data-ttu-id="23010-170">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="23010-170">Subkey Derivation and Authenticated Encryption</span></span>](data-protection/implementation/subkeyderivation.md)
        *   [<span data-ttu-id="23010-171">上下文标头</span><span class="sxs-lookup"><span data-stu-id="23010-171">Context headers</span></span>](data-protection/implementation/context-headers.md)
        *   [<span data-ttu-id="23010-172">密钥管理</span><span class="sxs-lookup"><span data-stu-id="23010-172">Key Management</span></span>](data-protection/implementation/key-management.md)
        *   [<span data-ttu-id="23010-173">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="23010-173">Key Storage Providers</span></span>](data-protection/implementation/key-storage-providers.md)
        *   [<span data-ttu-id="23010-174">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="23010-174">Key Encryption At Rest</span></span>](data-protection/implementation/key-encryption-at-rest.md)
        *   [<span data-ttu-id="23010-175">密钥永久性和更改设置</span><span class="sxs-lookup"><span data-stu-id="23010-175">Key Immutability and Changing Settings</span></span>](data-protection/implementation/key-immutability.md)
        *   [<span data-ttu-id="23010-176">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="23010-176">Key Storage Format</span></span>](data-protection/implementation/key-storage-format.md)
        *   [<span data-ttu-id="23010-177">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="23010-177">Ephemeral data protection providers</span></span>](data-protection/implementation/key-storage-ephemeral.md)
    *   [<span data-ttu-id="23010-178">兼容性</span><span class="sxs-lookup"><span data-stu-id="23010-178">Compatibility</span></span>](data-protection/compatibility/index.md)
        *   [<span data-ttu-id="23010-179">在应用程序之间共享 cookie</span><span class="sxs-lookup"><span data-stu-id="23010-179">Sharing cookies between applications</span></span>](data-protection/compatibility/cookie-sharing.md)
        *   [<span data-ttu-id="23010-180">在 ASP.NET 中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="23010-180">Replacing <machineKey> in ASP.NET</span></span>](data-protection/compatibility/replacing-machinekey.md)
*   [<span data-ttu-id="23010-181">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="23010-181">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
*   [<span data-ttu-id="23010-182">在开发期间安全存储应用密钥</span><span class="sxs-lookup"><span data-stu-id="23010-182">Safe storage of app secrets during development</span></span>](app-secrets.md)
*   [<span data-ttu-id="23010-183">Azure Key Vault 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="23010-183">Azure Key Vault configuration provider</span></span>](key-vault-configuration.md)
*   [<span data-ttu-id="23010-184">强制实施 SSL</span><span class="sxs-lookup"><span data-stu-id="23010-184">Enforcing SSL</span></span>](enforcing-ssl.md)
*   [<span data-ttu-id="23010-185">反请求伪造</span><span class="sxs-lookup"><span data-stu-id="23010-185">Anti-Request Forgery</span></span>](anti-request-forgery.md)
*   [<span data-ttu-id="23010-186">阻止打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="23010-186">Preventing Open Redirect Attacks</span></span>](preventing-open-redirects.md)
*   [<span data-ttu-id="23010-187">阻止跨网站脚本编写</span><span class="sxs-lookup"><span data-stu-id="23010-187">Preventing Cross-Site Scripting</span></span>](cross-site-scripting.md)
*   [<span data-ttu-id="23010-188">启用跨域请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="23010-188">Enabling Cross-Origin Requests (CORS)</span></span>](cors.md)
