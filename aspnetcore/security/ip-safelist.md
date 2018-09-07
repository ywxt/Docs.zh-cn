---
title: 适用于 ASP.NET Core 的客户端 IP 安全列表
author: damienbod
description: 了解如何编写中间件或操作筛选器来验证针对一组已批准的 IP 地址的远程 IP 地址。
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/31/2018
uid: security/ip-safelist
ms.openlocfilehash: 40fe7b67359efd1692490099c3fb529ba4a6148f
ms.sourcegitcommit: 08bf41d4b3e696ab512b044970e8304816f8cc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040104"
---
# <a name="client-ip-safelist-for-aspnet-core"></a><span data-ttu-id="9e0cc-103">适用于 ASP.NET Core 的客户端 IP 安全列表</span><span class="sxs-lookup"><span data-stu-id="9e0cc-103">Client IP safelist for ASP.NET Core</span></span>

<span data-ttu-id="9e0cc-104">通过[Damien Bowden](https://twitter.com/damien_bod)和[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9e0cc-104">By [Damien Bowden](https://twitter.com/damien_bod) and [Tom Dykstra](https://github.com/tdykstra)</span></span>
 
<span data-ttu-id="9e0cc-105">本文介绍两种方法来实现 IP 安全列表 （也称为允许列表）：</span><span class="sxs-lookup"><span data-stu-id="9e0cc-105">This article shows two ways to implement an IP safelist (also known as a whitelist):</span></span>

* <span data-ttu-id="9e0cc-106">通过使用 ASP.NET Core 中间件检查每个请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-106">By using ASP.NET Core middleware to check the remote IP address of every request.</span></span>
* <span data-ttu-id="9e0cc-107">通过使用 ASP.NET Core 操作筛选器检查的特定操作方法的请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-107">By using ASP.NET Core action filters to check the remote IP address of requests for specific action methods.</span></span>

<span data-ttu-id="9e0cc-108">示例应用程序说明了这两种方法。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-108">The sample app illustrates both approaches.</span></span> <span data-ttu-id="9e0cc-109">在每种情况下，包含已批准的客户端 IP 地址的字符串存储在一个应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-109">In each case, a string containing approved client IP addresses is stored in an app setting.</span></span> <span data-ttu-id="9e0cc-110">中间件或筛选器将字符串分析为列表，并检查远程 IP 是否在列表中。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-110">The middleware or filter parses the string into a list and  checks if the remote IP is in the list.</span></span> <span data-ttu-id="9e0cc-111">如果没有，则返回 HTTP 403 禁止访问状态代码。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-111">If not, an HTTP 403 Forbidden status code is returned.</span></span>

<span data-ttu-id="9e0cc-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/ip-safelist/samples/2.x/ClientIpAspNetCore)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="9e0cc-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/ip-safelist/samples/2.x/ClientIpAspNetCore) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="the-safelist"></a><span data-ttu-id="9e0cc-113">安全列表</span><span class="sxs-lookup"><span data-stu-id="9e0cc-113">The safelist</span></span>

<span data-ttu-id="9e0cc-114">在配置列表*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-114">The list is configured in the *appsettings.json* file.</span></span> <span data-ttu-id="9e0cc-115">它是以分号分隔的列表，并且可以包含 IPv4 和 IPv6 地址。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-115">It's a semicolon-delimited list and can contain IPv4 and IPv6 addresses.</span></span>

[!code-json[](ip-safelist/samples/2.x/ClientIpAspNetCore/appsettings.json?highlight=2)]

## <a name="middleware"></a><span data-ttu-id="9e0cc-116">中间件</span><span class="sxs-lookup"><span data-stu-id="9e0cc-116">Middleware</span></span>

<span data-ttu-id="9e0cc-117">`Configure`方法添加中间件，并向其构造函数参数中传递的安全列表的字符串。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-117">The `Configure` method adds the middleware and passes the safelist string to it in a constructor parameter.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_Configure&highlight=7)]

<span data-ttu-id="9e0cc-118">中间件将字符串分析为一个数组，并查找数组中的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-118">The middleware parses the string into an array and looks for the remote IP address in the array.</span></span> <span data-ttu-id="9e0cc-119">如果找不到的远程 IP 地址，中间件返回 HTTP 401 禁止访问。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-119">If the remote IP address is not found, the middleware returns HTTP 401 Forbidden.</span></span> <span data-ttu-id="9e0cc-120">对于 HTTP Get 请求跳过此验证过程。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-120">This validation process is bypassed for HTTP Get requests.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/AdminSafeListMiddleware.cs?name=snippet_ClassOnly)]

## <a name="action-filter"></a><span data-ttu-id="9e0cc-121">操作筛选器</span><span class="sxs-lookup"><span data-stu-id="9e0cc-121">Action filter</span></span>

<span data-ttu-id="9e0cc-122">如果您希望仅为特定控制器或操作方法的安全列表，请使用操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-122">If you want a safelist only for specific controllers or action methods, use an action filter.</span></span> <span data-ttu-id="9e0cc-123">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="9e0cc-123">Here's an example:</span></span> 

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Filters/ClientIdCheckFilter.cs)]

<span data-ttu-id="9e0cc-124">操作筛选器添加到服务容器。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-124">The action filter is added to the services container.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

<span data-ttu-id="9e0cc-125">然后可以在控制器或操作方法上使用筛选器。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-125">The filter can then be used on a controller or action method.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Controllers/ValuesController.cs?name=snippet_Filter&highlight=1)]

<span data-ttu-id="9e0cc-126">在示例应用中，筛选器应用于`Get`方法。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-126">In the sample app, the filter is applied to the `Get` method.</span></span> <span data-ttu-id="9e0cc-127">因此，当您测试应用程序通过发送`Get`API 请求，该属性就验证客户端 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-127">So when you test the app by sending a `Get` API request, the attribute is validating the client IP address.</span></span> <span data-ttu-id="9e0cc-128">当测试通过使用任何其他 HTTP 方法调用的 API 时，中间件就验证客户端 IP。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-128">When you test by calling the API with any other HTTP method, the middleware is validating the client IP.</span></span>

## <a name="razor-pages-filter"></a><span data-ttu-id="9e0cc-129">Razor 页面筛选器</span><span class="sxs-lookup"><span data-stu-id="9e0cc-129">Razor Pages filter</span></span> 

<span data-ttu-id="9e0cc-130">如果你想为 Razor 页面应用的安全列表，使用 Razor 页面筛选器。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-130">If you want a safelist for a Razor Pages app, use a Razor Pages filter.</span></span> <span data-ttu-id="9e0cc-131">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="9e0cc-131">Here's an example:</span></span> 

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Filters/ClientIdCheckPageFilter.cs)]

<span data-ttu-id="9e0cc-132">通过将其添加到 MVC 筛选器集合启用该筛选器。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-132">This filter is enabled by adding it to the MVC Filters collection.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

<span data-ttu-id="9e0cc-133">当您运行该应用程序，并请求 Razor 页面时，Razor 页面筛选器就验证客户端 IP。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-133">When you run the app and request a Razor page, the Razor Pages filter is validating the client IP.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e0cc-134">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9e0cc-134">Next steps</span></span>

<span data-ttu-id="9e0cc-135">[了解有关 ASP.NET Core 中间件的详细信息](xref:fundamentals/middleware/index)。</span><span class="sxs-lookup"><span data-stu-id="9e0cc-135">[Learn more about ASP.NET Core Middleware](xref:fundamentals/middleware/index).</span></span>
