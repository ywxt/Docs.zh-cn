---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[如何实现:] 缓存 ASP.NET 页面根据 HTTP 标头中的信息 |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何使基于页面的 HTTP 标头中的信息在 ASP.NET 输出缓存中的页面。 首先，潜在的 HTTP 页眉...
ms.author: aspnetcontent
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 64c5c1d82376b1a3ef7c4423c3b3a372ce5ab238
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821452"
---
<a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="5344f-104">[如何实现:] 缓存 ASP.NET 页面根据 HTTP 标头中的信息</span><span class="sxs-lookup"><span data-stu-id="5344f-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>
====================
<span data-ttu-id="5344f-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="5344f-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="5344f-106">在此视频的 Chris Pels 中显示了如何使基于页面的 HTTP 标头中的信息在 ASP.NET 输出缓存中的页面。</span><span class="sxs-lookup"><span data-stu-id="5344f-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="5344f-107">首先，可能的 HTTP 标头值已经过评审。</span><span class="sxs-lookup"><span data-stu-id="5344f-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="5344f-108">然后，创建了一个示例页，并随后将 OutputCache 指令用于 VaryByHeader 特性包含一个值为"接受的语言"，一个 HTTP 标头，来控制缓存基于用户的浏览器的语言。</span><span class="sxs-lookup"><span data-stu-id="5344f-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="5344f-109">在 IE 中设置为英语，然后在设置为使用法语的 FireFox 中查看示例页面。</span><span class="sxs-lookup"><span data-stu-id="5344f-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="5344f-110">最后，若要将缓存定义移到 CacheProfile web.config 文件中的选项进行讨论。</span><span class="sxs-lookup"><span data-stu-id="5344f-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="5344f-111">&#9654;观看视频 （12 分钟）</span><span class="sxs-lookup"><span data-stu-id="5344f-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
