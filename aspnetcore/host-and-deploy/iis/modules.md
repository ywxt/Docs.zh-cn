---
title: "使用 ASP.NET Core 的 IIS 模块"
author: guardrex
description: "参考文档，其中描述 ASP.NET Core 应用程序的活动和非活动 IIS 模块。"
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 03/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: host-and-deploy/iis/modules
ms.openlocfilehash: 405297bdd1ceac390b995ed6e15ae8d95bb8501f
ms.sourcegitcommit: a3e88639a6bcf8fb4d634036dac93130c464a097
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="using-iis-modules-with-aspnet-core"></a><span data-ttu-id="beaa8-103">使用 ASP.NET Core 的 IIS 模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-103">Using IIS Modules with ASP.NET Core</span></span>

<span data-ttu-id="beaa8-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="beaa8-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="beaa8-105">反向代理配置中，由 IIS 承载 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="beaa8-105">ASP.NET Core applications are hosted by IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="beaa8-106">一些本机 IIS 模块和所有 IIS 管理模块不是可用于处理请求的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="beaa8-106">Some of the native IIS modules and all of the IIS managed modules aren't available to process requests for ASP.NET Core apps.</span></span> <span data-ttu-id="beaa8-107">在许多情况下，ASP.NET Core 提供 IIS 本机和托管模块的功能的替代方法。</span><span class="sxs-lookup"><span data-stu-id="beaa8-107">In many cases, ASP.NET Core offers an alternative to the features of IIS native and managed modules.</span></span>

## <a name="native-modules"></a><span data-ttu-id="beaa8-108">本机模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-108">Native Modules</span></span>

<span data-ttu-id="beaa8-109">模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-109">Module</span></span> | <span data-ttu-id="beaa8-110">.NET 核心活动</span><span class="sxs-lookup"><span data-stu-id="beaa8-110">.NET Core Active</span></span> | <span data-ttu-id="beaa8-111">ASP.NET Core Option</span><span class="sxs-lookup"><span data-stu-id="beaa8-111">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="beaa8-112">**匿名身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-112">**Anonymous Authentication**</span></span><br>`AnonymousAuthenticationModule` | <span data-ttu-id="beaa8-113">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-113">Yes</span></span> | 
<span data-ttu-id="beaa8-114">**基本身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-114">**Basic Authentication**</span></span><br>`BasicAuthenticationModule` | <span data-ttu-id="beaa8-115">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-115">Yes</span></span> | 
<span data-ttu-id="beaa8-116">**客户端证书映射身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-116">**Client Certification Mapping Authentication**</span></span><br>`CertificateMappingAuthenticationModule` | <span data-ttu-id="beaa8-117">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-117">Yes</span></span> | 
<span data-ttu-id="beaa8-118">**CGI**</span><span class="sxs-lookup"><span data-stu-id="beaa8-118">**CGI**</span></span><br>`CgiModule` | <span data-ttu-id="beaa8-119">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-119">No</span></span> | 
<span data-ttu-id="beaa8-120">**配置验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-120">**Configuration Validation**</span></span><br>`ConfigurationValidationModule` | <span data-ttu-id="beaa8-121">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-121">Yes</span></span> | 
<span data-ttu-id="beaa8-122">**HTTP 错误**</span><span class="sxs-lookup"><span data-stu-id="beaa8-122">**HTTP Errors**</span></span><br>`CustomErrorModule` | <span data-ttu-id="beaa8-123">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-123">No</span></span> | [<span data-ttu-id="beaa8-124">状态代码页中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-124">Status Code Pages Middleware</span></span>](xref:fundamentals/error-handling#configuring-status-code-pages)
<span data-ttu-id="beaa8-125">**自定义日志记录**</span><span class="sxs-lookup"><span data-stu-id="beaa8-125">**Custom Logging**</span></span><br>`CustomLoggingModule` | <span data-ttu-id="beaa8-126">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-126">Yes</span></span> | 
<span data-ttu-id="beaa8-127">**默认文档**</span><span class="sxs-lookup"><span data-stu-id="beaa8-127">**Default Document**</span></span><br>`DefaultDocumentModule` | <span data-ttu-id="beaa8-128">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-128">No</span></span> | [<span data-ttu-id="beaa8-129">默认文件中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-129">Default Files Middleware</span></span>](xref:fundamentals/static-files#serve-a-default-document)
<span data-ttu-id="beaa8-130">**摘要式身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-130">**Digest Authentication**</span></span><br>`DigestAuthenticationModule` | <span data-ttu-id="beaa8-131">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-131">Yes</span></span> | 
<span data-ttu-id="beaa8-132">**目录浏览**</span><span class="sxs-lookup"><span data-stu-id="beaa8-132">**Directory Browsing**</span></span><br>`DirectoryListingModule` | <span data-ttu-id="beaa8-133">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-133">No</span></span> | [<span data-ttu-id="beaa8-134">目录浏览中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-134">Directory Browsing Middleware</span></span>](xref:fundamentals/static-files#enable-directory-browsing)
<span data-ttu-id="beaa8-135">**动态压缩**</span><span class="sxs-lookup"><span data-stu-id="beaa8-135">**Dynamic Compression**</span></span><br>`DynamicCompressionModule` | <span data-ttu-id="beaa8-136">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-136">Yes</span></span> | [<span data-ttu-id="beaa8-137">响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-137">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="beaa8-138">**跟踪**</span><span class="sxs-lookup"><span data-stu-id="beaa8-138">**Tracing**</span></span><br>`FailedRequestsTracingModule` | <span data-ttu-id="beaa8-139">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-139">Yes</span></span> | [<span data-ttu-id="beaa8-140">ASP.NET 核心日志记录</span><span class="sxs-lookup"><span data-stu-id="beaa8-140">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index#the-tracesource-provider)
<span data-ttu-id="beaa8-141">**文件缓存**</span><span class="sxs-lookup"><span data-stu-id="beaa8-141">**File Caching**</span></span><br>`FileCacheModule` | <span data-ttu-id="beaa8-142">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-142">No</span></span> | [<span data-ttu-id="beaa8-143">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-143">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="beaa8-144">**HTTP 缓存功能**</span><span class="sxs-lookup"><span data-stu-id="beaa8-144">**HTTP Caching**</span></span><br>`HttpCacheModule` | <span data-ttu-id="beaa8-145">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-145">No</span></span> | [<span data-ttu-id="beaa8-146">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-146">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="beaa8-147">**HTTP 日志记录**</span><span class="sxs-lookup"><span data-stu-id="beaa8-147">**HTTP Logging**</span></span><br>`HttpLoggingModule` | <span data-ttu-id="beaa8-148">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-148">Yes</span></span> | [<span data-ttu-id="beaa8-149">ASP.NET 核心日志记录</span><span class="sxs-lookup"><span data-stu-id="beaa8-149">ASP.NET Core Logging</span></span>](xref:fundamentals/logging/index)<br><span data-ttu-id="beaa8-150">实现： [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging)， [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)， [NLog](https://github.com/NLog/NLog.Extensions.Logging)， [Serilog](https://github.com/serilog/serilog-extensions-logging)</span><span class="sxs-lookup"><span data-stu-id="beaa8-150">Implementations: [elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging), [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), [NLog](https://github.com/NLog/NLog.Extensions.Logging), [Serilog](https://github.com/serilog/serilog-extensions-logging)</span></span>
<span data-ttu-id="beaa8-151">**HTTP 重定向**</span><span class="sxs-lookup"><span data-stu-id="beaa8-151">**HTTP Redirection**</span></span><br>`HttpRedirectionModule` | <span data-ttu-id="beaa8-152">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-152">Yes</span></span> | [<span data-ttu-id="beaa8-153">URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="beaa8-154">**IIS 客户端证书映射身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-154">**IIS Client Certificate Mapping Authentication**</span></span><br>`IISCertificateMappingAuthenticationModule` | <span data-ttu-id="beaa8-155">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-155">Yes</span></span> | 
<span data-ttu-id="beaa8-156">**IP 和域限制**</span><span class="sxs-lookup"><span data-stu-id="beaa8-156">**IP and Domain Restrictions**</span></span><br>`IpRestrictionModule` | <span data-ttu-id="beaa8-157">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-157">Yes</span></span> | 
<span data-ttu-id="beaa8-158">**ISAPI 筛选器**</span><span class="sxs-lookup"><span data-stu-id="beaa8-158">**ISAPI Filters**</span></span><br>`IsapiFilterModule` | <span data-ttu-id="beaa8-159">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-159">Yes</span></span> | [<span data-ttu-id="beaa8-160">中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-160">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="beaa8-161">**ISAPI**</span><span class="sxs-lookup"><span data-stu-id="beaa8-161">**ISAPI**</span></span><br>`IsapiModule` | <span data-ttu-id="beaa8-162">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-162">Yes</span></span> | [<span data-ttu-id="beaa8-163">中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-163">Middleware</span></span>](xref:fundamentals/middleware)
<span data-ttu-id="beaa8-164">**协议支持**</span><span class="sxs-lookup"><span data-stu-id="beaa8-164">**Protocol Support**</span></span><br>`ProtocolSupportModule` | <span data-ttu-id="beaa8-165">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-165">Yes</span></span> | 
<span data-ttu-id="beaa8-166">**请求筛选**</span><span class="sxs-lookup"><span data-stu-id="beaa8-166">**Request Filtering**</span></span><br>`RequestFilteringModule` | <span data-ttu-id="beaa8-167">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-167">Yes</span></span> | [<span data-ttu-id="beaa8-168">URL 重写中间件`IRule`</span><span class="sxs-lookup"><span data-stu-id="beaa8-168">URL Rewriting Middleware `IRule`</span></span>](xref:fundamentals/url-rewriting#irule-based-rule)
<span data-ttu-id="beaa8-169">**请求监视器**</span><span class="sxs-lookup"><span data-stu-id="beaa8-169">**Request Monitor**</span></span><br>`RequestMonitorModule` | <span data-ttu-id="beaa8-170">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-170">Yes</span></span> | 
<span data-ttu-id="beaa8-171">**URL 重写**</span><span class="sxs-lookup"><span data-stu-id="beaa8-171">**URL Rewriting**</span></span><br>`RewriteModule` | <span data-ttu-id="beaa8-172">Yes†</span><span class="sxs-lookup"><span data-stu-id="beaa8-172">Yes†</span></span> | [<span data-ttu-id="beaa8-173">URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-173">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="beaa8-174">**服务器端包括**</span><span class="sxs-lookup"><span data-stu-id="beaa8-174">**Server Side Includes**</span></span><br>`ServerSideIncludeModule` | <span data-ttu-id="beaa8-175">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-175">No</span></span> | 
<span data-ttu-id="beaa8-176">**静态压缩**</span><span class="sxs-lookup"><span data-stu-id="beaa8-176">**Static Compression**</span></span><br>`StaticCompressionModule` | <span data-ttu-id="beaa8-177">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-177">No</span></span> | [<span data-ttu-id="beaa8-178">响应压缩中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-178">Response Compression Middleware</span></span>](xref:performance/response-compression)
<span data-ttu-id="beaa8-179">**静态内容**</span><span class="sxs-lookup"><span data-stu-id="beaa8-179">**Static Content**</span></span><br>`StaticFileModule` | <span data-ttu-id="beaa8-180">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-180">No</span></span> | [<span data-ttu-id="beaa8-181">静态文件中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-181">Static File Middleware</span></span>](xref:fundamentals/static-files)
<span data-ttu-id="beaa8-182">**令牌缓存**</span><span class="sxs-lookup"><span data-stu-id="beaa8-182">**Token Caching**</span></span><br>`TokenCacheModule` | <span data-ttu-id="beaa8-183">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-183">Yes</span></span> | 
<span data-ttu-id="beaa8-184">**URI 缓存**</span><span class="sxs-lookup"><span data-stu-id="beaa8-184">**URI Caching**</span></span><br>`UriCacheModule` | <span data-ttu-id="beaa8-185">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-185">Yes</span></span> | 
<span data-ttu-id="beaa8-186">**URL 授权**</span><span class="sxs-lookup"><span data-stu-id="beaa8-186">**URL Authorization**</span></span><br>`UrlAuthorizationModule` | <span data-ttu-id="beaa8-187">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-187">Yes</span></span> | [<span data-ttu-id="beaa8-188">ASP.NET 核心标识</span><span class="sxs-lookup"><span data-stu-id="beaa8-188">ASP.NET Core Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="beaa8-189">**Windows 身份验证**</span><span class="sxs-lookup"><span data-stu-id="beaa8-189">**Windows Authentication**</span></span><br>`WindowsAuthenticationModule` | <span data-ttu-id="beaa8-190">是</span><span class="sxs-lookup"><span data-stu-id="beaa8-190">Yes</span></span> | 

<span data-ttu-id="beaa8-191">†The URL 重写模块`isFile`和`isDirectory`不使用 ASP.NET Core 应用中的更改由于[目录结构](xref:host-and-deploy/directory-structure)。</span><span class="sxs-lookup"><span data-stu-id="beaa8-191">†The URL Rewrite Module's `isFile` and `isDirectory` don't work with ASP.NET Core apps due to the changes in [directory structure](xref:host-and-deploy/directory-structure).</span></span>

## <a name="managed-modules"></a><span data-ttu-id="beaa8-192">托管的模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-192">Managed Modules</span></span>

<span data-ttu-id="beaa8-193">模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-193">Module</span></span> | <span data-ttu-id="beaa8-194">.NET 核心活动</span><span class="sxs-lookup"><span data-stu-id="beaa8-194">.NET Core Active</span></span> | <span data-ttu-id="beaa8-195">ASP.NET Core Option</span><span class="sxs-lookup"><span data-stu-id="beaa8-195">ASP.NET Core Option</span></span>
--- | :---: | ---
<span data-ttu-id="beaa8-196">AnonymousIdentification</span><span class="sxs-lookup"><span data-stu-id="beaa8-196">AnonymousIdentification</span></span> | <span data-ttu-id="beaa8-197">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-197">No</span></span> | 
<span data-ttu-id="beaa8-198">DefaultAuthentication</span><span class="sxs-lookup"><span data-stu-id="beaa8-198">DefaultAuthentication</span></span> | <span data-ttu-id="beaa8-199">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-199">No</span></span> | 
<span data-ttu-id="beaa8-200">FileAuthorization</span><span class="sxs-lookup"><span data-stu-id="beaa8-200">FileAuthorization</span></span> | <span data-ttu-id="beaa8-201">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-201">No</span></span> | 
<span data-ttu-id="beaa8-202">FormsAuthentication</span><span class="sxs-lookup"><span data-stu-id="beaa8-202">FormsAuthentication</span></span> | <span data-ttu-id="beaa8-203">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-203">No</span></span> | [<span data-ttu-id="beaa8-204">Cookie 身份验证中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-204">Cookie Authentication Middleware</span></span>](xref:security/authentication/cookie)
<span data-ttu-id="beaa8-205">OutputCache</span><span class="sxs-lookup"><span data-stu-id="beaa8-205">OutputCache</span></span> | <span data-ttu-id="beaa8-206">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-206">No</span></span> | [<span data-ttu-id="beaa8-207">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-207">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
<span data-ttu-id="beaa8-208">配置文件</span><span class="sxs-lookup"><span data-stu-id="beaa8-208">Profile</span></span> | <span data-ttu-id="beaa8-209">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-209">No</span></span> | 
<span data-ttu-id="beaa8-210">RoleManager</span><span class="sxs-lookup"><span data-stu-id="beaa8-210">RoleManager</span></span> | <span data-ttu-id="beaa8-211">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-211">No</span></span> | 
<span data-ttu-id="beaa8-212">ScriptModule-4.0</span><span class="sxs-lookup"><span data-stu-id="beaa8-212">ScriptModule-4.0</span></span> | <span data-ttu-id="beaa8-213">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-213">No</span></span> | 
<span data-ttu-id="beaa8-214">会话</span><span class="sxs-lookup"><span data-stu-id="beaa8-214">Session</span></span> | <span data-ttu-id="beaa8-215">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-215">No</span></span> | [<span data-ttu-id="beaa8-216">会话中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-216">Session Middleware</span></span>](xref:fundamentals/app-state)
<span data-ttu-id="beaa8-217">UrlAuthorization</span><span class="sxs-lookup"><span data-stu-id="beaa8-217">UrlAuthorization</span></span> | <span data-ttu-id="beaa8-218">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-218">No</span></span> | 
<span data-ttu-id="beaa8-219">UrlMappingsModule</span><span class="sxs-lookup"><span data-stu-id="beaa8-219">UrlMappingsModule</span></span> | <span data-ttu-id="beaa8-220">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-220">No</span></span> | [<span data-ttu-id="beaa8-221">URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="beaa8-221">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)
<span data-ttu-id="beaa8-222">UrlRoutingModule-4.0</span><span class="sxs-lookup"><span data-stu-id="beaa8-222">UrlRoutingModule-4.0</span></span> | <span data-ttu-id="beaa8-223">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-223">No</span></span> | [<span data-ttu-id="beaa8-224">ASP.NET 核心标识</span><span class="sxs-lookup"><span data-stu-id="beaa8-224">ASP.NET Core  Identity</span></span>](xref:security/authentication/identity)
<span data-ttu-id="beaa8-225">WindowsAuthentication</span><span class="sxs-lookup"><span data-stu-id="beaa8-225">WindowsAuthentication</span></span> | <span data-ttu-id="beaa8-226">否</span><span class="sxs-lookup"><span data-stu-id="beaa8-226">No</span></span> | 

## <a name="iis-manager-application-changes"></a><span data-ttu-id="beaa8-227">IIS 管理器应用程序更改</span><span class="sxs-lookup"><span data-stu-id="beaa8-227">IIS Manager application changes</span></span>

<span data-ttu-id="beaa8-228">使用 IIS 管理器配置设置， *web.config*更改应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="beaa8-228">Using IIS Manager to configure settings, the *web.config* file of the app is changed.</span></span> <span data-ttu-id="beaa8-229">如果部署的应用程序并包括*web.config*，使用 IIS 管理器所做的任何更改将被覆盖的部署*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="beaa8-229">If deploying an app and including *web.config*, any changes made with IIS Manger are overwritten by the deployed *web.config* file.</span></span> <span data-ttu-id="beaa8-230">如果在更改服务器的*web.config*文件中，复制已更新*web.config*到本地项目立即的文件。</span><span class="sxs-lookup"><span data-stu-id="beaa8-230">If changes are made to the server's *web.config* file, copy the updated *web.config* file to the local project immediately.</span></span>

## <a name="disabling-iis-modules"></a><span data-ttu-id="beaa8-231">禁用 IIS 模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-231">Disabling IIS modules</span></span>

<span data-ttu-id="beaa8-232">如果必须为一个应用程序的补充，到应用程序的禁用的服务器级别配置的 IIS 模块*web.config*文件可以禁用该模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-232">If an IIS module is configured at the server level that must be disabled for an app, an addition to the app's *web.config* file can disable the module.</span></span> <span data-ttu-id="beaa8-233">将模块保留原位和停用它 （如果可用） 使用配置设置，或者从应用程序中删除模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-233">Either leave the module in place and deactivate it using a configuration setting (if available) or remove the module from the app.</span></span>

### <a name="module-deactivation"></a><span data-ttu-id="beaa8-234">模块停用</span><span class="sxs-lookup"><span data-stu-id="beaa8-234">Module deactivation</span></span>

<span data-ttu-id="beaa8-235">多个模块提供而不从应用删除它们的配置设置，使它们可以禁用它们。</span><span class="sxs-lookup"><span data-stu-id="beaa8-235">Many modules offer a configuration setting that allows them to be disabled them without removing them from the app.</span></span> <span data-ttu-id="beaa8-236">这是最简单且最快速方式停用模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-236">This is the simplest and quickest way to deactivate a module.</span></span> <span data-ttu-id="beaa8-237">例如，如果希望禁用 IIS URL 重写模块，请使用`<httpRedirect>`元素如下所示。</span><span class="sxs-lookup"><span data-stu-id="beaa8-237">For example if wishing to disable the IIS URL Rewrite Module, use the `<httpRedirect>` element as shown below.</span></span> <span data-ttu-id="beaa8-238">禁用使用配置设置的模块的详细信息，请按照中的链接*子元素*部分[IIS `<system.webServer>` ](https://docs.microsoft.com/iis/configuration/system.webServer/)。</span><span class="sxs-lookup"><span data-stu-id="beaa8-238">For more information on disabling modules with configuration settings, follow the links in the *Child Elements* section of [IIS `<system.webServer>`](https://docs.microsoft.com/iis/configuration/system.webServer/).</span></span>

```xml
<configuration>
  <system.webServer>
     <httpRedirect enabled="false" />
  </system.webServer>
</configuration>
```

### <a name="module-removal"></a><span data-ttu-id="beaa8-239">模块删除</span><span class="sxs-lookup"><span data-stu-id="beaa8-239">Module removal</span></span>

<span data-ttu-id="beaa8-240">如果选择加入以移除模块中的设置与*web.config*、 解锁模块和解锁`<modules>`部分*web.config*第一个。</span><span class="sxs-lookup"><span data-stu-id="beaa8-240">If opting to remove a module with a setting in *web.config*, unlock the module and unlock the `<modules>` section of *web.config* first.</span></span> <span data-ttu-id="beaa8-241">步骤如下所述：</span><span class="sxs-lookup"><span data-stu-id="beaa8-241">The steps are outlined below:</span></span>

1. <span data-ttu-id="beaa8-242">解锁的服务器级别的模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-242">Unlock the module at the server level.</span></span> <span data-ttu-id="beaa8-243">在 IIS 管理器在 IIS 服务器上单击**连接**侧栏。</span><span class="sxs-lookup"><span data-stu-id="beaa8-243">Click on the IIS server in the IIS Manager **Connections** sidebar.</span></span> <span data-ttu-id="beaa8-244">打开**模块**中**IIS**区域。</span><span class="sxs-lookup"><span data-stu-id="beaa8-244">Open the **Modules** in the **IIS** area.</span></span> <span data-ttu-id="beaa8-245">单击列表中的模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-245">Click on the module in the list.</span></span> <span data-ttu-id="beaa8-246">在**操作**侧栏右侧，单击**解锁**。</span><span class="sxs-lookup"><span data-stu-id="beaa8-246">In the **Actions** sidebar on the right, click **Unlock**.</span></span> <span data-ttu-id="beaa8-247">解锁任意多个模块按计划从删除*web.config*更高版本。</span><span class="sxs-lookup"><span data-stu-id="beaa8-247">Unlock as many modules as are planned to remove from *web.config* later.</span></span>

2. <span data-ttu-id="beaa8-248">部署应用程序而无需`<modules>`主题中*web.config*。如果应用程序部署与*web.config*包含`<modules>`节不具有解锁部分首先在 IIS 管理器，配置管理器尝试解除锁定节时引发异常。</span><span class="sxs-lookup"><span data-stu-id="beaa8-248">Deploy the app without a `<modules>` section in *web.config*. If an app is deployed with a *web.config* containing the `<modules>` section without having unlocked the section first in the IIS Manager, the Configuration Manager throws an exception when attempting to unlock the section.</span></span> <span data-ttu-id="beaa8-249">因此，部署应用程序而无需`<modules>`部分。</span><span class="sxs-lookup"><span data-stu-id="beaa8-249">Therefore, deploy the app without a `<modules>` section.</span></span>

3. <span data-ttu-id="beaa8-250">解锁`<modules>`部分*web.config*。在**连接**栏中，单击在网站**站点**。</span><span class="sxs-lookup"><span data-stu-id="beaa8-250">Unlock the `<modules>` section of *web.config*. In the **Connections** sidebar, click the website in **Sites**.</span></span> <span data-ttu-id="beaa8-251">在**管理**区域中，打开**配置编辑器**。</span><span class="sxs-lookup"><span data-stu-id="beaa8-251">In the **Management** area, open the **Configuration Editor**.</span></span> <span data-ttu-id="beaa8-252">使用导航控件选择`system.webServer/modules`部分。</span><span class="sxs-lookup"><span data-stu-id="beaa8-252">Use the navigation controls to select the `system.webServer/modules` section.</span></span> <span data-ttu-id="beaa8-253">在**操作**侧栏右侧，单击到**解锁**部分。</span><span class="sxs-lookup"><span data-stu-id="beaa8-253">In the **Actions** sidebar on the right, click to **Unlock** the section.</span></span>

4. <span data-ttu-id="beaa8-254">此时，`<modules>`部分可以添加到*web.config*文件`<remove>`元素从应用中删除该模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-254">At this point, a `<modules>` section can be added to the *web.config* file with a `<remove>` element to remove the module from the app.</span></span> <span data-ttu-id="beaa8-255">多个`<remove>`可添加元素以移除多个模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-255">Multiple `<remove>` elements can be added to remove multiple modules.</span></span> <span data-ttu-id="beaa8-256">不要忘记，如果*web.config*更改服务器上立即进行本地项目中。</span><span class="sxs-lookup"><span data-stu-id="beaa8-256">Don't forget that if *web.config* changes are made on the server to make them immediately in the project locally.</span></span> <span data-ttu-id="beaa8-257">删除这种方式的模块不会影响服务器上的其他应用的模块使用。</span><span class="sxs-lookup"><span data-stu-id="beaa8-257">Removing a module this way won't affect the use of the module with other apps on the server.</span></span>

  ```xml
  <configuration> 
    <system.webServer> 
      <modules> 
        <remove name="MODULE_NAME" /> 
      </modules> 
    </system.webServer> 
  </configuration>
  ```

<span data-ttu-id="beaa8-258">对于与默认模块安装 IIS 安装，使用以下`<module>`部分，以移除默认模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-258">For an IIS installation with the default modules installed, use the following `<module>` section to remove the default modules.</span></span>

```xml
<modules>
  <remove name="CustomErrorModule" />
  <remove name="DefaultDocumentModule" />
  <remove name="DirectoryListingModule" />
  <remove name="HttpCacheModule" />
  <remove name="HttpLoggingModule" />
  <remove name="ProtocolSupportModule" />
  <remove name="RequestFilteringModule" />
  <remove name="StaticCompressionModule" /> 
  <remove name="StaticFileModule" /> 
</modules>
```

<span data-ttu-id="beaa8-259">IIS 模块也可能会删除与*Appcmd.exe*。</span><span class="sxs-lookup"><span data-stu-id="beaa8-259">An IIS module can also be removed with *Appcmd.exe*.</span></span> <span data-ttu-id="beaa8-260">提供`MODULE_NAME`和`APPLICATION_NAME`中下面显示的命令：</span><span class="sxs-lookup"><span data-stu-id="beaa8-260">Provide the `MODULE_NAME` and `APPLICATION_NAME` in the command shown below:</span></span>

```console
Appcmd.exe delete module MODULE_NAME /app.name:APPLICATION_NAME
```

<span data-ttu-id="beaa8-261">下面介绍了如何删除`DynamicCompressionModule`从默认网站：</span><span class="sxs-lookup"><span data-stu-id="beaa8-261">Here's how to remove the `DynamicCompressionModule` from the Default Web Site:</span></span>

```console
%windir%\system32\inetsrv\appcmd.exe delete module DynamicCompressionModule /app.name:"Default Web Site"
```

## <a name="minimum-module-configuration"></a><span data-ttu-id="beaa8-262">最小模块配置</span><span class="sxs-lookup"><span data-stu-id="beaa8-262">Minimum module configuration</span></span>

<span data-ttu-id="beaa8-263">若要运行 ASP.NET Core 应用所需的唯一模块是匿名身份验证模块和 ASP.NET 核心模块。</span><span class="sxs-lookup"><span data-stu-id="beaa8-263">The only modules required to run an ASP.NET Core app are the Anonymous Authentication Module and the ASP.NET Core Module.</span></span>

![显示最少模块配置到模块打开 IIS 管理器](modules/_static/modules.png)

## <a name="additional-resources"></a><span data-ttu-id="beaa8-265">其他资源</span><span class="sxs-lookup"><span data-stu-id="beaa8-265">Additional resources</span></span>

* [<span data-ttu-id="beaa8-266">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="beaa8-266">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="beaa8-267">IIS 模块概述</span><span class="sxs-lookup"><span data-stu-id="beaa8-267">IIS Modules Overview</span></span>](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
* [<span data-ttu-id="beaa8-268">自定义 IIS 7.0 角色和模块</span><span class="sxs-lookup"><span data-stu-id="beaa8-268">Customizing IIS 7.0 Roles and Modules</span></span>](https://technet.microsoft.com/library/cc627313.aspx)
* [<span data-ttu-id="beaa8-269">IIS `<system.webServer>`</span><span class="sxs-lookup"><span data-stu-id="beaa8-269">IIS `<system.webServer>`</span></span>](https://docs.microsoft.com/iis/configuration/system.webServer/)
