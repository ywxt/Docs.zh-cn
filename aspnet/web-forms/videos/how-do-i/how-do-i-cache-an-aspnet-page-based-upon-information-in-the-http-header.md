---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[如何实现:] 缓存 ASP.NET 页面根据 HTTP 标头中的信息 |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何使基于页面的 HTTP 标头中的信息在 ASP.NET 输出缓存中的页面。 首先，潜在的 HTTP 页眉...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: c90a3db1357df062909ad0e3b73fdeeb3dc16329
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824445"
---
<a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a>[如何实现:] 缓存 ASP.NET 页面根据 HTTP 标头中的信息
====================
通过[Chris Pels](https://twitter.com/chrispels)

在此视频的 Chris Pels 中显示了如何使基于页面的 HTTP 标头中的信息在 ASP.NET 输出缓存中的页面。 首先，可能的 HTTP 标头值已经过评审。 然后，创建了一个示例页，并随后将 OutputCache 指令用于 VaryByHeader 特性包含一个值为"接受的语言"，一个 HTTP 标头，来控制缓存基于用户的浏览器的语言。 在 IE 中设置为英语，然后在设置为使用法语的 FireFox 中查看示例页面。 最后，若要将缓存定义移到 CacheProfile web.config 文件中的选项进行讨论。

[&#9654;观看视频 （12 分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
