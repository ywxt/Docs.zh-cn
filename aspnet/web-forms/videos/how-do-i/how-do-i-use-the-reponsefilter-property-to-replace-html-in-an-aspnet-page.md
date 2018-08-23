---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[如何实现:]使用 Reponse.Filter 属性替换 ASP.NET 页面中的 HTML |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何使用 Reponse.Filter 属性以截获并更改发送到一个页面的 HTML。 首先，示例页创建 w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 0e8ae8b62bbb4ac1fc7e942cf3dd0438383cb510
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834545"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[如何实现:]使用 Reponse.Filter 属性替换 ASP.NET 页面中的 HTML
====================
通过[Chris Pels](https://twitter.com/chrispels)

在此视频的 Chris Pels 中显示了如何使用 Reponse.Filter 属性以截获并更改发送到一个页面的 HTML。 首先，使用某些简单文本创建一个示例页面。 然后，它可作为发送到用户的浏览器的当前流的替代流创建自定义的 Stream 类。 该自定义流类中的更改，且然后写出到响应流的流检索页的内容。 在此自定义的 Stream 类的 Write 方法自定义，以替换在基的响应流，从而更改就发送到用户的浏览器的 HTML。 最后，分配给 Response.Filter 属性页中新的流类\_加载事件，从而提供更改页面内容的机制。

[&#9654;观看视频 （13 分钟）](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
