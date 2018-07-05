---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[如何实现:]使用 Reponse.Filter 属性替换 ASP.NET 页面中的 HTML |Microsoft Docs'
author: rick-anderson
description: 在此视频的 Chris Pels 中显示了如何使用 Reponse.Filter 属性以截获并更改发送到一个页面的 HTML。 首先，示例页创建 w...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/29/2009
ms.topic: article
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: f871a3969da21a22bfe10e3a85f43db3e0e522e8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382356"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="d9a33-104">[如何实现:]使用 Reponse.Filter 属性替换 ASP.NET 页面中的 HTML</span><span class="sxs-lookup"><span data-stu-id="d9a33-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>
====================
<span data-ttu-id="d9a33-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d9a33-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d9a33-106">在此视频的 Chris Pels 中显示了如何使用 Reponse.Filter 属性以截获并更改发送到一个页面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="d9a33-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="d9a33-107">首先，使用某些简单文本创建一个示例页面。</span><span class="sxs-lookup"><span data-stu-id="d9a33-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="d9a33-108">然后，它可作为发送到用户的浏览器的当前流的替代流创建自定义的 Stream 类。</span><span class="sxs-lookup"><span data-stu-id="d9a33-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="d9a33-109">该自定义流类中的更改，且然后写出到响应流的流检索页的内容。</span><span class="sxs-lookup"><span data-stu-id="d9a33-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="d9a33-110">在此自定义的 Stream 类的 Write 方法自定义，以替换在基的响应流，从而更改就发送到用户的浏览器的 HTML。</span><span class="sxs-lookup"><span data-stu-id="d9a33-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="d9a33-111">最后，分配给 Response.Filter 属性页中新的流类\_加载事件，从而提供更改页面内容的机制。</span><span class="sxs-lookup"><span data-stu-id="d9a33-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="d9a33-112">&#9654;观看视频 （13 分钟）</span><span class="sxs-lookup"><span data-stu-id="d9a33-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
