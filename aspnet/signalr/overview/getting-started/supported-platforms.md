---
uid: signalr/overview/getting-started/supported-platforms
title: "受支持的平台 |Microsoft 文档"
author: pfletcher
description: "本指南介绍了 SignalR 支持哪些客户端和服务器。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 1379b9fb638f67896d88d7aa4312d95280ef7318
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
<a name="supported-platforms"></a><span data-ttu-id="4177f-103">支持的平台</span><span class="sxs-lookup"><span data-stu-id="4177f-103">Supported Platforms</span></span>
====================
<span data-ttu-id="4177f-104">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="4177f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="4177f-105">本指南介绍了 SignalR 支持哪些客户端和服务器。</span><span class="sxs-lookup"><span data-stu-id="4177f-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="4177f-106">问题和意见</span><span class="sxs-lookup"><span data-stu-id="4177f-106">Questions and comments</span></span>
> 
> <span data-ttu-id="4177f-107">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="4177f-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4177f-108">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="4177f-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="4177f-109">SignalR 支持在各种服务器和客户端配置下。</span><span class="sxs-lookup"><span data-stu-id="4177f-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="4177f-110">此外，每个传输选项具有一组自己的; 的要求如果传输的系统要求不可用，SignalR 会顺利地故障转移到其他传输。</span><span class="sxs-lookup"><span data-stu-id="4177f-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="4177f-111">有关 SignalR 支持的传输的详细信息，请参阅[传输和回退](introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="4177f-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="4177f-112">服务器系统要求</span><span class="sxs-lookup"><span data-stu-id="4177f-112">Server system requirements</span></span>

<span data-ttu-id="4177f-113">可以在各种服务器配置上承载的 SignalR 服务器组件。</span><span class="sxs-lookup"><span data-stu-id="4177f-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="4177f-114">本部分介绍支持的操作系统、.NET framework、 Internet 信息服务器和其他组件版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="4177f-115">支持的服务器操作系统</span><span class="sxs-lookup"><span data-stu-id="4177f-115">Supported server operating systems</span></span>

<span data-ttu-id="4177f-116">SignalR 服务器组件可以承载于以下服务器或客户端操作系统。</span><span class="sxs-lookup"><span data-stu-id="4177f-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="4177f-117">请注意，适用于 SignalR 使用 Websocket，Windows Server 2012 或 Windows 8 需要 （WebSocket 可以使用 Windows Azure 网站上，只要该站点的.NET framework 版本设置为 4.5，并且在站点的配置页中启用 Web 套接字）。</span><span class="sxs-lookup"><span data-stu-id="4177f-117">Note that for SignalR to use WebSockets, Windows Server 2012 or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="4177f-118">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4177f-118">Windows Server 2012</span></span>
- <span data-ttu-id="4177f-119">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="4177f-119">Windows Server 2008 r2</span></span>
- <span data-ttu-id="4177f-120">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4177f-120">Windows 10</span></span>
- <span data-ttu-id="4177f-121">Windows 8</span><span class="sxs-lookup"><span data-stu-id="4177f-121">Windows 8</span></span>
- <span data-ttu-id="4177f-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4177f-122">Windows 7</span></span>
- <span data-ttu-id="4177f-123">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4177f-123">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="4177f-124">支持的服务器.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="4177f-124">Supported server .NET Framework version</span></span>

<span data-ttu-id="4177f-125">在.NET Framework 4.5 上仅支持 SignalR 2。</span><span class="sxs-lookup"><span data-stu-id="4177f-125">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="4177f-126">请参阅[推荐的更新](#updates)增强可靠性、 兼容性、 稳定性和性能的更新的部分。</span><span class="sxs-lookup"><span data-stu-id="4177f-126">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="4177f-127">支持的服务器的 IIS 版本</span><span class="sxs-lookup"><span data-stu-id="4177f-127">Supported server IIS versions</span></span>

<span data-ttu-id="4177f-128">当 SignalR 承载于 IIS 中时，支持以下版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-128">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="4177f-129">请注意，是否使用客户端操作系统，例如用于开发 （Windows 8 或 Windows 7） 的完整版本的 IIS 或 Cassini 不应，因为将有 10 个并发连接的施加，这将非常快速地达到自连接以来的限制暂时性故障，频繁重新建立，而不会释放，立即在不再使用。</span><span class="sxs-lookup"><span data-stu-id="4177f-129">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="4177f-130">客户端操作系统上，应使用 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="4177f-130">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="4177f-131">此外请注意，适用于 SignalR 使用 WebSocket，必须使用 IIS 8 或 IIS 8 Express，服务器必须使用 Windows 8、 Windows Server 2012 或更高版本，必须在 IIS 中启用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="4177f-131">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="4177f-132">有关如何启用 WebSocket 在 IIS 中的信息，请参阅[IIS 8.0 WebSocket 协议支持](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。</span><span class="sxs-lookup"><span data-stu-id="4177f-132">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="4177f-133">IIS 8 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="4177f-133">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="4177f-134">IIS 7 和 7.5。</span><span class="sxs-lookup"><span data-stu-id="4177f-134">IIS 7 and 7.5.</span></span> <span data-ttu-id="4177f-135">支持[无扩展名的 Url](https://support.microsoft.com/kb/980368)是必需的。</span><span class="sxs-lookup"><span data-stu-id="4177f-135">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="4177f-136">IIS 必须运行在集成模式下;不支持经典模式。</span><span class="sxs-lookup"><span data-stu-id="4177f-136">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="4177f-137">如果在使用 Server-Sent 事件传输的经典模式下运行 IIS，可能遇到的最多 30 秒的消息延迟。</span><span class="sxs-lookup"><span data-stu-id="4177f-137">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="4177f-138">在承载应用程序必须在完全信任模式下运行。</span><span class="sxs-lookup"><span data-stu-id="4177f-138">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="4177f-139">客户端系统要求</span><span class="sxs-lookup"><span data-stu-id="4177f-139">Client system requirements</span></span>

<span data-ttu-id="4177f-140">SignalR 可在各种客户端平台。</span><span class="sxs-lookup"><span data-stu-id="4177f-140">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="4177f-141">本部分介绍有关在 web 浏览器、 Windows 桌面应用程序、 Silverlight 应用程序和移动设备使用 SignalR 的系统要求。</span><span class="sxs-lookup"><span data-stu-id="4177f-141">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="4177f-142">Web 浏览器</span><span class="sxs-lookup"><span data-stu-id="4177f-142">Web browsers</span></span>

<span data-ttu-id="4177f-143">SignalR 可在各种 web 浏览器，但通常情况下，支持的最新两个版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-143">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="4177f-144">使用 SignalR 在浏览器中的应用程序必须使用 jQuery 版本 1.6.4 或主要更高版本 （如 1.7.2、 1.8.2 或 1.9.1）。</span><span class="sxs-lookup"><span data-stu-id="4177f-144">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="4177f-145">SignalR 可在以下浏览器：</span><span class="sxs-lookup"><span data-stu-id="4177f-145">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="4177f-146">Microsoft Internet Explorer 版本 8、 9、 10 和 11。</span><span class="sxs-lookup"><span data-stu-id="4177f-146">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="4177f-147">现代，桌面版和移动版本支持。</span><span class="sxs-lookup"><span data-stu-id="4177f-147">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="4177f-148">Mozilla Firefox： 当前版本-1，Windows 和 Mac 版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-148">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="4177f-149">Google Chrome： 当前版本-1，Windows 和 Mac 版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-149">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="4177f-150">Safari： 当前版本-1，Mac 和 iOS 版本。</span><span class="sxs-lookup"><span data-stu-id="4177f-150">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="4177f-151">Opera： 当前版本-1，仅限 Windows。</span><span class="sxs-lookup"><span data-stu-id="4177f-151">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="4177f-152">Android 浏览器</span><span class="sxs-lookup"><span data-stu-id="4177f-152">Android browser</span></span>

<span data-ttu-id="4177f-153">除了需要某些浏览器，SignalR 使用各种传输具有其自己的要求。</span><span class="sxs-lookup"><span data-stu-id="4177f-153">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="4177f-154">下列传输支持在以下配置：</span><span class="sxs-lookup"><span data-stu-id="4177f-154">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="4177f-155">**Web 浏览器传输要求**</span><span class="sxs-lookup"><span data-stu-id="4177f-155">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="4177f-156">传输</span><span class="sxs-lookup"><span data-stu-id="4177f-156">Transport</span></span> | <span data-ttu-id="4177f-157">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4177f-157">Internet Explorer</span></span> | <span data-ttu-id="4177f-158">Chrome （Windows 或 iOS）</span><span class="sxs-lookup"><span data-stu-id="4177f-158">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="4177f-159">Firefox</span><span class="sxs-lookup"><span data-stu-id="4177f-159">Firefox</span></span> | <span data-ttu-id="4177f-160">Safari （OSX 或 iOS）</span><span class="sxs-lookup"><span data-stu-id="4177f-160">Safari (OSX or iOS)</span></span> | <span data-ttu-id="4177f-161">Android</span><span class="sxs-lookup"><span data-stu-id="4177f-161">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4177f-162">WebSockets</span><span class="sxs-lookup"><span data-stu-id="4177f-162">WebSockets</span></span> | <span data-ttu-id="4177f-163">10+</span><span class="sxs-lookup"><span data-stu-id="4177f-163">10+</span></span> | <span data-ttu-id="4177f-164">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-164">current - 1</span></span> | <span data-ttu-id="4177f-165">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-165">current - 1</span></span> | <span data-ttu-id="4177f-166">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-166">current - 1</span></span> | <span data-ttu-id="4177f-167">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-167">N/A</span></span> |
| <span data-ttu-id="4177f-168">服务器发送事件</span><span class="sxs-lookup"><span data-stu-id="4177f-168">Server-Sent Events</span></span> | <span data-ttu-id="4177f-169">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-169">N/A</span></span> | <span data-ttu-id="4177f-170">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-170">current - 1</span></span> | <span data-ttu-id="4177f-171">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-171">current - 1</span></span> | <span data-ttu-id="4177f-172">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-172">current - 1</span></span> | <span data-ttu-id="4177f-173">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-173">N/A</span></span> |
| <span data-ttu-id="4177f-174">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="4177f-174">ForeverFrame</span></span> | <span data-ttu-id="4177f-175">8+</span><span class="sxs-lookup"><span data-stu-id="4177f-175">8+</span></span> | <span data-ttu-id="4177f-176">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-176">N/A</span></span> | <span data-ttu-id="4177f-177">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-177">N/A</span></span> | <span data-ttu-id="4177f-178">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-178">N/A</span></span> | <span data-ttu-id="4177f-179">4.1</span><span class="sxs-lookup"><span data-stu-id="4177f-179">4.1</span></span> |
| <span data-ttu-id="4177f-180">长轮询</span><span class="sxs-lookup"><span data-stu-id="4177f-180">Long Polling</span></span> | <span data-ttu-id="4177f-181">8+</span><span class="sxs-lookup"><span data-stu-id="4177f-181">8+</span></span> | <span data-ttu-id="4177f-182">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-182">current - 1</span></span> | <span data-ttu-id="4177f-183">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-183">current - 1</span></span> | <span data-ttu-id="4177f-184">当前值-1</span><span class="sxs-lookup"><span data-stu-id="4177f-184">current - 1</span></span> | <span data-ttu-id="4177f-185">4.1</span><span class="sxs-lookup"><span data-stu-id="4177f-185">4.1</span></span> |

<span data-ttu-id="4177f-186">\*: 6 + 所需的全部功能。</span><span class="sxs-lookup"><span data-stu-id="4177f-186">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="4177f-187">不受支持的浏览器</span><span class="sxs-lookup"><span data-stu-id="4177f-187">Unsupported Browsers</span></span>

<span data-ttu-id="4177f-188">尽管 SignalR*可能*运行时未出现在旧的浏览器版本的主要问题，我们不主动测试 SignalR 在其中，通常不修复可能在它们中出现的 bug。</span><span class="sxs-lookup"><span data-stu-id="4177f-188">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="4177f-189">Windows 桌面和 Silverlight 应用程序</span><span class="sxs-lookup"><span data-stu-id="4177f-189">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="4177f-190">除了在 web 浏览器中运行，SignalR 可以承载于独立 Windows 客户端或 Silverlight 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4177f-190">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="4177f-191">Windows 桌面版和 Silverlight SignalR 应用程序具有以下系统要求。</span><span class="sxs-lookup"><span data-stu-id="4177f-191">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="4177f-192">Windows XP SP3 或更高版本支持使用.NET 4 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4177f-192">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="4177f-193">Windows Vista 或更高版本支持应用程序使用.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="4177f-193">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="4177f-194">除了操作系统和.NET framework 的要求，供 SignalR 传输都具有其自己的要求。</span><span class="sxs-lookup"><span data-stu-id="4177f-194">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="4177f-195">下列传输支持在以下配置：</span><span class="sxs-lookup"><span data-stu-id="4177f-195">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="4177f-196">**Windows 桌面版和 Silverlight 传输要求**</span><span class="sxs-lookup"><span data-stu-id="4177f-196">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="4177f-197">传输</span><span class="sxs-lookup"><span data-stu-id="4177f-197">Transport</span></span> | <span data-ttu-id="4177f-198">.NET 应用程序</span><span class="sxs-lookup"><span data-stu-id="4177f-198">.NET application</span></span> | <span data-ttu-id="4177f-199">Silverlight</span><span class="sxs-lookup"><span data-stu-id="4177f-199">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4177f-200">Web 套接字</span><span class="sxs-lookup"><span data-stu-id="4177f-200">Web Sockets</span></span> | <span data-ttu-id="4177f-201">Windows 8 + 和.NET 4.5 +</span><span class="sxs-lookup"><span data-stu-id="4177f-201">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="4177f-202">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-202">N/A</span></span> |
| <span data-ttu-id="4177f-203">不限次数帧</span><span class="sxs-lookup"><span data-stu-id="4177f-203">Forever Frame</span></span> | <span data-ttu-id="4177f-204">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-204">N/A</span></span> | <span data-ttu-id="4177f-205">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-205">N/A</span></span> |
| <span data-ttu-id="4177f-206">服务器发送事件</span><span class="sxs-lookup"><span data-stu-id="4177f-206">Server-Sent Events</span></span> | <span data-ttu-id="4177f-207">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="4177f-207">.NET 4+</span></span> | <span data-ttu-id="4177f-208">5+</span><span class="sxs-lookup"><span data-stu-id="4177f-208">5+</span></span> |
| <span data-ttu-id="4177f-209">长轮询</span><span class="sxs-lookup"><span data-stu-id="4177f-209">Long Polling</span></span> | <span data-ttu-id="4177f-210">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="4177f-210">.NET 4+</span></span> | <span data-ttu-id="4177f-211">5+</span><span class="sxs-lookup"><span data-stu-id="4177f-211">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="4177f-212">Windows 应用商店和 Windows Phone 应用程序</span><span class="sxs-lookup"><span data-stu-id="4177f-212">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="4177f-213">SignalR 可在 Windows 应用商店应用程序和 Windows Phone 8 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4177f-213">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="4177f-214">下列传输支持在以下配置：</span><span class="sxs-lookup"><span data-stu-id="4177f-214">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="4177f-215">**Windows 应用商店和 Windows Phone 传输要求**</span><span class="sxs-lookup"><span data-stu-id="4177f-215">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="4177f-216">传输</span><span class="sxs-lookup"><span data-stu-id="4177f-216">Transport</span></span> | <span data-ttu-id="4177f-217">Windows 应用商店 /.NET</span><span class="sxs-lookup"><span data-stu-id="4177f-217">Windows Store/ .NET</span></span> | <span data-ttu-id="4177f-218">Windows 应用商店 / JavaScript</span><span class="sxs-lookup"><span data-stu-id="4177f-218">Windows Store/ JavaScript</span></span> | <span data-ttu-id="4177f-219">Windows Phone/ IE</span><span class="sxs-lookup"><span data-stu-id="4177f-219">Windows Phone/ IE</span></span> | <span data-ttu-id="4177f-220">Windows Phone/ .NET</span><span class="sxs-lookup"><span data-stu-id="4177f-220">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="4177f-221">WebSockets</span><span class="sxs-lookup"><span data-stu-id="4177f-221">WebSockets</span></span> | <span data-ttu-id="4177f-222">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-222">N/A</span></span> | <span data-ttu-id="4177f-223">Win8+</span><span class="sxs-lookup"><span data-stu-id="4177f-223">Win8+</span></span> | <span data-ttu-id="4177f-224">8+</span><span class="sxs-lookup"><span data-stu-id="4177f-224">8+</span></span> | <span data-ttu-id="4177f-225">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-225">N/A</span></span> |
| <span data-ttu-id="4177f-226">不限次数帧</span><span class="sxs-lookup"><span data-stu-id="4177f-226">Forever Frame</span></span> | <span data-ttu-id="4177f-227">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-227">N/A</span></span> | <span data-ttu-id="4177f-228">Win8+</span><span class="sxs-lookup"><span data-stu-id="4177f-228">Win8+</span></span> | <span data-ttu-id="4177f-229">7.5+</span><span class="sxs-lookup"><span data-stu-id="4177f-229">7.5+</span></span> | <span data-ttu-id="4177f-230">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-230">N/A</span></span> |
| <span data-ttu-id="4177f-231">服务器发送事件</span><span class="sxs-lookup"><span data-stu-id="4177f-231">Server-Sent Events</span></span> | <span data-ttu-id="4177f-232">Win8+</span><span class="sxs-lookup"><span data-stu-id="4177f-232">Win8+</span></span> | <span data-ttu-id="4177f-233">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-233">N/A</span></span> | <span data-ttu-id="4177f-234">不可用</span><span class="sxs-lookup"><span data-stu-id="4177f-234">N/A</span></span> | <span data-ttu-id="4177f-235">8+</span><span class="sxs-lookup"><span data-stu-id="4177f-235">8+</span></span> |
| <span data-ttu-id="4177f-236">长轮询</span><span class="sxs-lookup"><span data-stu-id="4177f-236">Long Polling</span></span> | <span data-ttu-id="4177f-237">Win8+</span><span class="sxs-lookup"><span data-stu-id="4177f-237">Win8+</span></span> | <span data-ttu-id="4177f-238">Win8+</span><span class="sxs-lookup"><span data-stu-id="4177f-238">Win8+</span></span> | <span data-ttu-id="4177f-239">7.5+</span><span class="sxs-lookup"><span data-stu-id="4177f-239">7.5+</span></span> | <span data-ttu-id="4177f-240">8+</span><span class="sxs-lookup"><span data-stu-id="4177f-240">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="4177f-241">建议的更新</span><span class="sxs-lookup"><span data-stu-id="4177f-241">Recommended Updates</span></span>

<span data-ttu-id="4177f-242">建议进行 SignalR 服务器以下更新：</span><span class="sxs-lookup"><span data-stu-id="4177f-242">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="4177f-243">有可用的.NET Framework 4.5 的更新[此处](https://support.microsoft.com/kb/2750149)。</span><span class="sxs-lookup"><span data-stu-id="4177f-243">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="4177f-244">对于 ASP.NET，Microsoft 将定期发布 Qfe。</span><span class="sxs-lookup"><span data-stu-id="4177f-244">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="4177f-245">这些应应用为可用。</span><span class="sxs-lookup"><span data-stu-id="4177f-245">These should be applied as available.</span></span>
