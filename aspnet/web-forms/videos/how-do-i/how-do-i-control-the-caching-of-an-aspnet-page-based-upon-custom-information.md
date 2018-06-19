---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[如何:]控件的 ASP.NET 页缓存基于自定义信息 |Microsoft 文档'
author: rick-anderson
description: 在此视频 Chris Pels 演示如何控制缓存 ASP.NET 页基于自定义信息的条件。 创建一个示例页，然后 o。...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/19/2009
ms.topic: article
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: b785de4e1161ae82ee458148aee4b30820801147
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26528126"
---
<a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="77753-104">[如何:]控件的 ASP.NET 页缓存基于自定义信息</span><span class="sxs-lookup"><span data-stu-id="77753-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>
====================
<span data-ttu-id="77753-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="77753-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="77753-106">在此视频 Chris Pels 演示如何控制缓存 ASP.NET 页基于自定义信息的条件。</span><span class="sxs-lookup"><span data-stu-id="77753-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="77753-107">创建一个示例页，然后将 OutputCache 指令使用具有 VaryByCustom 属性，其中包含自定义值。</span><span class="sxs-lookup"><span data-stu-id="77753-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="77753-108">接下来，GetVaryCustomByString() 方法被重写在 global.asax 模块提供了自定义特性的处理。</span><span class="sxs-lookup"><span data-stu-id="77753-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="77753-109">在该方法返回是一个字符串，唯一标识该页面的缓存的版本。</span><span class="sxs-lookup"><span data-stu-id="77753-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="77753-110">最后，是有关如何缓存使用的自定义值可以使用以下几种方式为网站的讨论。</span><span class="sxs-lookup"><span data-stu-id="77753-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="77753-111">&#9654;观看视频 （12 分钟）</span><span class="sxs-lookup"><span data-stu-id="77753-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
