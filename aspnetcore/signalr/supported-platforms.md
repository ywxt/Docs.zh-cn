---
title: ASP.NET Core SignalR 支持的平台
author: tdykstra
description: ASP.NET Core SignalR 的受支持的平台
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/26/2018
uid: signalr/supported-platforms
ms.openlocfilehash: d6d74a55d35ddb34a6f66a171bfe3f343dd61b63
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577621"
---
# <a name="aspnet-core-signalr-supported-platforms"></a><span data-ttu-id="a5b03-103">ASP.NET Core SignalR 支持的平台</span><span class="sxs-lookup"><span data-stu-id="a5b03-103">ASP.NET Core SignalR supported platforms</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="a5b03-104">服务器系统要求</span><span class="sxs-lookup"><span data-stu-id="a5b03-104">Server system requirements</span></span>

<span data-ttu-id="a5b03-105">ASP.NET Core SignalR 支持 ASP.NET Core 所支持的任何服务器平台。</span><span class="sxs-lookup"><span data-stu-id="a5b03-105">SignalR for ASP.NET Core supports any server platform ASP.NET Core supports.</span></span>

## <a name="javascript-client"></a><span data-ttu-id="a5b03-106">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-106">JavaScript client</span></span>

<span data-ttu-id="a5b03-107">[JavaScript 客户端](https://www.npmjs.com/package/@aspnet/signalr)NodeJS 8 和更高版本和以下浏览器上运行：</span><span class="sxs-lookup"><span data-stu-id="a5b03-107">The [JavaScript client](https://www.npmjs.com/package/@aspnet/signalr) runs on NodeJS 8 and later versions and the following browsers:</span></span>

| <span data-ttu-id="a5b03-108">浏览者</span><span class="sxs-lookup"><span data-stu-id="a5b03-108">Browser</span></span> | <span data-ttu-id="a5b03-109">版本</span><span class="sxs-lookup"><span data-stu-id="a5b03-109">Version</span></span> |
| ------- | ------- |
| <span data-ttu-id="a5b03-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="a5b03-110">Microsoft Edge</span></span> | <span data-ttu-id="a5b03-111">当前</span><span class="sxs-lookup"><span data-stu-id="a5b03-111">current</span></span> |
| <span data-ttu-id="a5b03-112">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="a5b03-112">Mozilla Firefox</span></span> | <span data-ttu-id="a5b03-113">当前</span><span class="sxs-lookup"><span data-stu-id="a5b03-113">current</span></span> |
| <span data-ttu-id="a5b03-114">Google Chrome;包括 Android</span><span class="sxs-lookup"><span data-stu-id="a5b03-114">Google Chrome; includes Android</span></span> | <span data-ttu-id="a5b03-115">当前</span><span class="sxs-lookup"><span data-stu-id="a5b03-115">current</span></span> |
| <span data-ttu-id="a5b03-116">Safari;包含 iOS</span><span class="sxs-lookup"><span data-stu-id="a5b03-116">Safari; includes iOS</span></span> | <span data-ttu-id="a5b03-117">当前</span><span class="sxs-lookup"><span data-stu-id="a5b03-117">current</span></span> |
| <span data-ttu-id="a5b03-118">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a5b03-118">Microsoft Internet Explorer</span></span> | <span data-ttu-id="a5b03-119">11</span><span class="sxs-lookup"><span data-stu-id="a5b03-119">11</span></span> |
 
## <a name="net-client"></a><span data-ttu-id="a5b03-120">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-120">.NET client</span></span>

<span data-ttu-id="a5b03-121">[.NET 客户端](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/)在 ASP.NET Core 支持的任何服务器平台上运行。</span><span class="sxs-lookup"><span data-stu-id="a5b03-121">The [.NET client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) runs on any server platform supported by ASP.NET Core.</span></span>

<span data-ttu-id="a5b03-122">当服务器运行的 IIS 时，Websocket 传输要求安装 IIS 8.0 或更高版本，Windows Server 2012 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="a5b03-122">When the server runs IIS, the WebSockets transport requires IIS 8.0 or higher, on Windows Server 2012 or higher.</span></span> <span data-ttu-id="a5b03-123">其他传输在所有平台上都受支持。</span><span class="sxs-lookup"><span data-stu-id="a5b03-123">Other transports are supported on all platforms.</span></span>

## <a name="java-client"></a><span data-ttu-id="a5b03-124">Java 客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-124">Java client</span></span>

<span data-ttu-id="a5b03-125">[Java 客户端](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)支持 Java 8 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="a5b03-125">The [Java client](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) supports Java 8 and later versions.</span></span>

## <a name="unsupported-clients"></a><span data-ttu-id="a5b03-126">不受支持的客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-126">Unsupported clients</span></span>

<span data-ttu-id="a5b03-127">以下客户端可用，但会实验性的或非官方。</span><span class="sxs-lookup"><span data-stu-id="a5b03-127">The following clients are available but are experimental or unofficial.</span></span> <span data-ttu-id="a5b03-128">它们目前不支持和以往可能不支持。</span><span class="sxs-lookup"><span data-stu-id="a5b03-128">They are not supported now and may not ever be supported.</span></span>

* [<span data-ttu-id="a5b03-129">C + + 客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-129">C++ client</span></span>](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [<span data-ttu-id="a5b03-130">Swift 的客户端</span><span class="sxs-lookup"><span data-stu-id="a5b03-130">Swift client</span></span>](https://github.com/moozzyk/SignalR-Client-Swift)
