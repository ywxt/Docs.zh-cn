---
title: "ASP.NET Core 安全性概述"
author: rachelappel
description: "了解 ASP.NET Core 中的身份验证、授权和安全基础知识。"
manager: wpickett
ms.author: rachelap
ms.date: 11/01/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/index
ms.openlocfilehash: 7e5f6bc44241dc6fc11569a145a04340f1b3ee7f
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-core-security-overview"></a><span data-ttu-id="3ca05-103">ASP.NET Core 安全性概述</span><span class="sxs-lookup"><span data-stu-id="3ca05-103">ASP.NET Core Security Overview</span></span>

<span data-ttu-id="3ca05-104">通过 ASP.NET Core，开发者可轻松配置和管理其应用的安全性。</span><span class="sxs-lookup"><span data-stu-id="3ca05-104">ASP.NET Core enables developers to easily configure and manage security for their apps.</span></span> <span data-ttu-id="3ca05-105">ASP.NET Core 的功能包括管理身份验证、授权、数据保护、SSL 强制、应用机密、请求防伪保护及 CORS 管理。</span><span class="sxs-lookup"><span data-stu-id="3ca05-105">ASP.NET Core contains features for managing authentication, authorization, data protection, SSL enforcement, app secrets, anti-request forgery protection, and CORS management.</span></span> <span data-ttu-id="3ca05-106">通过这些安全功能，可以生成安全可靠的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="3ca05-106">These security features allow you to build robust yet secure ASP.NET Core apps.</span></span>

## <a name="aspnet-core-security-features"></a><span data-ttu-id="3ca05-107">ASP.NET Core 安全性功能</span><span class="sxs-lookup"><span data-stu-id="3ca05-107">ASP.NET Core security features</span></span>

<span data-ttu-id="3ca05-108">ASP.NET Core 提供许多用于保护应用安全的工具和库（包括内置标识提供程序），但也可使用第三方标志服务（如 Facebook、Twitter 或 LinkedIn）。</span><span class="sxs-lookup"><span data-stu-id="3ca05-108">ASP.NET Core provides many tools and libraries to secure your apps including built-in Identity providers but you can use 3rd party identity services such as Facebook, Twitter, or LinkedIn.</span></span> <span data-ttu-id="3ca05-109">利用 ASP.NET Core 可以轻松管理应用机密，无需将机密信息暴露在代码中就可存储和使用它们。</span><span class="sxs-lookup"><span data-stu-id="3ca05-109">With ASP.NET Core, you can easily manage app secrets, which are a way to store and use confidential information without having to expose it in the code.</span></span>

## <a name="authentication-vs-authorization"></a><span data-ttu-id="3ca05-110">身份验证 vs授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-110">Authentication vs. Authorization</span></span>

<span data-ttu-id="3ca05-111">身份验证是这样一个过程：由用户提供凭据，然后将其与存储在操作系统、数据库、应用或资源中的凭据进行比较。</span><span class="sxs-lookup"><span data-stu-id="3ca05-111">Authentication is a process in which a user provides credentials that are then compared to those stored in an operating system, database, app or resource.</span></span> <span data-ttu-id="3ca05-112">在授权过程中，如果凭据匹配，则用户身份验证成功，可执行已向其授权的操作。</span><span class="sxs-lookup"><span data-stu-id="3ca05-112">If they match, users authenticate successfully, and can then perform actions that they're authorized for, during an authorization process.</span></span> <span data-ttu-id="3ca05-113">授权指判断允许用户执行的操作的过程。</span><span class="sxs-lookup"><span data-stu-id="3ca05-113">The authorization refers to the process that determines what a user is allowed to do.</span></span>

<span data-ttu-id="3ca05-114">对身份验证的另一种理解是将其看作进入某一空间（如服务器、数据库、应用或资源）的方式，而将授权看作用户可对该空间（服务器、数据库或应用）内的对象执行的操作。</span><span class="sxs-lookup"><span data-stu-id="3ca05-114">Another way to think of authentication is to consider it as a way to enter a space, such as a server, database, app or resource, while authorization is which actions the user can perform to which objects inside that space (server, database, or app).</span></span>

## <a name="common-vulnerabilities-in-software"></a><span data-ttu-id="3ca05-115">软件中的常见漏洞</span><span class="sxs-lookup"><span data-stu-id="3ca05-115">Common Vulnerabilities in software</span></span>

<span data-ttu-id="3ca05-116">ASP.NET Core 和 EF 提供维护应用安全、预防安全漏洞的功能。</span><span class="sxs-lookup"><span data-stu-id="3ca05-116">ASP.NET Core and EF contain features that help you secure your apps and prevent security breaches.</span></span> <span data-ttu-id="3ca05-117">下表中链接的文档详细介绍了在 Web 应用中避免最常见安全漏洞的技术：</span><span class="sxs-lookup"><span data-stu-id="3ca05-117">The following list of links takes you to documentation detailing techniques to avoid the most common security vulnerabilities in web apps:</span></span>

* [<span data-ttu-id="3ca05-118">跨站点脚本攻击</span><span class="sxs-lookup"><span data-stu-id="3ca05-118">Cross-site scripting attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/cross-site-scripting)
* [<span data-ttu-id="3ca05-119">SQL 注入式攻击</span><span class="sxs-lookup"><span data-stu-id="3ca05-119">SQL injection attacks</span></span>](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [<span data-ttu-id="3ca05-120">跨站点请求伪造 (CSRF)</span><span class="sxs-lookup"><span data-stu-id="3ca05-120">Cross-Site Request Forgery (CSRF)</span></span>](https://docs.microsoft.com/aspnet/core/security/anti-request-forgery)
* [<span data-ttu-id="3ca05-121">打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="3ca05-121">Open redirect attacks</span></span>](https://docs.microsoft.com/aspnet/core/security/preventing-open-redirects)

<span data-ttu-id="3ca05-122">还应注意其他漏洞。</span><span class="sxs-lookup"><span data-stu-id="3ca05-122">There are more vulnerabilities that you should be aware of.</span></span> <span data-ttu-id="3ca05-123">有关详细信息，请参阅本文档中关于 ASP.NET Core 安全文档的部分。</span><span class="sxs-lookup"><span data-stu-id="3ca05-123">For more information, see the section in this document on *ASP.NET Security Documentation*.</span></span>

## <a name="aspnet-security-documentation"></a><span data-ttu-id="3ca05-124">ASP.NET Core 安全文档</span><span class="sxs-lookup"><span data-stu-id="3ca05-124">ASP.NET Security Documentation</span></span>

*   [<span data-ttu-id="3ca05-125">身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-125">Authentication</span></span>](authentication/index.md)
    *   [<span data-ttu-id="3ca05-126">标识简介</span><span class="sxs-lookup"><span data-stu-id="3ca05-126">Introduction to Identity</span></span>](authentication/identity.md)
    *   [<span data-ttu-id="3ca05-127">启用使用 Facebook、Google 和其他外部提供程序的身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-127">Enable authentication using Facebook, Google, and other external providers</span></span>](authentication/social/index.md)
    *   [<span data-ttu-id="3ca05-128">通过 WS 联合身份验证启用身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-128">Enable authentication with WS-Federation</span></span>](authentication/ws-federation.md)
    * [<span data-ttu-id="3ca05-129">配置 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-129">Configure Windows Authentication</span></span>](authentication/windowsauth.md)
    *   [<span data-ttu-id="3ca05-130">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="3ca05-130">Account confirmation and password recovery</span></span>](authentication/accconfirm.md)
    *   [<span data-ttu-id="3ca05-131">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-131">Two-factor authentication with SMS</span></span>](authentication/2fa.md)
    *   [<span data-ttu-id="3ca05-132">在没有标识的情况下使用 cookie 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ca05-132">Use cookie authentication without Identity</span></span>](authentication/cookie.md)
    *   [<span data-ttu-id="3ca05-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca05-133">Azure Active Directory</span></span>](authentication/azure-active-directory/index.md)
        *   [<span data-ttu-id="3ca05-134">将 Azure AD 集成到 ASP.NET Core Web 应用中</span><span class="sxs-lookup"><span data-stu-id="3ca05-134">Integrate Azure AD into an ASP.NET Core web app</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="3ca05-135">使用 Azure AD 从 WPF 应用调用 ASP.NET Core Web API</span><span class="sxs-lookup"><span data-stu-id="3ca05-135">Call an ASP.NET Core Web API from a WPF app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [<span data-ttu-id="3ca05-136">使用 Azure AD 在 ASP.NET Core Web 应用中调用 Web API</span><span class="sxs-lookup"><span data-stu-id="3ca05-136">Call a Web API in an ASP.NET Core web app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="3ca05-137">带有 Azure AD B2C 的 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="3ca05-137">An ASP.NET Core web app with Azure AD B2C</span></span>](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [<span data-ttu-id="3ca05-138">使用 IdentityServer4 保护 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="3ca05-138">Secure ASP.NET Core apps with IdentityServer4</span></span>](https://identityserver4.readthedocs.io)
*   [<span data-ttu-id="3ca05-139">授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-139">Authorization</span></span>](authorization/index.md)
    *   [<span data-ttu-id="3ca05-140">介绍</span><span class="sxs-lookup"><span data-stu-id="3ca05-140">Introduction</span></span>](authorization/introduction.md)
    *   [<span data-ttu-id="3ca05-141">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="3ca05-141">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
    *   [<span data-ttu-id="3ca05-142">简单授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-142">Simple authorization</span></span>](authorization/simple.md)
    *   [<span data-ttu-id="3ca05-143">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-143">Role-based authorization</span></span>](authorization/roles.md)
    *   [<span data-ttu-id="3ca05-144">基于声明的授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-144">Claims-based authorization</span></span>](authorization/claims.md)
    *   [<span data-ttu-id="3ca05-145">基于策略的授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-145">Policy-based authorization</span></span>](authorization/policies.md)
    *   [<span data-ttu-id="3ca05-146">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="3ca05-146">Dependency injection in requirement handlers</span></span>](authorization/dependencyinjection.md)
    *   [<span data-ttu-id="3ca05-147">基于资源的授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-147">Resource-based authorization</span></span>](authorization/resourcebased.md)
    *   [<span data-ttu-id="3ca05-148">基于视图的授权</span><span class="sxs-lookup"><span data-stu-id="3ca05-148">View-based authorization</span></span>](authorization/views.md)
    *   [<span data-ttu-id="3ca05-149">使用方案限制标识</span><span class="sxs-lookup"><span data-stu-id="3ca05-149">Limit identity by scheme</span></span>](authorization/limitingidentitybyscheme.md)
*   [<span data-ttu-id="3ca05-150">数据保护</span><span class="sxs-lookup"><span data-stu-id="3ca05-150">Data protection</span></span>](data-protection/index.md)
    *   [<span data-ttu-id="3ca05-151">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="3ca05-151">Introduction to data protection</span></span>](data-protection/introduction.md)
    *   [<span data-ttu-id="3ca05-152">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="3ca05-152">Get started with the Data Protection APIs</span></span>](data-protection/using-data-protection.md)
    *   [<span data-ttu-id="3ca05-153">使用者 API</span><span class="sxs-lookup"><span data-stu-id="3ca05-153">Consumer APIs</span></span>](data-protection/consumer-apis/index.md)
        *   [<span data-ttu-id="3ca05-154">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="3ca05-154">Consumer APIs Overview</span></span>](data-protection/consumer-apis/overview.md)
        *   [<span data-ttu-id="3ca05-155">目标字符串</span><span class="sxs-lookup"><span data-stu-id="3ca05-155">Purpose strings</span></span>](data-protection/consumer-apis/purpose-strings.md)
        *   [<span data-ttu-id="3ca05-156">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="3ca05-156">Purpose hierarchy and multi-tenancy</span></span>](data-protection/consumer-apis/purpose-strings-multitenancy.md)
        *   [<span data-ttu-id="3ca05-157">密码哈希</span><span class="sxs-lookup"><span data-stu-id="3ca05-157">Password hashing</span></span>](data-protection/consumer-apis/password-hashing.md)
        *   [<span data-ttu-id="3ca05-158">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="3ca05-158">Limit the lifetime of protected payloads</span></span>](data-protection/consumer-apis/limited-lifetime-payloads.md)
        *   [<span data-ttu-id="3ca05-159">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="3ca05-159">Unprotect payloads whose keys have been revoked</span></span>](data-protection/consumer-apis/dangerous-unprotect.md)
    *   [<span data-ttu-id="3ca05-160">配置</span><span class="sxs-lookup"><span data-stu-id="3ca05-160">Configuration</span></span>](data-protection/configuration/index.md)
        *   [<span data-ttu-id="3ca05-161">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="3ca05-161">Configure data protection</span></span>](data-protection/configuration/overview.md)
        *   [<span data-ttu-id="3ca05-162">默认设置</span><span class="sxs-lookup"><span data-stu-id="3ca05-162">Default settings</span></span>](data-protection/configuration/default-settings.md)
        *   [<span data-ttu-id="3ca05-163">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="3ca05-163">Machine-wide policy</span></span>](data-protection/configuration/machine-wide-policy.md)
        *   [<span data-ttu-id="3ca05-164">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="3ca05-164">Non DI-aware scenarios</span></span>](data-protection/configuration/non-di-scenarios.md)
    *   [<span data-ttu-id="3ca05-165">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="3ca05-165">Extensibility APIs</span></span>](data-protection/extensibility/index.md)
        *   [<span data-ttu-id="3ca05-166">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="3ca05-166">Core cryptography extensibility</span></span>](data-protection/extensibility/core-crypto.md)
        *   [<span data-ttu-id="3ca05-167">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="3ca05-167">Key management extensibility</span></span>](data-protection/extensibility/key-management.md)
        *   [<span data-ttu-id="3ca05-168">其他 API</span><span class="sxs-lookup"><span data-stu-id="3ca05-168">Miscellaneous APIs</span></span>](data-protection/extensibility/misc-apis.md)
    *   [<span data-ttu-id="3ca05-169">实现</span><span class="sxs-lookup"><span data-stu-id="3ca05-169">Implementation</span></span>](data-protection/implementation/index.md)
        *   [<span data-ttu-id="3ca05-170">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="3ca05-170">Authenticated encryption details</span></span>](data-protection/implementation/authenticated-encryption-details.md)
        *   [<span data-ttu-id="3ca05-171">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="3ca05-171">Subkey derivation and authenticated encryption</span></span>](data-protection/implementation/subkeyderivation.md)
        *   [<span data-ttu-id="3ca05-172">上下文标头</span><span class="sxs-lookup"><span data-stu-id="3ca05-172">Context headers</span></span>](data-protection/implementation/context-headers.md)
        *   [<span data-ttu-id="3ca05-173">密钥管理</span><span class="sxs-lookup"><span data-stu-id="3ca05-173">Key management</span></span>](data-protection/implementation/key-management.md)
        *   [<span data-ttu-id="3ca05-174">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="3ca05-174">Key storage providers</span></span>](data-protection/implementation/key-storage-providers.md)
        *   [<span data-ttu-id="3ca05-175">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="3ca05-175">Key encryption at rest</span></span>](data-protection/implementation/key-encryption-at-rest.md)
        *   [<span data-ttu-id="3ca05-176">密钥永久性和更改设置</span><span class="sxs-lookup"><span data-stu-id="3ca05-176">Key immutability and changing settings</span></span>](data-protection/implementation/key-immutability.md)
        *   [<span data-ttu-id="3ca05-177">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="3ca05-177">Key storage format</span></span>](data-protection/implementation/key-storage-format.md)
        *   [<span data-ttu-id="3ca05-178">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="3ca05-178">Ephemeral data protection providers</span></span>](data-protection/implementation/key-storage-ephemeral.md)
    *   [<span data-ttu-id="3ca05-179">兼容性</span><span class="sxs-lookup"><span data-stu-id="3ca05-179">Compatibility</span></span>](data-protection/compatibility/index.md)
        *   [<span data-ttu-id="3ca05-180">在应用之间共享 Cookie</span><span class="sxs-lookup"><span data-stu-id="3ca05-180">Share cookies among apps</span></span>](data-protection/compatibility/cookie-sharing.md)
        *   [<span data-ttu-id="3ca05-181">在 ASP.NET 中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="3ca05-181">Replace <machineKey> in ASP.NET</span></span>](data-protection/compatibility/replacing-machinekey.md)
*   [<span data-ttu-id="3ca05-182">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="3ca05-182">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
*   [<span data-ttu-id="3ca05-183">在开发期间安全存储应用密钥</span><span class="sxs-lookup"><span data-stu-id="3ca05-183">Safe storage of app secrets during development</span></span>](app-secrets.md)
*   [<span data-ttu-id="3ca05-184">Azure Key Vault 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="3ca05-184">Azure Key Vault configuration provider</span></span>](key-vault-configuration.md)
*   [<span data-ttu-id="3ca05-185">强制实施 SSL</span><span class="sxs-lookup"><span data-stu-id="3ca05-185">Enforce SSL</span></span>](enforcing-ssl.md)
*   [<span data-ttu-id="3ca05-186">防请求伪造</span><span class="sxs-lookup"><span data-stu-id="3ca05-186">Anti-Request Forgery</span></span>](anti-request-forgery.md)
*   [<span data-ttu-id="3ca05-187">阻止打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="3ca05-187">Prevent open redirect attacks</span></span>](preventing-open-redirects.md)
*   [<span data-ttu-id="3ca05-188">阻止跨站点脚本编写</span><span class="sxs-lookup"><span data-stu-id="3ca05-188">Prevent Cross-Site Scripting</span></span>](cross-site-scripting.md)
*   [<span data-ttu-id="3ca05-189">启用跨域请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="3ca05-189">Enable Cross-Origin Requests (CORS)</span></span>](cors.md)
