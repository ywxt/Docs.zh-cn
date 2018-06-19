---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[如何:]使用 Reponse.Filter 属性替换 ASP.NET 页中的 HTML |Microsoft 文档'
author: rick-anderson
description: 在此视频 Chris Pels 演示如何使用 Reponse.Filter 属性以截获并更改发送到页面的 HTML。 首先，示例创建了一个页 w...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/29/2009
ms.topic: article
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 3e7c1f2a947d185d7c2a01deb75e42c92ba914c3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26525526"
---
<a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a><span data-ttu-id="2ae37-104">[如何:]使用 Reponse.Filter 属性替换 ASP.NET 页中的 HTML</span><span class="sxs-lookup"><span data-stu-id="2ae37-104">[How Do I:] Use the Reponse.Filter Property to Replace HTML in an ASP.NET Page</span></span>
====================
<span data-ttu-id="2ae37-105">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="2ae37-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="2ae37-106">在此视频 Chris Pels 演示如何使用 Reponse.Filter 属性以截获并更改发送到页面的 HTML。</span><span class="sxs-lookup"><span data-stu-id="2ae37-106">In this video Chris Pels shows how to use the Reponse.Filter property to intercept and alter the HTML being sent to a page.</span></span> <span data-ttu-id="2ae37-107">首先，使用一些简单的文本创建一个示例页。</span><span class="sxs-lookup"><span data-stu-id="2ae37-107">First, a sample page is created with some simple text.</span></span> <span data-ttu-id="2ae37-108">然后，它用作替换流为当前的流发送到用户的浏览器创建自定义流类。</span><span class="sxs-lookup"><span data-stu-id="2ae37-108">Then, a custom Stream class is created which serves as the replacement stream for the current stream being sent to the user's browser.</span></span> <span data-ttu-id="2ae37-109">该自定义流类中从流中，更改，，然后写出到响应流中检索页面内容。</span><span class="sxs-lookup"><span data-stu-id="2ae37-109">In that custom stream class the contents of the page are retrieved from the stream, altered, and then written out to the response stream.</span></span> <span data-ttu-id="2ae37-110">在此自定义流类 Write 方法自定义，以替换在基的响应流中，从而更改就发送到用户的浏览器的 HTML。</span><span class="sxs-lookup"><span data-stu-id="2ae37-110">In this custom Stream class the Write method is customized to replace the HTML in the base Response stream, thereby altering what is sent to the user's browser.</span></span> <span data-ttu-id="2ae37-111">最后，分配给 Response.Filter 属性页中新的流类\_加载事件，从而，提供更改页面内容的机制。</span><span class="sxs-lookup"><span data-stu-id="2ae37-111">Finally, the new stream class is assigned to the Response.Filter property in the Page\_Load event, thereby, providing the mechanism for altering the page content.</span></span>

[<span data-ttu-id="2ae37-112">&#9654;观看视频 （13 分钟）</span><span class="sxs-lookup"><span data-stu-id="2ae37-112">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
