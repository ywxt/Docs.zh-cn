---
title: ASP.NET Core 安全性概述
author: tdykstra
description: 了解 ASP.NET Core 中的身份验证、授权和安全基础知识。
ms.author: tdykstra
ms.date: 11/01/2017
uid: security/index
ms.openlocfilehash: d371d37690b6d641f8e584f5e51dcc074a581622
ms.sourcegitcommit: 08bf41d4b3e696ab512b044970e8304816f8cc56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040077"
---
# <a name="overview-of-aspnet-core-security"></a><span data-ttu-id="23729-103">ASP.NET Core 安全性概述</span><span class="sxs-lookup"><span data-stu-id="23729-103">Overview of ASP.NET Core Security</span></span>

<span data-ttu-id="23729-104">通过 ASP.NET Core，开发者可轻松配置和管理其应用的安全性。</span><span class="sxs-lookup"><span data-stu-id="23729-104">ASP.NET Core enables developers to easily configure and manage security for their apps.</span></span> <span data-ttu-id="23729-105">ASP.NET Core 的功能包括管理身份验证、授权、数据保护、SSL 强制、应用机密、请求防伪保护及 CORS 管理。</span><span class="sxs-lookup"><span data-stu-id="23729-105">ASP.NET Core contains features for managing authentication, authorization, data protection, SSL enforcement, app secrets, anti-request forgery protection, and CORS management.</span></span> <span data-ttu-id="23729-106">通过这些安全功能，可以生成安全可靠的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="23729-106">These security features allow you to build robust yet secure ASP.NET Core apps.</span></span>

## <a name="aspnet-core-security-features"></a><span data-ttu-id="23729-107">ASP.NET Core 安全性功能</span><span class="sxs-lookup"><span data-stu-id="23729-107">ASP.NET Core security features</span></span>

<span data-ttu-id="23729-108">ASP.NET Core 提供许多用于保护应用安全的工具和库（包括内置标识提供程序），但也可使用第三方标志服务（如 Facebook、Twitter 或 LinkedIn）。</span><span class="sxs-lookup"><span data-stu-id="23729-108">ASP.NET Core provides many tools and libraries to secure your apps including built-in Identity providers but you can use 3rd party identity services such as Facebook, Twitter, or LinkedIn.</span></span> <span data-ttu-id="23729-109">利用 ASP.NET Core 可以轻松管理应用机密，无需将机密信息暴露在代码中就可存储和使用它们。</span><span class="sxs-lookup"><span data-stu-id="23729-109">With ASP.NET Core, you can easily manage app secrets, which are a way to store and use confidential information without having to expose it in the code.</span></span>

## <a name="authentication-vs-authorization"></a><span data-ttu-id="23729-110">身份验证 vs授权</span><span class="sxs-lookup"><span data-stu-id="23729-110">Authentication vs. Authorization</span></span>

<span data-ttu-id="23729-111">身份验证是这样一个过程：由用户提供凭据，然后将其与存储在操作系统、数据库、应用或资源中的凭据进行比较。</span><span class="sxs-lookup"><span data-stu-id="23729-111">Authentication is a process in which a user provides credentials that are then compared to those stored in an operating system, database, app or resource.</span></span> <span data-ttu-id="23729-112">在授权过程中，如果凭据匹配，则用户身份验证成功，可执行已向其授权的操作。</span><span class="sxs-lookup"><span data-stu-id="23729-112">If they match, users authenticate successfully, and can then perform actions that they're authorized for, during an authorization process.</span></span> <span data-ttu-id="23729-113">授权指判断允许用户执行的操作的过程。</span><span class="sxs-lookup"><span data-stu-id="23729-113">The authorization refers to the process that determines what a user is allowed to do.</span></span>

<span data-ttu-id="23729-114">对身份验证的另一种理解是将其看作进入某一空间（如服务器、数据库、应用或资源）的方式，而将授权看作用户可对该空间（服务器、数据库或应用）内的对象执行的操作。</span><span class="sxs-lookup"><span data-stu-id="23729-114">Another way to think of authentication is to consider it as a way to enter a space, such as a server, database, app or resource, while authorization is which actions the user can perform to which objects inside that space (server, database, or app).</span></span>

## <a name="common-vulnerabilities-in-software"></a><span data-ttu-id="23729-115">软件中的常见漏洞</span><span class="sxs-lookup"><span data-stu-id="23729-115">Common Vulnerabilities in software</span></span>

<span data-ttu-id="23729-116">ASP.NET Core 和 EF 提供维护应用安全、预防安全漏洞的功能。</span><span class="sxs-lookup"><span data-stu-id="23729-116">ASP.NET Core and EF contain features that help you secure your apps and prevent security breaches.</span></span> <span data-ttu-id="23729-117">下表中链接的文档详细介绍了在 Web 应用中避免最常见安全漏洞的技术：</span><span class="sxs-lookup"><span data-stu-id="23729-117">The following list of links takes you to documentation detailing techniques to avoid the most common security vulnerabilities in web apps:</span></span>

* [<span data-ttu-id="23729-118">跨站点脚本攻击</span><span class="sxs-lookup"><span data-stu-id="23729-118">Cross-site scripting attacks</span></span>](xref:security/cross-site-scripting)
* [<span data-ttu-id="23729-119">SQL 注入式攻击</span><span class="sxs-lookup"><span data-stu-id="23729-119">SQL injection attacks</span></span>](https://docs.microsoft.com/ef/core/querying/raw-sql)
* [<span data-ttu-id="23729-120">跨站点请求伪造 (CSRF)</span><span class="sxs-lookup"><span data-stu-id="23729-120">Cross-Site Request Forgery (CSRF)</span></span>](xref:security/anti-request-forgery)
* [<span data-ttu-id="23729-121">打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="23729-121">Open redirect attacks</span></span>](xref:security/preventing-open-redirects)

<span data-ttu-id="23729-122">还应注意其他漏洞。</span><span class="sxs-lookup"><span data-stu-id="23729-122">There are more vulnerabilities that you should be aware of.</span></span> <span data-ttu-id="23729-123">有关详细信息，请参阅本文档中有关 ASP.NET Core 安全文档的部分。</span><span class="sxs-lookup"><span data-stu-id="23729-123">For more information, see the section in this document on *ASP.NET Core Security Documentation*.</span></span>

## <a name="aspnet-core-security-documentation"></a><span data-ttu-id="23729-124">ASP.NET Core 安全文档</span><span class="sxs-lookup"><span data-stu-id="23729-124">ASP.NET Core Security Documentation</span></span>

*   [<span data-ttu-id="23729-125">身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-125">Authentication</span></span>](xref:security/authentication/index)
    *   [<span data-ttu-id="23729-126">标识简介</span><span class="sxs-lookup"><span data-stu-id="23729-126">Introduction to Identity</span></span>](xref:security/authentication/identity)
    *   [<span data-ttu-id="23729-127">启用使用 Facebook、Google 和其他外部提供程序的身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-127">Enable authentication using Facebook, Google, and other external providers</span></span>](xref:security/authentication/social/index)
    *   [<span data-ttu-id="23729-128">通过 WS 联合身份验证启用身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-128">Enable authentication with WS-Federation</span></span>](xref:security/authentication/ws-federation)
    * [<span data-ttu-id="23729-129">配置 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-129">Configure Windows Authentication</span></span>](xref:security/authentication/windowsauth)
    *   [<span data-ttu-id="23729-130">帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="23729-130">Account confirmation and password recovery</span></span>](xref:security/authentication/accconfirm)
    *   [<span data-ttu-id="23729-131">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-131">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
    *   [<span data-ttu-id="23729-132">在没有标识的情况下使用 cookie 身份验证</span><span class="sxs-lookup"><span data-stu-id="23729-132">Use cookie authentication without Identity</span></span>](xref:security/authentication/cookie)
    *   [<span data-ttu-id="23729-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23729-133">Azure Active Directory</span></span>](xref:security/authentication/azure-active-directory/index)
        *   [<span data-ttu-id="23729-134">将 Azure AD 集成到 ASP.NET Core Web 应用中</span><span class="sxs-lookup"><span data-stu-id="23729-134">Integrate Azure AD into an ASP.NET Core web app</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="23729-135">使用 Azure AD 从 WPF 应用调用 ASP.NET Core Web API</span><span class="sxs-lookup"><span data-stu-id="23729-135">Call an ASP.NET Core Web API from a WPF app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-native-aspnetcore/)
        *   [<span data-ttu-id="23729-136">使用 Azure AD 在 ASP.NET Core Web 应用中调用 Web API</span><span class="sxs-lookup"><span data-stu-id="23729-136">Call a Web API in an ASP.NET Core web app using Azure AD</span></span>](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-webapi-openidconnect-aspnetcore/)
        *   [<span data-ttu-id="23729-137">带有 Azure AD B2C 的 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="23729-137">An ASP.NET Core web app with Azure AD B2C</span></span>](https://azure.microsoft.com/resources/samples/active-directory-b2c-dotnetcore-webapp/)
    *   [<span data-ttu-id="23729-138">使用 IdentityServer4 保护 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="23729-138">Secure ASP.NET Core apps with IdentityServer4</span></span>](https://identityserver4.readthedocs.io)
*   [<span data-ttu-id="23729-139">授权</span><span class="sxs-lookup"><span data-stu-id="23729-139">Authorization</span></span>](xref:security/authorization/index)
    *   [<span data-ttu-id="23729-140">介绍</span><span class="sxs-lookup"><span data-stu-id="23729-140">Introduction</span></span>](xref:security/authorization/introduction)
    *   [<span data-ttu-id="23729-141">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="23729-141">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
    *   [<span data-ttu-id="23729-142">简单授权</span><span class="sxs-lookup"><span data-stu-id="23729-142">Simple authorization</span></span>](xref:security/authorization/simple)
    *   [<span data-ttu-id="23729-143">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="23729-143">Role-based authorization</span></span>](xref:security/authorization/roles)
    *   [<span data-ttu-id="23729-144">基于声明的授权</span><span class="sxs-lookup"><span data-stu-id="23729-144">Claims-based authorization</span></span>](xref:security/authorization/claims)
    *   [<span data-ttu-id="23729-145">基于策略的授权</span><span class="sxs-lookup"><span data-stu-id="23729-145">Policy-based authorization</span></span>](xref:security/authorization/policies)
    *   [<span data-ttu-id="23729-146">要求处理程序中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="23729-146">Dependency injection in requirement handlers</span></span>](xref:security/authorization/dependencyinjection)
    *   [<span data-ttu-id="23729-147">基于资源的授权</span><span class="sxs-lookup"><span data-stu-id="23729-147">Resource-based authorization</span></span>](xref:security/authorization/resourcebased)
    *   [<span data-ttu-id="23729-148">基于视图的授权</span><span class="sxs-lookup"><span data-stu-id="23729-148">View-based authorization</span></span>](xref:security/authorization/views)
    *   [<span data-ttu-id="23729-149">使用方案限制标识</span><span class="sxs-lookup"><span data-stu-id="23729-149">Limit identity by scheme</span></span>](xref:security/authorization/limitingidentitybyscheme)
*   [<span data-ttu-id="23729-150">数据保护</span><span class="sxs-lookup"><span data-stu-id="23729-150">Data protection</span></span>](xref:security/data-protection/index)
    *   [<span data-ttu-id="23729-151">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="23729-151">Introduction to data protection</span></span>](xref:security/data-protection/introduction)
    *   [<span data-ttu-id="23729-152">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="23729-152">Get started with the Data Protection APIs</span></span>](xref:security/data-protection/using-data-protection)
    *   [<span data-ttu-id="23729-153">使用者 API</span><span class="sxs-lookup"><span data-stu-id="23729-153">Consumer APIs</span></span>](xref:security/data-protection/consumer-apis/index)
        *   [<span data-ttu-id="23729-154">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="23729-154">Consumer APIs Overview</span></span>](xref:security/data-protection/consumer-apis/overview)
        *   [<span data-ttu-id="23729-155">目标字符串</span><span class="sxs-lookup"><span data-stu-id="23729-155">Purpose strings</span></span>](xref:security/data-protection/consumer-apis/purpose-strings)
        *   [<span data-ttu-id="23729-156">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="23729-156">Purpose hierarchy and multi-tenancy</span></span>](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)
        *   [<span data-ttu-id="23729-157">哈希密码</span><span class="sxs-lookup"><span data-stu-id="23729-157">Hash passwords</span></span>](xref:security/data-protection/consumer-apis/password-hashing)
        *   [<span data-ttu-id="23729-158">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="23729-158">Limit the lifetime of protected payloads</span></span>](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)
        *   [<span data-ttu-id="23729-159">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="23729-159">Unprotect payloads whose keys have been revoked</span></span>](xref:security/data-protection/consumer-apis/dangerous-unprotect)
    *   [<span data-ttu-id="23729-160">配置</span><span class="sxs-lookup"><span data-stu-id="23729-160">Configuration</span></span>](xref:security/data-protection/configuration/index)
        *   [<span data-ttu-id="23729-161">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="23729-161">Configure data protection</span></span>](xref:security/data-protection/configuration/overview)
        *   [<span data-ttu-id="23729-162">默认设置</span><span class="sxs-lookup"><span data-stu-id="23729-162">Default settings</span></span>](xref:security/data-protection/configuration/default-settings)
        *   [<span data-ttu-id="23729-163">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="23729-163">Machine-wide policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)
        *   [<span data-ttu-id="23729-164">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="23729-164">Non DI-aware scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)
    *   [<span data-ttu-id="23729-165">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="23729-165">Extensibility APIs</span></span>](xref:security/data-protection/extensibility/index)
        *   [<span data-ttu-id="23729-166">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="23729-166">Core cryptography extensibility</span></span>](xref:security/data-protection/extensibility/core-crypto)
        *   [<span data-ttu-id="23729-167">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="23729-167">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)
        *   [<span data-ttu-id="23729-168">其他 API</span><span class="sxs-lookup"><span data-stu-id="23729-168">Miscellaneous APIs</span></span>](xref:security/data-protection/extensibility/misc-apis)
    *   [<span data-ttu-id="23729-169">实现</span><span class="sxs-lookup"><span data-stu-id="23729-169">Implementation</span></span>](xref:security/data-protection/implementation/index)
        *   [<span data-ttu-id="23729-170">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="23729-170">Authenticated encryption details</span></span>](xref:security/data-protection/implementation/authenticated-encryption-details)
        *   [<span data-ttu-id="23729-171">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="23729-171">Subkey derivation and authenticated encryption</span></span>](xref:security/data-protection/implementation/subkeyderivation)
        *   [<span data-ttu-id="23729-172">上下文标头</span><span class="sxs-lookup"><span data-stu-id="23729-172">Context headers</span></span>](xref:security/data-protection/implementation/context-headers)
        *   [<span data-ttu-id="23729-173">密钥管理</span><span class="sxs-lookup"><span data-stu-id="23729-173">Key management</span></span>](xref:security/data-protection/implementation/key-management)
        *   [<span data-ttu-id="23729-174">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="23729-174">Key storage providers</span></span>](xref:security/data-protection/implementation/key-storage-providers)
        *   [<span data-ttu-id="23729-175">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="23729-175">Key encryption at rest</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest)
        *   [<span data-ttu-id="23729-176">密钥永久性和设置</span><span class="sxs-lookup"><span data-stu-id="23729-176">Key immutability and settings</span></span>](xref:security/data-protection/implementation/key-immutability)
        *   [<span data-ttu-id="23729-177">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="23729-177">Key storage format</span></span>](xref:security/data-protection/implementation/key-storage-format)
        *   [<span data-ttu-id="23729-178">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="23729-178">Ephemeral data protection providers</span></span>](xref:security/data-protection/implementation/key-storage-ephemeral)
    *   [<span data-ttu-id="23729-179">兼容性</span><span class="sxs-lookup"><span data-stu-id="23729-179">Compatibility</span></span>](xref:security/data-protection/compatibility/index)
        *   [<span data-ttu-id="23729-180">在 ASP.NET 中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="23729-180">Replace <machineKey> in ASP.NET</span></span>](xref:security/data-protection/compatibility/replacing-machinekey)
*   [<span data-ttu-id="23729-181">通过授权保护的用户数据创建应用</span><span class="sxs-lookup"><span data-stu-id="23729-181">Create an app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
*   [<span data-ttu-id="23729-182">在开发期间安全存储应用机密</span><span class="sxs-lookup"><span data-stu-id="23729-182">Safe storage of app secrets in development</span></span>](xref:security/app-secrets)
*   [<span data-ttu-id="23729-183">Azure Key Vault 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="23729-183">Azure Key Vault configuration provider</span></span>](xref:security/key-vault-configuration)
*   [<span data-ttu-id="23729-184">强制实施 SSL</span><span class="sxs-lookup"><span data-stu-id="23729-184">Enforce SSL</span></span>](xref:security/enforcing-ssl)
*   [<span data-ttu-id="23729-185">防请求伪造</span><span class="sxs-lookup"><span data-stu-id="23729-185">Anti-Request Forgery</span></span>](xref:security/anti-request-forgery)
*   [<span data-ttu-id="23729-186">阻止打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="23729-186">Prevent open redirect attacks</span></span>](xref:security/preventing-open-redirects)
*   [<span data-ttu-id="23729-187">阻止跨站点脚本编写</span><span class="sxs-lookup"><span data-stu-id="23729-187">Prevent Cross-Site Scripting</span></span>](xref:security/cross-site-scripting)
*   [<span data-ttu-id="23729-188">启用跨域请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="23729-188">Enable Cross-Origin Requests (CORS)</span></span>](xref:security/cors)
*   [<span data-ttu-id="23729-189">在应用之间共享 Cookie</span><span class="sxs-lookup"><span data-stu-id="23729-189">Share cookies among apps</span></span>](xref:security/cookie-sharing)
*   [<span data-ttu-id="23729-190">IP 安全列表</span><span class="sxs-lookup"><span data-stu-id="23729-190">IP safelist</span></span>](xref:security/ip-safelist)
