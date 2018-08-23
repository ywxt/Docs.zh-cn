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
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="5f9c6-104">[如何实现:]使用 Reponse.Filter 属性替换 ASP.NET 页面中的 HTML</span><span class="sxs-lookup"><span data-stu-id="5f9c6-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>
====================
<span data-ttu-id="5f9c6-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="5f9c6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="5f9c6-106">在此视频的 Chris Pels 中显示了如何使用 Reponse.Filter 属性以截获并更改发送到一个页面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="5f9c6-107">首先，使用某些简单文本创建一个示例页面。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="5f9c6-108">然后，它可作为发送到用户的浏览器的当前流的替代流创建自定义的 Stream 类。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="5f9c6-109">该自定义流类中的更改，且然后写出到响应流的流检索页的内容。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="5f9c6-110">在此自定义的 Stream 类的 Write 方法自定义，以替换在基的响应流，从而更改就发送到用户的浏览器的 HTML。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="5f9c6-111">最后，分配给 Response.Filter 属性页中新的流类\_加载事件，从而提供更改页面内容的机制。</span><span class="sxs-lookup"><span data-stu-id="5f9c6-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="5f9c6-112">&#9654;观看视频 （13 分钟）</span><span class="sxs-lookup"><span data-stu-id="5f9c6-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
